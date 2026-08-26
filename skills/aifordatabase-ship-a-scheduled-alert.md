---
name: aifordatabase-ship-a-scheduled-alert
description: Take a database alert from draft to published schedule safely — create a paused draft, preview it without delivery, test exactly one live action, then publish an immutable version.
api: AI for Database API
base_url: https://app.aifordatabase.com/api/v1
auth: 'Authorization: Bearer afd_...'
scopes: [connections, query, workflows, workflow_credentials]
operations:
  - listConnections
  - executeQuery
  - createWorkflowCredential
  - createWorkflow
  - getWorkflow
  - previewWorkflow
  - testWorkflowAction
  - updateWorkflow
  - listWorkflowRuns
  - deleteWorkflow
generated: '2026-08-26'
method: generated
source: openapi/aifordatabase-openapi.yml + https://www.aifordatabase.com/docs/agent-workflow-lifecycle/
---

# Ship a scheduled database alert without surprising anyone

This is the six-step lifecycle the provider publishes, mapped to real operationIds.
Follow it in order. Each step is deliberately cheaper to undo than the next one.

## 01 — Discover
`listConnections` (`GET /connections`). Pick the connection the alert watches.

## 02 — Validate the condition
`executeQuery` (`POST /connections/{id}/query`) with the exact SQL the alert will run.

Write it as an **alert condition**: the query should return rows *only when the
condition is true*. Run it now against real data and confirm it returns nothing on a
normal day. A query that always returns rows becomes an alert that always fires.

## 03 — Draft
If the alert delivers to an authenticated destination, create the secret first:
`createWorkflowCredential` (`POST /workflow-credentials`). It is encrypted,
write-only and bound to its destination host. Secret headers **cannot** be supplied
inline in a workflow definition — reference `credentialId`.
*Needs the `workflow_credentials` scope **and** an organization admin role.*

Then `createWorkflow` (`POST /workflows`) with `triggerType` `SCHEDULE` (plus a cron
`triggerConfig`) or `MANUAL`, your query `steps` (1–5), and your `actions` (max 10,
type `EMAIL` or `WEBHOOK`). Set `stopIfEmpty: true` on the condition step — that is
the mechanism that turns a query into an alert.

**A new workflow is a paused draft. Creating it never schedules a delivery.**

## 04 — Preview
`previewWorkflow` (`POST /workflows/{id}/preview`). This runs the draft's queries
**only**. It never contacts an external system, never creates a delivery and never
persists a run. Inspect the step results. This is your free rehearsal — use it.

## 05 — Test exactly one action
`testWorkflowAction` (`POST /workflows/{id}/actions/{order}/test`) with
`{"confirmDelivery": true}`.

**This sends a real message to the real destination.** The required
`confirmDelivery` flag exists so it cannot happen by accident — omitting it returns
**428**. Test one action, read the sanitized delivery attempts it returns, and stop.
On **422** the test ran but delivery failed; `error.details.run` carries the run and
its attempts.

Do **not** retry this call blindly. It may have completed even if you got no
response.

## 06 — Publish
`updateWorkflow` (`PATCH /workflows/{id}`) with `isActive: true`. This validates and
atomically publishes an **immutable** production version; the schedule runs that
version, not the live draft.

Two preconditions the contract enforces:
- **`expectedDraftRevision`** must accompany any change to a draft field, step or
  action. Read the current `draftRevision` from `getWorkflow` first. A stale value
  returns **409**; omitting it entirely returns **428**.
- **`acknowledgedWarnings`** — if a publish attempt returns warnings, resubmit those
  exact strings to confirm you meant it.

Then `listWorkflowRuns` (`GET /workflows/{id}/runs`) to inspect execution history.

## Undoing it

- **Stop future runs:** `updateWorkflow` with `isActive: false`.
- **Remove it entirely:** `deleteWorkflow` (`DELETE /workflows/{id}`).
- **Cannot be undone:** anything already delivered. `triggerWorkflow`
  (`POST /workflows/{id}/run`) and `testWorkflowAction` both perform real external
  delivery, and no operation in this API recalls a sent message.

The provider publishes **no restore window, no soft-delete retention and no undo
period** for any of these. Treat a delete as permanent.
