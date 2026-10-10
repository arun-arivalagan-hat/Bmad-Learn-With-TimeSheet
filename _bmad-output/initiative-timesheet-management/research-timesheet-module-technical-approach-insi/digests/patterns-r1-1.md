# Digest patterns-r1-1: timesheet approval architecture patterns

Round 1, accessed 2026-10-10. WebFetch worked. Claims marked "search-summary" come from WebSearch result text only, not a fetched page, so confidence is capped at med/low.

## Claims

1. Claim: GOV.UK Notify scheduled bulk emails/texts went out 15 or 30 minutes late after the 30 Oct 2022 BST-to-GMT change. Cause: Celery scheduling has open issues with timezone changes. Fix: restart/redeploy the scheduler; redeploy after future clock changes; add monitoring on scheduled sends. Immediate sends were unaffected.
   - source: https://status.notifications.service.gov.uk/incidents/2r3ffvbqql09
   - publisher: GOV.UK Notify status page (incident and postmortem)
   - pub_date: 2022-11-09 (postmortem); older than the 2-year window, but a primary production incident
   - accessed: 2026-10-10
   - confidence: high (fetched). Fixed since? Unknown; the page says a permanent fix was pending.
   - class: production incident (single source; for a "pattern failed" claim count as anecdote unless corroborated by item 2)

2. Claim: Scheduled sends in other products misfired or duplicated around DST changes. A SaaS changelog says sends could go out at the wrong time and rarely duplicate around the transition. A local-time server cron slid when clocks shifted. Advice: store UTC, convert at the edges, and choose "fixed local time" or "fixed UTC" per schedule, never a mix.
   - source: search-summary of firstsales.io changelog, a DEV/dataconomy post and techinterview.org LLD (URLs surfaced in the search, not fetched)
   - publisher: vendor blogs
   - pub_date: 2026 (dataconomy 2026-05-18); others not stated
   - accessed: 2026-10-10
   - confidence: low (search-summary only)
   - class: vendor and community anecdote. Together with item 1 this is two or more independent reports of DST scheduling failure, but only item 1 is verified.

3. Claim: Reminder dedup practice: queues are at-least-once, so handlers must be idempotent. Record send state in a table with a unique constraint on (user, kind, period key) and insert before sending. Use a business-period key, not a timestamp, as the dedup key. Guard against double schedulers with a TTL lock. Reset stale "in progress" rows with a cleanup job, and do not hold row locks during vendor HTTP calls.
   - source: search-summary of subtracker.io, oneuptime.com/blog/post/2026-09-14-cron-stable-business-key-side-effects/view, openreplay and others
   - publisher: vendor and practitioner blogs
   - pub_date: 2025 to 2026-09-14
   - accessed: 2026-10-10
   - confidence: low-med (search-summary, several consistent sources)
   - class: practitioner guidance, advocacy-adjacent

4. Claim: Slack chat.postMessage is generally limited to about 1 message per second per channel, with a workspace-wide cap of several hundred per minute. Short bursts are tolerated but not guaranteed. On HTTP 429, honor Retry-After. Queue per channel.
   - source: https://docs.slack.dev/reference/methods/chat.postMessage/ and https://docs.slack.dev/apis/web-api/rate-limits
   - publisher: Slack (official docs)
   - pub_date: undated (live docs)
   - accessed: 2026-10-10
   - confidence: med (search-summary of the official pages, not fetched; version claims need re-check)
   - class: official doc

5. Claim: Microsoft Teams Office 365 Connector webhooks were retired. Microsoft's notice MC1181996 (updated 2026-04-15) says connector webhooks must move to Workflows (Power Automate) before 2026-05-18. Another vendor page says support ended 2026-04-30. Legacy URLs reportedly return 401. Workflows webhooks accept MessageCard payloads without buttons, support shared channels, and added private channels in April 2026. Bot name/icon customization is not available for Adaptive Cards via webhook.
   - source: https://mc.merill.net/message/MC1181996
   - publisher: Microsoft Message Center mirror (mc.merill.net); also patchmypc.com and Coralogix docs
   - pub_date: 2026-04-15
   - accessed: 2026-10-10
   - confidence: med (search-summary; the two dates conflict)
   - class: official notice via mirror

6. Claim: Workflow engine trade-off. Temporal's own approval guide says one workflow can hold approval state, wait without consuming compute, use durable timers for reminders and escalation, and keep an audit record at every step. Airwallex used Temporal for an approval system and reported flexibility and easy failure handling, but integration challenges.
   - source: https://docs.temporal.io/guides/reliable-document-approvals and https://temporal.io/in-use/interactive-business-process-with-temporal
   - publisher: Temporal (vendor)
   - pub_date: undated
   - accessed: 2026-10-10
   - confidence: low-med (search-summary, vendor advocacy)
   - class: vendor advocacy

