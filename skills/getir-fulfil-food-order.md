---
name: Fulfil a GetirFood order end to end
description: Receive a pushed GetirFood order, approve it inside the 30-second answer window, and drive it through prepare and handover or deliver depending on who carries it.
api: openapi/getir-food-openapi.yml
operations: [postAuthLogin, postFoodordersPeriodicUnapproved, postFoodordersActive, getFoodordersFoodorderid, postFoodordersFoodorderidVerify, postFoodordersFoodorderidVerifyscheduled, postFoodordersFoodorderidPrepare, postFoodordersFoodorderidHandover, postFoodordersFoodorderidDeliver]
---

# Fulfil a GetirFood order end to end

## How orders arrive

Getir **pushes** orders to two partner-hosted URLs you register (new order, cancel order),
by `POST`, authenticated with a shared `x-api-key` header. See
`asyncapi/getir-food-webhooks.yml`.

If you cannot process a pushed order, fall back to **`postFoodordersPeriodicUnapproved`**
(`POST /food-orders/periodic/unapproved`) or **`postFoodordersActive`**
(`POST /food-orders/active`). The docs say explicitly: *do not constantly query
`/unapproved`.* Both are exempt from the rate limiter, which is not an invitation to poll.

## The clock

- An order must be **answered (approved or cancelled) within 30 seconds**, or the restaurant
  is called automatically by IVR.
- The **confirmation time limit is 5 minutes**. A restaurant that reaches it is automatically
  closed and its orders cancelled.
- At least **1 minute must elapse** between `verify` → `prepare` and between
  `prepare` → `deliver`.

## Steps

1. **Authenticate — `postAuthLogin`.** Token is valid 1 hour; send it as the `token` header.

2. **Read the order — `getFoodordersFoodorderid`** (`GET /food-orders/{foodOrderId}`) if you
   need the full record beyond the webhook payload.

3. **Branch on `status`:**
   - `400` — immediate order, or a pre-approved scheduled order → approve with
     **`postFoodordersFoodorderidVerify`** (`POST /food-orders/{foodOrderId}/verify`).
   - `325` — scheduled order → approve with
     **`postFoodordersFoodorderidVerifyscheduled`**
     (`POST /food-orders/{foodOrderId}/verify-scheduled`).

   After approval the status becomes `350` and the order no longer appears in
   `/food-orders/periodic/unapproved`. One hour before a scheduled order's delivery time the
   status moves to `500` and it behaves like an immediate order.

4. **Mark it being prepared — `postFoodordersFoodorderidPrepare`**
   (`POST /food-orders/{foodOrderId}/prepare`). Wait at least 1 minute after step 3.

5. **Branch on `deliveryType`:**
   - `1` — **Getir courier**: call **`postFoodordersFoodorderidHandover`**
     (`POST /food-orders/{foodOrderId}/handover`) when the courier takes the bag. Everything
     after that is handled by Getir.
   - `2` — **restaurant's own courier**: call **`postFoodordersFoodorderidDeliver`**
     (`POST /food-orders/{foodOrderId}/deliver`) on delivery. Wait at least 1 minute after
     step 4.

## Idempotency

There is **no idempotency key** on this API. Re-issuing a completed transition returns a
domain error rather than replaying the original response — notably
`2 FoodOrderAlreadyVerified`, `3 FoodOrderStatusInvalidError`, `4 FoodOrderStatusLock`,
`74 FoodOrderPreparedTimeLimitError`, `62 FoodOrderDeliveredToClientTimeLimitError`.
Treat every transition as **at-most-once** and reconcile from `getFoodordersFoodorderid`
after any ambiguous failure. See `conventions/getir-conventions.yml`.

## Errors worth handling explicitly

`1 FoodOrderNotFound` (404) · `3 FoodOrderStatusInvalidError` · `14 CourierStatusInvalid` ·
`15 CourierNotReachedToRestaurant` · `71 FoodOrderHasNoCourierError` ·
`64 FoodOrderCourierMismatchError` · `38 RestaurantIsNotOpen` ·
`79 CannotVerifyBeforeActivationError`. Full registry: `errors/getir-error-codes.yml`.

## Testing

Test environment: `https://food-external-api-gateway.development.getirapi.com`.
Place test orders at `https://web-workspace.development.getirapi.com/` (default OTP `1234`,
address must be Arnavutköy Mahallesi). See `sandbox/getir-sandbox.yml`.
