# Digest payroll-inputs-r1-1 (accessed 2026-10-10)

Method note: WebFetch worked, but several fetches returned partial or login pages. Many claims below rest on WebSearch summaries (marked search-summary, so med or low). No local files read. Round 1 only, about 17 tool calls.

## Claims

### Vendor handoff and cut-off (Q2)

1. claim: Zoho People syncs LOP (attendance and leave details) into Zoho Payroll, with employee and work-location sync. Pay Period in People must match Pay Schedule in Payroll. The "Processing Day" is the cut-off to generate the LOP report. It must be on or before Payday, and a pay run cannot be approved before it. Fetched page did NOT mention payable days or overtime; search summary of regional (UAE/Kuwait) pages said optional "Fetch Payable Days" and "Fetch overtime hours" toggles exist, which I could not confirm for India.
   - source: https://www.zoho.com/in/payroll/help/employer/integrations/integrations-people.html (regional variants: zoho.com/en-kw/payroll/help/employer/integrations/integrations-people.html)
   - publisher: Zoho Payroll help; date: none shown; confidence: high (LOP and Processing Day, fetched), low (overtime and payable days for India); class: vendor documentation; sources_count: 1

2. claim: Zoho integration is one-way (People to Payroll). LOP can be pushed from People (Leave > Reports > LOP Reports > Push to Payroll) or fetched on the Pay Runs tab. It cannot be enabled while People's Leave and Attendance module is on (as summarised by search).
   - source: same Zoho pages (search-summary, not fully verified by fetch); publisher: Zoho; date: none; confidence: med; class: vendor documentation; sources_count: 1

3. claim: Keka has an attendance cut-off date per pay group. Only LOP days before the cut-off count in that month's salary. Later LOP is not considered. Set under Payroll > Settings > Pay Groups > Pay Schedule.
   - source: https://help.keka.com/admin/knowledge/how-to-set-up-attendance-cut-off-date-for-payroll-processing (fetch returned only a login page; claim from search-summary); alt: support.keka.com/support/solutions/articles/84000380259
   - publisher: Keka; date: none; confidence: med; class: vendor documentation; sources_count: 1

4. claim: Keka's run-payroll flow has a "Leave, Attendance & Daily Wages" step with an LOP Summary (system-calculated LOP days per employee). Admin can edit on an LOP Adjustment tab or bulk-import LOP via Excel. LOP overridden in the pay run does not appear in leave history. LOP reversal is possible for earlier months and paid in the current payroll. The same search found no explicit "lock attendance" step in Keka.
   - source: https://help.keka.com/hc/en-us/articles/39946563404561-Running-payroll-on-Keka ; https://help.keka.com/admin/knowledge/how-to-adjust-loss-of-pay-lop-of-a-single-employee-or-that-of-a-group
   - publisher: Keka; date: none; confidence: med (search-summary); class: vendor documentation; sources_count: 1

5. claim: greytHR has per-department attendance cycles with a start and cut-off date. Admin can lock attendance records by Project, Grade or Department. Payroll Overview sets the month's cut-off range and the "Number of Work Days". Payroll has a Lock/Unlock button per month, and the previous month's payroll should be locked before processing the next. greytHR warns that changing cut-offs changes past attendance and causes payroll errors.
   - source: https://www.greythr.com/help-admin/attendance-settings/configure-attendance-settings/ ; https://www.greythr.com/help-admin/payroll/view-payroll-summary-glance
   - publisher: greytHR help; date: none; confidence: med (search-summary only); class: vendor documentation; sources_count: 1

6. claim: RazorpayX Payroll has two documented external-attendance handoffs. (a) Jibble: leaves and shifts sync, Payroll calculates LOP at run time, and the monthly LOP report is synced before executing payroll. (b) UbiAttendance: the built-in Attendance module must be turned off, API access requested from support, and LoP is pushed by a manual monthly sync ("Sync Employee LoPs"). Built-in attendance edits to past records need admin or manager approval.
   - source: https://razorpay.com/docs/payroll/integrations/jibble/ ; https://razorpay.com/docs/payroll/employees/attendance-leaves.md
   - publisher: Razorpay; date: none; confidence: med (search-summary); class: vendor documentation; sources_count: 1

7. claim: Darwinbox: no help-center documentation of attendance lock or payroll cut-off was found. Only marketing says attendance with shift and overtime rules feeds payroll and that input reconciliation is automated. A third-party tool (Gigin) exports approved timesheets or attendance to Darwinbox per cycle.
   - source: https://darwinbox.com/blog/10-best-payroll-attendance-software-enterprises ; https://darwinbox.com/products/payroll
   - publisher: Darwinbox (marketing); date: none; confidence: low; class: vendor marketing; sources_count: 1

### Inputs and the timesheet question (Q1, Q4)

8. claim: Across the vendors above, the documented time-driven input to payroll is LOP days (or payable days) from attendance and leave. Overtime hours come in from attendance (Zoho overtime fetch, regional page; Darwinbox shift and overtime rules). Timesheet hours are not described by Zoho, greytHR or Razorpay as a payroll input. This is my synthesis of claims 1-7. No vendor page in this round lists shift or night allowance as a time-system input.
   - source: claims 1-7; confidence: low-med; class: synthesis; sources_count: multiple, but absence-based

9. claim: Keka claims that for IT businesses every hour logged against a project flows into client billing and payroll for both full-time and contractual staff. Contractors and full-time staff can be paid "directly from timesheets" with overtime and billing rates calculated. It also markets billable utilization and bench dashboards. Keka's PSA help (Target Billable Utilization report) is the utilization side. This shows timesheet-driven payroll is a vendor-claimed capability, mainly for contract or hourly staff. It is not evidence of how salaried IT staff are typically paid.
   - source: https://www.keka.com/hr-software-for-it-businesses (fetched) ; https://help.keka.com/admin/understanding-and-accessing-the-time-summary-in-keka-psa (search-summary)
   - publisher: Keka (marketing and help); date: none; confidence: high (that Keka claims it), low (as evidence of market norm); class: vendor marketing; sources_count: 1

