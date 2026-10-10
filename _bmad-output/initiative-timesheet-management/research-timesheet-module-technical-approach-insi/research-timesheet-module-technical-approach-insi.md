---
title: 'technical research: Technical approach for a timesheet module inside an HRMS'
type: 'technical'
topic: 'Technical approach for a timesheet module inside an HRMS'
decision: 'Integration, approval and audit, notification patterns and stack or deployment options for a small team'
source: 'native run'
status: complete
preset: 'standard'
validation: 'normal'
created: '2026-10-10'
updated: '2026-10-10'
---

# Technical research: timesheet module inside an HRMS

**Decision this research serves:** which integration, approval and audit, and notification approaches to use, and which stack and deployment options fit a small team. It lays out options with trade-offs and does not pick a winner. Your HRMS stack was unknown, so options are general.

## Executive summary

**Options that the evidence supports.**
1. **Integration:** receive events by webhook, then fetch current data from the HRMS API (notify-then-fetch), and reconcile with incremental polling. Use SCIM or SSO for identity [1][3][10].
2. **Approvals and audit:** a status column, a transition table and an append-only audit table in the application database, with corrections as separate adjustment entries. A workflow engine such as Temporal is only worth its operating burden if you need durable multi-day timers or cross-service orchestration [14][15].
3. **Reminders:** idempotent scheduled sends keyed by business period, stored in UTC, with a unique constraint to stop duplicates [11].
4. **Payroll handoff:** a one-way push of LOP days with a cut-off, as Zoho does, not a raw timesheet feed [6].
5. **Stack:** PostgreSQL is the most-used database in the 2025 Stack Overflow survey (55.6%) [16]. Choose the web framework by your team's skills. Deploy on a major cloud with an India region if data residency matters [18].

**Biggest caveat.** Evidence is thin in places. Most vendor claims are search-summary only, there is no hiring or productivity data, and observability, backups and CI/CD were not searched.

## 1. Integration and interoperability

- **Identity and provisioning.** SCIM PATCH is atomic per request and naturally idempotent, pagination is stateless, and clients must tolerate inconsistent results [1]. Entra ID provisioning cycles about every 40 minutes, so changes lag [2] (vendor page, search summary).
- **Events from an HRMS.** BambooHR sends an `employee.updated` webhook with the changed fields, retries on 5xx up to 5 times, and states no ordering or exactly-once guarantee. It recommends notify-then-fetch [3].
- **Rate limits differ widely.** Keka allows 50 requests a minute and the API is a paid add-on [4]. Zoho People limits are per plan per day, from 5,000 to 25,000 [5]. SAP SuccessFactors recommends server-side pagination and delta reads, and reportedly applies rate limits from release 2608 (single source) [8]. Merge's unified API gives 100 to 600 requests a minute per linked account and syncs roughly every 6 hours at standard [10].
- **Versioning.** Workday ships two feature releases a year and changes web-service versions only for breaking changes [9].
- **Payroll handoff.** Zoho People pushes LOP days to Zoho Payroll one way; the Processing Day cut-off must be on or before payday, and the pay run can't be approved before it [6]. RazorpayX's UbiAttendance integration pushes LOP monthly by manual sync [7]. Nothing was found on CSV import specifics or payroll lock for Razorpay or greytHR.

**Confidence: medium and low.** RFC 7644 and Zoho's limits page were read in full; most vendor claims are search summaries.

## 2. Architecture patterns in practice

- **Corrections after lock.** Accounting systems append rather than edit: voiding adds the exact opposite rows, and a separate accounting date lets a correction post to the period it belongs to [15]. This fits your "adjustment entry" constraint. Pain point: corrections hidden in the UI can be mistaken for real entries, so show and match them [15] (single forum source).
- **Workflow modelling.** Temporal can hold approval state, durable reminder timers and an audit record [14], but needs a database, workers and developers who write deterministic code, so it suits teams with a platform engineer [14]. For a linear draft, submitted, approved or rejected flow, no small-team head-to-head report was found; a status column plus transition and audit tables is a reasonable option, not a sourced recommendation [14].
- **Reminders.** GOV.UK Notify's scheduled messages went out 15 to 30 minutes late after a daylight-saving change, so store times in UTC and monitor scheduled sends [11]. Queues deliver at least once, so dedupe with a unique key on (user, kind, period) [11]. Slack allows about one message a second per channel and returns 429 with Retry-After [12]. **Microsoft Teams Office 365 connector webhooks were retired in 2026; use Workflows (Power Automate)** [13].

**Not found:** ledger post-mortems, payroll retro-pay practice, and email provider limits.

## 3. Implementation reality: stack and deployment

| Topic | What sources say | Source |
|---|---|---|
| Web frameworks (2025 survey) | Next.js 20.8%, ASP.NET Core 19.7%, FastAPI 14.8%, Spring Boot 14.7%, Django 12.6%, Laravel 8.9% | [16] |
| Databases | PostgreSQL 55.6%, MySQL 40.5%, SQL Server 30.1% | [16] |
| Row locks | PostgreSQL row locks block only writers of the same row, not plain reads | [17] |
| India regions | AWS Mumbai and Hyderabad, Azure Pune, Hyderabad, Chennai, Mumbai, Google Cloud Mumbai and Delhi | [18] |
| PaaS | Render and Fly.io list no India region | [19] |
| Cost sample | AWS Fargate about $0.0405 per vCPU-hour in US East; a single source | [20] |
| Kubernetes at small scale | Regret evidence is anecdote and vendor content; one team moved a small service to ECS Fargate in 3 days | digest |

**Not found:** hiring and productivity data, observability, backups and CI/CD, and 6-to-12-month experience reports.

## Cross-dimension insights

