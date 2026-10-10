---
title: 'domain research: Timesheet and time-billing domain in IT and professional services'
type: 'domain'
topic: 'Timesheet and time-billing domain in IT and professional services'
decision: 'Get vocabulary, rules and handoffs of timesheets, billing and utilization right in the spec'
source: 'native run'
status: complete
preset: 'standard'
validation: 'normal'
created: '2026-10-10'
updated: '2026-10-10'
---

# Domain research: timesheets, billing and utilization

**Decision this research serves:** get the vocabulary, rules and handoffs right in the timesheet spec, and inform its open questions (billable flag, late sheets, locked approvals).

## Executive summary

**What to do.** Put the billable flag on the **project**, with an optional non-billable task inside a billable project, as Harvest and Projectworks do [4][9]. Treat an approved week as **locked**, and handle later fixes as recorded adjustments tied to the original week rather than edits [10]. Never let a late or wrong sheet be a reason to withhold pay for hours worked [13][14].

**Findings that drive this.**
1. The flow is entry, then approval by the project manager (and sometimes finance), then billing and utilization reporting. The main failure is slow or unclear approval, which delays invoices and leaks revenue [1][2].
2. Utilization and realization are different measures: utilization is time, realization is money [6]. Sources disagree on the denominators, so the spec must define its own.
3. US recordkeeping is simple: daily and weekly hours for non-exempt staff, with payroll records kept 3 years and time cards 2 years [11][12].

**Biggest caveat.** Most sources are vendor blogs. The benchmark figures are secondhand, nothing on the payroll handoff was found, and this is US-only and not legal advice.

## 1. Value chain: hours to billing

- **Flow.** Team members log time, the project manager or delivery lead reviews it against scope and billing rules, the approver approves, rejects or returns it, and approved time goes to finance for invoicing and to operations for utilization and profitability [1][16].
- **Owners.** Employee, project manager, finance, delivery or operations. Approval ownership between finance and delivery is often unclear, and that is a named failure mode [1]. Resource-manager ownership was not found.
- **Where billable is decided.** Harvest and Projectworks decide at project level, with non-billable tasks allowed inside billable projects [9]. Kantata sets it on tasks and projects [8]. NetSuite classifies at time-entry level [15] (search-summary source, low confidence).
- **Locks and corrections.** Harvest locks entries once invoiced and requires withdrawing approval and marking them uninvoiced to edit [10]. Other tools use auto-lock after a number of days, or a "historic adjustment" tied to the original week [10].
- **Leakage.** Value earned but never collected, caused by late or bulk entry, wrong codes, forgotten hours and slow approvals [2][3]. Vendors suggest an average lag of more than 3 days between work and logging is a warning sign [3] (vendor heuristic, no research cited).

**Confidence: medium-low.** Mostly vendor blogs and help pages. Primary industry research (SPI, TSIA) was not retrieved.

## 2. Rules of the game (US default, not legal advice)

| Rule | What sources say | Sources |
|---|---|---|
| Non-exempt records | Employer keeps hours worked each workday and week, pay rates, and earnings | [11][12] |
| Retention | Payroll records 3 years; time cards and wage tables 2 years | [11][12] |
| Method | Any complete and accurate timekeeping method is acceptable, including electronic systems | [11][12] |
| Work "suffered or permitted" | Work time must be paid whatever the reason; a late or wrong timesheet cannot justify withholding pay for hours worked | [13][14] |
| Exempt employees | Reduced records only; daily hours are not required for exempt EAP staff (single-source on some details) | [11][12] |

**Not found:** an FLSA rule on editing records after approval or what an audit trail must hold; PTO rules; the current exempt salary threshold (the page was not retrievable). Government-contract rules (DCAA) appear only in search summaries, single-source, and suggest the strictest practice is recording the original entry, the corrected entry and the employee's concurrence. Other countries differ: the UK keeps working-time records for 2 years, and one India source says 5 years, each single-source. Check the rules for your country before launch.

