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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Getir is an Istanbul-based on-demand delivery company, founded in 2015, that pioneered the
ultrafast "groceries in minutes" model and grew into a super-app spanning rapid grocery,
large-basket grocery (GetirBüyük), water (GetirSu), restaurant food delivery
(GetirYemek / GetirFood) and local-merchant commerce (GetirÇarşı / GetirLocals).

Its developer surface is a **partner-integration platform**, not a public product API: POS and
integrator companies connect restaurant point-of-sale systems to GetirFood.

- Website: https://getir.com/
- Developer portal: https://developers.getir.com/
- Integration docs: https://developers.getir.com/food/documentation/giris
- API reference: https://developers.getir.com/food/api-documentation
- Status page: https://getir-food-integration.instatus.com/
- Support: getiryemekapi@getir.com

## GetirFood API

Swagger 2.0, version 1.5.8 — 54 paths, 62 operations, 63 definitions, live at
`https://food-external-api-gateway.getirapi.com/swagger.json`.

Covers restaurant configuration (open/close, working hours, delivery zones, average preparation
time, courier service, payment methods), menu and product/option availability, chain menus, and
the full food-order lifecycle: verify, verify-scheduled, prepare, handover, deliver, cancel,
transfer to another restaurant, and invoice attachment.

Orders are **pushed** to two partner-registered webhook URLs (new order, cancel order) over
HTTP POST with a shared `x-api-key`; `/food-orders/periodic/unapproved` and
`/food-orders/active` are the documented backup queries.

## What is in this repo

| Artifact | Path |
|---|---|
| OpenAPI / Swagger (verbatim + YAML) | `openapi/` |
| Overlay of our enhancements | `overlays/` |
| Authentication profile | `authentication/` |
| API conventions | `conventions/` |
| Error registry (99 published codes) | `errors/` |
| Rate limits (52 endpoints) | `rate-limits/` |
| Webhook catalog | `asyncapi/` |
| Sandbox / test data | `sandbox/` |
| Data model | `data-model/` |
| Lifecycle + changelog | `lifecycle/`, `changelog/` |
| Conformance | `conformance/` |
| Packages | `packages/` |
| MCP servers + tool crosswalk | `mcp/` |
| Agent skills | `skills/` |
| Agentic access contracts | `agentic-access/` |
| Domain security + well-known probes | `security/`, `well-known/` |
| llms.txt | `llms/` |

## What Getir does not publish

No OpenAPI 3.x, GraphQL, gRPC or AsyncAPI; no official MCP server; no A2A agent card; no
`/.well-known/` documents on any host; no official SDK or CLI; no deprecation policy, SLA,
trust center, bug bounty or published compliance certifications; no Postman collection.

## Corporate note

In February 2026 Uber agreed to acquire Getir's Türkiye delivery business (food, grocery,
retail and water); the Turkish Competition Authority cleared the transaction in June 2026. As
of 2026-07-31 the GetirFood developer portal, docs API, production gateway and status page are
all live and serving.
