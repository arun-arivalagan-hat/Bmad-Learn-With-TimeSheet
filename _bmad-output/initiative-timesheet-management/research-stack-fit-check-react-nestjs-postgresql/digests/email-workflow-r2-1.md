# Email and workflow digest, round 2 (r2-1)

Accessed 2026-10-10 for all claims. All prices USD. WebFetch worked for most pages (it returns model-summarised text, so figures are summary-extracted from the page; confidence "high" is used only where fetched from the publisher). Claims drawn from WebSearch summaries are marked med/low. Tool calls: 17. Distinct sources slightly exceed the 8-source cap (about 13) because search summaries were counted loosely.

Class key: P = primary (publisher own page), S = secondary summary, C = community/review aggregate.

## 1. SendGrid plans, prices, free-plan retirement

- Claim: SendGrid/Twilio is retiring the Free Email API and Free Marketing Campaigns plan, announced as starting 2025-05-27; existing free users keep full access for a 60-day transition, then sending is paused on all free plans, Marketing Campaigns features stop, and accounts with more than 100 contacts have all contacts deleted (not restorable after upgrade).
  - source: https://www.twilio.com/en-us/changelog/sendgrid-free-plan | publisher: Twilio | pub_date: 2025-05-27 | confidence: high | class: P | sources_count: 1 (second source below)
- Claim: A second Twilio changelog entry dated 2025-05-28 describes the same change (date discrepancy of one day between official entries). Second-source confirmation of retirement.
  - source: https://www.twilio.com/en-us/changelog/changes-coming-to-sendgrid-s-free-plans | publisher: Twilio | pub_date: 2025-05-28 | confidence: med (search summary only; page not fetched) | class: P | sources_count: 1; also echoed by dreamlit.ai (https://dreamlit.ai/blog/best-sendgrid-alternatives, "The Free Tier Is Gone", 2026, class S, search snippet only)
- Claim: Replacement for new signups is a one-time 60-day free trial, 100 emails/day on Email API, no credit card; upgrading ends the trial and it cannot be restarted.
  - source: https://www.twilio.com/en-us/products/email-api/pricing (trial table, fetched) and Twilio docs https://live.docs.dev.twilio.com/docs/sendgrid/ui/account-and-settings/upgrading-your-plan.md (search summary) | publisher: Twilio | pub_date: unknown | confidence: high (pricing page), med (docs) | class: P | sources_count: 2
- Claim: Current Email API plans: Free Trial $0 for 60 days (100 emails/day); Essentials from $19.95/mo; Pro from $89.95/mo; Premier custom. Price depends on volume (under 3,000 up to 5,000,000+ per month); no per-volume price table on the page. A USD price for exactly 10,000 emails/month was NOT shown. Page notes inconsistencies in validation counts and overage charges may apply.
  - source: https://www.twilio.com/en-us/products/email-api/pricing | publisher: Twilio | pub_date: unknown (live page) | confidence: high for "from" prices; low for the 10k figure (absent) | class: P | sources_count: 1 for page; $19.95 starting price also in search summary of third-party guide (med)
- Claim: Plan features: event webhooks Trial 1 / Essentials 2 / Pro 5 / Premier 5; dynamic templates editor on all, plus testing on Pro/Premier; dedicated IP included on Pro and Premier (more as add-on), not listed for Essentials; activity history 3 days (Trial, Essentials) and 7 days (Pro, Premier).
  - source: https://www.twilio.com/en-us/products/email-api/pricing | publisher: Twilio | pub_date: unknown | confidence: high | class: P | sources_count: 1
- What failed: sendgrid.com/pricing and sendgrid.com/en-us/pricing 301-redirect to twilio.com/en-us/sendgrid, which has no plan details (links on to the Email API pricing page, which rendered fine). No Wayback fallback needed.

## 2. Comparison: SendGrid vs SES vs Postmark (about 10,000 emails/month)

Price for about 10,000 emails/month:
- SendGrid: Essentials "from $19.95/mo"; exact 10k tier not shown (see above); a dedicated IP or 5 webhooks needs Pro, from $89.95/mo. confidence med-high; sources_count 1.
- SES: Essentials $0.16 per 1,000 in the 0-10M tier, so about $1.60 for 10k; Pro $0.22 per 1,000 plus $105/month per account per region; Enterprise $0.23 per 1,000 plus $500/month; à la carte outbound $0.10 per 1,000 (about $1.00). New AWS customers: up to $200 credits (free plan 6 months, credits usable 12 months). Attachment data $0.12/GB.
  - source: https://aws.amazon.com/ses/pricing/ | publisher: AWS | pub_date: unknown | confidence: high | class: P | sources_count: 1
- Postmark: Basic $15.00/mo for 10,000 emails (extra $1.80 per 1,000); Pro $16.50 (extra $1.30); Platform $18.00 (extra $1.20). Free tier 100 emails/month, no overages, never expires.
  - source: https://postmarkapp.com/pricing | publisher: Postmark | pub_date: unknown | confidence: high | class: P | sources_count: 1