### Statutory items (Q3). Two-source rule applied

10. claim: ESI wages include overtime allowance and night shift allowance for contribution. Overtime counts for contribution but not for deciding coverage. Contribution is by wage period and the return shows employee-wise days for which wages were paid and wages paid. Rules deem a time-rated employee paid without working a day to have worked the full standard days (26 for monthly-rated).
   - sources: https://esic.gov.in/wages (fetched; last reviewed 2025-04-04); ESIC FAQ booklet https://esic.gov.in/press/ESIC_FAQ_booklet.pdf and ESI (Central) Rules via search-summary
   - publisher: ESIC; confidence: high (overtime, night shift), med (days and 26 detail); class: statutory/regulator; sources_count: 2 (one fetched, one search-summary)
   - note: ESIC pages show conflicting contribution rates (4.75%/1.75% vs 3.25%/0.75%); the second is likely current but not verified. This does not depend on time data.

11. claim: Overtime under the Factories Act s.59: work over 9 hours/day or 48 hours/week earns twice the "ordinary rate of wages" (basic plus allowances, excluding bonus and overtime). Supreme Court (Philips India v Labour Court) held double rate applies only past the statutory limits. This is the Factories Act only; I did not retrieve the Karnataka or other state Shops and Establishments rules that normally cover IT offices.
   - source: https://www.caseon.in/section/section-59-the-factories-act-1948 (fetched); Goa Form 33 https://ifbgoa.goa.gov.in/sites/default/files/FORM33.PDF (search-summary)
   - publisher: caseon.in (legal database, not official); Goa govt; date: none; confidence: med; class: statute text; sources_count: 2; flag: neither is labour.gov.in

12. claim: EPF: contributions are on basic wages, DA and retaining allowance. Days of no wages are non-contributory (NCP) days, so wage base prorates with LOP. Practitioner view says a >=15k-basic employee gets NCP only if LOP pushes basic below the ceiling; this is a forum view, not statute.
   - source: https://community.greythr.com/t/non-contributory-period-ncp-days-in-pf-and-calculation/4958 ; https://factohr.com/ncp-days-in-pf/ (both search-summary)
   - publisher: greytHR community, factoHR (vendor/blog); confidence: low-med; class: practitioner; sources_count: 2, both non-official. LEAD: verify on epfindia.gov.in.

13. claim: Reported, NOT verified officially: EPF mandatory wage ceiling raised from Rs 15,000 to Rs 25,000 via S.O. 5109(E) dated 17 Sep 2026, with transition in Sept 2026 and full effect from Oct 2026. Contributions above the ceiling reported as voluntary under the "EPF Scheme 2026". This changes the LOP-versus-ceiling logic in claim 12.
   - sources: https://www.india-briefing.com/news/india-epf-wage-ceiling-inr-25000-mandatory-coverage-payroll-47197.html/ ; https://www.azbpartners.com/?p=89618 ; https://www.corporateprofessionals.com/articles/epf-wage-ceiling-moves-to-%E2%82%B925000-key-changes-and-employer-impact/ (all search-summary)
   - publisher: India Briefing, AZB & Partners, Corporate Professionals; date: about 2026-09-22; confidence: med; class: secondary legal commentary; sources_count: 3 non-official. Gazette not seen.

14. claim: Professional tax is a state matter. Karnataka (Act 1976, amended 2023): no tax below Rs 25,000 monthly gross, Rs 200 above; a greytHR note says revised slabs from 1 Apr 2025 (Rs 300 in February). Whether LOP-reduced salary is the test base was NOT found in any source; the threshold is on salary "paid or payable" (inference only).
   - source: https://www.setindiabiz.com/learning/karnataka-professional-tax-amendment-2023 ; https://product-updates.greythr.com/en/revised-karnataka-professional-tax-slabs-now-live-KwPXQWqO (search-summary)
   - publisher: SetIndiaBiz, greytHR; confidence: low; class: secondary; sources_count: 2 non-official; sources conflict.

## Leads
- Keka PSA help section "Timesheet Integration for Payroll Automation": https://help.keka.com/hc/en-us/sections/39012953366673-PSA-Professional-Services-Automation
- Zoho People Kuwait page for overtime/payable-days toggles; find the India equivalent or Zoho People "Push to Payroll" doc.
- Gigin integration pages (gigin.ai/integrations/keka, /darwinbox): third-party timesheet-to-payroll export, evidence of the handoff pattern.
- epfindia.gov.in FAQ and gazette S.O. 5109(E) for the ceiling and NCP rules; the 4 Labour Codes (Code on Wages and Social Security) for overtime and "wages" definition.
- State Shops and Establishments Acts (e.g. Karnataka) for IT overtime. Check whether Karnataka exempts IT firms.
- Official state PT acts for LOP treatment.

## Looked for and could not find
- Darwinbox help-center docs on attendance lock or payroll cut-off.
- Any vendor page stating shift or night allowance are computed from attendance, other than ESIC treating them as wages.
- Any source showing that salaried IT employees' payroll is timesheet-driven. Q4 evidence is only Keka's claim, and that is for contract and full-time staff alike.
- Official EPFO or labour.gov.in pages (none surfaced in search; the ceiling change rests on secondary sources).
- How LOP affects PT or the ESI wage threshold.
- Fully fetched vendor pages for Keka cut-off (login wall), greytHR and Razorpay (search-summary only).
