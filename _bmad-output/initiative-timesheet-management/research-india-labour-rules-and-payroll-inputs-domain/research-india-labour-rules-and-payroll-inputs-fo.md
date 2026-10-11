---
title: 'domain research: India labour rules and payroll inputs for IT timesheets'
type: 'domain'
topic: 'India labour rules and payroll inputs for IT timesheets'
decision: 'Which Indian labour rules and retention periods apply to timesheet records, and what payroll needs beyond approved hours'
source: 'native run'
status: complete
preset: 'standard'
validation: 'normal'
created: '2026-10-10'
updated: '2026-10-10'
---

# Domain research: India labour rules and payroll inputs for IT timesheets

**Decision this research serves:** which Indian labour rules and retention periods apply to timesheet records, and what payroll needs beyond approved hours. This is a summary of public sources, **not legal advice**. No official gazette or government page was read for any legal claim, so confidence is capped at medium and every legal point needs confirmation by your legal or compliance team.

## Executive summary

**Answer 1: which rules apply.** India's four Labour Codes came into force on **21 November 2025**, and the final Central Rules followed on **8 May 2026** [1][2]. Most private IT employers sit under their **state** rules, and many state rules were still pending in May 2026 [3]. For records, the Central Wages Rules (Rule 51) require three registers (employee, wages and overtime, attendance muster roll), electronic form allowed, kept **5 years after the last entry** [4]. Your 5-year starting value matches this, but only from secondary sources.

**Answer 2: what payroll needs.** In the vendor documentation I found (Zoho, Keka, greytHR, Razorpay), payroll takes **loss-of-pay (LOP) or payable days from attendance and leave**, behind a **cut-off date** after which later changes don't count that month [5][6][7][8]. Timesheet hours were not described as a payroll input by any of them. Overtime comes from attendance [5].

**What this means for your spec.** CAP-15 assumes payroll reads approved timesheet hours. Indian practice suggests payroll for salaried staff runs on attendance and leave, so confirm with your payroll team what it will actually consume. Keep CAP-15 only if some group (contractors, overtime claims) needs hours.

**Biggest caveat.** All legal claims rest on law-firm and compliance-blog summaries. Several figures conflict between sources.

## 1. Which Indian rules apply

| Topic | What sources say | Confidence | Sources |
|---|---|---|---|
| Labour Codes in force | All four Codes (Wages, Industrial Relations, Social Security, OSH) in force from 21 Nov 2025 | med | [1] |
| Central Rules | Final Central Rules notified 8 May 2026 | med | [2] |
| State rules | Many state rules still pending as of May 2026; no current per-state list found | med (5 months old) | [3] |
| Records | Three registers: employee, wages and overtime, attendance muster roll; electronic form allowed | med | [4] |
| Retention | Registers kept 5 years after the last entry (Rule 51); older rules cited 3 years; practice blogs suggest up to 7 | med / low | [4][9] |
| Overtime pay | At least twice the normal rate of wages | med | [10] |
| Working hours | OSH Code: 8 hours a day, 48 a week, subject to state limits; the spread-over and quarterly overtime caps conflict between sources (125 vs 144 hours a quarter) | low | [11] |
| Telangana IT/ITeS | Exempt from some hours provisions of its Shops Act until 30 May 2028, with conditions: 48-hour weekly cap, overtime beyond it, weekly off | med | [12] |
| Karnataka IT/ITeS | Exempt from the Standing Orders Act until 10 June 2029; hours and overtime for IT not confirmed | med / low | [12] |
| Tamil Nadu, Maharashtra | IT-specific hours and overtime rules not confirmed | low | none found |
| Salaried staff | Some state Acts exclude managerial and supervisory staff; the 48-hour cap is described as applying to IT too | low | [11] |

**Not found:** anything India-specific on correcting or locking approved time records; whether daily or only weekly hours must be recorded under the attendance register; state retention periods under the state rules.

## 2. What payroll needs beyond approved hours

- **Core input:** LOP days or payable days, coming from attendance and leave, not from timesheets [5][6][7][8].
- **Cut-off and lock:** Zoho has a Processing Day before payday; Keka counts only LOP before the pay-group cut-off; greytHR can lock attendance by project, grade or department and lock a payroll month [5][6][7].
- **Late corrections:** Keka and Razorpay allow LOP adjustments or reversals paid in the current run [6][8].
- **Overtime:** comes from attendance and shift rules (Zoho, Darwinbox marketing) [5].
- **Statutory items tied to time data:** the EPF wage ceiling reportedly rose to Rs 25,000 (S.O. 5109(E), 17 Sep 2026), per three secondary sources only [13]; ESI was checked on an official page [14]. Provident fund, ESI and professional tax depend on paid days, so payroll needs reliable paid-day counts.
- **Shift or night allowance:** no vendor page listed these as time-system inputs.

**Confidence: low to medium.** Most claims come from search summaries of vendor help pages; Darwinbox documentation was not found.

## Cross-dimension insights

- Timesheets and attendance are different records in India. Your spec's non-goal "attendance or clock-in tracking" fits: the attendance register is another system, and the timesheet is a weekly effort record for billing and utilization.
- The 5-year register retention and a payroll cut-off both point to the same design: lock approved weeks and keep adjustments as recorded entries, as your spec already requires.

## Recommendations