## 3. Language and mental models (glossary)

| Term | Meaning used in this domain | Source |
|---|---|---|
| Billable hours | Time on client work that can be invoiced under a contract | [4] |
| Non-billable hours | Necessary work that cannot be invoiced: internal meetings, admin, training | [4] |
| Billable utilization | Billable hours divided by available hours. Targets cited: 70-80% for service firms, 70-85% for IT services (vendor, undated) | [5] |
| Total utilization | Billable plus non-billable productive hours divided by available hours | [5] |
| Realization | Value invoiced divided by the value of billed hours logged. It can exceed 100% on fixed-fee work | [6] |
| Revenue leakage | Billable value earned but never collected | [2] |
| Rate card | Price per role or person used to value hours (term used by PSA tools; not separately sourced) | [8] |
| Lock or period close | Entries become read-only once approved or invoiced | [10] |
| Adjustment entry | A correction recorded against the original week instead of an edit | [10] |
| Timesheet states | Draft, submitted, approved, rejected, locked, billed; sources differ on "locked" vs "billed" | [10][16] |

**Where sources disagree** (the spec must pick):
- The **utilization denominator**: total working hours, or net of leave.
- The **realization ceiling**: 100%, or above on fixed-fee work.
- **"Locked" vs "billed"** as separate states.
- **Approval scope** of the project manager vs the line manager.

Not found as a standard term: "utilization realization". No formal "over-allocation" definition was found.

## Cross-dimension insights

- The billable flag, the lock state and the audit trail are connected: if billable lives on the project, a lock after approval protects billed numbers, and an adjustment entry keeps the audit trail intact. This matches the spec's constraint that approved hours are immutable.
- The legal rule that pay cannot be withheld for late sheets fits the spec's CAP-10: a late sheet is accepted and carries only a recorded late mark, and it argues against any hard lock on submission.

## Recommendations

| Recommendation | Feeds | Confidence basis |
|---|---|---|
| Billable flag on the project, with optional non-billable tasks | Spec constraint (already set) | Medium: Harvest and Projectworks [4][9] |
| States: draft, submitted, approved, rejected, locked, billed; define "locked" vs "billed" explicitly | Spec capabilities and glossary | Low-medium: sources disagree [10][16] |
| Define utilization and realization formulas in the spec | Spec glossary | Medium: formulas stable, denominators vary [5][6][7] |
| Corrections after approval are adjustment entries tied to the original week | Spec constraint (already set) | Low-medium [10] |
| Keep time records at least 3 years (payroll) and 2 years (time cards) in the US; confirm your country | Spec constraint | High for the US [11][12] |
| Define who approves: project manager for hours, line manager for leave, finance only on exceptions | Spec CAP-6 | Low [1][15] |

## Open questions

- How do approved hours reach payroll, and what are the cost rate and overtime handoffs? No source found.
- Which country's rules apply to your company? This report is US-default.
- What do exempt IT staff need to record? Depends on your policy, since FLSA does not require daily hours for them.
- What are current utilization benchmarks from a primary source (SPI Research, TSIA)?
- How do fixed-price and retainer work convert hours to revenue?

## Owner decisions (2026-10-10)

- Retention is a **generic US-style rule**: submitted sheets, approved sheets and change history kept at least 3 years. The country question is closed.
- Confirmed: approved means locked, utilization uses total available hours, the named project reviewer approves, and everyone submits weekly effort only.
- One sheet per employee per week is enforced. The weekly sheet is published and must be submitted by 11:59 pm UTC on the day after publication (Saturday for the usual Friday publication, published by the Project 1 owner in the app); the project reviewer then approves or rejects.
- Retention by country is closed: the generic 3-year rule has no country-specific follow-up.
- The payroll handoff is out of scope, so the "payroll handoff" open question is closed.
- Late sheets carry a late penalty that is only a recorded late mark; it never withholds, delays or reduces pay, which fits the pay rule found in this research.

