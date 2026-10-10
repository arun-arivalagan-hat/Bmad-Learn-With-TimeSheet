# Digest rules-r1-1: legal/compliance rules affecting a timesheet module (US default)
Public-source summary, not legal advice. All accessed 2026-10-10. Note: WebFetch/WebSearch return model-summarised page text, so quotes are as relayed, not verified verbatim.

## Claims

1. Non-exempt employees: employer must record name, address, DOB if under 19, sex, occupation, workweek start, pay basis, hours worked each workday and workweek, regular rate, straight-time and overtime earnings, additions/deductions, total wages per pay period, pay date and period covered.
   - URLs: https://www.dol.gov/agencies/whd/fact-sheets/21-flsa-recordkeeping (DOL WHD, Fact Sheet 21, "Revised July 2008"); https://www.ecfr.gov/api/renderer/v1/content/enhanced/current/title-29?part=516 (eCFR, 29 CFR 516.2; no currency date shown on page, latest cited amendment 85 FR 86788, Dec 30 2020)
   - confidence: high | class: regulatory-primary | sources_count: 2

2. Retention: payroll records 3 years (29 CFR 516.5); basic time and earnings cards, wage rate tables, and records of wage additions/deductions 2 years (516.6). Records must be available for inspection; central-office records must be produced within 72 hours of notice (516.7).
   - URLs: same two as claim 1 (Fact Sheet 21; eCFR Part 516)
   - confidence: high (page currency for eCFR not confirmed) | class: regulatory-primary | sources_count: 2

3. No particular form required; any timekeeping method is acceptable if complete and accurate. Fixed-schedule workers: employer may record the schedule but must record actual hours worked on an exception basis (516.2 says actual hours when they differ from schedule). Electronic/automated data systems allowed if viewable, clear, identifiable by date/pay period, and transcribable on request (516.1(a)).
   - URLs: Fact Sheet 21; eCFR Part 516
   - confidence: high | class: regulatory-primary | sources_count: 2

4. Work not requested but suffered or permitted is work time that must be paid; reason is immaterial (voluntary overtime to finish tasks or fix errors counts); employer who knows or has reason to believe work continues owes pay. Implication for the module: a late or incorrect timesheet cannot be a basis to withhold pay for hours actually worked. (This implication is my inference; the sources state the "suffered or permitted" rule, not the late-timesheet case specifically.)
   - URLs: https://www.dol.gov/agencies/whd/fact-sheets/22-flsa-hours-worked (DOL WHD, Fact Sheet 22, "Revised July 2008", confirmed by fetch; note the first fetch of fact-sheets/23-... returned 404); https://www.ecfr.gov/api/renderer/v1/content/enhanced/current/title-29?part=785&section=785.11 (eCFR, 29 CFR 785.11, no currency date)
   - confidence: high on the rule, low on the late-timesheet inference | class: regulatory-primary | sources_count: 2

5. Exempt employees: employers still keep reduced records. 516.3 (EAP exemptions) requires most identity/occupation/workweek/pay-basis items but not the hours-and-overtime pay items (a)(6)-(10), plus wage basis in enough detail to compute total remuneration. So FLSA does not require daily hours for exempt EAP staff. Fact Sheet 17A does not address hour recording for exempt staff.
   - URLs: eCFR Part 516 (516.3, 516.11, 516.12); https://www.dol.gov/agencies/whd/fact-sheets/17a-overtime (does not address it)
   - confidence: med | class: regulatory-primary | sources_count: 1 (single-source; the second source is silent)

6. Exemption basics: exempt status depends on duties plus salary basis; job titles do not determine status. Fact Sheet 17A lists $684/week salary level and computer-employee exemption (salary at least $684/week, or hourly at least $27.63, for systems analysts, programmers, software engineers, similar). That page is "last revised September 2019", so the figures may be outdated. Currency NOT verified: the DOL rulemaking page returned 403 and an overtime-factsheet URL returned 404.
   - URL: https://www.dol.gov/agencies/whd/fact-sheets/17a-overtime (DOL WHD, revised Sept 2019)
   - confidence: low on current thresholds; med on structure | class: regulatory-primary, possibly stale | sources_count: 1 (single-source)

