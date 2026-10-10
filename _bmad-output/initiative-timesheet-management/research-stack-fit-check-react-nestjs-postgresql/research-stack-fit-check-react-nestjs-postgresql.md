---
title: 'technical research (select): Stack fit check: React TypeScript, NestJS, PostgreSQL, database approval pattern, SendGrid, AWS'
type: 'technical (select)'
topic: 'Stack fit check: React TypeScript, NestJS, PostgreSQL, database approval pattern, SendGrid, AWS'
decision: "Confirm or challenge the owner's chosen stack for the timesheet module against the main alternatives"
source: 'native run'
status: complete
preset: 'standard'
validation: 'normal'
created: '2026-10-10'
updated: '2026-10-10'
---

# Technical research (select): stack fit check

**Decision this research serves:** confirm or challenge the owner's stack for the timesheet module: React with TypeScript, NestJS, PostgreSQL, a status column plus audit table for approvals, SendGrid for email, and AWS. It feeds `bmad-architecture`; the spec is unchanged because stack choice is outside the spec.

## Executive summary

**Five of six picks hold up. One is challenged: SendGrid.**

| Pick | Verdict | Why |
|---|---|---|
| React with TypeScript | Not challenged | Little evidence was gathered; a common default for form-heavy apps |
| NestJS | Holds, with one pitfall | Current and maintained; its scheduler runs every job in every instance, so reminders need a lock [3] |
| PostgreSQL | Holds, strongest fit | Partial unique indexes, row-level security and locks fit the locked-record and audit needs; MySQL has no partial indexes [4][5] |
| Status column plus audit table | Holds | Matches a linear draft, submitted, approved flow; a workflow engine adds burden without a clear need [6][7] |
| SendGrid | **Challenged** | Free plan retired in 2025; paid plans start at $19.95 a month vs about $1.60 for 10,000 emails on SES; reviewers report account suspensions and slow support [8][9][10] |
| AWS | Holds | India regions (Mumbai, Hyderabad) with RDS in both; cost not established [11][12] |

**Biggest caveat.** The evidence is thin in places: no 6-to-12-month team retrospectives were found, no official cloud cost figures were retrievable, and many claims rest on search summaries. The comparison is a fit check, not a benchmark.

## Decision matrix

Ratings: **Strong** = documented support; **OK** = works with a caution; **Unproven** = no evidence found.

| Criterion | NestJS | Django / FastAPI / Spring Boot | PostgreSQL | MySQL |
|---|---|---|---|---|
| Documented, current release | Strong: v12.1.1 on 28 Sep 2026 [1] | Not researched | Strong: majors 14 to 18 supported [2] | Not researched |
| Scheduled jobs for reminders | OK: runs in every process; use `@OnOneInstance()` with a lock store [3] | Not researched | n/a | n/a |
| One sheet per employee per week | n/a | n/a | Strong: unique constraint, partial unique index [4] | OK: unique constraint, no partial index [4] |
| Locked and append-only records | n/a | n/a | Strong: row-level security, separate application role [5] | Unproven |
| Team experience after 6 to 12 months | Unproven (anecdotes on ORM upgrades) | Unproven | Unproven | Unproven |
| Adoption in the 2025 Stack Overflow survey | NestJS 6.7%, below Django 12.6%, FastAPI 14.8%, Spring Boot 14.7% | as shown | 55.6% | 40.5% |

## Per-decision findings

**NestJS and Node.** NestJS v12.0.0 was released on 27 Aug 2026 and v12.1.1 on 28 Sep 2026, confirmed from GitHub releases only [1]. Node 22 is supported to 2027-04-30, Node 24 to 2028-04-30, and Node 26 enters LTS on 2026-10-28 [2]. Pitfall confirmed in the official docs: every cron job runs in every process, so three instances run a daily job three times; the docs recommend `@OnOneInstance()` from `@nestjs/locks` with a PostgreSQL or Redis store [3]. ORM choice (TypeORM vs Prisma) shows only low-confidence anecdotes.

**PostgreSQL.** Partial unique indexes and row-level locks are documented; MySQL 8.4 has no partial indexes [4]. For append-only audit tables, a policy allowing only INSERT and SELECT gives append-only behaviour for the application role. Table owners bypass row-level security unless `FORCE ROW LEVEL SECURITY` is set, and an owner can grant privileges back, so the application must connect as a role that does not own the tables [5]. PostgreSQL 14 reaches end of life on 2026-11-12, so start on a newer major [2].

**Approval workflow.** For a linear flow, a status column plus transition and audit tables avoids new infrastructure. Temporal Cloud costs about $50 per million actions, and a workflow's event history is capped at 51,200 events or 50 MB [6]. No source describes a small team outgrowing a status column, or regretting an engine; this is not evidence either way. EventBridge Scheduler supports cron and one-time schedules with an IANA time zone (UTC by default) at 60-second precision [7].

**Email service.** SendGrid retired its free plan on 2025-05-27, confirmed by two Twilio entries, and replaced it with a 60-day trial at 100 emails a day [8]. Paid plans start at Essentials $19.95 and Pro $89.95 a month; the exact 10,000-email price was not found [8].

