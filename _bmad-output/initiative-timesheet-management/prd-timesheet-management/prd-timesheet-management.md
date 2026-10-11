---
title: Timesheet Management
status: final
created: 2026-10-11
updated: 2026-10-11
---

# PRD: Timesheet Management
*Working title: confirm.*

## 0. Document purpose

*To confirm:* the working title, the legal question in section 9, and the assumptions in section 10.

This PRD is for the module owner, project managers, HR and finance stakeholders, and the teams who run UX, architecture and ticket slicing next. It builds on the spec (`../spec-timesheet-management/spec-timesheet-management.md`, with `glossary.md` and `premium-tier.md`), the product brief, the PRFAQ, the brainstorm and six research folders, and does not duplicate them. Spec capability IDs (CAP-n) are kept, and each FR (FR-n) names the CAP it realizes. Terms follow the glossary in section 3; inferred points are tagged `[ASSUMPTION]` and indexed in section 10. Stack, hosting and vendor choices belong to the architecture step.

## 1. Vision

Timesheet Management is a weekly timesheet inside the HRMS. Each employee records the effort they spent per project in one short sitting, and billing and resourcing read the approved hours without re-keying anything.

Today the weekly report on the HAT form is not tied to billing or utilization, and project managers spend about 19 hours a week collecting and checking hours (owner figure, unverified). The module captures real effort per project, routes it to the named project reviewer for approval, and locks approved hours so they never change silently.

It must also be quick enough that people submit on time without being chased. Reminders, copy-last-week and a late-mark rule that HR owns serve that goal. The module reports hours and never touches pay.

## 2. Target User

Scale for v1: 160 employees and 20 projects.

### 2.1 Jobs to be done
- **Employee:** report my week accurately in one sitting, and not be chased.
- **Project reviewer:** approve clean sheets quickly and send back wrong ones with a comment.
- **Project 1 owner:** publish the week's sheet and see who has submitted.
- **Project manager:** stop spending hours collecting and checking hours by hand.
- **Finance:** read approved hours per project with an audit trail.
- **HR:** see approved hours and late marks, and decide any consequences.

### 2.2 Non-users (v1)
- Clients; there is no client-facing view.
- Anyone needing payroll, loss-of-pay or leave processing; these are out of scope.

### 2.3 Key user journeys

- **UJ-1. Meera submits her week before the deadline.**
  - **Persona + context:** Meera, an engineer on two projects, wants to finish the timesheet in one sitting.
  - **Entry state:** signed in through the HRMS; her Project 1 owner published the sheet on Friday.
  - **Path:** opens the week, copies last week's sheet, edits hours for Project 1 and Project 2, adds 8 PTO hours for one leave day, writes accomplishments and a Beginner/Intermediate/Advanced learning, submits.
  - **Climax:** the sheet shows as submitted with her name and email filled in automatically, and she taps a smiley.
  - **Resolution:** the sheet waits for her project reviewer; no reminder arrives.
  - **Edge case:** she remembers a mistake after submitting; she reopens the sheet before approval, fixes it, and resubmits; the history shows the change.

- **UJ-2. Ravi reviews sheets and sends one back.**
  - **Persona + context:** Ravi, a project reviewer, has sheets waiting on Monday morning.
  - **Entry state:** receives a reviewer reminder.
  - **Path:** sees sheets with anomalies listed first, approves all unflagged sheets in one action, opens a flagged sheet (a 40-hour week after a 12-hour week), and rejects it with a comment.
  - **Climax:** the employee gets the sheet back with his comment.
  - **Resolution:** the employee edits and resubmits; Ravi approves.
  - **Edge case:** the Project 1 owner can see the sheet's status but cannot approve or reject it.

- **UJ-3. Anita misses the deadline.**
  - **Persona + context:** Anita was on leave on Friday and opens the published sheet on Monday.
  - **Path:** submits late, or requests an extension with a reason.
  - **Climax:** a late submission is accepted and carries a late mark; an approved extension request waives it.
  - **Resolution:** she sees her own late marks; HR sees them and decides any consequences.

- **UJ-4. Priya publishes the week.** *(Short form: this journey has one scene.)* Priya, a Project 1 owner, publishes the sheet on Friday for her team, then watches who has and has not submitted. She does not approve.

## 3. Glossary

Terms are used exactly. Full definitions are in `../spec-timesheet-management/glossary.md`; the core ones:

- **Sheet** — one employee's weekly timesheet; exactly one per employee per week.
- **Sheet states** — Draft, Submitted, Rejected, Approved. Approved means locked.
- **Project block** — one project's entry: project, tasks/activities, hours and reviewer; up to 5 per sheet; Project 1 is the primary project.
- **Published sheet** — the sheet the Project 1 owner has made available; the deadline counts from publication.
- **Project reviewer** — the person named for a project who approves or rejects its hours.
- **Late mark** — recorded mark on a sheet submitted after the deadline; visible to the employee, the project reviewer and HR; never affects pay.
- **Adjustment entry** — a recorded correction to an approved sheet.
- **Billable flag** — a flag set on a project that marks its hours as billable.
- **Project 1 owner** — the owner of an employee's primary project.
- **Project manager** — manages projects and people; the module's primary customer.
- **Reporting manager** — the employee's line manager.
- **Finance** — reads approved hours and exports.
- **Weekly effort** — hours per project per week, never per day.

