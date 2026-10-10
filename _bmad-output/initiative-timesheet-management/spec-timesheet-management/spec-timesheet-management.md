---
id: SPEC-timesheet-management
companions: [premium-tier.md, glossary.md]
sources: [../brainstorm-timesheet-delight/brainstorm-timesheet-delight.md, ../research-employee-engagement-in-timesheet-filling/research-employee-engagement-in-timesheet-filling.md, ../research-timesheet-and-time-billing-domain-in-it/research-timesheet-and-time-billing-domain-in-it.md, ../research-india-labour-rules-and-payroll-inputs-fo/research-india-labour-rules-and-payroll-inputs-fo.md, ../research-timesheet-module-technical-approach-insi/research-timesheet-module-technical-approach-insi.md, ../research-bamboohr-rippling-keka-timesheet-teardow/research-bamboohr-rippling-keka-timesheet-teardow.md]
---

> **Canonical contract.** This SPEC and the files in `companions:` are the complete, preservation-validated contract for what to build, test, and validate. Source documents listed in frontmatter are for traceability — consult them only if you need narrative rationale or prose color this contract intentionally omits.

# Timesheet Management

## Why

Employees report weekly work on the HAT timesheet form, but the hours are not tied to billing or utilization. This initiative captures actual work effort per project and links it to billing and utilization, so billing and resourcing decisions rest on real hours rather than plans. It should also be quick and pleasant enough that people submit on time without being chased.

## Capabilities

- **CAP-1**
  - **intent:** An employee selects the timesheet week they are reporting.
  - **success:** A sheet cannot be submitted without a week; the chosen week is stored with the sheet.
- **CAP-2**
  - **intent:** An employee logs effort on up to 5 projects, each with project, tasks/activities, hours and reviewer; Project 1 is the primary project (most time spent).
  - **success:** A sheet with Project 1 filled and Projects 2-5 optionally filled is accepted; a block missing any of its four fields, or a sixth block, is refused.
- **CAP-3**
  - **intent:** An employee records PTO hours for the week at 8 hours per day.
  - **success:** PTO of 0 or a multiple of 8 is accepted; any other value is refused.
- **CAP-4**
  - **intent:** An employee records key accomplishments and key learnings, each learning tagged Beginner, Intermediate or Advanced.
  - **success:** A sheet without accomplishments, or with a learning lacking one of the three levels, is refused.
- **CAP-5**
  - **intent:** An employee submits the completed sheet, and the system records the submitter's name and email automatically.
  - **success:** A submitted sheet shows the submitter's name and email to the owner without the employee typing them; every required field is enforced at submit.
- **CAP-6** (proposed, unconfirmed)
  - **intent:** The reviewer named for each project approves or rejects the hours submitted against that project; a rejection carries a reason and shows the employee what changed.
  - **success:** A reviewer sees only sheets with hours against their project; a rejected line returns to the employee with a reason and a one-click fix and resubmit; a rejection without a reason is refused.
- **CAP-7** (proposed, unconfirmed)
  - **intent:** Approved hours roll up by project, employee and week into billable vs non-billable hours and utilization, and finance can export them per project with an audit trail.
  - **success:** For a given week, the roll-up for each project equals the sum of its approved hours; unapproved hours are excluded; the export reproduces the roll-up and lists who approved each line and when.
- **CAP-8**
  - **intent:** An employee starts a new week's sheet by copying the previous week's sheet and editing it.
  - **success:** Copying prefills projects, tasks and reviewers from the prior week with hours left editable; the copy is a new sheet, and the original is unchanged.
- **CAP-9**
  - **intent:** An employee reopens a submitted sheet before approval to correct it, with every change recorded.
  - **success:** A submitted, unapproved sheet can be reopened and resubmitted by its owner; the history shows who changed what and when; an approved sheet cannot be reopened.
- **CAP-10**
  - **intent:** An employee submits the published weekly sheet by 11:59 pm UTC on the day after it is published (Saturday for the usual Friday publication), and one who misses that deadline can still submit late, with a late penalty, or request an extension with a reason.
  - **success:** A sheet submitted by 11:59 pm UTC on the day after publication counts as on time; a later sheet is accepted, marked late, and carries a late penalty (a recorded late mark counted per employee and visible to the project reviewer); an extension request records its reason and waives the penalty; none of these blocks submission.
- **CAP-11** (proposed)
  - **intent:** A reviewer sees sheets with anomalies first and approves clean sheets in bulk.
  - **success:** A sheet with hours over the anomaly threshold, hours on a closed project, or a large jump from the prior week is flagged and listed first; selecting all unflagged sheets approves them in one action.
- **CAP-12**
  - **intent:** An employee gives a one-tap smiley rating after submitting, as a measure of how the process feels.
  - **success:** The rating is stored with the sheet, is optional, and never blocks or delays submit.
- **CAP-13** (proposed)
  - **intent:** An employee sees a private weekly insight card of their hours by project.
  - **success:** The card shows the employee's own hours per project for a week and is visible only to them; learnings stay private unless the employee shares them.