| | SendGrid | Amazon SES | Postmark |
|---|---|---|---|
| About 10,000 emails a month (USD) | from $19.95 | about $1.60 | $15 (Basic) [9] |
| Free tier | 60-day trial only [8] | New-account credits, no perpetual free tier [9] | 100 emails a month [9] |
| Idempotency keys | Not found | Not found | Not supported [9] |
| India | Not found | Mumbai API and SMTP endpoints; Hyderabad API only (no SMTP) [11] | Not found |
| Reputation | Account suspensions and slow support in two independent sources [10] | Not researched | Not researched |

New SES accounts start on the Essentials plan from 2026-07-21; re-verify the plan terms [9].

**AWS.** AWS says Fargate, RDS and Secrets Manager are core services in all regions at launch, RDS endpoints exist in Mumbai and Hyderabad, and CloudFront is a global service [11]. Azure has four India regions and Google Cloud has Mumbai and Delhi; AWS leads developer use at 43.3% vs 26.3% for Azure and 24.6% for Google Cloud [12]. Per-service availability of Fargate and EventBridge Scheduler in the India regions was not confirmed, and no official monthly cost was retrievable; one third-party estimate puts a small Azure PostgreSQL instance in Central India at about USD 18 a month (single source).

## Cross-dimension insights

- Picking SES would keep email on the same cloud, but it needs sandbox exit and sending setup, and no source showed whether it supports idempotent sends. The spec's rule of one reminder per employee, kind and week should be enforced in your own database with a unique key, whichever email service you use.
- The reminder lock matters twice: NestJS runs jobs in every instance, and AWS schedulers can invoke more than once, so a unique key in PostgreSQL protects both.

## Recommendations (for `bmad-architecture`)

| Recommendation | Confidence basis |
|---|---|
| Keep React with TypeScript, NestJS, PostgreSQL and the status-plus-audit pattern | Medium: documentation supports fit; no retrospective evidence |
| Use an application database role that does not own the tables, with INSERT and SELECT only on audit tables | Medium: PostgreSQL documentation [5] |
| Enforce one reminder per employee, kind and week with a unique key; use `@OnOneInstance()` if you run several instances | Medium [3] |
| Reconsider SendGrid; compare it with SES (cheapest, same cloud) before committing | Medium: pricing and reputation from vendor changelog and two reviews [8][9][10] |
| Start on a PostgreSQL major newer than 14 and Node 24 or 26 LTS | Medium [2] |
| Get a real AWS cost estimate for your region before budgeting | Low: no official figure found |

## Open questions

- What is the real monthly AWS cost in Mumbai or Hyderabad? Use the AWS calculator.
- Are Fargate and EventBridge Scheduler available in both India regions?
- What is SendGrid's exact price at your volume, and does SES support idempotent sends?
- Would Django, FastAPI or Spring Boot fit better? No retrospectives were found, so this stays unanswered.
- Does React with TypeScript need a grid library for the timesheet form? Not researched.

## Source appendix

| # | Supports | Publisher | Pub date | Accessed | Confidence |
|---|---|---|---|---|---|
| 1 | NestJS releases | NestJS GitHub releases, see `digests/backend-cloud-r2-1.md` claim 1 | 2026-08/09 | 2026-10-10 | med |
| 2 | Node and PostgreSQL support dates | nodejs/release schedule and PostgreSQL versioning pages, see `digests/backend-db-r1-1.md` and `backend-cloud-r2-1.md` | 2026 | 2026-10-10 | med |
| 3 | Scheduler in every process | NestJS documentation, see `digests/backend-cloud-r2-1.md` claim 3 | n/d | 2026-10-10 | high |
| 4 | Partial unique indexes, MySQL | PostgreSQL and MySQL documentation, see `digests/backend-db-r1-1.md` claim 7 | n/d | 2026-10-10 | med-high |
| 5 | Row-level security, privileges | PostgreSQL documentation, see `digests/backend-cloud-r2-1.md` claims 4-5 | n/d | 2026-10-10 | high |
| 6 | Temporal pricing and limits | Temporal pricing page and docs, see `digests/workflow-email-r1-1.md` claims 12-13 | 2026 | 2026-10-10 | med |
| 7 | EventBridge Scheduler | AWS documentation, see `digests/workflow-email-r1-1.md` claim 14 | n/d | 2026-10-10 | med |
| 8 | SendGrid free-plan retirement, plans | Twilio changelog and pricing, see `digests/email-workflow-r2-1.md` | 2025-05 | 2026-10-10 | med |
| 9 | SES and Postmark pricing | AWS and Postmark pricing pages, see `digests/workflow-email-r1-1.md` claims 1-7 | 2026 | 2026-10-10 | med |
| 10 | SendGrid reputation | Capterra and Trustpilot, see `digests/workflow-email-r1-1.md` claim 11 | 2026 | 2026-10-10 | low-med |
| 11 | AWS regions and services | AWS documentation, see `digests/cloud-r1-1.md` and `backend-cloud-r2-1.md` claim 6 | n/d | 2026-10-10 | med |
| 12 | Cloud adoption and India regions | Stack Overflow Developer Survey 2025 and provider pages, see `digests/cloud-r1-1.md` | 2025 | 2026-10-10 | med |

## Staleness map

Per the pack's freshness bars, version and compatibility claims ([1]-[3], [11]) should be re-checked within 1 month, by **2026-11-10**, and before building. Pricing ([8]-[9]) within 3 months, by **2027-01-10**. Ecosystem signals ([10], [12]) within 6 months, by **2027-04-10**. The earliest action is the 1-month version re-check, which also covers PostgreSQL 14 reaching end of life on 2026-11-12. Dates were set by hand, not computed with the staleness script.
