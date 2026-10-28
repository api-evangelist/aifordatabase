# AI for Database

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

AI for Database is a natural-language data layer for operational databases, built by Wavicle.tech. It connects read-only to PostgreSQL, MySQL, MariaDB, SQL Server, MongoDB, SQLite and Google Sheets, translates plain-English questions into SQL, returns the SQL alongside the answer, pins results as self-refreshing dashboards, and runs scheduled workflows that fire email, webhook or Slack alerts when a query condition becomes true. The public REST API is explicitly designed for AI agents: a scoped Bearer-auth contract (afd_ keys, nine permission scopes) documented by a live OpenAPI 3.1 spec with 80 operations, a paused-draft workflow lifecycle with a real dry-run preview and a confirmation-gated live action test, human query approval, and agent-native discovery surfaces at llms.txt, llms-full.txt and a JSON capability manifest.

**Areas:** Artificial Intelligence · Database · Analytics · Developer Tools · Natural Language Query · Text-to-SQL · Dashboards · Business Intelligence · Workflow Automation · Alerts · Agent-Native · llms-txt

## AI for Database on APIs.io

Everything profiled for AI for Database is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/aifordatabase/](https://apis.io/providers/aifordatabase/)** — or go straight to one of the APIs or properties below.

### APIs (12)

- [AI for Database Chat API](https://apis.io/apis/aifordatabase/aifordatabase-chat-api/) — Send natural-language messages and receive AI-generated SQL and insights
- [AI for Database Connections API](https://apis.io/apis/aifordatabase/aifordatabase-connections-api/) — Manage database connections, schemas, annotations, and execute SQL queries
- [AI for Database Conversations API](https://apis.io/apis/aifordatabase/aifordatabase-conversations-api/) — Manage chat conversation history
- [AI for Database Dashboards API](https://apis.io/apis/aifordatabase/aifordatabase-dashboards-api/) — Create and manage dashboards and their widgets
- [AI for Database Keys API](https://apis.io/apis/aifordatabase/aifordatabase-keys-api/) — Manage platform API keys
- [AI for Database Metrics API](https://apis.io/apis/aifordatabase/aifordatabase-metrics-api/) — Define and evaluate metric formulas against connections
- [AI for Database Query Approval API](https://apis.io/apis/aifordatabase/aifordatabase-query-approval-api/) — Submit queries for human approval before execution
- [AI for Database Saved Queries API](https://apis.io/apis/aifordatabase/aifordatabase-saved-queries-api/) — Store, parameterize, and execute reusable SQL queries
- [AI for Database Usage API](https://apis.io/apis/aifordatabase/aifordatabase-usage-api/) — View usage records and budget information
- [AI for Database Webhooks API](https://apis.io/apis/aifordatabase/aifordatabase-webhooks-api/) — Manage webhook endpoints, deliveries, and test events
- [AI for Database Workflow Credentials API](https://apis.io/apis/aifordatabase/aifordatabase-workflow-credentials-api/) — Manage encrypted, destination-bound credentials for workflow actions
- [AI for Database Workflows API](https://apis.io/apis/aifordatabase/aifordatabase-workflows-api/) — Build and run scheduled or manual multi-step workflows

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Aifordatabase Webhooks](https://apis.io/asyncapis/aifordatabase/aifordatabase-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [aifordatabase-mcp](https://apis.io/servers/aifordatabase/aifordatabase-mcp/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Aifordatabase Openapi Overlay](https://apis.io/overlays/aifordatabase/aifordatabase-openapi-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Aifordatabase Authentication](https://apis.io/security/aifordatabase/aifordatabase-authentication/)
- [Aifordatabase Domain Security](https://apis.io/security/aifordatabase/aifordatabase-domain-security/)
- [Aifordatabase Trust Center](https://apis.io/security/aifordatabase/aifordatabase-trust-center/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Aifordatabase Plans Pricing](https://apis.io/plans/aifordatabase/aifordatabase-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Aifordatabase Rate Limits](https://apis.io/rate-limits/aifordatabase/aifordatabase-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.aifordatabase.com/)
- [Documentation](https://www.aifordatabase.com/docs/)
- [Getting started](https://www.aifordatabase.com/docs/quickstart/)
- [API reference](https://www.aifordatabase.com/docs/endpoints/)
- [Pricing](https://www.aifordatabase.com/pricing/)
- [Sign up](https://app.aifordatabase.com/signup)
- [Support](https://www.aifordatabase.com/contact/)
- [Blog](https://www.aifordatabase.com/blog/)
- [Trust centre](https://www.aifordatabase.com/trust/)
- [Terms of service](https://www.aifordatabase.com/terms/)
- [Privacy policy](https://www.aifordatabase.com/privacy/)

## API Evangelist rating

**Kin Score 60.3** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.7 |
| Contract quality | 61.4 |
| Contract governance | 4.5 |
| Operational transparency | 39.5 |
| Developer ergonomics | 66.1 |
| Access clarity | 77.6 |

**Agent readiness 36.3** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 27.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/aifordatabase/](https://apis.io/providers/aifordatabase/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for AI for Database: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/aifordatabase/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
