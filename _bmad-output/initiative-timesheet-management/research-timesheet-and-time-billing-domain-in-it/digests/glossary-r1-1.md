# Glossary digest r1-1: timesheet, billing, utilization vocabulary

Accessed 2026-10-10 for all. WebFetch worked for 3 pages (marked fetched); all other claims come from WebSearch result summaries only (confidence capped at med/low). Pub dates mostly not shown on pages: "n/s" = not stated.
Class legend: V = vendor doc/help; B = vendor blog/calculator; F = forum/community; S = search-summary only.

## Claims

1. term: billable vs non-billable hours
   definition: Billable = time on work chargeable to a client under a contract/service agreement that generates revenue (client meetings, deliverables, client-tied research, client IT troubleshooting). Non-billable = necessary business tasks that cannot be invoiced directly (internal meetings, admin, training, onboarding, business development).
   source: https://www.getharvest.com/time-tracking/billable-vs-non-billable-hours | publisher: Harvest | pub_date: n/s | confidence: high (fetched) | class: B

2. term: billable utilization
   definition: Billable hours / total available hours x 100. Targets cited: 70-80% service businesses, 70-85% consulting and IT services, ~60-75% creative agencies; non-billable ideally under 20-25% for client-facing roles.
   source: https://www.getharvest.com/time-tracking/billable-utilization-vs-total-utilization | publisher: Harvest | pub_date: n/s (benchmark freshness unverified) | confidence: high for formula, med for targets (vendor, undated) | class: B

3. term: total utilization (overall/resource utilization)
   definition: Total productive hours (billable + non-billable such as admin, internal meetings, training) / total available hours x 100. No target given on the page. A 100% total can hide a billable shortfall.
   source: same Harvest URL (fetched) plus search summary | confidence: high for definition | class: B

4. term: utilization (denominator variants)
   definition: Keka PSA defines billable utilization against "hours available" (total working hours for the resource in a period) vs billable hours billed to projects, and lets admins set a target billable utilization and compare in a report. Everhour calculators: gross utilization (billable / gross hours, e.g. 160) vs net utilization (billable / (gross - PTO - holidays - unpaid leave)). Example: 160 gross, 27 PTO, 8 holiday, 100 billable = 62.5% gross, 80.0% net. Advice: label the denominator on every report.
   source: https://help.keka.com/hc/en-us/articles/39946716426513-Managing-Target-Billable-Utilization ; https://everhour.com/calculators/calculate-available-hours (family of Everhour calculator pages) | publisher: Keka; Everhour | pub_date: n/s | confidence: med (search summary) | class: V / S

5. term: utilization benchmark (alt)
   definition: Firms commonly target 70-75% billable utilization; sustained above 80% flagged as burnout risk (Boyer & Associates / search summary). Agencies 75-85% (another summary).
   source: https://www.boyerassoc.com/blog/resource-utilization-in-professional-services-why-billable-hours-are-only-half-the-story/ | publisher: Boyer & Associates | pub_date: n/s | confidence: low-med (summary only) | class: S

6. term: utilization (BQE definition)
   definition: Ratio of billable hours to total hours worked, as percent (6 of 8 hours = 75%).
   source: https://www.bqe.com/blog/utilization-vs.-realization-of-billable-time-in-bqe-core | publisher: BQE | pub_date: 2020-10-28, updated 2026-09-09 | confidence: high (fetched) | class: B/V

