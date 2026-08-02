---
name: Manage GetirFood menu and restaurant availability
description: Toggle product and option availability, update chain menu prices, and open, close or throttle a restaurant when the kitchen is under pressure.
api: openapi/getir-food-openapi.yml
operations: [postAuthLogin, getRestaurantsMenu, getProductsProductidStatus, putProductsProductidStatus, putProductsChainidChainproductidStatus, postProductsProductidInactivateasoption, postProductsProductidActivateasoption, postChainmenusChainmenuoidUpdateprices, putRestaurantsStatusClose, putRestaurantsStatusOpen, putRestaurantsAveragepreparationtime, putRestaurantsDeliverydurationBusyness]
---

# Manage GetirFood menu and restaurant availability

## Rate limit warning — read this first

Almost every operation in this skill sits in the **2 requests / 60 seconds per token** bucket
with a 30-second block. Batch your changes and never loop over a menu calling one endpoint per
item without pacing. See `rate-limits/getir-rate-limits.yml`.

## Steps

1. **Authenticate — `postAuthLogin`**; send the token as the `token` header.

2. **Read the menu — `getRestaurantsMenu`** (`GET /restaurants/menu`) to resolve product ids,
   option categories and options. Option products come from
   `getRestaurantsOptionproducts` (`GET /restaurants/option-products`).

3. **Check a product's availability — `getProductsProductidStatus`**
   (`GET /products/{productId}/status`), or by chain id with
   **`getProductsChainidChainproductidStatus`**
   (`GET /products/chain-id/{chainProductId}/status`).

4. **Toggle a product — `putProductsProductidStatus`**
   (`PUT /products/{productId}/status`), or chain-wide with
   **`putProductsChainidChainproductidStatus`**
   (`PUT /products/chain-id/{chainProductId}/status`).

5. **Toggle a product *as an option* —**
   **`postProductsProductidInactivateasoption`** /
   **`postProductsProductidActivateasoption`**
   (`POST /products/{productId}/(in)activate-as-option`), with the chain-id variants
   **`postProductsChainidChainproductidInactivateasoption`** /
   **`postProductsChainidChainproductidActivateasoption`**.
   A product being unavailable as a standalone item and as an add-on are separate switches.

6. **Toggle an individual option —
   `putRestaurantsOptionproductsChainidChainoptionproductidOptioncategoriesChainoptioncategoryidOptionsChainoptionidStatus`**
   (`PUT /restaurants/option-products/chain-id/{chainOptionProductId}/option-categories/{chainOptionCategoryId}/options/{chainOptionId}/status`).

7. **Update chain prices — `postChainmenusChainmenuoidUpdateprices`**
   (`POST /chain-menus/{chainMenuOID}/update-prices`). Resolve the menu first with
   `getChainmenus` (`GET /chain-menus`) and `getChainmenusChainmenuoid`
   (`GET /chain-menus/{chainMenuOID}`). **This is the only price-mutation operation in the
   published contract — there is no per-product price endpoint.**

## Restaurant-level pressure valves

- **Slow the kitchen down** — `putRestaurantsAveragepreparationtime`
  (`PUT /restaurants/average-preparation-time`).
- **Flag a busy period** — `putRestaurantsDeliverydurationBusyness`
  (`PUT /restaurants/delivery-duration/busyness`) adds 15 minutes to the delivery duration
  when set true.
- **Stop taking orders** — `putRestaurantsStatusClose` (`PUT /restaurants/status/close`);
  reopen with `putRestaurantsStatusOpen` (`PUT /restaurants/status/open`).
- **Courier service** — `postRestaurantsCourierDisable` /
  `postRestaurantsCourierEnable` (`POST /restaurants/courier/(dis|en)able`).
- **Zones** — `putRestaurantsZonesZoneidInactive` / `putRestaurantsZonesZoneidActive`
  (`PUT /restaurants/zones/{zoneId}/(in)active`) to narrow the delivery area rather than
  closing entirely.

Note that Getir will **auto-close** a restaurant that misses the 5-minute order confirmation
limit — closing deliberately is better than being closed.

## Errors

`40 ProductNotBelongsToRestaurantError` · `41 ProductNotActiveError` ·
`27 InactiveProductsInFoodOrder` · `80–84` chain product/option resolution failures ·
`92 RestaurantNotFound` · `38 RestaurantIsNotOpen`.
Full registry: `errors/getir-error-codes.yml`.
