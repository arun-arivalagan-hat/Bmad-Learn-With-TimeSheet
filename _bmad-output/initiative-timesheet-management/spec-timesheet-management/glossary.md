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
| Adjustment entry | A dated correction to approved block hours, recorded directly by the named reviewer when eligible or an eligible alternate in the current tier at any time, with a mandatory reason and a notice to the named reviewer, the first valid recording winning, with eligibility, block version and net hours rechecked at recording time and no separate request object, carrying the block, the change in hours, the net hours before and after, the reason and the eligibility result, bound to the net hours reviewed, recorded against the original week on top of the preserved original block and never a silent edit; counted in the net roll-up without double-counting; HR sees adjustment history for audit only |
| HR exception queue | The list of blocks, extension requests and adjustment-needed flags with no eligible decider or recorder; HR is notified on entry and assigns an eligible alternate who holds no HR role, never deciding or recording; the adjustment-needed flag is raised by HR with a reason and is open, assigned or recorded; entries, refused assignments and assignments are recorded in the history |
| Eligible decider | The single rule (spec constraints) for deciding a block or an extension request, recording an adjustment or being assigned from the HR queue: at the instant, on authoritative HRMS data, not the employee, not the conflicted named reviewer, not that sheet's Project 1 owner (snapshotted and current owner, or every candidate owner while flagged) or delegate (naming in effect, or having published that sheet), active, not on approved leave, and for queue assignment holding no HR role; an HR-role holder may decide only in a separate reporting-manager or delivery-manager capacity; the check fails closed when HRMS data cannot be verified; designating a delegate is independent of this rule and grants no eligibility |
| Extension request status | Pending, approved or declined; an approved extension records a waiver and the original late mark stays in the history as waived |
| Block version | Each resubmission of a project block creates a new version; approve and reject apply to the exact version the reviewer saw, and a stale action is refused |
| Leave-only sheet | A sheet type (not a state) for a timesheet week whose Monday to Friday working days are all covered by approved HRMS leave; PTO is derived from HRMS; no submission, reviewer approval, late mark or reminder; excluded from the unpublished list; zero project hours for finance; converts automatically only when the sheet has no blocks, publication, recorded decision or late mark, otherwise the case is flagged for authorized, audited resolution |
| Issued export | A dated snapshot of the finance export that is retained and never rewritten; later exports carry the dated adjustment history |
| Published sheet | The weekly sheet the Project 1 owner, their delegate or HR has made available to an employee, usually on Friday; published per employee per week; the submission deadline (publication plus 24 hours) counts from publication |
| Timesheet week | Monday 00:00 to the next Monday 00:00 in Asia/Kolkata; timestamps are stored in UTC and shown in IST |
| Submission deadline | The publication timestamp plus 24 hours; stored in UTC, shown in IST; never shortened when publication is late or the deadline falls after the week ends |
| Delegate publisher | An active employee not on approved leave when named and explicitly designated by the Project 1 owner to publish sheets in the owner's place; designation is independent of the Eligible Decider rule and grants no decision eligibility; a naming is the owner plus the current timesheet week only, covers all that owner's employees' sheets for that week, expires at the Monday 00:00 IST that ends the week and must be in effect when publishing; publishes and views submission status only, never approves or rejects, may publish their own sheet without ever deciding it, and stays excluded from deciding a sheet they published after the naming expires |
| Assignment-pending flag | A sheet attribute, not a state, with four reason codes: missing primary project, conflicting primary project, missing owner, multiple owners; HR is notified for all four and the case is listed in the assignment-resolution list; a missing or conflicting primary project waives the Project 1 requirement while it is open (no Project 1 is guessed, the employee may submit otherwise valid blocks); a missing or multiple owners code does not waive it and the sheet goes to HR for publication after the cut-off; all candidate owners are excluded from deciding when the primary project conflicts or owners are multiple; it leaves when the HRMS verifiably shows exactly one primary project and one owner; recorded decisions and lateness judgements are never rewritten |
| Assignment snapshot | The employee's primary project and owner recorded at publication; the sheet keeps them for status view, submit and extension routing, and a later HRMS transfer does not refuse a submit; an HRMS change after publication flags the affected pending item for resolution and never rewrites a recorded decision |
| Held late mark | A late mark recorded in history but not counted, for a first submission that fell after the deadline when a qualifying attempt (an HRMS-caused refused submit on the same sheet, recorded before the first successful submission) exists or an observed outage window overlaps the period between publication and the deadline; a failed attempt recorded after the deadline is a trigger for review, never proof of an outage; the sheet is flagged outage-affected, the actual submission time is kept, and an automatically raised extension request, judged on system-recorded evidence, resolves it (approved: waived; declined: counts) |
| Observed outage window | A period in which the module observed the HRMS as unavailable, recorded with start, end and how it was observed; used as evidence for a held late mark |
| HR publish cut-off | Friday 12:00 PM IST (06:30 UTC) of the timesheet week; from then HR may publish any sheet still unpublished, for all projects; the first successful publication wins |
| Awaiting submission / Not submitted | HR's view of a published sheet: awaiting submission before its deadline, not submitted after it; no late mark attaches to a sheet never submitted |
| Late mark | The late penalty: a recorded mark on a sheet submitted after the deadline, counted per employee and visible to the employee, project reviewer, reporting manager and HR; it never affects pay by itself; HR sees it and decides any consequences; a waived mark stays in the audit history, shown as waived; a mark on an outage-affected submission is held until resolved |
| Weekly effort | Hours per project for a week; the only entry level in this module, including for salaried IT staff |
| Project block | One project's entry on a sheet: project, tasks/activities and hours entered by the employee, plus the project's HRMS-assigned reviewer shown read-only; up to 5 per sheet |
| Project reviewer | The person the HRMS assigns as reviewer of a project, who approves or rejects the hours in that project's block |
| Project 1 owner | The HRMS owner of the employee's primary project (one primary project per employee in the HRMS), snapshotted at publication; publishes the sheet and sees submission status; never approves, and is excluded from deciding that employee's sheet, by the snapshotted and the current assignment |
| Reporting manager | The employee's line manager; read-only view of direct reports' hours, late marks and approval status; decides only as the first eligible decider in the alternate chain (self-review, an ineligible or conflicted reviewer, the matching extension request, or an adjustment), never otherwise and never for a sheet where they are the employee or that sheet's Project 1 owner or delegate |
| Alternate approver | The person who decides a project block when its named reviewer is the employee who submitted the sheet, or is inactive in HRMS, on approved leave or conflicted as that sheet's Project 1 owner or delegate: a tiered chain: the employee's designated reporting manager when eligible, and holders of the delivery-manager HRMS role only when the reporting manager is ineligible, eligibility being the Eligible Decider rule; when none is eligible the block or extension request enters the HR exception queue, HR assigns an eligible alternate, and HR in the HR role never approves, rejects or decides |
| Authorized delivery manager | A role designated in the HRMS by an authorized HR administrator; several holders are allowed, they act only as the second tier after the reporting manager, any eligible holder may decide and the first valid decision wins; which holders count for a given employee is a provisional default (all holders) |
| Self-review | A project block whose named reviewer is the employee who submitted the sheet; no one approves, rejects or adjusts their own block |