7. term: realization (billing realization)
   definition: Value invoiced vs the billable value of hours logged. BQE: total value invoiced / value of billed hours logged; hourly billing caps at 100%, and its worked example shows 136.27% (fixed-fee/over-billing can exceed 100%). Other sources (Karbon, Everhour, summaries): amount billed / (hours worked x standard rate); example $60,000 logged, $51,000 billed = 85%. Some firms measure on hours rather than dollars. Typical healthy range cited 85-95%, below 80% a problem; Clio 2024 law-firm average 88% (via MinuteDock).
   source: https://www.bqe.com/blog/utilization-vs.-realization-of-billable-time-in-bqe-core (fetched); https://karbonhq.com/resources/what-is-realization-rate/ ; https://everhour.com/calculators/realization-rate-vs-utilization-rate ; https://minutedock.com/academy/billable-vs-non-billable-hours | publisher: BQE; Karbon; Everhour; MinuteDock | confidence: high for BQE, med for others | class: V/B/S

8. term: "utilization realization"
   definition: Not found as a standard term. Sources treat utilization as a capacity metric (time) and realization as a value metric (money); numerator of utilization becomes the denominator of realization. A team can show strong utilization and weak realization if work is written down or discounted.
   source: search summary of the sources in claim 7 | confidence: med (absence claim) | class: S

9. term: revenue leakage (billing leakage)
   definition: Gap between work performed and revenue actually billed and collected; unbilled/underbilled time, missed time or expense entries, scope creep, pricing errors, missed rate increases, wrong discounting. Distinct from bad debt (billed but unpaid). Vendor-cited stats: unbilled work 10-20% of effort; 42% of firms affected, avg 4.3% annual revenue lost (secondary vendor citation, indicative only).
   source: https://www.accelo.com/glossary/what-is-revenue-leakage ; https://www.bigtime.net/blogs/revenue-leakage ; https://www.psohub.com/blog/how-to-calculate-revenue-leakage | publisher: Accelo; BigTime; PSOhub | pub_date: n/s | confidence: med (summary) | class: S

10. term: bench time
    definition: Period when employees are not deployed on billable work (no project demand or allocation gaps). One tool (Workstatus) computes unutilized capacity as Available Hours - Estimated Hours.
    source: https://www.saviom.com/blog/?p=20187 ; https://www.runn.io/blog/bench-time ; https://support.workstatus.io/en/article/capacity-and-bench-reports-ofndl6/ | publisher: Saviom; Runn; Workstatus | pub_date: n/s | confidence: med | class: S

11. term: rate card; bill rate vs cost rate
    definition: Certinia PSA: rate card = suggested bill rates and average cost rates per resource role, optionally by region, practice, group, account. Suggested Bill Rate = default rate charged for the role; Average Cost Rate = default internal cost for the role. Informational, used on resource requests/assignments; matched by role, start date, region, practice, group, account; a blank-key default card acts as fallback. Dated rates let bill/cost rates change over time (Beta in 2026.1). Keka reference rate cards: Bill Rate and Suggested Cost per role, with rate category (onsite/offsite).
    source: https://help.certinia.com/main/2026.1/Content/PSA/Features/RateCards/RateCardsOverview.htm ; https://help.certinia.com/main/2024.3/Content/PSA/Features/RateCards/RateCardFields.htm ; https://help.keka.com/hc/en-us/articles/39946620257041-Adding-and-managing-reference-rate-cards | publisher: Certinia; Keka | pub_date: n/s | confidence: med-high (vendor docs, via summary) | class: V

12. term: time and materials (T&M) vs fixed price vs retainer
    definition: T&M = bill actual time spent plus reimbursed materials/expenses; client bears scope risk; suits unclear scope. Fixed price = one predetermined price for defined deliverables; provider bears overrun risk; suits clear scope. Retainer = recurring (typically monthly) fee for access to a predetermined amount of time/services (managed IT, advisory). Birdview covers retainer, T&M, fixed fee invoicing in PSA.
    source: https://birdviewpsa.com/blog/automate-invoicing-psa-billing-types/ ; https://timingapp.com/blog/fixed-price-vs-time-and-material-how-to-charge-clients/ ; https://wavect.io/software-development-guide/fixed-price-vs-time-and-materials/ | publisher: Birdview; Timing; Wavect | pub_date: n/s | confidence: med (vendor blogs, summary) | class: S

