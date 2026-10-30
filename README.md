# Getir

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

Getir is an Istanbul-based on-demand delivery company, founded in 2015, that pioneered the ultrafast "groceries in minutes" model and grew into a super-app spanning rapid grocery (Getir), large-basket grocery (GetirBüyük), water (GetirSu), restaurant food delivery (GetirYemek / GetirFood) and local-merchant commerce (GetirÇarşı / GetirLocals). Its developer-facing surface is a partner-integration platform rather than a public product API: Getir publishes the GetirFood API — a Swagger 2.0 contract at food-external-api-gateway.getirapi.com covering restaurant onboarding, menu and product status, working hours, delivery zones, payment methods and the full food-order lifecycle (verify, prepare, handover, deliver, cancel, transfer) — for POS and integrator companies that connect restaurant point-of-sale systems to GetirFood. Orders are pushed to partners over webhooks, with a documented rate limiter, a 99-entry service error registry, published test cards and a dedicated test environment. In February 2026 Uber agreed to acquire Getir's Türkiye delivery business, cleared by the Turkish Competition Authority in June 2026.

**Areas:** Company · Food Delivery · Grocery Delivery · On-Demand Delivery · Logistics · Restaurant · Point-of-Sale · Marketplace · Turkey · Partner Integration

## Getir on APIs.io

Everything profiled for Getir is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/getir/](https://apis.io/providers/getir/)** — or go straight to one of the APIs or properties below.

### APIs (8)

- [Getir Auth API](https://apis.io/apis/getir/getir-auth-api/) — Secret keys provided to your company will be used for login. After successful login, you must use the token returned to your company in other endpoints. The…
- [Getir Chain Menus API](https://apis.io/apis/getir/getir-chain-menus-api/) — The chain-menus API from Getir — 4 operation(s) for chain-menus.
- [Getir Changelog API](https://apis.io/apis/getir/getir-changelog-api/) — The changelog API from Getir — 1 operation(s) for changelog.
- [Getir Food Orders API](https://apis.io/apis/getir/getir-food-orders-api/) — Endpoints about food orders
- [Getir Health API](https://apis.io/apis/getir/getir-health-api/) — This endpoint can be used to check the health of the application
- [Getir Payment Methods API](https://apis.io/apis/getir/getir-payment-methods-api/) — The payment-methods API from Getir — 1 operation(s) for payment-methods.
- [Getir Products API](https://apis.io/apis/getir/getir-products-api/) — Endpoints in the products section can be used with product information obtained from restaurant endpoints.
- [Getir Restaurants API](https://apis.io/apis/getir/getir-restaurants-api/) — Endpoints about restaurant and courier opening and closing features can be seen in the restaurants section.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Getir Food Webhooks](https://apis.io/asyncapis/getir/getir-food-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [getir-mcp.yml](https://apis.io/servers/getir/getir-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Getir Agentic Access](https://apis.io/agentic-access/getir/getir-agentic-access/)

#### Collections (1)

Postman and Open Collection request collections.

- [GetirFood API Documentation](https://apis.io/collections/getir/open-getir-food/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Getir Food Overlay](https://apis.io/overlays/getir/getir-food-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Getir Authentication](https://apis.io/security/getir/getir-authentication/)
- [Getir Domain Security](https://apis.io/security/getir/getir-domain-security/)

#### Rate limits (1)

Published request limits.

- [Getir Rate Limits](https://apis.io/rate-limits/getir/getir-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://getir.com/)
- [Documentation](https://developers.getir.com/food/documentation/giris)
- [Getting started](https://developers.getir.com/food/documentation/giris)
- [API reference](https://developers.getir.com/food/api-documentation)
- [Privacy policy](https://getir.com/yardim/gizlilik-politikasi/)
- [GitHub](https://github.com/getir)
- [Status](https://getir-food-integration.instatus.com/)

## API Evangelist rating

**Kin Score 33.4** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 71.7 |
| Contract quality | 43.2 |
| Contract governance | 4.5 |
| Operational transparency | 57.9 |
| Developer ergonomics | 25.6 |
| Access clarity | 10.5 |

**Agent readiness 31.8** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | platform (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 20.6** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/getir/](https://apis.io/providers/getir/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Getir: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/getir/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