## 4. Features

### 4.1 Sheet entry and submission

**Description:** The employee picks a week and fills project blocks, PTO, accomplishments and learnings, then submits. Name and email come from the signed-in identity. Realizes UJ-1.

#### FR-1: Pick the week (CAP-1)
An employee selects the week being reported. **Consequences:** a sheet cannot be submitted without a week; a second sheet for the same employee and week is refused.

#### FR-2: Log project blocks (CAP-2)
An employee logs up to 5 project blocks, each with project, tasks/activities, hours and reviewer; Project 1 is required, Projects 2 through 5 optional. **Consequences:**
- A block missing any of its four fields is refused; a sixth block is refused.
- Hours are entered in 0.5-hour increments and per project per week, never per day.
- Projects and reviewers come from the HRMS, not a separately maintained list.
- Every employee, including exempt IT staff, enters weekly effort only, never daily hours.

#### FR-3: Record PTO (CAP-3)
An employee records PTO hours at 8 per day. **Consequences:** 0 or a multiple of 8 is accepted; anything else is refused.

#### FR-21: Weekly hours cap (CAP-2, CAP-3)
**Consequences:** project hours plus PTO total at most 40 per week; a sheet above 40 is refused. `[ASSUMPTION: no overtime or holiday handling in v1; the cap is a flat 40.]`

#### FR-4: Accomplishments and learnings (CAP-4)
**Consequences:** a sheet without accomplishments is refused; each learning needs one of Beginner, Intermediate or Advanced.

#### FR-5: Submit (CAP-5)
**Consequences:** the sheet shows the submitter's name and email without typing; all required fields are enforced at submit.

#### FR-6: Copy last week (CAP-8)
**Consequences:** the copy prefills projects, tasks and reviewers with hours editable; it is a new sheet and the original is unchanged.

#### FR-7: Reopen before approval (CAP-9)
**Consequences:** the employee who submitted an unapproved sheet can reopen and resubmit it; history records who changed what and when; an approved sheet cannot be reopened.

#### FR-8: Smiley rating (CAP-12)
**Consequences:** optional, stored with the sheet, never blocks or delays submit.

#### FR-9: Weekly insight card (CAP-13)
**Consequences:** shows the employee's own hours per project for a week, visible only to them; learnings stay private unless shared.

### 4.2 Publishing, deadline and late marks

**Description:** The Project 1 owner publishes the week; the deadline is 11:59 pm UTC on the day after publication. Late sheets are accepted with a late mark; extensions waive it. Realizes UJ-3, UJ-4.

#### FR-10: Publish the sheet (CAP-16)
The Project 1 owner publishes the weekly sheet, usually on Friday. **Consequences:**
- An employee cannot start the week's sheet until it is published.
- Publication records who published and when, and the deadline counts from that moment.
- Publication opens the whole sheet, including Projects 2 through 5.
- Employees are notified when their sheet is published, on whatever day that is.
- If the owner has not published, HR can publish on the owner's behalf; the deadline still counts from publication.

#### FR-11: Deadline and late mark (CAP-10)
**Consequences:**
- A sheet submitted by 11:59 pm UTC on the day after publication is on time, for every employee regardless of time zone.
- A later sheet is accepted and carries a late mark; nothing blocks submission.
- Lateness is judged on the first submission only; a sheet that was on time and is later rejected and resubmitted after the deadline gets no late mark.
- A sheet is never marked late unless it was published.
- The late mark is the only mark that can attach to an approved sheet.

#### FR-12: Extension request (CAP-10)
An employee requests an extension with a reason. **Consequences:** the request records its reason; the project reviewer for the employee's Project 1 block approves or declines it `[ASSUMPTION: the Project 1 reviewer decides, since a sheet has several reviewers]`; an approved extension waives the late mark. There is no limit on how many extensions an employee can request.

#### FR-13: Employee sees own late marks (CAP-18)
**Consequences:** the employee sees each late mark with the week and the deadline missed, and no one else's.

#### FR-14: Reminders (CAP-14)
**Consequences:** an employee with no submitted sheet gets a reminder before the deadline; a project reviewer with pending sheets gets one; employees on approved leave get none; at most one reminder per person, kind and week.

#### FR-22: Submission status view for the Project 1 owner (CAP-16)
**Consequences:** the Project 1 owner sees which of their published sheets were submitted on time, submitted late, or not yet submitted; the view is read-only and never lets the owner approve or reject.

### 4.3 Approval and review

**Description:** The named project reviewer approves or rejects with a comment. The Project 1 owner only views; the reporting manager has no approval role (read-only view in FR-20). Realizes UJ-2.

