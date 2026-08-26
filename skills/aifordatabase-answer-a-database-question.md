---
name: aifordatabase-answer-a-database-question
description: Discover a database connection, read its cached schema, then answer a question either deterministically with SQL or in natural language via the chat endpoint.
api: AI for Database API
base_url: https://app.aifordatabase.com/api/v1
auth: 'Authorization: Bearer afd_...'
scopes: [connections, query, chat, usage]
operations:
  - listConnections
  - getConnectionSchema
  - executeQuery
  - sendChatMessage
  - listAnnotations
  - getUsageBudget
generated: '2026-08-26'
method: generated
source: openapi/aifordatabase-openapi.yml + https://www.aifordatabase.com/docs/agent-querying-databases/
---

# Answer a question from a live database

## When to use this
The user asks something whose answer lives in an operational database — revenue,
churn, open tickets, failed payments — and you have an `afd_` key with at least the
`connections` and `query` scopes.

## Steps

1. **Find the connection.** `listConnections` — `GET /connections?page=1&pageSize=20`.
   Returns sanitized entries only: id, name, type (`POSTGRES` / `MYSQL` / `MARIADB` /
   `MSSQL` / `MONGODB` / `SQLITE`), host, database, isActive. Database passwords are
   never returned. Take the `id` as your `connectionId`.
   *Requires the `connections` scope.*

2. **Read the schema before writing any SQL.** `getConnectionSchema` —
   `GET /connections/{id}/schema`. This is the cached introspection: tables, columns,
   relationships. Do **not** issue discovery queries against the database; the schema
   is already here. If it is stale or empty, `introspectConnectionSchema`
   (`POST /connections/{id}/schema`) re-introspects.

3. **Read the business context.** `listAnnotations` —
   `GET /connections/{id}/annotations`. Annotations attach meaning to tables and
   columns (what "active" means, which column is the revenue column). Use them; they
   are the difference between a correct query and a plausible one.

4. **Choose your path.**
   - **Deterministic and free:** `executeQuery` —
     `POST /connections/{id}/query` with `{"sql": "..."}`. No AI in the loop, no
     credits consumed. Returns `columns`, `rows`, `rowCount`, `executionTime`.
     Results cap at 500 rows, so **aggregate in SQL** rather than pulling raw tables.
   - **Natural language:** `sendChatMessage` — `POST /chat` with
     `{"message": "...", "connectionId": "..."}`. Returns the answer, the SQL it
     generated, and the result set. Pass `conversationId` from a previous response to
     keep context on follow-ups.
     *Consumes AI credits.* For a repeated or already-known query, prefer
     `executeQuery`.

5. **Report the SQL, not just the number.** Both paths return the SQL that produced
   the answer. Show it. The product's own framing is "the assistant that shows its
   work" — an unverifiable number is worth less than a checkable one.

## Guardrails

- **Watch the budget before you spend it.** `getUsageBudget` —
  `GET /usage/budget` returns `included`, `topUp`, `used`, `remaining` in cents for
  the current period. `sendChatMessage` returns **402** when credits are exhausted.
  Self-throttle rather than discovering the wall.
- **Connections are read-only by default.** Do not assume a write will succeed, and
  do not attempt one to find out.
- **On 422**, the database's own error message is passed through verbatim in
  `error.message`. Fix the SQL and retry — the failure is yours, not transient.
- **On 429** (`RATE_LIMITED`), back off exponentially with jitter. Free is 60
  general / 20 chat requests per minute per organization; Pro 300/100; Enterprise
  1000/500. **No rate-limit headers are returned**, so track your own call rate.
- **Paginate properly.** `page` / `pageSize`; continue until
  `page >= meta.pagination.totalPages`. There is no cursor.

## Envelope

Every response is `{data, error, meta}`, with `data` and `error` mutually exclusive.
Keep `meta.requestId` in your logs — it is the only handle for tracing a failed call.
