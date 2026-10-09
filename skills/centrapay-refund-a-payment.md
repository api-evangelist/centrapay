---
generated: '2026-10-09'
method: generated
name: centrapay-refund-a-payment
title: Refund a paid Payment Request
description: Look up a Payment Request, refund all or part of it, and confirm the refund in its activity log.
api: openapi/centrapay-openapi.yml
operations:
- getPaymentRequest
- listPaymentRequestsByExternalRef
- refundPaymentRequest
- listPaymentRequestActivities
source: 'Grounded in openapi/centrapay-openapi.yml; every operationId verified verbatim in the spec. Auth: X-Api-Key header
  (https://docs.centrapay.com/api/auth). Idempotency: https://docs.centrapay.com/api/idempotency.'
---
# Refund a paid Payment Request

1. Find the payment: `getPaymentRequest` by id, or `listPaymentRequestsByExternalRef` (GET /api/payment-requests/external-ref/{externalRef}) with your order reference.
2. `refundPaymentRequest` (POST /api/payment-requests/{paymentRequestId}/refund) with required `value` and `externalRef`. Use a unique `externalRef` per refund, because retries with the same reference are how you avoid duplicate refunds (see the idempotency docs).
3. `listPaymentRequestActivities` (GET /api/payment-requests/{paymentRequestId}/activities) to confirm the refund activity was recorded.

A refund moves money, so get a human to confirm the amount first.

Errors: https://docs.centrapay.com/api/http-status-codes. Rate limits: https://docs.centrapay.com/api/rate-limits.