#### FR-15: Approve or reject with comment (CAP-6)
**Consequences:**
- A project reviewer sees only sheets with hours against their project, and approves or rejects only their own project's block.
- A rejection requires a comment and returns only that block to the employee, who sees what was rejected and why, fixes it in one click and resubmits.
- The sheet is Approved and locked when every block is approved; until then it is Submitted.
- Approved blocks are not reopened by another reviewer's rejection.

#### FR-16: Anomaly-first review and bulk approve (CAP-11)
**Consequences:** a sheet with hours on a closed project or a sheet whose total hours differ from the prior week by more than 15 hours is flagged and listed first `[ASSUMPTION: the 15-hour jump is a starting value]`; selecting all unflagged sheets approves them in one action.

#### FR-17: Corrections after approval (CAP-9, CAP-7)
**Consequences:** a correction to an approved sheet is a recorded adjustment entry, never a silent edit, with a reason and who made it. `[ASSUMPTION: the project reviewer records adjustments.]`

### 4.4 Reporting and HR visibility

#### FR-18: Hours roll-up and finance export (CAP-7)
**Consequences:** approved hours roll up by project, employee and week into billable and non-billable hours and utilization (denominator: total available hours); unapproved hours are excluded; the export reproduces the roll-up and lists who approved each line and when.

#### FR-19: HR read-only view (CAP-17)
**Consequences:** HR sees approved hours, late marks and approval status for any employee and week; HR cannot edit sheets, hours or late marks.

#### FR-20: Reporting manager read-only view (CAP-17 extended)
A reporting manager sees their direct reports' approved hours, late marks and approval status per week. **Consequences:** the reporting manager cannot edit, approve, reject or waive anything; they see only their own direct reports.

## 5. Non-goals

- Payroll calculation or processing, loss-of-pay, payable days, payroll cut-off (CAP-15 is retired; its id is not reused).
- Leave balances or leave approval.
- Invoicing; the module supplies billable hours, not invoices.
- Attendance or clock-in tracking.
- Auto-drafting from calendar or tickets, ambient capture, an hours marketplace, a continuous rolling week.
- Public rankings or lists of late employees.
- Pay consequences of any kind: the module never withholds, delays or reduces pay.

## 6. MVP Scope

### 6.1 In Scope
FR-1 through FR-22, for about 160 employees and 20 projects. Everything ships free; there is no pricing.

### 6.2 Out of Scope for MVP
Everything in section 5, plus the paid-tier candidates in `premium-tier.md` and a client-facing view.

## 7. Success Metrics

**Primary**
- **SM-1**: Share of sheets submitted on time, measured as one minus the late-mark rate per week, from launch. No target yet. Validates FR-6, FR-10, FR-11, FR-14.
- **SM-2**: An employee completes a full sheet in one sitting, and finance reads a week's approved hours per project without re-keying; checked by a short monthly question to employees and finance. Validates FR-5, FR-18.

**Secondary**
- **SM-3**: Smiley rating trend. No target. Validates FR-8.
- **SM-4**: Weekly hours project managers spend collecting hours, against the ~19-hour baseline; checked by asking project managers monthly. No target is set.

**Counter-metrics (do not optimize)**
- **SM-C1**: Late marks issued. Do not minimize at the cost of accuracy; HR consequences must not push employees to submit careless sheets. Counterbalances SM-1.
- **SM-C2**: Rejection rate. Do not push it to zero by approving without checking. Counterbalances FR-16 bulk approve.

`[ASSUMPTION: the owner's "late mark" measure is read as the late-mark rate being the on-time measure; no numeric targets are set.]`

## 8. Cross-Cutting Requirements

- **Data governance:** submitted sheets, approved sheets and change history are kept at least 3 years (owner's generic rule). HR sees late marks and approved hours; learnings are private unless shared.
- **Auditability:** approved hours are immutable; every change and approval is recorded with who and when.
- **Identity and data:** identity, projects and reviewers come from the HRMS.
- **Experience:** the module should feel quick and forgiving; it never shames. Gamification, if ever added, is opt-in and team-level only. HR, not this module, decides any consequences of late marks, so late marks must be accurate.
- **Reminders:** scheduled in UTC, at most one reminder per person, kind and week.
- **Fairness:** an approved sheet is never reported as incorrect; an extension waives the late mark.
- **Legal:** the owner confirmed 3-year retention; India's 5-year rule is not adopted. Late-mark handling and retention have had no legal review; the owner accepts this risk and has closed the question.

## 9. Open questions

No questions are open. Resolved decisions are logged in `.memlog.md`.

## 10. Assumptions Index

- FR-16 — the anomaly jump threshold of 15 hours is a starting value.
- Section 7 — late mark read as the on-time measure; no targets.
- FR-12 — the Project 1 reviewer decides extensions.
- FR-17 — the project reviewer records adjustments.
- FR-21 — flat 40-hour cap, no overtime or holiday handling.
- Section 7 — SM-2 and SM-4 are checked by a monthly question; no tooling.
