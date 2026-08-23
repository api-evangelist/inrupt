---
name: inrupt-subscribe-to-pod-events
description: >-
  Subscribe to Inrupt ESS change notifications and receive verified webhooks when Pod resources change
  or when Access Requests and Access Grants move through their lifecycle.
api: Inrupt Change Notifications API (ESS Notification Delivery Service)
spec: openapi/inrupt-notification-openapi.yaml
base_url: https://notification.{ess-domain}
operations:
  - negotiate
  - createSubscription
  - listSubscriptions
  - fetchSubscription
  - removeSubscription
  - getJsonWebKeySet
  - listDeliveryFailures
generated: '2026-08-23'
method: generated
source: >-
  openapi/inrupt-notification-openapi.yaml (operationIds verified present) plus
  https://docs.inrupt.com/ess/services/service-notification/notification-delivery-service
---

# Subscribe to Inrupt ESS Pod and consent events

Use this when an application must react to something happening in a Pod — a file changed, or a person
granted or revoked consent — instead of polling for it.

## Before you start

- You need a bearer token: a Solid-OIDC access token, or an ESS Access Token from the RFC 8693 token
  exchange at `POST https://platform.{ess-domain}/access/token`. Default TTL is **5 minutes**. Treat a
  `401` as routine: re-exchange and retry once.
- You need a **public HTTPS endpoint** to receive the POSTs. There is no polling delivery mode.
- Every subscription that names a resource must use the **canonical URI** form
  `{storage-id}/sc/{resource-id}`, not the path form `{storage-id}/sp/{resource-path}`. This is an ESS
  3.0 requirement and a subscription built on a path URI is the most common silent breakage.

## Steps

1. **(Optional) Negotiate the protocol** — `negotiate` (`POST /`). Send the protocols and features you
   can accept; the response names the negotiated protocol, the subscription endpoint for it, and the
   available features. Skip this if you already know you are using webhooks.

2. **Create the subscription** — `createSubscription` (`POST /subscriptions`). Body:
   - `type` — an array from: `AccessRequestPending`, `AccessRequestDenied`, `AccessGrantIssued`,
     `AccessGrantRevoked`, `AccessGrantExpired`, `ResourceCreated`, `ResourceUpdated`,
     `ResourceDeleted`, `ContainerCreated`, `ContainerUpdated`, `ContainerDeleted`.
   - `dispatch` — `{ "type": "webhook", "uri": "https://your.app/hook" }`. Optionally add
     `authentication` for mTLS, with a PEM `serverCertificate`.
   - `storage` — **required** whenever the `type` array contains any Resource*/Container* event.
     Omit it for consent-only subscriptions such as `AccessRequestPending`.
   - `purpose` — optional, max 1024 characters.
   - `dataMinimization.retentionPeriod` — optional ISO-8601 duration (`P30D`, `PT2H30M`) telling
     downstream processors how long they may retain the message contents.

   A success is `201` with the created subscription. `400` returns an
   `HttpValidationProblem` whose `violations[]` names the offending `field` and `in`.

   **There is no idempotency key.** Repeating this call creates a second subscription and you will get
   duplicate webhooks. Before retrying a request that timed out, call `listSubscriptions` and check.

3. **Fetch the signing keys once, and cache them** — `getJsonWebKeySet` (`GET /jwks`). Public, no auth.

4. **Verify every inbound webhook before acting on it.** Messages are signed per
   **RFC 9421 HTTP Message Signatures**; match the `kid` in the signature to a key from the JWK Set.
   An unverified notification must be dropped, not processed — the endpoint is public.

5. **Read the payload.** Fields: `id`, `subscription`, `published`, `type`, `purpose`, `controller`,
   `audience`, `resource`, `dataMinimization`. `controller` is who created the request or grant;
   `audience` is who the notification is for. Honour `dataMinimization.retentionPeriod` if present —
   it is a consent constraint travelling with the event, not a hint.

6. **Handle missed deliveries** — `listDeliveryFailures`
   (`GET /subscriptions/{identifier}/delivery-failures`) returns what ESS could not deliver and the
   response your endpoint gave. Redelivery attempts are bounded by the deployment's
   `INRUPT_NOTIFICATION_DISPATCH_RETRY_LIMIT`, so a long outage means permanent gaps; reconcile by
   re-reading state, not by assuming the stream is complete.

7. **Clean up** — `removeSubscription` (`DELETE /subscriptions/{identifier}`). Subscriptions also carry
   an `expiration`.

## Paging

`listSubscriptions` (`GET /subscriptions`) takes `page` and `pageSize` (max **100**, default **10**)
and returns `Link: <...>; rel="next"` / `rel="prev"`. The absence of a `next` link is the end.

## What you cannot do here

System-wide subscriptions (every grant in the deployment, regardless of who it is for) live under
`/system/subscriptions` and require the caller to be on the system-manager allow list. Notifications on
the user endpoints are filtered to what the subscribing agent is already authorized to see.