| Recommendation | Feeds | Confidence basis |
|---|---|---|
| Keep 5 years from the last entry as the starting retention value; confirm with legal | Spec retention constraint | Medium: two secondary sources [4] |
| Ask the payroll team what it consumes (LOP days, hours, overtime) before building CAP-15 | Spec CAP-15 and open questions | Medium: vendors consistently use LOP days [5][6][7][8] |
| If CAP-15 stays, add a cut-off date after which approved hours go to payroll as adjustments | Spec CAP-15 | Low: vendor practice only |
| Confirm the operating state (Karnataka, Telangana, Maharashtra, Tamil Nadu) and its IT/ITeS exemptions | Spec open questions | Low: state rules patchy [12] |
| Have compliance review overtime and the 48-hour cap before any overtime feature | Future spec | Low: sources conflict [11] |

## Open questions

- Which state or states does your company operate in, and are its state Labour Code rules in force?
- Is the 5-year retention confirmed by the primary text of the Wages Rules and your state's rules?
- What does your payroll consume: LOP days, timesheet hours, overtime, or all three?
- Is the EPF wage ceiling change official? Check the gazette.
- Do daily hours need to be kept in the attendance muster roll, even though the timesheet is weekly?

## Owner decisions (2026-10-10)

- India-specific rules were **not adopted**: the owner chose a generic US-style retention rule (at least 3 years). The 5-year India figure and the state-rule questions are kept here as reference only.
- Retention by country is closed: the generic 3-year rule has no country-specific follow-up.
- LOP days, payable days, the payroll cut-off and the payroll handoff are **out of scope**, so the payroll recommendations and CAP-15 are not applied. CAP-15 is retired.

## Source appendix

| # | Supports | Publisher | Pub date | Accessed | Confidence |
|---|---|---|---|---|---|
| 1 | Codes in force | [K&S Partners](https://ksandk.com/md/labour-employment/all-four-labour-codes-enforced-from-21-november-2025/), [DLA Piper](https://knowledge.dlapiper.com/dlapiperknowledge/globalemploymentlatestdevelopments/2025/government-of-india-notifies-the-labour-codes-ushers-a-new-era-of-compliances) | 2025-11 | 2026-10-10 | med |
| 2 | Central Rules notified | [BDO India](https://www.bdo.in/en-gb/insights/alerts-updates/alert-final-central-rules-notified-under-all-four-labour-codes) | 2026-05-12 | 2026-10-10 | med |
| 3 | State rules pending | [BDO India](https://www.bdo.in/en-gb/insights/alerts-updates/alert-final-central-rules-notified-under-all-four-labour-codes), [iPleaders](https://blog.ipleaders.in/labour-codes-2026-implementation-complete-guide-to-what-is-in-force-what-changed-and-what-to-do-now/) | 2026-05 | 2026-10-10 | med |
| 4 | Registers, retention | [Taxmann](https://www.taxmann.com/post/blog/wages-central-rules-2026-code-on-wages-chapter-wise-guide/), [TaxClue](https://taxclue.in/blog/rule-51-52-code-on-wages-central-rules-2026-registers-and-wage-slip/) | 2026 | 2026-10-10 | med |
| 5 | Zoho handoff, overtime | [Zoho Payroll help](https://www.zoho.com/in/payroll/help/employer/integrations/integrations-people.html) | n/d | 2026-10-10 | med/low |
| 6 | Keka cut-off, LOP | [Keka](https://help.keka.com/hc/en-us/articles/39946563404561-Running-payroll-on-Keka) | n/d | 2026-10-10 | med |
| 7 | greytHR lock, cut-off | [greytHR help](https://www.greythr.com/help-admin/attendance-settings/configure-attendance-settings/) | n/d | 2026-10-10 | med |
| 8 | Razorpay LOP sync | [Razorpay docs](https://razorpay.com/docs/payroll/employees/attendance-leaves.md) | n/d | 2026-10-10 | med |
| 9 | Older retention, practice | [TaxClue](https://taxclue.in/blog/section-50-code-on-wages-2019-records-returns-and-notices/) | 2026 | 2026-10-10 | low |
| 10 | Overtime at 2x | [BDO India](https://www.bdo.in/en-gb/insights/alerts-updates/alert-final-central-rules-notified-under-all-four-labour-codes) | 2026-05-12 | 2026-10-10 | med |
| 11 | Hours caps (conflicting) | [Right to Information wiki](https://righttoinformation.wiki/working-hours-overtime-spread-over-osh-code-india), [EZHRM](https://ezhrm.in/overtime-rules-india-2026-labour-codes-changed/) | 2026 | 2026-10-10 | low |
| 12 | Telangana, Karnataka exemptions | [AZB & Partners](https://www.azbpartners.com/bank/labour-law-exemptions-for-indian-technology-and-outsourcing-employers-in-bangalore-hyderabad/) | 2024-06-18 | 2026-10-10 | med |
| 13 | EPF wage ceiling | three secondary sources, see `digests/payroll-inputs-r1-1.md` | 2026-09 | 2026-10-10 | low |
| 14 | ESI | ESIC page, see `digests/payroll-inputs-r1-1.md` | n/d | 2026-10-10 | med |

## Staleness map

Labour law and state status change often, so re-verify every legal claim ([1]-[4], [9]-[13]) against official sources **before launch**, and re-check status by **2027-01-10** (3 months). Vendor handoff docs ([5]-[8]) re-check by **2027-04-10** (6 months). The earliest action is the pre-launch legal verification. Dates were set by hand, not computed with the staleness script.
