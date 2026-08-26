---
name: aifordatabase-govern-query-approval
description: Route a query through human approval before it executes — define approval rules, submit a query, poll its status, and approve or reject it.
api: AI for Database API
base_url: https://app.aifordatabase.com/api/v1
auth: 'Authorization: Bearer afd_...'
scopes: [query, connections]
operations:
  - listApprovalRules
  - createApprovalRule
  - updateApprovalRule
  - deleteApprovalRule
  - submitQueryForApproval
  - getQueryApprovalStatus
  - listPendingQueries
  - approveQuery
  - rejectQuery
generated: '2026-08-26'
method: generated
source: openapi/aifordatabase-openapi.yml
---

# Put a human in front of a risky query

The `Query Approval` surface is the reason an agent can be given database access at
all: a query can be *submitted* rather than *run*, and a person decides.

## Set the policy

- `listApprovalRules` — `GET /approval-rules` (403 without permission).
- `createApprovalRule` — `POST /approval-rules`.
- `updateApprovalRule` / `deleteApprovalRule` — `PATCH` / `DELETE /approval-rules/{id}`.

## Submit instead of executing

`submitQueryForApproval` — `POST /queries/submit`. Returns **202**: accepted for
review, not executed. This is the operation to reach for when a query touches
something you were not explicitly asked to touch.

## Track it

- `getQueryApprovalStatus` — `GET /queries/{id}/status`. Poll this; there is no
  callback for approval state in the contract.
- `listPendingQueries` — `GET /queries/pending` (needs permission; 403 otherwise).

## Decide

- `approveQuery` — `POST /queries/{id}/approve`. **422** means the approved query then
  failed to execute; read `error.details`.
- `rejectQuery` — `POST /queries/{id}/reject`.

## Guardrails

- Approval is a **one-way door in one direction only**: a pending query can be
  rejected, but there is no un-approve operation. Once approved, it runs.
- Do not self-approve as an automation. If your key can both submit and approve, the
  control is decorative — hold a key with `query` scope for submission and leave
  approval to a human key.
- **403** on the pending/rules endpoints means the key lacks the authority to see
  other people's submissions. That is the control working; do not route around it.