7. Employment tax records: IRS says keep at least 4 years after the tax is due or paid, whichever is later. Combined with FLSA 3-year payroll rule, a 4-year-plus payroll retention is the safer reading, but the IRS page covers tax records, not timesheets.
   - URL: https://www.irs.gov/businesses/small-businesses-self-employed/how-long-should-i-keep-records (IRS; last-updated date not shown in fetch result)
   - confidence: med | class: regulatory-primary | sources_count: 1 for the IRS point; FLSA side has 2 (claim 2)

8. Editing/correcting after submission: FLSA text retrieved sets no explicit rule for edits or audit-trail contents; only that records must be accurate and available for inspection. Strictest practice comes from DCAA guidance (claim 9): preserve original charge, corrected charge, employee concurrence/approval, and reason.
   - sources_count: 0 for an FLSA edit rule (see "could not find"); DCAA see claim 9
   - confidence: low | class: gap

9. Government-contract end (two lines): DFARS 252.242-7006 accounting-system criterion 9 (timekeeping) and 10 (labor distribution) are the basis; DCAA guidance expects employee-certified timesheets approved by supervisors, completed daily with all hours including uncompensated overtime, changes showing original charge, corrected charge and employee concurrence, and segregation of timekeeping from payroll. Floor checks are used to test it. (FAR 52.203-13 fetched does NOT cover timekeeping; do not cite it for this.)
   - URLs: https://www.acquisition.gov/dfars/252.242-7006-accounting-system-administration. and https://www.dcaa.mil/Portals/88/Chapter%205%20DFARS%20Business%20Sys%2007_01_2020%20(508F).pdf (surfaced by WebSearch, not fetched directly; DCAAM 7641.90 dated Nov 2023, audit chapter Version 2.0 July 2020); also vendor guides (cbh.com, aprio.com) agree, secondary.
   - confidence: med (search-summary only, primary pages not opened) | class: regulatory-primary via search summary | sources_count: 2 (DFARS clause + DCAA audit program) but neither fetched

10. Other countries differ.
    - UK: Working Time Regulations 1998 reg 9 requires records adequate to show compliance with limits, kept 2 years; no need to log every daily hour. Sources: https://www.legislation.gov.uk/uksi/1998/1833/regulation/9/made (original 1998 text, amendments not checked) and https://www.acas.org.uk/working-time-rules (Acas). A secondary source (Brightmine) says from 6 April 2026 annual-leave records must be kept 6 years; single-source, unverified. No GOV.UK page found.
    - India: no single national rule found; state Shops and Establishments Acts (e.g. Delhi, Maharashtra, Tamil Nadu on indiacode.nic.in) set hours and registers. labour.gov.in Compliance Handbook for the four Labour Codes (https://www.labour.gov.in/static/uploads/2026/02/83978455025732b99b0165def80ab171.pdf) says attendance/muster, wage, overtime and fines registers, physical or electronic, preserved 5 years. Handbook is a summary, not rule text.
    - EU: not researched.
    - confidence: UK med (2 sources), India low-med (1 summary doc) | sources_count: UK 2, India 1 (single-source)

## Leads
- Verify the current EAP salary threshold on dol.gov (rulemaking page returned 403) and eCFR 29 CFR 541.600/541.400; the 2019 figure may not be current.
- Fetch 29 CFR 516.1 to 516.7 page header for eCFR currency date; fetch irs.gov Publication 15 (Circular E) for the exact 4-year wording.
- Open DCAA Chapter 5 PDF and DCAAM 7641.90 directly to confirm the timesheet-change wording.
- DOL FAQ https://www.dol.gov/agencies/whd/flsa/faq (surfaced, not opened) may cover recordkeeping and late timesheets.
- UK: legislation.gov.uk current reg 9 version and any 2026 amendment on annual-leave records; India: the Code on Wages and OSH Code rules for the 5-year retention text.
- State laws (e.g. California, New York) often impose longer retention and meal/rest records; not researched.

## Looked for and could not find
- Any DOL/eCFR text saying how time records may be edited after submission or what an audit trail must contain (FLSA requires accuracy and availability only).
- A DOL statement that exempt employees must or need not record hours beyond the 516.3 text above.
- A DOL statement that employers may not withhold pay for late timesheets (only the general suffered-or-permitted rule).
- PTO/leave record rules under federal law (FLSA does not mandate PTO; not retrieved).
- Current EAP salary threshold with a verified page date; GOV.UK page for UK record-keeping; FAR text on labor charging.
