---
generated: '2026-10-09'
method: generated
name: centrapay-online-checkout
title: Online checkout with a Payment Request
description: Create a Centrapay Payment Request for an e-commerce order, send the customer to pay (redirect or popup), then
  retrieve it to decide the outcome and void it if the customer abandoned.
api: openapi/centrapay-openapi.yml
operations:
- createPaymentRequest
- getPaymentRequest
- voidPaymentRequest
source: 'Grounded in openapi/centrapay-openapi.yml; every operationId verified verbatim in the spec. Auth: X-Api-Key header
  (https://docs.centrapay.com/api/auth). Idempotency: https://docs.centrapay.com/api/idempotency.'
---
# Online checkout with a Payment Request

1. `createPaymentRequest` (POST /api/payment-requests) with required `configId` and `value`; for the redirect flow also set `redirectPaidUrl` and `redirectCancelUrl`. Use `externalRef` for your order id.
2. Send the customer to pay (redirect, or the Checkout popup SDK). Centrapay appends `paymentRequestId` on redirect back.
3. `getPaymentRequest` (GET /api/payment-requests/{paymentRequestId}) and act on its status. Never assume success because the customer came back or the popup closed.
4. If the status is still `new` because the customer dismissed checkout, call `voidPaymentRequest` (POST /api/payment-requests/{paymentRequestId}/void).

This mirrors Centrapay's own published skill (skills/provider/centrapay-e-commerce-integration/).

Errors: https://docs.centrapay.com/api/http-status-codes. Rate limits: https://docs.centrapay.com/api/rate-limits.
