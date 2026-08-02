---
name: Authenticate and read a GetirFood restaurant
description: Exchange GetirFood partner secret keys for a session token and read the restaurant's current configuration — menu, working hours, delivery zones and payment methods.
api: openapi/getir-food-openapi.yml
operations: [postAuthLogin, getRestaurants, getRestaurantsMenu, getRestaurantsWorkinghours, getRestaurantsZones, getRestaurantsPaymentmethods]
---

# Authenticate and read a GetirFood restaurant

Base URL (production): `https://food-external-api-gateway.getirapi.com`
Base URL (test): `https://food-external-api-gateway.development.getirapi.com`

## Before you start

- Credentials are **not self-service**. Getir issues an `appSecretKey` (company) and a
  `restaurantSecretKey` (per restaurant) after a POS/integrator company is approved. Contact
  `getiryemekapi@getir.com`.
- All dates and times returned by the API are **GMT**.
- Minimum TLS is **TLSv1.2**.

## Steps

1. **Log in — `postAuthLogin`** (`POST /auth/login`).
   Body carries `appSecretKey` and `restaurantSecretKey`. The response
   (`Login Response Schema`) returns `restaurantId` and `token`.
   The token is valid for **1 hour**; there is no refresh flow — call this operation again.

2. **Send the token on every subsequent call.** Every other operation takes a required
   `token` **request header** (57 of the 62 operations declare it explicitly). Omitting it
   returns `{"code":-2,"error":"ValidationError","message":"\"token\" is required","source":"headers"}`.

3. **Read the restaurant — `getRestaurants`** (`GET /restaurants`).
   Returns the restaurant record the token is scoped to, including brand and open/closed state.

4. **Read the menu — `getRestaurantsMenu`** (`GET /restaurants/menu`) and
   **`getRestaurantsOptionproducts`** (`GET /restaurants/option-products`) for option products.
   Product and option names come back as bilingual `{tr, en}` objects.

5. **Read the schedule — `getRestaurantsWorkinghours`** (`GET /restaurants/working-hours`).

6. **Read delivery zones — `getRestaurantsZones`** (`GET /restaurants/zones`) and
   **`getRestaurantsZonesEta`** (`GET /restaurants/zones/eta`) for ETA options.

7. **Read payment methods — `getRestaurantsPaymentmethods`**
   (`GET /restaurants/payment-methods`); the catalogue of all methods is
   **`getPaymentmethods`** (`GET /payment-methods`).

## Rate limits — this is the strict surface

Steps 3–7 all sit in the **2 requests / 60 seconds per token** bucket (30-second block on
breach). Cache the results; do not poll them. The default budget elsewhere is 300 requests /
60 seconds with a 20-second block. See `rate-limits/getir-rate-limits.yml`.

## Errors

Errors are a proprietary envelope `{code, error, message, details, source}` — **not**
RFC 9457. Relevant registry entries: `92 RestaurantNotFound`, `73 RestaurantAppNotFound`.
Full registry: `errors/getir-error-codes.yml`.

## Health and version

`getHealth` (`GET /health`) and `getChangelog` (`GET /changelog`) are unauthenticated.