## Source appendix

| # | Supports | Publisher | Pub date | Accessed | Confidence |
|---|---|---|---|---|---|
| 1 | Flow, owners, failures | [Birdview PSA](https://birdviewpsa.com/blog/timesheet-approval-workflow-consulting-it-services/) | 2026-09-28 | 2026-10-10 | med |
| 2 | Leakage causes | [Birdview PSA](https://birdviewpsa.com/blog/reduce-revenue-leakage-professional-services/) | 2026-09-14 | 2026-10-10 | med |
| 3 | Realization, lag heuristic | [Synthelio](https://synthelio.com/post/realization-rate-where-professional-services-fees-leak) | 2026-09-07 | 2026-10-10 | med/low |
| 4 | Billable vs non-billable | [Harvest](https://www.getharvest.com/time-tracking/billable-vs-non-billable-hours) | n/d | 2026-10-10 | high |
| 5 | Utilization formulas and targets | [Harvest](https://www.getharvest.com/time-tracking/billable-utilization-vs-total-utilization) | n/d | 2026-10-10 | high/med |
| 6 | Utilization vs realization | [BQE](https://www.bqe.com/blog/utilization-vs.-realization-of-billable-time-in-bqe-core) | 2020, updated 2026-09 | 2026-10-10 | high |
| 7 | Utilization denominator | [Keka](https://help.keka.com/hc/en-us/articles/39946716426513-Managing-Target-Billable-Utilization) | n/d | 2026-10-10 | med |
| 8 | Billable on tasks and projects | [Kantata](https://knowledge.kantata.com/hc/en-us/articles/37158751310875-Glossary-of-Kantata-OX-Terms) | n/d | 2026-10-10 | med |
| 9 | Billable at project level | [Harvest Help](https://support.getharvest.com/hc/en-us/articles/24510797704717) | n/d | 2026-10-10 | med |
| 10 | Locks and adjustments | Harvest and other vendor help pages, see `digests/value-chain-r1-1.md` claim 11 | n/d | 2026-10-10 | low-med |
| 11 | FLSA records, retention | [DOL Fact Sheet 21](https://www.dol.gov/agencies/whd/fact-sheets/21-flsa-recordkeeping) | 2008 (revised) | 2026-10-10 | high |
| 12 | FLSA records, retention | [eCFR 29 CFR 516](https://www.ecfr.gov/api/renderer/v1/content/enhanced/current/title-29?part=516) | current, undated | 2026-10-10 | high |
| 13 | Hours worked, suffered or permitted | [DOL Fact Sheet 22](https://www.dol.gov/agencies/whd/fact-sheets/22-flsa-hours-worked) | 2008 (revised) | 2026-10-10 | high |
| 14 | Work not requested | [eCFR 29 CFR 785.11](https://www.ecfr.gov/api/renderer/v1/content/enhanced/current/title-29?part=785&section=785.11) | current, undated | 2026-10-10 | high |
| 15 | NetSuite classification | [Oracle NetSuite OpenAir help](https://docs.oracle.com/en/cloud/saas/netsuite-openair/nsoa-online-help/) and partner blogs | n/d | 2026-10-10 | low |
| 16 | HRMS approval chains | [Keka PSA](https://help.keka.com/hc/en-us/articles/39946828609041) | n/d | 2026-10-10 | low-med |

## Staleness map

Regulatory claims ([11]-[14]) must be re-verified as current before any launch, whatever their date; the DOL fact sheets were last revised in 2008 and the eCFR page shows no currency date. Vendor definitions ([4]-[9]) are stable, with a 3-year freshness bar, so re-check by **2029-10-10**. Benchmarks ([5]) should be re-checked within 2 years, by **2028-10-10**. The earliest action is the legal re-verification before launch. Dates were set by hand from the pack's freshness bars, not computed with the staleness script.