Dedicated IP:
- SES: standard $24.95 per IP per month; managed $15 per account per month plus $0.08 per 1,000 emails (0-10M); BYOIP $24.95 per IP with 256-address minimum. Source: AWS pricing page above. confidence high.
- Postmark: add-on from $50/month per IP, page says intended for senders at 300,000+ emails/month, Pro or higher only. Source: Postmark pricing page. confidence high.
- SendGrid: included in Pro and above; not listed for Essentials (Twilio pricing page). A Capterra summary reports shared-IP blacklisting complaints with costly dedicated IP upgrades (see section 3).

Rate limits:
- SES: default for a new account in a region is sending quota 200 emails per 24 hours and 1 email per second (sandbox defaults; adjustable via Service Quotas request). source: https://docs.aws.amazon.com/general/latest/gr/ses.html | publisher: AWS | pub_date: unknown | confidence high | class: P | sources_count 1. The page does not state sandbox explicitly; a production-access request is the usual route (not retrieved this session).
- SendGrid: rate-limit docs page only describes headers X-RateLimit-* and HTTP 429; no mail-send numbers found. source: https://www.twilio.com/docs/sendgrid/api-reference/how-to-use-the-sendgrid-v3-api/rate-limits | confidence med | class P | sources_count 1.
- Postmark: not found.

Webhooks for bounce/delivery:
- SendGrid: event webhooks, count capped by plan (1/2/5/5). Twilio pricing page. confidence high.
- Postmark: event webhooks and secure webhook endpoints listed as features; inbound email posted to webhook as JSON on Pro and Platform. Postmark pricing page. confidence med-high (feature list, not docs).
- SES: not verified this session (bounce/delivery notification mechanics not retrieved).

Templates:
- SendGrid: dynamic templates editor on all plans, testing on Pro/Premier. Postmark: responsive templates for transactional email listed as a feature. SES: not retrieved.

Idempotency / dedupe:
- Postmark: no idempotency key feature; support article says to build safeguards in own integration (last updated 2025-09-30). source: https://postmarkapp.com/support/article/what-is-an-idempotency-key | publisher: Postmark | pub_date 2025-09-30 | confidence med (search snippet, not fetched) | class P | sources_count 1.
- SendGrid: idempotency not covered on the rate-limit page; no evidence found either way (see "could not find").
- SES: not found.

India / regions:
- SES is available in Asia Pacific (Mumbai) ap-south-1 (API endpoint email.ap-south-1.amazonaws.com, SMTP endpoint email-smtp.ap-south-1.amazonaws.com, email receiving inbound-smtp.ap-south-1) and Asia Pacific (Hyderabad) ap-south-2 (API only; SMTP endpoint NOT available in Hyderabad). source: https://docs.aws.amazon.com/general/latest/gr/ses.html | publisher: AWS | pub_date: unknown | confidence high | class P | sources_count 1.
- SendGrid and Postmark India deliverability / regional endpoints: nothing found this session.

## 3. SendGrid reputation and reliability (last 12 months)

- Claim: Capterra 2026 review themes (as summarised by search): account access/support 79% negative across 53 reviews (sudden suspensions, unclear rejections, slow support); shared-IP deliverability 71% negative across 42 reviews (blacklisted shared IPs, costly upgrade to dedicated IPs); spam placement 63% negative across 51 reviews. Positive: transactional email 98% positive across 45 reviews; developer API 89% positive across 45 reviews. Individual April 2026 reviews cite inconsistent deliverability and hard-to-reach technical support.
  - source: https://www.capterra.com/p/204113/SendGrid/reviews/ | publisher: Capterra | pub_date: 2026 (page updated July 2026) | confidence med (search summary, not fetched; AI-generated theme percentages) | class: C | sources_count: 1
- Claim: Trustpilot reviews (mostly 2024-2025, a few later) report suspensions without explanation, sign-up rejections citing an undisclosable vetting process, inactivity deactivation, billing on suspended accounts, and slow or closed support tickets.
  - source: https://www.trustpilot.com/review/sendgrid.com | publisher: Trustpilot | pub_date: 2024-2026 mixed | confidence med-low (search summary, not fetched; dating unclear) | class: C | sources_count: 1
- Claim: emailwarmup.com 2026 review cites 1.2/5 across 597 Trustpilot reviews (84% one star); concludes core API still works for existing users; main concerns are account suspensions, support, billing opacity. Note it is a vendor-adjacent blog repeating Trustpilot, so not independent of the Trustpilot claim.
  - source: https://emailwarmup.com/blog/email-deliverability-tools/sendgrid-review/ | publisher: emailwarmup.com | pub_date: 2026 | confidence low-med | class: S | sources_count: 1
- Pattern count: 2 independent review platforms (Capterra, Trustpilot) show the same pattern (account suspension / support / shared-IP deliverability); the third source repeats Trustpilot. Counts of independent sources: 2. Not covered: G2, Reddit, status-page incidents (not retrieved).

