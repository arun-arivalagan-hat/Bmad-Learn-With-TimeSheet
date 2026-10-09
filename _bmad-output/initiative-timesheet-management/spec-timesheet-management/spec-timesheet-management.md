---
id: SPEC-timesheet-management
companions: []
sources: []
---

> **Canonical contract.** This SPEC and the files in `companions:` are the complete, preservation-validated contract for what to build, test, and validate. Source documents listed in frontmatter are for traceability — consult them only if you need narrative rationale or prose color this contract intentionally omits.

# Timesheet Management

## Why

Employees report weekly work on the HAT timesheet form, but the hours are not tied to billing or utilization. This initiative captures actual work effort per project and links it to billing and utilization, so billing and resourcing decisions rest on real hours rather than plans.

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
  - **intent:** The reviewer named for each project approves or rejects the hours submitted against that project.
  - **success:** A reviewer sees only sheets with hours against their project; a rejected line returns to the employee with a reason.
- **CAP-7** (proposed, unconfirmed)
  - **intent:** Approved hours roll up by project, employee and week into billable vs non-billable hours and utilization.
  - **success:** For a given week, the roll-up for each project equals the sum of its approved hours; unapproved hours are excluded.

## Constraints

- A sheet has at most 5 project blocks; each has exactly project, tasks/activities, hours and reviewer.
- PTO is entered in hours, 8 per day.
- The submitter's name and email come from the signed-in identity, never from form fields.

## Non-goals

- Payroll, leave balances or leave approval.
- Invoicing; this initiative supplies billable hours, not invoices.
- Attendance or clock-in tracking.

## Success signal

An employee completes and submits a full weekly sheet in one sitting, and billing can read that week's approved hours per project without re-keying anything.

## Assumptions

- Only Project 1 is required; Projects 2-5 are optional, although the source form marks every field required.
- Hours are in 0.5 steps, and project hours plus PTO total at most 40 per week.
- CAP-6 and CAP-7 are in scope for this initiative although the form does not mention them.
- Non-goals above are inferred from the objective, not stated by the user.

## Open Questions

- Where do the project and reviewer lists and user identity come from: an existing HAT-HRMS source, or admin-maintained lists?
- What is the tech stack and deployment target?
- Where does the billable flag live: on the project, the employee, or the timesheet line?
- Can a submitted sheet be edited or resubmitted for the same week, and is one sheet per employee per week enforced?
