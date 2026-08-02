---
name: Cancel or transfer a GetirFood order
description: Reject an order with a valid Getir cancel reason, or move an accepted order to another restaurant in the same company when the original cannot fulfil it.
api: openapi/getir-food-openapi.yml
operations: [postAuthLogin, getFoodordersFoodorderidCanceloptions, postFoodordersFoodorderidCancel, getFoodordersFoodorderidAvailablerestaurantsfortransfer, postFoodordersFoodorderidTransfertoanotherrestaurant]
---

# Cancel or transfer a GetirFood order

## Cancel

1. **Authenticate — `postAuthLogin`**; send the returned value as the `token` header.

2. **Fetch the valid reasons — `getFoodordersFoodorderidCanceloptions`**
   (`GET /food-orders/{foodOrderId}/cancel-options`). Returns the cancel-reason set with
   bilingual `{tr, en}` messages. **This endpoint has its own tight budget: 40 requests /
   600 seconds, 60-second block.** Cache the reason list.

3. **Cancel — `postFoodordersFoodorderidCancel`**
   (`POST /food-orders/{foodOrderId}/cancel`), supplying a reason from step 2.

Cancelling counts as *answering* the order, so it satisfies the 30-second answer window.

**Errors:** `11 FoodOrderCanNotBeCancelled` · `13 FoodOrderAlreadyCancelled` ·
`12 FoodOrderCancelCallerTypeInvalid` · `59 FoodOrderNotHaveCancelReasonError` ·
`42 FoodOrderCannotBeAborted`.

## Transfer to another restaurant

1. **Find eligible targets —
   `getFoodordersFoodorderidAvailablerestaurantsfortransfer`**
   (`GET /food-orders/{foodOrderId}/available-restaurants-for-transfer`). This operation is
   **exempt from the rate limiter**.

2. **Transfer — `postFoodordersFoodorderidTransfertoanotherrestaurant`**
   (`POST /food-orders/{foodOrderId}/transfer-to-another-restaurant`).

Transfer is heavily precondition-checked. The registry names each failure, and they are worth
mapping one-to-one in your integration:

- `87 DeliveryTypeNotEligibleForFoodOrderTransfer` — wrong delivery type
- `88 StatusNotEligibleForFoodOrderTransfer` — wrong order status
- `89 TransferredFoodOrderError` — already transferred once
- `90 TransferFoodOrderTimeLimitError` — outside the transfer window
- `93 ChainRestaurantIsNotAllowedForFoodOrderTransfer`
- `94 ProductNotFoundOnTargetRestaurant`
- `80–84` — chain product / option category / option missing on the source or target product
- `85 InactiveItemsOnTargetProductError`
- `86 PriceMismatchOnTargetProductError`
- `91 PromoNotAvailableForTargetRestaurant`

Full registry: `errors/getir-error-codes.yml`.

## Cancellations you did not initiate

Getir pushes consumer- and Getir-initiated cancellations to your **cancel-order webhook**,
with a `cancelReason` object carrying `id`, bilingual `messages` and `cancelSource`.
`postFoodordersPeriodicCancelled` (`POST /food-orders/periodic/cancelled`) is the backup
query. See `asyncapi/getir-food-webhooks.yml`.

## No idempotency

There is no idempotency key. A retried cancel returns `13 FoodOrderAlreadyCancelled`; a
retried transfer returns `89 TransferredFoodOrderError`. Reconcile with
`getFoodordersFoodorderid` rather than blind-retrying.