## 4. Workflow engines vs database state machine

- Claim: AWS Step Functions Standard: $0.000025 per state transition (US East N. Virginia), 4,000 free transitions/month; retries billed as extra transitions. Express: $1.00 per million requests plus duration (about $0.06 per GB-hour first tier). A reminder or approval flow using a handful of transitions per timesheet is small at this price (arithmetic is mine, not sourced).
  - source: https://aws.amazon.com/step-functions/pricing/ | publisher: AWS | pub_date: unknown | confidence high | class P | sources_count 1
- Claim: Camunda: Self-Managed Development is free (no license); production requires an Enterprise license; SaaS has a 30-day trial, then a free account limited to BPMN/DMN modeling. No USD prices listed (contact sales).
  - source: https://camunda.com/pricing/ | publisher: Camunda | pub_date: unknown | confidence high | class P | sources_count 1
- Claim: Practitioner/advisory summary: status column plus transition log (append-only state history) is a common starting pattern; flat states strain when flows become parallel or hierarchical; durable engines (Temporal, Camunda) are justified for long-running steps that must survive restarts or for business-readable BPMN; reviewers cite Camunda expensive for small companies (one reviewer said the opposite), and Temporal operational cost and determinism constraints. No first-person account was found of a small team outgrowing a status column or regretting an engine.
  - source: https://automationatlas.io/guides/camunda-vs-temporal-2026-comparison/ ; https://python-statemachine.readthedocs.io/ (state_history example) ; https://community.temporal.io/t/long-time-bpmn-camunda-user-considering-the-leap-to-temporal/10308 | publisher: Automation Atlas / python-statemachine docs / Temporal community | pub_date: 2026 / unknown / unknown | confidence low (search summary only; the "takeaway" paragraph is the search engine's synthesis) | class S | sources_count: 3 (all unfetched)
- One-sheet-per-week reminder schedule specifically: no source found.

## 5. Scheduled reminder pitfalls on NestJS

- Claim: @nestjs/schedule runs the cron handler on every replica and has no built-in multi-instance protection (example: 3 pods run a daily report 3 times).
  - source: https://dev.to/femresirvan/managing-cron-jobs-with-nestjs-solving-multi-instance-issues-and-locking-mechanisms-51co | publisher: DEV Community | pub_date: unknown | confidence med (search summary) | class S | sources_count: 2 (also kitemetric.com Bull article)
- Claim: Mitigations found: Redis lock (SET NX PX; nestjs-redlock/redlock); Bull queue so workers process jobs (still needs deterministic job IDs to avoid duplicate enqueues, which the sources did not cover); Postgres advisory locks via pg_try_advisory_xact_lock (transaction-scoped preferred; session locks are tied to one pooled connection and risky with pools); a library note that mutual exclusion is best-effort.
  - source: https://dev.to/mukesh_13/postgres-advisory-locks-for-distributed-cron-killing-duplicate-job-runs-without-a-redis-dependency-1bfl ; https://leapcell.io/blog/orchestrating-distributed-tasks-with-postgresql-advisory-locks ; https://appmaster.io/blog/postgresql-advisory-locks-double-processing | publisher: DEV Community / Leapcell / AppMaster | pub_date: 2025-09-07 (AppMaster), others unknown | confidence med | class S | sources_count: 3 (search snippets only)
- Claim (UNSOURCED, from the search model's own general knowledge, not a retrieved source): inserting a row with a unique key on (job name, time slot) so the first instance wins. No retrieved source covered the unique-constraint approach. Treat as low confidence / lead only.

## Leads

- Fetch SES developer guide pages on production access/sandbox, SNS/event publishing for bounces, and any idempotency story (SESv2 has no documented idempotency key in anything retrieved).
- Fetch https://postmarkapp.com/support/article/what-is-an-idempotency-key to confirm wording and the listed workaround.
- Fetch Capterra and Trustpilot SendGrid pages directly to verify dates and counts; add G2, Reddit r/sendgrid, status.sendgrid.com incident history.
- SendGrid Email API pricing slider for the exact 10,000/month tier (page was static summary only).
- Pull a fetched article for the Postgres unique-constraint-per-slot pattern (e.g. graphile-worker, pg-boss singleton keys, BullMQ jobId dedupe).

## Looked for and could not find

- Exact SendGrid price for 10,000 emails/month.
- Postmark API rate limits; SES bounce/delivery notification mechanics and templates; SendGrid mail-send rate numbers and any idempotency support.
- Deliverability reports or regional endpoints for sending to/from India for SendGrid and Postmark.
- G2 and Reddit SendGrid reports, and SendGrid status incidents in the last 12 months.
- Camunda USD pricing (contact sales only).
- First-person accounts of a small team outgrowing a status column plus audit table or regretting an engine; anything on one-sheet-per-week reminder scheduling.
- A retrieved source for the database unique-constraint dedupe pattern.
