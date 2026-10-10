# Digest workflow-email-r1-1 (accessed 2026-10-10)

Notes: WebFetch worked, but it returns a small-model summary of each page, so claims are single-pass summaries. Currency for all prices is shown only as "$" and is not stated explicitly (assumed USD, not confirmed). pub_date is "unknown" where a page shows none. Class: V = vendor primary, S = search summary of third party, D = vendor docs.

## Claims

1. Amazon SES outbound is $0.10 per 1,000 emails (a la carte). Plan tiers: Essentials $0.16, Pro $0.22, Enterprise $0.23 per 1,000.
   - source: https://aws.amazon.com/ses/pricing/ | publisher: AWS | pub_date: unknown | confidence: med | class: V | sources_count: 1
2. SES has no perpetual free tier. New customers get up to $200 in AWS Free Tier credits. The free plan lasts 6 months and credits must be used within 12 months.
   - source: https://aws.amazon.com/ses/pricing/ | AWS | unknown | med | V | 1
3. SES change: new accounts, and account-region combinations with no metered SES activity since 2025-06-01, "will start on the Essentials plan beginning July 21, 2026". Upgrades are immediate. Most downgrades take effect next billing cycle. Re-verify the plan semantics.
   - source: https://aws.amazon.com/ses/pricing/ | AWS | unknown | med | V | 1
4. SES dedicated IPs: Standard is $24.95/month per IP. Managed is $15/month per account plus $0.08 per 1,000 emails. BYOIP is $24.95 per IP with a 256-address minimum.
   - source: https://aws.amazon.com/ses/pricing/ | AWS | unknown | med | V | 1
5. SES quotas: the sandbox allows 200 emails per 24h and 1 email per second. Out of sandbox, quotas depend on the use case and can be raised. Max 50 recipients per message. Max message size 40 MB (v2 API/SMTP). Up to 10 event destinations per configuration set. Templates: 20,000 per region, 500 KB each. Quotas are per region.
   - source: https://docs.aws.amazon.com/ses/latest/dg/quotas.html | AWS | unknown | high | D | 1
6. Postmark pricing (USD): Free is 100 emails/month with 45-day retention, and there is no tier between 100 and 10,000. Basic is $15/month for 10,000 emails (overage $1.80 per 1,000). Pro is $16.50 (overage $1.30). Platform is $18 (overage $1.20). Dedicated IP starts at $50/month and is available only for senders of 300,000+ emails/month on Pro or higher. Templates are included on all plans. Transactional and broadcast mail use separate message streams.
   - source: https://postmarkapp.com/pricing | Postmark (ActiveCampaign) | unknown | med | V | 1
   - Caveat: the Basic/Pro/Platform prices look oddly close together, so verify them on the live page.
7. Postmark does not support idempotency keys. Its support center says to build safeguards into your own integration. Other providers (Resend, Lettermint, MailPace, etc.) do support them, with a 24h window.
   - source: https://postmarkapp.com/support/article/what-is-an-idempotency-key (surfaced via search, content not fetched directly) | Postmark | unknown | med | S | 1
8. SendGrid retired its Free Email API and Free Marketing Campaigns plans, announced 2025-05-28. Existing free users kept access for 60 days. After that, sending is paused on free plans, Marketing Campaign features end, and accounts with more than 100 contacts have contacts deleted (not restorable). Paid plans are unaffected. The changelog gives no explicit end date. New accounts get a free trial, "no credit card required" (Twilio SendGrid page).
   - source: https://www.twilio.com/en-us/changelog/changes-coming-to-sendgrid-s-free-plans | Twilio | 2025-05-28 | high | V | 2 (changelog fetched, plus search summary of a second changelog entry and third-party posts)
9. The new-account SendGrid trial is reported as 60 days at 100 emails/day via API/SMTP, with sending stopping at the end. This comes from a third-party summary, not the vendor page.
   - source: search summary citing https://www.usecarly.com/blog/sendgrid-pricing/ and a Bubble forum PSA (https://forum.bubble.io/t/psa-sendgrid-ending-their-free-tier-plan/374463) | usecarly / Bubble forum | unknown | low | S | 2
10. Reported SendGrid paid pricing: Essentials from $19.95/month (50k-100k emails) and Pro from $89.95/month. This is third-party only. The vendor pricing page could not be read: sendgrid.com/pricing and twilio.com/en-us/sendgrid/pricing loop through redirects, and the main Twilio page shows no prices.
    - source: https://www.usecarly.com/blog/sendgrid-pricing/ (via search summary) | usecarly | 2026 (per summary) | low | S | 1
