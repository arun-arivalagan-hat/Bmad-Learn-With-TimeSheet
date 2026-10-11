# Pain and behavior, round 2, digest 1

Method note: WebSearch and WebFetch both worked. Most claims below come from WebSearch result summaries (not full page reads), so they are medium or low confidence. Only two pages were fetched in full (apps365, Gramener). No review page or forum thread was fetched directly. Accessed 2026-10-10 for all.

## Findings

1. Claim: Harvest reviews on Capterra (4.6 average, 646 reviews as of Mar 2026) rarely complain about entry effort. Recurring cons are reporting, integrations (QuickBooks), limited customization/scale, price. Single mentions: a non-admin user cannot see a personal time summary without adding up manually; offline limits; the timer failing to save on a poor connection.
   - Source: https://www.capterra.com/p/75598/Harvest/reviews/ | Publisher: Capterra | pub_date: 2026 (page title "Reviews 2026") | confidence: med (search summary only; the cons are scattered rather than a clear pattern; high-rated product, so the 1-3 star view is not isolated) | class: vendor-review-aggregator, user-voice
2. Claim: Replicon reviewers consistently praise multi-level approval workflows. Mobile is split: negative (a 2023 review calls mobile deployment poor and slow; a 2019 review reports login trouble) versus positive (2024-2026 reviews say it is "super easy to track time on the go when I forget at my desk"). Other cons: setup and learning curve, sluggishness, hard to find job numbers, limited customization.
   - Source: https://www.capterra.co.uk/reviews/5782/replicon-timebill (also getapp.ca/reviews/1282/replicon-timebill, actitime.com/software-collections/replicon-review) | Publisher: Capterra UK / GetApp | pub_date: 2019-2026 mixed | confidence: med-low (search summary; reviews are individual and the older ones may be stale) | class: vendor-review-aggregator, user-voice
3. Claim: A marketing agency reported 85% timesheet compliance after adopting timezone-aware daily reminders (email, push, in-app), next-day auto follow-up for missed logs, and weekly recap emails showing logged and unlogged hours. No baseline is given, and it is a vendor-published case study of the vendor's own product.
   - Source: https://www.apps365.com/case-studies/marketing-agency-timesheet-reminders/ | Publisher: Apps365 (Time Tracker 365) | pub_date: 2025-06-18 (modified 2026-03-18) | confidence: low-med (fetched in full, but vendor marketing with no baseline) | class: vendor-case-study
4. Claim: Blind thread on hating weekly status updates/timesheets: commenters call it performative busywork "to justify existence". This is one thread, so it is a weak pattern.
   - Source: https://www.teamblind.com/post/does-anyone-else-hate-writing-weekly-status-updates-timesheets-spend-more-time-explaining-work-than-doing-it-by44e92m | Publisher: Blind | pub_date: unknown | confidence: low (search summary only) | class: forum, user-voice
5. Claim: Float's guidance says people see timesheets as busy work, that the simplest fix is to make logging so easy no reminders are needed, and that managers should explain the benefits (productivity, blockers, correct pay). This is vendor opinion, not evidence.
   - Source: https://float.com/resources/timesheet-reminder | Publisher: Float | pub_date: unknown | confidence: low | class: vendor-blog
6. Claim: A 2019 comment on an employee blog says filling a week takes about 10 minutes, calls it "the most struggling 10 minutes of my week", and says cloning or Excel upload copies tasks but not hours, so entering hours stays tedious. The commenter had 80 pending hours. This is a single anecdote.
   - Source: https://blog.gramener.com/state-of-timesheets-and-why-i-fill-them/amp/ | Publisher: Gramener blog (comment) | pub_date: ~2019-03 (comment dated 25/03/2019; "8 years ago") | confidence: low (single anecdote; fetched in full) | class: employee-blog-comment, older
7. Claim: Cost figures for late or erroneous timesheets are cited secondhand by vendors. EY 2022: about $250k per 1,000 employees per year in time-and-attendance errors; another blog cites $291 per payroll error correction, 15 per pay period. The originals were not located.
   - Source: https://imagetotable.ai/blog/month-end-timesheet-processing-payroll-close (via search summary); also https://www.joinhomebase.com/blog/timesheet-reminders | Publisher: vendor blogs citing EY | pub_date: 2022 data | confidence: low (secondhand; contradictory framings) | class: secondhand-stat
8. Claim: Undated roundup figures: 38% of US companies still use paper timesheets or punch cards; Deloitte (attributed) says 50% of professionals without automated tracking find manual data entry and adjustment the most time-consuming part. Underlying year unknown.
   - Source: search summary for the "late timesheets survey" query; the roundup URL was not pinned down (https://www.humanresourcesonline.net/is-lateness-a-problem-in-your-office was returned, but it is an AIA whitepaper on lateness, not this stat) | pub_date: updated Oct 2025 per the summary | confidence: low | class: secondhand-stat
9. Claim: Legal constraint relevant to approval and lateness features: under the FLSA an employer can discipline late submission but cannot delay wage payment. Connecticut forbids withholding pay for late time sheets. This limits "hard lock" enforcement features.
   - Source: https://www.cbia.com/news/hr-safety/hr-hotline-time-sheets-late-no-pay | Publisher: CBIA | pub_date: unknown | confidence: low-med (search summary) | class: legal-guidance, US-only

## Pattern counts (independent sources)
- Entry effort and tedium as a pain: 3 weak sources (Gramener comment, Blind, Float opinion). No review-site evidence either way.
- Reminders improve compliance: 1 vendor case study (apps365) only.
- Mobile is useful for catching forgotten entries: 1 source (Replicon reviews); mobile quality is split.
- Approval workflows are a strength in enterprise tools (Replicon): 1 source.

## Leads
- Capterra Harvest reviews, filtered to 1-3 stars: https://www.capterra.com/p/75598/Harvest/reviews/?page=10 through page=25 (page-numbered; worth fetching and filtering by rating).
- Capterra Replicon individual review: https://www.capterra.com/p/5782/Replicon-TimeBill/reviews/4815824/
- Vendor blogs likely to cite primary stats on late timesheets: https://www.memtime.com/blog/late-timesheets-problems, https://www.ontheclock.com/blog/late-timesheets, https://www.clicktime.com/blog/how-to-get-employees-to-complete-timesheets, https://clockify.me/timesheets-questions-answered
- EY 2022 payroll error study (original) and Deloitte manual-entry stat (original); neither was located.
- Reddit and Hacker News threads via direct fetch, for example Reddit search URLs for r/projectmanagement and r/consulting (may be blocked).

## Looked for and could not find
- 1-3 star review text for Clockify, Toggl, Deltek, Zoho People, Workday time tracking, and G2, Trustpilot, Software Advice or app-store pages. Only Harvest and Replicon summaries via Capterra were surfaced, and they were not filtered by star rating.
- Any Reddit thread (r/sysadmin, r/projectmanagement, r/consulting, r/ExperiencedDevs) or Hacker News thread on hating or forgetting timesheets. Search returned none; one Blind thread appeared.
- Any independent survey or study from the last 2 years with numbers on late timesheets, time spent filling them, or approval delays. Only vendor-cited secondhand statistics (EY 2022, Deloitte, undated) and one vendor case study turned up.
- Reviews complaining specifically about rejections or reminder annoyance.
