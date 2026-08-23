---
name: inrupt-agent-request-consent
description: >-
  Have an AI agent ask a person for consent to their Solid Pod data through the Inrupt ESS MCP Resource
  Service, wait for the human to approve, then read only what was granted.
api: Inrupt ESS MCP Resource Service
manifest: mcp/inrupt-mcp.yml
base_url: https://mcp.{ess-domain}/api
operations:
  - requestAccess
  - checkAccessRequestStatus
  - hasMatchingAccessGrant
  - getResource
generated: '2026-08-23'
method: generated
source: >-
  https://docs.inrupt.com/ess/services/service-mcp/mcp-resource and
  https://docs.inrupt.com/guides/integrating-with-ess-mcp (tool names and parameters verified against
  Inrupt's published reference tables)
---

# Ask a person for their data, then read it

This is the flow Inrupt built ESS 3.0's MCP service for: an agent that needs someone's private data
asks for it, a human decides, and the agent reads only what was granted.

## Connect

1. Authenticate the user with **your own** external OIDC Identity Provider (it must be on the ESS
   deployment's trusted-issuer allow list) and get an `id_token`.
2. Exchange it for an ESS Access Token:
   `POST https://platform.{ess-domain}/access/token`,
   `grant_type=urn:ietf:params:oauth:grant-type:token-exchange`,
   `subject_token=<id_token>`,
   `subject_token_type=urn:ietf:params:oauth:token-type:id_token`.
3. Connect an MCP client over **streamable HTTP** to `https://mcp.{ess-domain}/api` with
   `Authorization: Bearer <access_token>`.

The token's default TTL is **5 minutes**. Use `expires_in` to re-exchange before it lapses, and treat
a `401` as "re-exchange and retry", not as an error to surface.

## Steps

1. **Check first, ask second.** Call `hasMatchingAccessGrant` with `resourceUrl`, `mode` (`read` is
   the only supported mode today), `dataSubject` (the WebID that would have issued the grant), and
   optionally `purposeUrl` and `status`. If it returns a grant URL, skip to step 4. Asking again for
   access you already hold is the most common way an agent annoys the person it works for.

2. **Ask** — `requestAccess` with `resource`, `permission` (`read`), `dataSubject` (the WebID of the
   Resource Owner) and `purpose`. `purpose` is not decoration: it is recorded in the Verifiable
   Credential the person reviews, and it is what they are actually consenting to. Write it for them,
   not for your logs. You get back an Access Request URL with status `pending`.

3. **Wait** — `checkAccessRequestStatus` with `accessRequestUrl`, until the status leaves `pending`
   for `granted`, `denied` or `cancelled`.

   **You cannot approve it yourself.** Approving an Access Request is deliberately not an MCP tool;
   the person does it in a separate interface. If the answer is `denied`, that is an answer — do not
   re-request the same resource in a loop.

   *Better than polling:* if your deployment also runs the Notification Delivery Service, subscribe to
   `AccessGrantIssued` and `AccessRequestDenied` instead (see `inrupt-subscribe-to-pod-events`). The
   MCP surface has no tool for this, which is the one real gap in the flow.

4. **Read** — `getResource` with `resourceUrl` and `accessGrantUrl`. ESS validates that the grant
   exists, is not revoked, has not expired, covers this resource, was issued **to you**
   (`isProvidedTo` must match your identity) and carries the required modes.

## Boundaries you cannot cross

Every tool is scoped to the authenticated **delegator**. You can only create requests attributed to
the current user, only check requests issued to them, only verify grants where they are the grantee,
and only read with grants they were issued. Attempting anything else fails with an authorization
error. Do not design around this — it is the security model, and it is what lets a person hand an
agent a token without handing it their whole Pod.

## Consent can be withdrawn at any time

An Access Grant can be revoked by its issuer with immediate effect, and grants also expire. ESS checks
grant status server-side on every access as of 3.0, so a call that worked a minute ago can correctly
return `403` now. Re-check with `hasMatchingAccessGrant` rather than caching the fact that you once
had access, and never cache the *data* longer than any `dataMinimization.retentionPeriod` you were
given.