## Timesheet states

Sheet states derive from the states of its project blocks. Each block is Draft, Submitted, Rejected or Approved, and its own status is always shown. Precedence: Approved when every block is approved; otherwise Changes required while any block is rejected and not yet resubmitted; otherwise Submitted after submit; otherwise Draft.

| Sheet state | Meaning |
|---|---|
| Draft | Started, not submitted; the employee can edit |
| Submitted | Sent to the project reviewers; the employee can reopen rejected blocks and blocks no reviewer has decided yet |
| Changes required | Any block is rejected and not yet resubmitted; the employee edits that block and resubmits; approved blocks stay locked |
| Approved | Every project block accepted by its reviewer; locked |

| Block state | Meaning |
|---|---|
| Rejected | A block returned with a comment by its reviewer |
| Approved | A block accepted by its reviewer; immutable, and never unlocked by reopening; a correction is an adjustment entry |

Billing and invoicing states belong to another system because invoicing is a non-goal.

## Where sources disagree

- Utilization denominator: total hours or hours net of leave. This spec uses total available hours (confirmed).
- Whether "locked" and "billed" are separate states.
- Whether the project manager or the line manager approves. This spec: only the named project reviewer approves; the line manager has a read-only view and decides only as the first eligible decider in the alternate chain (confirmed).
