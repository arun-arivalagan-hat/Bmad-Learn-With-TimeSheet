# Glossary

Source: research-timesheet-and-time-billing-domain-in-it. Mostly vendor sources; the research was US-default and is not legal advice; the operating country is India.

| Term | Meaning in this spec |
|---|---|
| Billable hours | Time on client work that can be invoiced under a contract |
| Non-billable hours | Necessary work that cannot be invoiced: internal meetings, admin, training |
| Billable flag | Set on the project; an individual task inside a billable project may be non-billable |
| Billable utilization | Billable hours divided by total available hours |
| Total utilization | Billable plus non-billable productive hours divided by total available hours |
| Realization | Value invoiced divided by the value of billed hours logged; can exceed 100% on fixed-fee work |
| Revenue leakage | Billable value earned but never collected |
| Rate card | Price per role or person used to value hours |
| Lock | An approved sheet becomes read-only |
| Adjustment entry | A correction to an approved sheet, recorded against the original week and never a silent edit |
| Loss of pay (LOP) days | Unpaid days in a pay period, from attendance and leave data; payroll deducts pay for them |
| Payable days | Days in a pay period an employee is paid for, from attendance and leave data |
| Payroll cut-off date | Date after which changes no longer count in that period's payroll; later changes become adjustments in the next period |
| Weekly effort | Hours per project for a week; the only entry level in this module, including for salaried IT staff |

## Timesheet states

| State | Meaning |
|---|---|
| Draft | Started, not submitted; the employee can edit |
| Submitted | Sent to the project reviewer; the employee can reopen it until approval |
| Rejected | Returned with a reason; the employee edits and resubmits |
| Approved | Accepted by the reviewer; locked |

Billing and invoicing states belong to another system because invoicing is a non-goal.

## Where sources disagree

- Utilization denominator: total hours or hours net of leave. This spec uses total available hours (confirmed).
- Whether "locked" and "billed" are separate states.
- Whether the project manager or the line manager approves.
