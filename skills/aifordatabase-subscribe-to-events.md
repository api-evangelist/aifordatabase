---
name: aifordatabase-subscribe-to-events
description: Register a signed webhook endpoint, send a test event, and read the delivery log — including what the provider does not publish about signature verification.
api: AI for Database API
base_url: https://app.aifordatabase.com/api/v1
auth: 'Authorization: Bearer afd_...'
scopes: [webhooks]
operations:
  - listWebhookEndpoints
  - createWebhookEndpoint
  - getWebhookEndpoint
  - updateWebhookEndpoint
  - deleteWebhookEndpoint
  - testWebhookEndpoint
  - listWebhookDeliveries
generated: '2026-08-26'
method: generated
source: openapi/aifordatabase-openapi.yml + asyncapi/aifordatabase-webhooks.yml
---

# Receive events from AI for Database

Requires the `webhooks` scope and a **Pro plan or above** — webhook integrations are
not available on Free.

## Register

`createWebhookEndpoint` — `POST /webhooks` with `{"url": "...", "events": [...]}`.
Pass `["*"]` to subscribe to everything.

The response carries `secret` — **the full signing secret, shown only on creation**.
Every later read masks it. Capture it on this response or you will have to recreate
the endpoint.

## Verify the test delivery

`testWebhookEndpoint` — `POST /webhooks/{id}/test` sends a real event to your URL.
Then `listWebhookDeliveries` — `GET /webhooks/{id}/deliveries` returns the log:
`event`, `payload`, `statusCode`, `attempts`, `deliveredAt`.

## Manage

- `listWebhookEndpoints` — `GET /webhooks`
- `updateWebhookEndpoint` — `PATCH /webhooks/{id}` (change url, events, or set
  `isActive: false` to stop delivery without deleting)
- `deleteWebhookEndpoint` — `DELETE /webhooks/{id}`

## Two gaps you must plan around

1. **The event vocabulary is not published.** `events` is an unconstrained array of
   strings in the OpenAPI, with no enum and no event-reference page on the docs site.
   You cannot enumerate valid event types from anything public. Subscribe with
   `["*"]`, send a test, and read the `event` field off real deliveries to learn the
   names empirically.
2. **Signature verification is not documented.** The provider calls these "signed
   event webhooks" and issues a per-endpoint secret, but neither the signature header
   name nor the algorithm appears in the OpenAPI or the docs. Until the provider
   publishes it, you cannot implement verification correctly — do not pretend to.
   Treat inbound payloads as untrusted, confirm state via a `GET` against the API
   before acting on an event, and ask the provider for the signing scheme.

## Not the same thing: outbound workflow actions

A workflow `WEBHOOK` action is the opposite direction — the platform calling *your*
destination when a scheduled query fires. Those are configured on the workflow
(`WebhookActionConfig`), must be public HTTPS on port 443, reject private and
reserved networks, and take their secret headers from an encrypted, destination-bound
workflow credential rather than inline. See
`skills/aifordatabase-ship-a-scheduled-alert.md`.