11. SendGrid reputation, last 12 months. Capterra 2026 reviews are mostly critical of account management: sudden suspensions, slow support, shared-IP blacklisting. Transactional delivery gets better marks. EmailWarmup (2026) rates it 2.5/5 and cites 95.5% delivery and 91.3% inbox placement. EmailWarmup sells deliverability tools, so it is a conflicted source. Independent sources: 2 (Capterra review aggregate, EmailWarmup). One more blog (emaillistvalidation.com) only says a single complaint can trigger throttling. No official statement was found.
    - source: https://www.capterra.com/p/204113/SendGrid/reviews/ ; https://emailwarmup.com/blog/email-deliverability-tools/sendgrid-review/ | Capterra / EmailWarmup | 2026 | low-med | S | 2
12. Temporal Cloud (pay-as-you-go): $50 per million actions, dropping to $25 at higher volume. No minimums. $150 in credits for 90 days. Business add-on from $500/month or 10% of usage. The page does not mention self-hosting.
    - source: https://temporal.io/pricing | Temporal | unknown | med | V | 1
13. Temporal docs: a workflow waiting on a human decision consumes no worker compute, and its state is persisted. Event history has a hard limit of 51,200 events or 50 MB. An Airwallex talk reports integration challenges coordinating signals and queries for synchronous user requests.
    - source: https://docs.temporal.io/guides/reliable-document-approvals ; https://temporal.io/in-use/interactive-business-process-with-temporal | Temporal | unknown | med | S | 2 (same vendor; vendor-authored)
14. EventBridge Scheduler: supports cron, rate and one-time `at()` schedules with an IANA time zone (UTC by default). Precision is 60 seconds without a flexible window. DST handling: a spring-forward skips a non-existent time, and fall-back runs once. UTC schedules are not DST-adjusted. One-time schedules still count against quota after they run, so delete them.
    - source: https://docs.aws.amazon.com/scheduler/latest/UserGuide/schedule-types.html | AWS | unknown | high | D | 1
15. NestJS @nestjs/schedule: `@Cron()` has a `timeZone` option. The scheduler "runs every job in every process", so 3 instances means 3 runs. The docs name `@OnOneInstance()` from `@nestjs/locks` (shared PostgreSQL or Redis lock) and `@WithoutOverlapping()`. `ScheduleModule.forRoot()` should be imported once.
    - source: https://docs.nestjs.com/techniques/task-scheduling | NestJS | unknown | med (the `@nestjs/locks` detail is new to me, so confirm it exists) | D | 1
16. BullMQ: a custom jobId dedupes while the job exists in the queue. Once a job is removed (removeOnComplete/removeOnFail), the ID can be reused, so it is not a durable idempotency guard. IDs cannot contain ":" or be all digits.
    - source: https://docs.bullmq.io/guide/jobs/job-ids | BullMQ | unknown | high | D | 1
17. Synthesis (not sourced): a DB-level unique key on (employee, reminder_kind, week) written before or atomically with the send gives true idempotency regardless of the scheduler. Sending is at-least-once across a send and a crash, so the dedupe is best-effort.

## Leads
- A direct comparison of DB state machine vs a workflow engine for small teams: the search returned only Temporal-authored sources. Look for independent post-mortems.
- Step Functions and Camunda were not researched (budget).
- SES and SendGrid idempotency: no source found. SendGrid Mail Send API has no documented idempotency key (not verified).
- SendGrid docs for rate limits, webhooks (Event Webhook, signed), templates, Deliverability tooling, and dedicated IP price: not read.
- SES event publishing via SNS/EventBridge configuration sets, the SES account-level suppression list, and SES India/Mumbai region availability: not read.
- Postmark webhooks, rate limits and bounce handling: not read.
- Bubble forum PSA and Twilio changelog (sendgrid-free-plan): confirm the exact end date of the free plan.

## Looked for and could not find
- SendGrid current price, currency and trial terms from the vendor page (redirect loop).
- Explicit currency on any pricing page.
- Pricing page publication or update dates.
- Any official SendGrid statement on suspensions or reliability in the last 12 months; no independent incident data (status history) was retrieved.
- India-specific sending considerations (DLT is SMS-only; email rules, regional endpoints, data residency): not searched.
- SendGrid, SES and Postmark per-second rate limits for the default plan (SES partially covered).
- Any real-world report from teams comparing Temporal vs DB state for timesheet-like workflows.
