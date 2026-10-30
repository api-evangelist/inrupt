# Inrupt

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Inrupt is the enterprise company founded by Sir Tim Berners-Lee and John Bruce to commercialize Solid, the open decentralized-data specification he created at MIT. Its flagship product is the Enterprise Solid Server (ESS), a Kubernetes-deployed platform of cooperating services that gives each person or organization a Pod — a personal data store with fine-grained access control, auditing, and W3C Verifiable-Credential-based Access Requests and Grants. ESS ships an Access Grant service, an Authorization service using Access Control Policies (ACP), a Pod Storage service implementing the Solid Protocol, a Notification Delivery service that pushes signed webhooks to remote HTTPS endpoints, a Platform Management service with a token-exchange and admin provisioning API, an optional hybrid keyword-plus-semantic Search service, and — since ESS 3.0 — an MCP Resource Service exposing consent-mediated tools to AI agents. Inrupt also runs PodSpaces, a hosted developer-preview deployment of ESS, and publishes first-party JavaScript and Java client SDKs.

**Areas:** Company · Solid · Personal Data Stores · Decentralized Identity · Privacy · Access Control · Verifiable Credentials · Linked Data · RDF · Consent Management · Data Wallets · Agent Infrastructure

## Inrupt on APIs.io

Everything profiled for Inrupt is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/inrupt/](https://apis.io/providers/inrupt/)** — or go straight to one of the APIs or properties below.

### APIs (8)

- [Inrupt Pod Storage API (Solid Protocol)](https://apis.io/apis/inrupt/pod-storage/) — The ESS Pod Storage Service implements the Solid Protocol over HTTP — LDP-style container and resource CRUD in RDF (Turtle, JSON-LD) and binary form, with…
- [Inrupt Solid OpenID Provider](https://apis.io/apis/inrupt/solid-oidc/) — Inrupt's hosted Solid-OIDC identity provider for PodSpaces WebIDs. It publishes a standard OpenID Connect discovery document at…
- [Inrupt Access Grant Service (VC API)](https://apis.io/apis/inrupt/access-grant/) — The ESS Access Grant Service issues, queries, verifies, derives and status-checks W3C Verifiable Credentials that carry Access Requests and Access Grants —…
- [Inrupt ESS MCP Resource Service](https://apis.io/apis/inrupt/mcp-resource/) — Added in ESS 3.0, the MCP Resource Service exposes four Model Context Protocol tools — requestAccess, checkAccessRequestStatus, hasMatchingAccessGrant and…
- [Inrupt ESS Platform Management API](https://apis.io/apis/inrupt/platform-management/) — The Platform Management service hosts the ESS Admin API used to provision users before they first log in — creating a provisioning account, attaching a…
- [Inrupt Discovery API](https://apis.io/apis/inrupt/inrupt-discovery-api/) — WebSocket Discovery
- [Inrupt Jsonkeys API](https://apis.io/apis/inrupt/inrupt-jsonkeys-api/) — Public JSON Web Keys
- [Inrupt Subscription API](https://apis.io/apis/inrupt/inrupt-subscription-api/) — Subscription Management

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Inrupt Notifications Webhooks](https://apis.io/asyncapis/inrupt/inrupt-notifications-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Inrupt ESS MCP Resource Service](https://apis.io/servers/inrupt/inrupt-ess-mcp-resource-service/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Inrupt Notification Overlay](https://apis.io/overlays/inrupt/inrupt-notification-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Inrupt Authentication](https://apis.io/security/inrupt/inrupt-authentication/)
- [Inrupt Domain Security](https://apis.io/security/inrupt/inrupt-domain-security/)
- [Inrupt Trust Center](https://apis.io/security/inrupt/inrupt-trust-center/)
- [Inrupt Vulnerability Disclosure](https://apis.io/security/inrupt/inrupt-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Inrupt Scopes](https://apis.io/scopes/inrupt/inrupt-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Inrupt Plans Pricing](https://apis.io/plans/inrupt/inrupt-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Inrupt Rate Limits](https://apis.io/rate-limits/inrupt/inrupt-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.inrupt.com/)
- [Documentation](https://docs.inrupt.com/)
- [Getting started](https://docs.inrupt.com/sdk/javascript-sdk/tutorial/)
- [API reference](https://docs.inrupt.com/ess/services/)
- [Sign up](https://start.inrupt.com/)
- [Support](https://inrupt.atlassian.net/servicedesk)
- [Blog](https://www.inrupt.com/blog)
- [Security](https://www.inrupt.com/security)
- [Trust centre](https://www.inrupt.com/trust)
- [Terms of service](https://www.inrupt.com/terms-conditions)
- [Privacy policy](https://www.inrupt.com/privacy-policy)
- [GitHub](https://github.com/inrupt)
- [Status](https://status.inrupt.com/)

## API Evangelist rating

**Kin Score 61.0** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 68.3 |
| Contract quality | 51.3 |
| Contract governance | 18.2 |
| Operational transparency | 92.1 |
| Developer ergonomics | 73.2 |
| Access clarity | 50.0 |

**Agent readiness 49.6** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | templated |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | — |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 41.1** — Payments

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/inrupt/](https://apis.io/providers/inrupt/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Inrupt: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/inrupt/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
