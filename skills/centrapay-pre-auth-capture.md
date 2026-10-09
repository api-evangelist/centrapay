---
generated: '2026-10-09'
method: generated
name: centrapay-pre-auth-capture
title: Pre-authorise, then confirm or release
description: Create a pre-auth Payment Request, then either confirm (capture) the authorised funds or release them.
api: openapi/centrapay-openapi.yml
operations:
- createPaymentRequest
- getPaymentRequest
- confirmPaymentRequest
- releasePaymentRequest
source: 'Grounded in openapi/centrapay-openapi.yml; every operationId verified verbatim in the spec. Auth: X-Api-Key header
  (https://docs.centrapay.com/api/auth). Idempotency: https://docs.centrapay.com/api/idempotency.'
---
# Pre-authorise, then confirm or release

1. `createPaymentRequest` with `preAuth: true` plus required `configId` and `value`.
2. After the customer authorises, check the state with `getPaymentRequest`.
3. Capture with `confirmPaymentRequest` (POST /api/payment-requests/{paymentRequestId}/confirm), or give the hold back with `releasePaymentRequest` (POST /api/payment-requests/{paymentRequestId}/release).

Both confirm and release move money, so never retry them blindly. Re-read the Payment Request first.

Errors: https://docs.centrapay.com/api/http-status-codes. Rate limits: https://docs.centrapay.com/api/rate-limits.