7. Claim: Temporal has real operating overhead. Self-hosting needs a database, metrics and workers. Temporal Cloud bills by actions plus storage. Deterministic workflow code is "foreign", and new team members often write non-deterministic code that breaks on replay. It suits teams with a platform engineer. For 2-to-5-person teams the author suggests Inngest or Vercel Workflow instead.
   - source: https://dev.to/alexcloudstar/temporal-vs-inngest-vs-vercel-workflow-in-2026-picking-a-durable-engine-2geo
   - publisher: DEV Community (Alex Cloudstar, individual blogger)
   - pub_date: "Apr 25", 2026 inferred from the title; year not shown on the page
   - accessed: 2026-10-10
   - confidence: med (fetched; opinion piece, no production numbers)
   - class: practitioner opinion

8. Claim: A consultancy case (Spiralscout) reports that without a clear decomposition model, inconsistencies in a Temporal system compound and become costly to unwind once several people contribute. Single source.
   - source: https://spiralscout.com/case/temporal-workflow-architecture-consulting-enterprise
   - publisher: Spiralscout (consultancy marketing)
   - pub_date: undated
   - accessed: 2026-10-10
   - confidence: low
   - class: anecdote

9. Claim: Accounting corrections are appended, not edited. Voiding appends the exact opposite rows, so both stay visible. Accounting (effective) date is separate from entry date, so a correction can post to the period it belongs to. Read views are derived and rebuildable from the journal. FOCUS billing spec lists three correction styles (replacement, delta append, ledger append); ledger append gives full auditability at the cost of data growth. Business Central allows an entry to be reversed only once.
   - source: https://focus.finops.org/docs/specification/v1-4/attributes/correction-handling/ and https://learn.microsoft.com/en-gb/training/modules/create-process-journal-entries-dynamics-365-business-central/4-reverse and https://docs.go.aiinsurance.io/financials/accounting-model/overview
   - publisher: FinOps Foundation (Linux Foundation); Microsoft Learn; an insurance-accounting vendor
   - pub_date: undated
   - accessed: 2026-10-10
   - confidence: med (search-summary of official docs)
   - class: official doc and spec. Nothing here is payroll-specific.

10. Claim: Operational pain with reversals. A Sage 50 user thread shows a reversed, previously reconciled entry caused a $10k discrepancy. Corrections are hidden by default in the UI, so the reversal was mistaken for a real entry. The suggested practice is to match corrections first. A forum thread notes that prior-period-error rules can require retrospective correction, in tension with strict append-only.
    - source: https://communityhub.sage.com/ca/sage_50/f/reconciliation-deposits-and-banking/248837/correction-journal-entry-disappeared/599137 and https://discuss.frappe.io/t/discussion-immutable-ledger/31153/53
    - publisher: Sage community hub; Frappe forum
    - pub_date: undated
    - accessed: 2026-10-10
    - confidence: low (search-summary)
    - class: anecdote (user support threads)

11. Claim: Practical synthesis, not a sourced claim. For a linear draft, submitted, approved/rejected flow, evidence in items 6 to 8 points to a status column plus a transition table plus an audit table in the app database, with a workflow engine only if multi-day durable timers or cross-service orchestration are needed. The search found no head-to-head small-team report; this is inference from vendor and blog sources.
    - confidence: low
    - class: inference

## Leads (not fetched)
- https://docs.temporal.io/guides/reliable-document-approvals (fetch it for the timer and reminder design)
- https://www.suprsend.com/post/delayed-notifications-without-cron (polling granularity, limits of cron plus DB polling)
- https://oneuptime.com/blog/post/2026-09-14-cron-stable-business-key-side-effects/view (stable business key for cron side effects)
- https://focus.finops.org/docs/specification/v1-4/attributes/correction-handling/ (verify the three correction styles by fetch)
- https://mc.merill.net/message/MC1181996 (resolve the 05-18 vs 04-30 date conflict)
- https://discuss.frappe.io/t/discussion-immutable-ledger/31153/53 (ERPNext immutable-ledger debate)
- Kubernetes CronJob docs (duplicate or missed runs)

## Looked for and could not find
- Production post-mortems of event-sourced or append-only ledger failures. The query returned only product docs and forum threads.
- Payroll-specific practice (retro pay, off-cycle adjustments after period close). Not reached in round 1.
- Bitemporal or temporal-table trade-offs from practitioners (SQL Server system-versioned, Postgres). Not searched in round 1.
- Small-team reports comparing Temporal, Camunda or Step Functions against a DB state machine. Only vendor and blog opinion found.
- Per-project reviewer routing and timesheet-specific cut-off or period-close scheduling patterns. Not searched in round 1.
- Email provider rate limits (SES, SendGrid, Postmark) and Teams bot limits. Not searched in round 1.