- Your payroll cut-off and the audit pattern reinforce each other: lock the week at approval, and post later changes as adjustments to the next period, the way both Zoho's payroll push and accounting reversals behave.
- If your HRMS is one of Keka, Zoho or BambooHR, the integration option differs: Keka's API is paid with a low rate limit, Zoho's is per plan, and BambooHR offers webhooks. Knowing the HRMS would narrow this section.

## Recommendations (for `bmad-architecture`)

| Option | Feeds | Confidence basis |
|---|---|---|
| Webhook then fetch, with incremental polling to reconcile | Architecture: integration | Medium: BambooHR and Merge guidance [3][10] |
| Status column, transition table and append-only audit table in the application database | Architecture: approvals | Low-medium: practitioner accounts [14][15] |
| Idempotent reminders keyed by business period, UTC | Architecture: notifications | Medium: one high-confidence incident [11] |
| Slack and Teams via Workflows; not the retired Teams connectors | Architecture: notifications | Medium [12][13] |
| One-way LOP push with a cut-off | Spec CAP-15 | Medium: Zoho documentation [6] |
| PostgreSQL; pick the framework by team skill; major cloud with an India region | Architecture: stack and deployment | Medium: survey and provider pages [16][18] |

## Open questions

- What is your existing HRMS and its stack? Several answers above depend on it.
- What are email provider and Teams bot limits? They were not searched.
- Observability, backups and CI/CD costs for a small team? Not searched.
- Do you need a workflow engine, or is a database state machine enough? No small-team report found.
- Is SAP's 2026 rate-limit change real? It rests on one source.

## Owner decisions (2026-10-10)

- Scope is the timesheet module only: stack, hosting, observability, backups and CI/CD are out of scope and belong to the architecture step.
- The payroll handoff is out of scope, so the one-way LOP push recommendation is not applied.
- Module-relevant findings kept in the spec: UTC, once-per-period reminders, Teams via Workflows, append-only adjustments.

## Source appendix

| # | Supports | Publisher | Pub date | Accessed | Confidence |
|---|---|---|---|---|---|
| 1 | SCIM behaviour | [IETF RFC 7644](https://www.rfc-editor.org/rfc/rfc7644) | 2015-09 | 2026-10-10 | high |
| 2 | Entra provisioning cycle | Delinea help page, see `digests/integration-r1-1.md` claim 4 | n/d | 2026-10-10 | low |
| 3 | BambooHR webhooks | [BambooHR docs](https://documentation.bamboohr.com/docs/permissioned-webhooks) | n/d | 2026-10-10 | med |
| 4 | Keka API limits | [Keka developers](https://developers.keka.com/reference/rate-limit) | n/d | 2026-10-10 | med |
| 5 | Zoho People API limits | [Zoho](https://www.zoho.com/people/api/api-limits.html) | n/d | 2026-10-10 | high |
| 6 | Zoho LOP push | [Zoho Payroll help](https://www.zoho.com/in/payroll/help/employer/integrations/integrations-people.html) | n/d | 2026-10-10 | med |
| 7 | Razorpay LOP sync | [Razorpay docs](https://razorpay.com/docs/payroll/employees/attendance-leaves.md) | n/d | 2026-10-10 | med |
| 8 | SAP SuccessFactors | [SAP KBA](https://userapps.support.sap.com/sap/support/knowledge/en/3792944) | 2026 | 2026-10-10 | low |
| 9 | Workday releases | University release notices, see `digests/integration-r1-1.md` claims 14-15 | 2026 | 2026-10-10 | med |
| 10 | Merge unified API | Merge docs, see `digests/integration-r1-1.md` claim 16 | n/d | 2026-10-10 | med |
| 11 | Notify DST incident, dedupe | GOV.UK Notify post-incident notes and engineering posts, see `digests/patterns-r1-1.md` claims 1-3 | 2022 and later | 2026-10-10 | high / med |
| 12 | Slack rate limits | Slack API docs, see `digests/patterns-r1-1.md` claim 4 | n/d | 2026-10-10 | med |
| 13 | Teams connector retirement | Microsoft notice MC1181996, see `digests/patterns-r1-1.md` claim 5 | 2026-04-15 | 2026-10-10 | med |
| 14 | Temporal trade-offs | Temporal guide and engineering posts, see `digests/patterns-r1-1.md` claims 6-8 | 2026 | 2026-10-10 | med |
| 15 | Append-only corrections | FOCUS billing spec, accounting references, see `digests/patterns-r1-1.md` claims 9-10 | n/d | 2026-10-10 | low-med |
| 16 | Frameworks and databases | Stack Overflow Developer Survey 2025, see `digests/stack-deployment-r1-1.md` | 2025 | 2026-10-10 | med |
| 17 | Row locks | PostgreSQL documentation, see `digests/stack-deployment-r1-1.md` claim 4 | n/d | 2026-10-10 | med |
| 18 | India regions | AWS, Azure and Google Cloud region pages, see `digests/stack-deployment-r1-1.md` claims 5-7 | n/d | 2026-10-10 | med |
| 19 | Render, Fly.io regions | Provider region pages, see `digests/stack-deployment-r1-1.md` claims 8-9 | n/d | 2026-10-10 | med |
| 20 | Fargate pricing | AWS pricing page, see `digests/stack-deployment-r1-1.md` claim 10 | n/d | 2026-10-10 | low |

## Staleness map

Per the pack's freshness bars, version and compatibility claims ([2], [4]-[10]) should be re-checked within 1 month, by **2026-11-10**, and certainly before building. Ecosystem signals ([16]) within 6 months, by **2027-04-10**. Patterns ([11], [14], [15]) within 2 years, by **2028-10-10**. The earliest action is the 1-month version re-check. Dates were set by hand from the pack's freshness bars, not computed with the staleness script.