- **CAP-14**
  - **intent:** Employees get a reminder when their sheet is unsubmitted, and approvers get a reminder when sheets await approval.
  - **success:** An employee with no submitted sheet for the week receives a reminder before the deadline; an approver with pending sheets receives one; employees on approved leave receive none.
- **CAP-15** (retired: the payroll handoff is out of scope; the id is never reused)
- **CAP-16**
  - **intent:** The owner of an employee's Project 1 (the primary project) publishes the weekly sheet in the app, usually on Friday, which makes it available to that employee to fill in.
  - **success:** An employee cannot start a week's sheet until the Project 1 owner has published it; publication records who published and when; the submission deadline counts from that moment.

## Constraints

- A sheet has at most 5 project blocks; each has exactly project, tasks/activities, hours and reviewer.
- PTO is entered in hours, 8 per day.
- The submitter's name and email come from the signed-in identity, never from form fields.
- The billable flag lives on the project.
- Identity, project list and reviewer list come from the existing HRMS, not admin-maintained lists.
- Approved hours are immutable; a later correction creates a recorded adjustment, never a silent edit.
- Hours are for billing and resourcing, never a performance score; no public individual rankings or shaming lists.
- An employee has exactly one sheet per week; a second sheet for the same employee and week is refused.
- A sheet is in exactly one state: draft, submitted, rejected or approved; approved means locked. After submission the named project reviewer approves or rejects it. Terms are defined in `glossary.md`.
- Hours are entered per project per week, never per day; every employee, including exempt IT staff, submits weekly effort only.
- Submitted sheets, approved sheets and their change history are kept at least 3 years, a generic rule modelled on the US; the owner confirms it for the operating country.
- A late, rejected or incorrect sheet never changes pay for hours worked; this module reports hours and never withholds, delays or reduces pay, and the late penalty is only a recorded late mark.
- Reminders are scheduled against UTC and sent at most once per employee, reminder kind and week, so a retry or a clock change never sends a duplicate or a late reminder.

## Non-goals

- Payroll calculation or processing, leave balances or leave approval.
- Any payroll handoff: loss-of-pay (LOP) days, payable days, the payroll cut-off, and the payroll data format are out of scope (CAP-15 retired).
- Invoicing; this initiative supplies billable hours, not invoices.
- Attendance or clock-in tracking.
- Auto-drafting the week from calendar or tickets in v1 (see `premium-tier.md`).
- Ambient time capture, an hours marketplace, and a continuous rolling week.
- Choosing the tech stack, hosting, observability, backups or CI/CD; these belong to the architecture step, not this spec.

## Success signal

An employee completes and submits a full weekly sheet in one sitting, and billing can read that week's approved hours per project without re-keying anything.

## Assumptions

- Only Project 1 is required; Projects 2-5 are optional, although the source form marks every field required.
- Hours are in 0.5 steps, and project hours plus PTO total at most 40 per week.
- CAP-6 and CAP-7 are in scope for this initiative although the form does not mention them; the brainstorm extended them but they remain unconfirmed.
- Non-goals inferred from the objective are not stated by the user.
- Anomaly thresholds (such as a 45-hour week) are starting values for the owner to set.
- Reopening is only by the original employee and only before approval.
- Approvals (CAP-6) stay in the core product although competitors gate them behind paid plans, because they are core in an HRMS module.
- All capabilities ship free for now with no pricing; `premium-tier.md` lists future candidates only, and its competitor prices come from vendor pages without a second source.
- The owner holds that reminders and copy-last-week raise on-time submission; this is a belief, not research evidence, and the on-time rate is still to be measured.
- The submission deadline is 11:59 pm UTC on the day after the sheet is published (owner), so Saturday 11:59 pm UTC for the usual Friday publication; a late sheet is still accepted, marked late, and carries the late penalty.
- Publication by the Project 1 owner opens the whole sheet for the employee, including Projects 2-5; the owner's answer was cut off, so confirm this.
- The 11:59 pm UTC deadline is a fixed instant for every employee regardless of local time zone.
- If a sheet is published on a day other than Friday, the deadline is still 11:59 pm on the following day; the owner said publication is mostly Friday.
- Late-sheet handling never delays pay or hard-locks submission; this rests on US guidance and has not had legal review.
- Approved means locked, with no separate billed state, because invoicing is a non-goal (confirmed).
- Utilization and realization use total available hours as the denominator in `glossary.md` (confirmed).
- The named project reviewer approves project hours; line-manager and finance approval roles are out of scope for now (confirmed).
- The late penalty is the late mark: a recorded mark counted per employee and visible to the project reviewer (confirmed by the owner).
- An approved extension request waives the late penalty for that sheet.
- The 3-year retention is the owner's generic rule, based on US practice with no country-specific follow-up; the domain research was US-default, mostly vendor-sourced, and is not legal advice.

## Open Questions

None.
