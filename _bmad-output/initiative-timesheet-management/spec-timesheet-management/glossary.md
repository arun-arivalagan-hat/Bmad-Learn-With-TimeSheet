# Glossary

Source: research-timesheet-and-time-billing-domain-in-it. Mostly vendor sources; the research was US-default and is not legal advice; the owner chose generic US-style rules.

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
| Published sheet | The weekly sheet the Project 1 owner has made available to an employee, usually on Friday; the submission deadline (11:59 pm UTC the next day) counts from publication |
| Late mark | The late penalty: a recorded mark on a sheet submitted after the deadline, counted per employee and visible to the employee, project reviewer, reporting manager and HR; it never affects pay by itself; HR sees it and decides any consequences |
| Weekly effort | Hours per project for a week; the only entry level in this module, including for salaried IT staff |
| Project block | One project's entry on a sheet: project, tasks/activities, hours and reviewer; up to 5 per sheet |
| Project reviewer | The person named for a project who approves or rejects the hours in that project's block |
| Project 1 owner | The owner of an employee's primary project; publishes the sheet and sees submission status; never approves |
| Reporting manager | The employee's line manager; read-only view of direct reports' hours and late marks; never approves |

## Timesheet states

| State | Meaning |
|---|---|
| Draft | Started, not submitted; the employee can edit |
| Submitted | Sent to the project reviewer; the employee can reopen it until approval |
| Rejected | A block returned with a comment; the employee edits that block and resubmits |
| Approved | Every project block accepted by its reviewer; locked |

Billing and invoicing states belong to another system because invoicing is a non-goal.

## Where sources disagree

- Utilization denominator: total hours or hours net of leave. This spec uses total available hours (confirmed).
- Whether "locked" and "billed" are separate states.
- Whether the project manager or the line manager approves. This spec: only the named project reviewer approves; the line manager has a read-only view (confirmed).
