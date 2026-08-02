# Getir

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