13. term: timesheet states
    definition: Ruddr (entry-level): Not Submitted (gray) -> Pending Approval (yellow, multi-step progress visible) -> Approved (green) or Rejected (red, reason required, editable, resubmit). Automatic-approval projects create entries as Approved. No separate "billed" status; entries on a published invoice are locked for everyone including admins; manually approved entries locked for submitter unless permissioned. ProWorkflow (weekly, Mon-Sun, per staff): Open, Submitted, Approved, Locked; declined returns to Open; approved/locked can be unlocked. Upland PSA: Open, Submitted, Approved, Rejected. Toggl: Unsubmitted, Submitted/Pending, Approved, Rejected; approval locks, admin can revert. ServiceNow: time sheet approved when all time cards approved; reject cascades.
    source: https://help.ruddr.io/time/time-entry-status (fetched) ; https://help.proworkflow.com/en/articles/4212172-how-do-i-use-the-timesheet-approval ; https://help.uplandsoftware.com/psa/en/userguides/mobileguide/11041.htm ; https://support.toggl.com/what-do-the-different-timesheet-statuses-mean | publisher: Ruddr; ProWorkflow; Upland; Toggl | pub_date: n/s | confidence: high for Ruddr, med for rest | class: V

14. term: timesheet lock / period close; post-lock adjustments
    definition: Day.io: locked payroll period can be reopened for all or per-employee rows. STP: lock with per-user exemptions (managers can edit past timesheets) and grace days. Timegate: locked periods unlockable by admins and relocked; each lock has a transaction number; once locked AND closed it can no longer change (audit). Sage Intacct (GL, accounting analogy): locked period cannot be reopened or changed even by adjustments; workaround is locking the preceding period. Tempo request: after lock, users could still submit/approve/reject/reopen timesheets (gap in workflow control).
    source: https://support.day.io/hc/en-us/articles/14825579433111-How-to-Perform-a-Payroll-Period-Locking ; https://support.stp.one/hc/en-us/articles/38876280457629 ; https://success-timegate.teamsoftware.com/PDFs/Essentials/Jan-2022-Prior-Period-Adjustments.pdf ; https://www.intacct.com/ia/docs/en_AU/help_action/General_Ledger/Open_and_close_books/lock-closed-periods.htm ; https://ideas.tempo.io/ideas/T-I-3608 | publisher: Day.io; STP; Team Software (Timegate); Sage Intacct; Tempo | confidence: med (summary) | class: V/S

15. term: approval levels (project manager vs line manager)
    definition: Planview KeyedIn: PMs approve time logged to their projects; line managers approve remaining time and the overall submission. Maconomy (Deltek): PM approves project costs; line manager gets overview of all employees. Southampton Business World: all rows need line manager approval, some also PM and/or cost centre manager; line manager sees all rows. Access Definitiv: option to route a PM's own timesheet to their line manager to avoid self-approval (default Self). Workfront: only line-manager approval supported; community requests PM approval. Redmine: Level 1/Level 2 approve permissions requested.
    source: https://success.planview.com/KeyedIn/KeyedIn_Product_Help/Timesheets/Timesheet_Approvals ; https://help.deltek.com/Product/maconomy/Documentation/ConceptsGuide/Project_and_Time_Sheet_Approval_PSO.html ; https://help-definitiv.theaccessgroup.com/en/articles/15550429-project-manager-timesheet-approval-mode-setup-and-user-guide ; https://experienceleaguecommunities.adobe.com/t5/workfront-ideas/project-managers-should-be-able-to-approve-time-booked-to-their/idi-p/528661 | publisher: Planview; Deltek; Access Group; Adobe community | confidence: med-high | class: V/F

