# Digest hr-appraisal-r1-1 (user-voice: HR/ops timesheet pain; timesheet compliance vs appraisal)
Accessed 2026-10-11. One round, 8 searches + 2 fetches. Not legal advice.
Tool status: WebSearch worked (summaries only; site: operator ignored). WebFetch worked for the Reddit mirror; BLOCKED (HTTP 403) for the Fishbowl page. Claims from search summaries are medium/low.

## Claims

1. Claim: Missed timesheets (called DTE) at a large professional-services firm notify the approver and coach each time; repeated misses affect year-end review and bonus (AIP) payout. Described as an employee-forum account of policy (de facto official, not quoted from a policy document).
   - Quotes: "It will affect your year end review and AIP payout." / "A few won't matter, a bunch will start affecting your year end bonuses." / "Each time you miss, the approver for that timesheet and your coach will be notified."
   - Community: Reddit, company-specific subreddit (mirror snapshot)
   - Source: https://reddit.sentinel-team.org/posts/1pmlzzz/snapshots/2025-12-15T16%3A31%3A27.18579Z
   - Publisher: Reddit Sentiment Analyzer (mirror of a Reddit thread)
   - Date: post approx mid-Feb 2025 (OLDER than 18 months); snapshot 2025-12-15
   - Confidence: high (page fetched)
   - Class: official-policy-as-reported + bonus/rating link (US-style firm, not Indian IT)
   - distinct_voices: 3 of 7 commenters link misses to review/bonus; communities: 1

2. Claim: Tolerance threshold is fuzzy and varies by group ("about 90% on-time", "6 permitted misses"); one commenter says colleagues were let go over non-submission (anecdote).
   - Quotes: "You are permitted 6 misses on DTE activities and then it will begin impacting your compliance" / "I have colleagues who were let go due to compliance if you don't submit your timesheet."
   - Community: same Reddit thread; source/publisher/date as claim 1
   - Confidence: med (unverified anecdote, threshold differs between commenters)
   - Class: manager/group discretion + complaint-ish advice
   - distinct_voices: 3 (threshold), 1 (let go); communities: 1

3. Claim: Prompt correction of a missed sheet is viewed more favourably (advice, one voice).
   - Community: same thread. Confidence: low. distinct_voices: 1; communities: 1

4. Claim: Indian IT/services: an unverified Fishbowl reply says skipped timelogs lead to salary being held ("if you skip timelogs they will hold your salary"). Poster was a recent joiner who filled on-duty but not timelog.
   - Community: Fishbowl (Indian IT employer, name omitted)
   - Source: https://www.fishbowlapp.com/post/hi-sharks-i-joined-birlasoft-recently-i-was-not-able-to-fill-timelog-but-filled-onduty-though-i-contacted-hr-but-there-is
   - Publisher: Fishbowl; date unknown
   - Confidence: low (page fetch 403; search-summary only)
   - Class: complaint / peer claim about pay hold, not appraisal rating
   - distinct_voices: 1; communities: 1

5. Claim: HR guidance says chronic non-submission is handled as a performance issue and timesheet concerns can be raised in performance reviews (vendor/HR guidance, not employee voice).
   - Source: https://www.brighthr.com/articles/time-management/timesheets/timesheets-for-performance/ (and a timesheet-compliance guide at https://help.totalsynergy.com/en/articles/15454919-timesheet-compliance)
   - Publisher: BrightHR; Total Synergy. Date unknown. Confidence: low-med (search summary only)
   - Class: vendor guidance. distinct_voices: 0 employee voices; communities: 0 forum

6. Claim: Spreadsheet-based timesheet review raises reconciliation effort and error likelihood; moving to in-month exception alerts reduces month-end work; time/attendance errors cost a vendor-cited ~$250,000 per 1,000 employees per year (unverified).
   - Source: https://imagetotable.ai/blog/month-end-timesheet-processing-payroll-close ; https://help.factorialhr.com/en_US/proactively-catch-timesheet-errors-with-alerts ; https://www.rosterelf.com/free-award-and-payroll-templates/payroll-reconciliation-excel
   - Publisher: vendors. Date unknown. Confidence: low (vendor marketing, search summary)
   - Class: vendor-claim, NOT HR-practitioner voice. distinct_voices: 0; communities: 0

7. Claim: One source notes an employer cannot withhold pay solely because a timesheet was late (jurisdiction unspecified; not legal advice). Source: search summary of a vendor glossary (hyperbots.com); confidence low.

8. Claim (context, not timesheet): Indian IT appraisals are tied to compliance in other forms, e.g. anniversary appraisals held for office-attendance non-compliance, and a low-rating/PIP developer reported appraisal stopped.
   - Source: https://www.peoplematters.in/news/compensation-benefits/tcs-halts-anniversary-appraisals-over-work-from-office-non-compliance-47935 (news, org-level, dated within ~12 months by listing; exact date not verified); Reddit r/developersIndia PIP story via news coverage (https://www.india.com/viral/reddit-tcs-it-industry-employee-performance-improvement-plan-java-developer-india-satya-nadella-ratan-tata-8267695/amp/)
   - Confidence: low-med (search summary). Class: adjacent evidence only; no timesheet link. distinct_voices: 1; communities: 1

## Patterns
- Only one fetched employee thread (1 community, 7 voices) links late timesheets to review/bonus. By the two-community rule this is a SINGLE-COMMUNITY OBSERVATION; no prevalence claim ("common"/"unusual") can be made.
- Penalty shape described: notification to approver/coach first, then threshold-based effect on year-end review/bonus; thresholds vary by group (suggests partly managerial/group discretion).
- Indian IT: only one weak, unfetched hint (salary hold), plus attendance-compliance-linked appraisal holds as an analogue.
- Words used: "compliance", "DTE", "timelog", "on-duty", "misses", "year end review", "AIP payout", "hold your salary", "let go", "PIP", "C/D band".

## Leads
- Fishbowl post (blocked); try a different fetch route or search for the same thread text.
- Reddit r/developersIndia, r/IndianWorkplace with words "timelog", "timesheet compliance", "PSA/Sapphire/Kronos" (phrases unverified).
- Glassdoor/AmbitionBox review text for "timesheet" in Cons (not reachable via search this round).

## Looked for and could not find
- Any AmbitionBox, Glassdoor, Blind, Quora, r/india, r/IndianWorkplace page about timesheets affecting hike/rating (search ignored site: filters; zero hits).
- Any employee fairness voice (late because of someone else; wrong hours manager-approved): none found.
- Any HR/payroll practitioner first-person voice on Excel/email timesheet pain: only vendor material.
- Official written policy text tying timesheets to hike: none found.