16. term: PTO vs holiday vs leave in timesheets
    definition: Everhour: PTO, company holidays, sick and unpaid leave reduce net available hours (not counted as non-billable; non-billable stays in the denominator). Track holidays and leave as separate columns for auditability. Paid-leave treatment follows employer policy (FLSA does not require pay for time not worked).
    source: https://everhour.com/calculators/calculate-available-hours | publisher: Everhour | pub_date: n/s | confidence: med-low (single vendor, summary) | class: S

17. term: capacity / over-allocation
    definition: Gross capacity = fixed baseline (e.g. 40 h/wk, 2,080 h/yr); net = gross minus holidays, PTO, unpaid leave, absences (Everhour). Over-allocation: no source retrieved gave a formal definition; only descriptions of allocation imbalance (some people under-utilized, others overburdened).
    source: https://everhour.com/calculators/calculate-available-hours ; https://www.mosaicapp.com/post/how-smarter-resource-planning-reduces-bench-time | confidence: low for over-allocation, med for capacity | class: S

18. term: weekly status "accomplishments / learnings" sections
    definition: Found only in education and generic templates: accomplishments this week, challenges, goals next week, key learnings ("What I've learned" in UBC template); Butler uses red flags, issues, accomplishments by date, action items; Coastal asks hours rounded to nearest 1/4 hour. No PSA vendor evidence that practitioners attach such sections to timesheets.
    source: https://blogs.ubc.ca/worklearnlibrary/files/2024/10/Biweekly-Status-Report.docx ; https://ww2.coastal.edu/mmurphy2/files/courses/fa25/ist659/ist_659_status_report.docx | publisher: UBC; Coastal Carolina Univ. | confidence: low for this use case | class: S

## Conflicting definitions
- Utilization denominator: Harvest/Keka "total available hours" (Keka: total working hours in period) vs BQE "total hours worked" vs Everhour gross vs net (leave removed). Same billable hours yield 62.5% vs 80%. Spec must pick and label.
- "Total utilization": Harvest includes all productive time; one summary noted some sources do not count non-billable as utilization at all.
- Realization: dollar-based (billed / hours x standard rate) vs hours-based; BQE says hourly billing caps at 100% but fixed-fee cases exceed it (136%); others treat 100% as ceiling.
- Benchmarks: IT/consulting 70-85% (Harvest) vs 70-75% typical, >80% burnout (Boyer) vs agencies 75-85%.
- Retainer vs T&M: Metova says retainer = set cost for set time; Wavect treats T&M as a weekly retainer. Boundary blurry.
- "Locked": ProWorkflow has distinct Locked state; Toggl and Ruddr lock implicitly on approval/invoice; Ruddr says no "billed" status, lock-on-invoice instead. Intacct period locks forbid even adjustments, while time tools allow unlock.
- Approval scope: PM approves only project rows (KeyedIn, Maconomy) vs line manager only (Workfront).
- Leakage: BQE does not use the word; shows two gaps (worked-to-invoiced, invoiced-to-collected). Accela/BigTime-type sources treat leakage as unbilled-and-uncollected, separate from bad debt.

## Leads
- Certinia, Deltek Maconomy, Planview KeyedIn docs (full pages) for approval chains and rate logic.
- Industry research bodies not reached: SPI Research (PS Maturity Benchmark) for utilization and realization benchmarks; AFSP/Thomson Reuters/Clio for realization; Gartner for PSA.
- Sage Intacct and Deltek docs for correction entries (reversal/adjusting entries after close).
- Keka PSA help for HRMS-specific hybrid (leave + timesheet).

## Looked for and could not find
- Formal definition of over-allocation (no source retrieved).
- Standalone "utilization realization" definition.
- PSA vendor documentation of adjustment/correction entries after lock (only unlock/reopen patterns).
- Any standard "billed" timesheet state (Ruddr says none).
- Benchmark data from independent research bodies dated within 2 years (all benchmarks vendor, undated).
- Practitioner use of "key accomplishments/learnings" in timesheets.
- WebFetch worked for only 3 of the sources; remaining claims are search-summary and capped at med.
