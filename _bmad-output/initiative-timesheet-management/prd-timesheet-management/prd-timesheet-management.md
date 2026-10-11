---
title: Timesheet Management
status: final
created: 2026-10-11
updated: 2026-10-11
---

# PRD: Timesheet Management
*Working title: confirm.*

## 0. Document purpose

*To confirm:* the working title, the open questions in section 9, and the assumptions in section 10.

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
  - **Edge case:** she remembers a mistake after submitting; she reopens the block no reviewer has decided yet, fixes it, and resubmits; the history shows the change.

- **UJ-2. Ravi reviews sheets and sends one back.**
  - **Persona + context:** Ravi, a project reviewer, has sheets waiting on Monday morning.
  - **Entry state:** receives a reviewer reminder.
  - **Path:** sees sheets with anomalies listed first, approves his own block on all unflagged sheets in one action, opens a flagged sheet (a 40-hour week after a 12-hour week), and rejects his block of it with a comment.
  - **Climax:** the employee gets the block back with his comment.
  - **Resolution:** the employee edits and resubmits; Ravi approves.
  - **Edge case:** the Project 1 owner can see the sheet's status but cannot approve or reject it.
  - **Edge case:** when Ravi is inactive in the HRMS or on approved leave, the blocks that name him go to the alternate approver chain and are decided there (FR-24).
  - **Edge case:** Ravi is also a project manager whose own sheet names him as the reviewer of his own block; he sees no approve or reject action there, and his reporting manager decides it (FR-23).

- **UJ-3. Anita misses the deadline.**
  - **Persona + context:** Anita was on leave on Friday and opens the published sheet on Monday.
  - **Path:** submits late, or requests an extension with a reason.
  - **Climax:** a late submission is accepted and carries a late mark; an approved extension request waives it.
  - **Resolution:** she sees her own late marks; HR sees them and decides any consequences.
  - **Edge case:** Anita is on leave for one day, not the whole week, so her sheet is a normal sheet and the late mark applies; a week fully covered by approved leave is a leave-only sheet with nothing to submit (FR-25).

- **UJ-4. Priya publishes the week.** *(Short form: this journey has one scene.)* Priya, a Project 1 owner, publishes the sheet on Friday for her team, then watches who has and has not submitted. She does not approve. *Edge case:* when Priya is away she names a delegate for that week, and if neither publishes by Friday 12:00 PM IST, HR publishes it; the deadline counts from whenever it is published.

## 3. Glossary

Terms are used exactly. Full definitions are in `../spec-timesheet-management/glossary.md`; the core ones:

- **Sheet** — one employee's weekly timesheet; exactly one per employee per week.
- **Sheet states** — Draft, Submitted, Changes required, Approved, derived from the project blocks by precedence: Approved when every block is approved, otherwise Changes required while any block is rejected and not yet resubmitted, otherwise Submitted after submit, otherwise Draft; each block's own status (Draft, Submitted, Rejected or Approved) is always shown. Approved means locked, and approved blocks stay locked when another block is rejected or reopened.
- **Approved block** — one project's hours in a sheet that its authorized reviewer has approved; those hours are locked.
- **Approved sheet** — a sheet in which every project block is approved.
- **Timesheet week** — Monday 00:00 to the next Monday 00:00 in Asia/Kolkata; timestamps are stored in UTC and shown in IST.
- **Submission deadline** — the publication timestamp plus 24 hours; never shortened when publication is late or the deadline falls after the week ends.
- **Project block** — one project's entry: project, tasks/activities and hours entered by the employee, plus the project's HRMS-assigned reviewer shown read-only; up to 5 per sheet; Project 1 is the employee's HRMS primary project.
- **Published sheet** — the sheet the Project 1 owner, their delegate or HR has made available; published per employee per week; the deadline counts from publication.
- **Delegate publisher** — an active employee not on approved leave when named and explicitly designated by the Project 1 owner; a naming is the owner plus the current timesheet week only, covers all that owner's employees' sheets for that week and expires at the Monday 00:00 IST that ends it; designation is independent of the Eligible Decider rule and grants no decision eligibility; publishes and views submission status only, never approves or rejects, may publish their own sheet without ever deciding it, and stays excluded from deciding a sheet they published after the naming expires.
- **Assignment-pending flag** — a sheet attribute, not a state, with four reason codes: missing primary project, conflicting primary project, missing owner, multiple owners (FR-2); HR is notified for all four and the case is listed in the assignment-resolution list; a missing or conflicting primary project waives the Project 1 requirement while it is open; a missing or multiple owners code does not, and the sheet goes to HR for publication after the cut-off; it leaves when the HRMS verifiably shows exactly one primary project and one owner.
- **Assignment snapshot** — the employee's primary project and owner recorded at publication; the sheet keeps them for status view, submit and extension routing (FR-2, FR-10).
- **Observed outage window** — a period in which the module observed the HRMS as unavailable, with start, end and how it was observed; evidence for a held late mark (FR-11).
- **Held late mark** — a late mark recorded in history but not counted, for a first submission after the deadline when a qualifying HRMS-caused refused submit on the same sheet was recorded before that submission, or an observed outage window overlaps the period between publication and the deadline (FR-11); a failed attempt recorded after the deadline is never proof of an outage by itself; an automatically raised extension request resolves it.
- **Project reviewer** — the person the HRMS assigns as reviewer of a project, who approves or rejects its hours.
- **Late mark** — recorded mark on a sheet submitted after the deadline; visible to the employee, the project reviewer, the reporting manager and HR; the Project 1 owner sees only whether a sheet was on time or late; never affects pay; a waived mark stays in the audit history, shown as waived; a mark on an outage-affected submission is held until resolved.
- **Undecided block** — a project block that no reviewer has approved or rejected yet.
- **HR publish cut-off** — Friday 12:00 PM IST (06:30 UTC) of the timesheet week; from then HR may publish a sheet still unpublished.
- **Extension request** — an employee's request, with a reason, to waive the late mark on a sheet (FR-12); its status is pending, approved or declined.
- **HR exception queue** — the list of blocks, extension requests and adjustment-needed flags with no eligible decider or recorder; HR is notified on entry and assigns an eligible alternate who holds no HR role, never deciding or recording (FR-24); an adjustment-needed flag is raised by HR with a reason and is open, assigned or recorded (FR-17).
- **Eligible decider** — the single rule for deciding a block or an extension request, recording an adjustment or being assigned from the HR queue: at the instant, on authoritative HRMS data, not the employee, not the conflicted named reviewer, not that sheet's Project 1 owner (snapshotted and current owner, or every candidate owner while flagged) or delegate (naming in effect, or having published that sheet), active, not on approved leave, and for a queue assignment holding no HR role; an HR-role holder may decide only in a separate reporting-manager or delivery-manager capacity; the check fails closed when HRMS data cannot be verified; designating a delegate is independent of it. All other sections refer to this rule.
- **Adjustment entry** — a dated correction to approved block hours, recorded directly by the named reviewer when eligible or an eligible alternate in the current tier, at any time (the first valid recording wins) on top of the preserved original block, with no separate request object; never a silent edit; counted in the net roll-up without double-counting.
- **Block version** — each resubmission of a project block creates a new version; approve and reject apply to the exact version reviewed.
- **Leave-only sheet** — a sheet type, not a state, for a week whose Monday to Friday working days are all covered by approved HRMS leave (FR-25).
- **Issued export** — a dated snapshot of the finance export that is retained and never rewritten; later exports carry the dated adjustment history.
- **Billable flag** — a flag set on a project that marks its hours as billable.
- **Project 1 owner** — the HRMS owner of the employee's primary project (one per employee in the HRMS); never approves, and is excluded from deciding that employee's sheet.
- **Project manager** — manages projects and people; the module's primary customer.
- **Reporting manager** — the employee's line manager; reads direct reports' hours, late marks and approval status, and decides only as the first eligible decider in the alternate chain (self-review, an ineligible or conflicted reviewer, the matching extension request, or an adjustment), never otherwise and never for a sheet where they are the employee or that sheet's Project 1 owner or delegate.
- **Alternate approver** — who decides a project block when its named reviewer is the employee who submitted the sheet, or is inactive in the HRMS, on approved leave or conflicted as that sheet's Project 1 owner or delegate (FR-24): a tiered chain, the employee's designated reporting manager when eligible and holders of the delivery-manager HRMS role only when the reporting manager is ineligible, eligibility being the Eligible Decider rule; when none is eligible the block or extension request enters the HR exception queue and HR assigns an eligible alternate; HR in the HR role never approves, rejects or decides.
- **Authorized delivery manager** — a role designated in the HRMS by an authorized HR administrator; several holders are allowed, they act as the second tier only, any eligible holder may decide and the first valid decision wins.
- **Self-review** — a project block whose named reviewer is the employee who submitted the sheet; no one approves, rejects or adjusts their own block.
- **Finance** — reads approved hours and exports.
- **Weekly effort** — hours per project per week, never per day.

## 4. Features

### 4.1 Sheet entry and submission

**Description:** The employee picks a week and fills project blocks, PTO, accomplishments and learnings, then submits. Name and email come from the signed-in identity. Realizes UJ-1.

#### FR-1: Pick the week (CAP-1)
An employee selects the week being reported. **Consequences:** a sheet cannot be submitted without a week; a second sheet for the same employee and week is refused.

#### FR-2: Log project blocks (CAP-2)
An employee logs up to 5 project blocks, each with project, tasks/activities and hours; the reviewer comes from the project's HRMS assignment and is shown, not entered; Project 1 is the employee's HRMS primary project and is required except while an assignment-pending flag for a missing or conflicting primary project is open, Projects 2 through 5 optional. **Consequences:**
- A block missing its project, tasks/activities or hours is refused; a sixth block is refused.
- The reviewer is display-only; a project with no HRMS reviewer assignment is flagged for resolution and its blocks route down the alternate chain (FR-24).
- Hours are entered in 0.5-hour increments and per project per week, never per day.
- Projects and reviewers come from the HRMS, not a separately maintained list.
- Every employee, including exempt IT staff, enters weekly effort only, never daily hours.
- A leave-only sheet (FR-25) carries no project blocks.
- The sheet carries an assignment-pending flag (an attribute; the sheet and block states are unchanged) with one of four reason codes: missing primary project, conflicting primary project, missing owner or multiple owners. HR is notified for all four and the case is listed in an assignment-resolution list with who, when, why and the reason code recorded; a primary-project problem and an owner-mapping problem stay distinct.
- A missing or conflicting primary project waives the Project 1 requirement while the flag is open: no Project 1 is guessed and no block is treated as Project 1, the employee may submit otherwise valid blocks, and each block routes by its own project's HRMS reviewer or down the alternate chain (FR-24). A missing or multiple owners code does not waive it, because Project 1 is known; the sheet goes to HR for publication after the cut-off (FR-10). For a conflicting primary project or multiple owners, every candidate owner is excluded from deciding that sheet.
- The flag leaves when the HRMS verifiably shows exactly one primary project and one owner for the employee; a draft sheet then follows the normal Project 1 rule, and recorded submissions, decisions and lateness judgements are kept and never rewritten. HR publishing after the cut-off never makes the employee late (FR-10).
- Publication snapshots the employee's primary project and owner. The sheet keeps that Project 1 and owner for status view, submit and extension routing, and a later HRMS transfer does not refuse the submit. If the HRMS primary project or owner then changes, the affected pending submission, decision or extension is flagged for resolution in the assignment-resolution list as a post-publication assignment change (not a fifth reason code) and no recorded decision is rewritten. A submit that cannot verify the HRMS data it needs is an HRMS-caused refusal (FR-11).

#### FR-3: Record PTO (CAP-3)
An employee records PTO hours at 8 per day. **Consequences:** 0 or a multiple of 8 is accepted; anything else is refused. On a leave-only sheet (FR-25) PTO is derived from approved HRMS leave and never entered.

#### FR-21: Weekly hours cap (CAP-2, CAP-3)
**Consequences:** project hours plus PTO total at most 40 per week; a sheet above 40 is refused, the employee sees why, and a refused over-40 attempt never changes the lateness decision; an HRMS-caused refusal follows FR-11. `[ASSUMPTION: no overtime or holiday handling in v1; the cap is a flat 40.]`

#### FR-4: Accomplishments and learnings (CAP-4)
**Consequences:** a sheet without accomplishments is refused; each learning needs one of Beginner, Intermediate or Advanced.

#### FR-5: Submit (CAP-5)
**Consequences:** the sheet shows the submitter's name and email without typing; all required fields are enforced at submit; a submit that needs HRMS data that cannot be verified fails closed (section 8, FR-11).

#### FR-6: Copy last week (CAP-8)
**Consequences:** the copy prefills projects and tasks with hours editable, and reviewers are taken from the HRMS at the time of copying; it is a new sheet and the original is unchanged; if the HRMS cannot be verified the copy is refused with a retry message and no reviewer is taken from stale data (section 8).

#### FR-7: Reopen rejected and undecided blocks (CAP-9)
**Consequences:** the employee who submitted the sheet can reopen and resubmit a rejected block or a block no reviewer has decided yet; history records who changed what and when; an approved block is never reopened, and a change to approved hours is an adjustment entry (FR-17). Each resubmission of a block creates a new block version. An approval and a reopen on the same block cannot both succeed: the first valid one wins and the other is told.

#### FR-8: Smiley rating (CAP-12)
**Consequences:** optional, stored with the sheet, never blocks or delays submit.

#### FR-9: Weekly insight card (CAP-13)
**Consequences:** shows the employee's own hours per project for a week, visible only to them; learnings stay private unless shared.

### 4.2 Publishing, deadline and late marks

**Description:** The Project 1 owner, their delegate or, after the Friday cut-off, HR publishes the week for each employee; the deadline is 24 hours after publication. Late sheets are accepted with a late mark; extensions waive it. Realizes UJ-3, UJ-4.

#### FR-10: Publish the sheet (CAP-16)
The Project 1 owner publishes the weekly sheet, usually on Friday. **Consequences:**
- An employee cannot start the week's sheet until it is published.
- Publication records who published (owner, delegate or HR) and when, and the deadline counts from that moment; the first successful publication wins and a published sheet is never published again.
- Publication opens the whole sheet, including Projects 2 through 5.
- Employees are notified when their sheet is published, on whatever day that is.
- The owner may name a delegate for the current timesheet week only; designating a delegate is independent of the Eligible Decider rule and grants no decision eligibility: the delegate must be an active employee not on approved leave when named and be explicitly designated by the owner `[ASSUMPTION: whether a narrower HRMS role is required is not yet defined; until confirmed, any active employee not on approved leave when named and explicitly designated is eligible]`. A naming is the owner plus one timesheet week, covers all of that owner's employees' sheets for that week and expires at the Monday 00:00 IST that ends the week; past weeks are published by the owner or HR. Each naming, change and expiry is audited and pending decisions are re-evaluated when one occurs. The delegate can publish while the naming is in effect and see the submission status in FR-22, and can never approve or reject a block; a delegate who published a sheet stays excluded from deciding that same sheet after the naming expires, and historical actions are unchanged.
- Publication is per employee per week. The HRMS identifies one primary project per employee, and the owner and publisher come from that assignment, never from what the employee types to influence late status; an employee with any of the four assignment-pending reason codes (FR-2) is flagged for resolution and never given a guessed owner, so only HR can publish that sheet after the cut-off and the unresolved assignment never makes the employee late. Publication snapshots the employee's primary project and owner (FR-2).
- Publishing is separate from deciding: an employee who is their own sheet's owner or delegate may publish it and still never approves, rejects or decides any part of it. A publish that needs HRMS data that cannot be verified fails closed with a message to retry and the attempt is recorded; the deadline counts only from a successful publication.
- A sheet may be published for the current week or a past week; no maximum publication window is set `[ASSUMPTION: none applies until the owner sets one]`.
- HR can publish any sheet still unpublished after Friday 12:00 PM IST (06:30 UTC) of its timesheet week, for all projects; before then HR cannot publish. After the cut-off the owner or delegate can still publish while the sheet is unpublished. The deadline is publication plus 24 hours, so a publishing delay never makes an employee late.

#### FR-11: Deadline and late mark (CAP-10)
**Consequences:**
- A sheet first submitted at or before its publication time plus 24 hours is on time, for every employee regardless of time zone; the deadline is stored in UTC, shown in IST, and never shortened when publication is late or the deadline falls after the week ends.
- A later sheet is accepted and carries a late mark; nothing blocks submission.
- Lateness is judged on the first submission only; a sheet that was on time and is later rejected and resubmitted after the deadline gets no late mark; the resubmission time is kept as history and the first submission time is never erased.
- A sheet is never marked late unless it was published.
- An HRMS-caused refusal at submit is not a submission and is never counted against the employee automatically: the action fails closed with a retry message and the attempt, its timestamp, the actor and the action are recorded. Only a refused submit on the same sheet that the HRMS caused is a qualifying attempt; HRMS checks are validated before the over-40 check, and refused copies and publishes do not qualify.
- If the first successful submission falls after the deadline and a qualifying attempt was recorded before that submission (even one recorded after the deadline), or an observed HRMS outage window overlaps the period between publication and the deadline, no late mark counts automatically: the mark is recorded in the history as held, the sheet is flagged outage-affected, the actual submission time is kept and never backdated, and an extension request is raised automatically with the attempt or outage as its reason and decided under FR-12, the decider judging the evidence (approved: the mark is shown as waived; declined: the mark counts with the actual submission time).
- A failed attempt recorded after the deadline only triggers that review and never by itself proves that an outage prevented submission before the deadline; the decider uses system-recorded evidence and observed outage information where available, and the full audit history is kept. An employee who could not sign in and has no recorded attempt uses a normal extension request. The module records observed HRMS outage windows (start, end, how observed). The grace period or deadline-extension policy for an outage is not set (section 9).
- The late mark is the only mark that can attach to an approved sheet; adjustment entries and change history are records, not marks.

#### FR-12: Extension request (CAP-10)
An employee requests an extension with a reason. **Consequences:**
- The request records its reason and has its own status: pending, approved or declined.
- The HRMS-assigned reviewer of the employee's Project 1 decides it when eligible `[ASSUMPTION: the Project 1 reviewer decides, since a sheet has several reviewers]`; the reviewer comes from the HRMS assignment, so no submitted block is needed. When that reviewer is the employee, inactive in the HRMS, on approved leave or conflicted as that sheet's Project 1 owner or delegate, or when the HRMS has no primary-project or reviewer assignment for the employee (also flagged for resolution), the eligible alternate chain of FR-23 decides it, with only the routing class fixed when the request is made (the Project 1 reviewer or the alternate chain) and the deciding person re-evaluated, so a pending request reroutes under the same events as a block and never sticks on an ineligible person, and eligibility re-checked at decision time; when nobody is eligible it goes to the HR exception queue (FR-24). HR assigns a decider but never decides.
- An approved extension records a waiver; the original late mark stays in the audit history, shown as waived, and is never deleted.
- An extension request raised automatically for an outage-affected submission (FR-11) follows the same status, routing, decision and waiver rules as one the employee makes.
- There is no limit on how many extensions an employee can request.

#### FR-13: Employee sees own late marks (CAP-18)
**Consequences:** the employee sees each late mark with the week and the deadline missed, and no one else's.

#### FR-14: Reminders (CAP-14)
**Consequences:** an employee with no submitted sheet gets a reminder before the deadline; a project reviewer with pending sheets gets one; employees on approved leave get none; at the Friday 12:00 PM IST cut-off the owner, any delegate and HR each get one reminder that sheets are still unpublished; at most one reminder per person, kind and week.

#### FR-22: Submission status view for the Project 1 owner (CAP-20)
**Consequences:** the Project 1 owner, and a delegate named for that week, see which of the owner's published sheets were submitted on time, submitted late, or not yet submitted; the view is read-only and never lets the owner or delegate approve or reject.

### 4.3 Approval and review

**Description:** The named project reviewer approves or rejects with a comment. The Project 1 owner only views; the reporting manager decides only as the first eligible decider in the alternate chain (FR-23, FR-24; otherwise a read-only view in FR-20). No one decides a block on their own sheet. Realizes UJ-2.

#### FR-15: Approve or reject with comment (CAP-6)
**Consequences:**
- A project reviewer sees only sheets with hours against their project, and approves or rejects only their own project's block.
- Each approve or reject applies to the exact block version the reviewer saw; a decision on a stale version is refused with a message to reload.
- A rejection requires a comment and returns only that block to the employee, who sees what was rejected and why, fixes it in one click and resubmits.
- The sheet is Approved and locked when every block is approved; otherwise it shows Changes required while any block is rejected and not yet resubmitted, and Submitted otherwise after submit; each block's own status is always shown.
- Approved blocks stay locked and are not reopened by another reviewer's rejection or by the employee reopening another block.
- No one approves or rejects a block on their own sheet; such a block follows FR-23.

#### FR-16: Anomaly-first review and bulk approve (CAP-11)
**Consequences:** a sheet with hours on a closed project or a sheet whose total hours differ from the prior week by more than 15 hours is flagged and listed first `[ASSUMPTION: the 15-hour jump is a starting value]`; selecting all unflagged sheets approves, in one action, the reviewer's own block on each, every block validated separately against the version reviewed and approved individually; a sheet becomes approved only when every block is approved.

#### FR-17: Corrections after approval (CAP-9, CAP-7, CAP-24)
**Consequences:** a correction to approved block hours, whether or not the whole sheet is approved yet, is a dated adjustment entry on top of the preserved original block, never a silent edit, with a reason and who recorded it.
- An actor who passes the Eligible Decider rule at the time of recording initiates and records it directly: the named reviewer when eligible or an eligible alternate in the current tier of the alternate chain (FR-23, FR-24), at any time; either may act under the shared decision rules, the first valid recording wins and the other actor is told. The entry carries the block, the change in hours, the net hours before and after, a reason, the recorder and the eligibility result. No one adjusts their own block, that sheet's Project 1 owner or delegate never records one, and HR never does.
- There is no separate adjustment-request object. When neither the named reviewer nor any alternate is eligible, HR raises an adjustment-needed flag on the approved block with a reason; the flag (open, assigned or recorded) enters the HR exception queue (FR-24) and HR assigns an eligible alternate who then records the adjustment. HR may raise and manage the flag (assign, track) but never records or approves an adjustment, and the queue records none.
- Each adjustment is bound to the net hours the recorder reviewed; eligibility, block version and net hours are rechecked at recording time, and a stale or concurrent adjustment is refused with a message to reload.
- Adjustments follow the 0.5-hour increment; an adjustment that would make a block's net approved hours negative is refused.
- A reason is mandatory and the named reviewer is notified on every adjustment.
- The employee is notified when an adjustment is recorded, with the affected reporting week, the change in hours, the reason and the resulting net hours.
- HR can view adjustment history for audit but cannot create, modify, approve or reject an adjustment.
- Whether the 40-hour cap applies to adjustments is not decided `[ASSUMPTION: the owner decides; no cap rule is applied to adjustments until then]`. A time limit for recording an adjustment and an employee dispute route are deferred to V2 (section 9).

### 4.4 Reporting and HR visibility

#### FR-18: Hours roll-up and finance export (CAP-7)
**Consequences:** the hours of approved blocks roll up by project, employee and week into billable and non-billable hours and utilization (denominator: total available hours), each approved block counted once and including dated adjustment entries (FR-17); hours in blocks not yet approved are excluded, even when other blocks on the same sheet are approved; the export reproduces the roll-up as of its issue and lists who approved each line and when; an issued export is never rewritten, and a later export carries the dated adjustment history; a leave-only sheet (FR-25) reports zero project hours.

#### FR-19: HR read-only view (CAP-17)
**Consequences:** HR sees approved hours, late marks and approval status for any employee and week; from the cut-off HR sees a list of unpublished sheets, which excludes leave-only sheets (FR-25); HR sees the assignment-resolution list (FR-2) and late marks held for an outage (FR-11); for a published sheet HR sees the employee, projects, publication time, deadline and publisher, as awaiting submission before the deadline and not submitted after it, with no late mark for a sheet never submitted; HR can view adjustment history for audit (FR-17) but cannot edit sheets, hours, late marks or adjustment entries and never approves or rejects hours; its write actions are publishing an unpublished sheet after the cut-off (FR-10) and assigning an alternate decider from the exception queue for a block, an extension request or an adjustment-needed flag when none is eligible (FR-24), and raising an adjustment-needed flag with a reason (FR-17); in the HR role HR never decides or records any of them and cannot assign an HR-role holder.

#### FR-20: Reporting manager read-only view (CAP-19)
A reporting manager sees their direct reports' approved hours, late marks and approval status per week. **Consequences:** the reporting manager cannot edit or waive anything and decides only as the first eligible decider in the alternate chain (FR-23, FR-24) for a self-review block, a block whose reviewer is ineligible or conflicted, the matching extension request, or an adjustment (FR-17), and never for a sheet where they are the employee or that sheet's Project 1 owner or delegate; they see only their own direct reports.

#### FR-23: Alternate approver for self-review (CAP-21)
When the reviewer named for a project block is the employee who submitted the sheet (for example a project manager reviewing their own hours), an alternate approver decides that block instead. **Consequences:**
- The employee sees no approve or reject action on a block of their own sheet.
- The block goes down a tiered chain: the employee's designated reporting manager when eligible, and holders of the delivery-manager HRMS role (designated by an authorized HR administrator; several holders are allowed and the first valid decision wins) only when the reporting manager is ineligible; the same tiering applies to blocks, extension requests and adjustments. A decider is eligible only if they pass the Eligible Decider rule; when none is eligible, the block enters the HR exception queue and HR assigns one (FR-24) `[ASSUMPTION: which delivery-manager holders count for a given employee is a provisional default of all holders; the owner confirms]`.
- The alternate approver decides only that block; the sheet is Approved and locked only when every block is approved.
- The history records that it was a self-review case and who decided it.
- The Project 1 owner never approves.

#### FR-24: Absent reviewer and the HR exception queue (CAP-22)
When the reviewer named for a project block is inactive in the existing HRMS, on approved leave or conflicted as that sheet's Project 1 owner or delegate (ineligible for that sheet only), the alternate approver decides that block, so it does not stay pending. **Consequences:**
- The block goes to the same tiered chain of eligible deciders as FR-23. Eligibility is checked when the block is routed, at each new block version, at decision time, on HRMS active or leave change events and by a periodic fallback sweep `[ASSUMPTION: the sweep frequency is not set; the owner specifies it]`, with approved leave judged at the instant of the check and owner and delegate status judged at decision time on authoritative HRMS data. If required HRMS data is unavailable or cannot be verified, the check fails closed: the action is refused with a message to retry and eligibility is never assumed; a retroactive HRMS change flags the affected records for audited resolution and never rewrites a recorded decision.
- A reviewer on approved leave is ineligible to decide during that leave, so an eligible alternate handles the decision; the block is rerouted promptly when its reviewer becomes ineligible.
- The named reviewer, when eligible, and the eligible alternate of the current tier may both act after routing; only one valid decision can be recorded for a block and the other actor is told; a block is never automatically routed back to a returning reviewer.
- When no decider is eligible, the block, extension request or adjustment-needed flag enters an HR exception queue and HR is notified. HR assigns an alternate who passes the Eligible Decider rule and holds no HR role; an attempt to assign an HR-role holder, including the assigning user, is refused and logged; an HR-role holder may decide only in a separate capacity as a reporting manager or delivery-manager holder when eligible under the normal chain, never through assignment; in the HR role HR never approves, rejects, decides or records an adjustment.
- The assignment covers that block, extension request or adjustment-needed flag until it is decided and is re-checked at each new block version and at decision time; the history records who assigned, when, why and the eligibility result.
- Routing, reassignment and queue notices are event notifications, separate from the weekly reminder cap (FR-14), and must not bypass any notification controls the product defines.
- The shared decision rules apply equally to blocks, extension requests and adjustments: the normal decider, when eligible, and the eligible alternate of the current tier may both act, only one valid decision is recorded and the other actor is told; each decision binds to the version seen (the block version, the extension request as stored, or the net hours reviewed) and a stale action is refused with a message to reload; every decision records who, when and the eligibility result.
- The alternate approver decides only that block; the sheet is Approved and locked only when every block is approved.
- The history records the reason and who decided it.
- An entry unresolved after the waiting-days number escalates from the queue to an escalation contact; neither the number nor the contact is set, so the escalation has no time limit until they are `[ASSUMPTION: the owner supplies the waiting days and the escalation contact before build]`.

#### FR-25: Leave-only sheets (CAP-23)
A week fully covered by approved leave in the existing HRMS is a leave-only sheet, so the employee has nothing to submit and no reviewer has anything to approve. **Consequences:**
- A sheet is leave-only when every working day from Monday to Friday of the timesheet week is covered by approved HRMS leave; Saturday and Sunday are ignored and public holidays are not recognised in v1, so a holiday counts as covered only if HRMS records approved leave for it `[ASSUMPTION: this coverage rule is the approved default; the owner can revisit it]`.
- PTO is derived from HRMS at 8 hours per covered working day (40 for a full week) and is never entered by the employee.
- The leave-only classification is shown clearly; it is a sheet type, not a fifth state.
- There is no employee submission, no reviewer approval, no late mark and no reminder, and the sheet is left out of the unpublished list; finance reports zero project hours for it.
- Eligibility is recalculated when HRMS leave is approved, cancelled or amended. A sheet converts to or from leave-only automatically only when it has no project blocks, no publication, no recorded decision (a block decision, an extension decision or an adjustment entry) and no late mark.
- If any of those exist, the case is flagged for authorized, audited resolution; the sheet is never silently converted, republished, stripped of history or used to rewrite an issued export. If a submission races a leave approval, the submission wins and the sheet is flagged, not converted.
- If HRMS leave data cannot be verified, the classification fails closed: the sheet keeps its current type and is re-evaluated at the next HRMS event or the sweep (section 8).
- A leave-only sheet is not published and sends no publication notice. If leave is cancelled and the week is no longer fully covered, a sheet that has none of those becomes a normal sheet to publish and the deadline counts from publication as usual.

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
FR-1 through FR-25, for about 160 employees and 20 projects. Everything ships free; there is no pricing.

### 6.2 Out of Scope for MVP
Everything in section 5, plus the paid-tier candidates in `premium-tier.md` and a client-facing view.

## 7. Success Metrics

**Primary**
- **SM-1**: Share of sheets submitted on time, measured as one minus the late-mark rate per week, from launch. No target yet. Validates FR-6, FR-10, FR-11, FR-14.
- **SM-2**: An employee completes a full sheet in one sitting, and finance reads a week's approved hours per project without re-keying; checked by a short monthly question to employees and finance `[ASSUMPTION: a monthly question with no tooling]`. Validates FR-5, FR-18.

**Secondary**
- **SM-3**: Smiley rating trend. No target. Validates FR-8.
- **SM-4**: Weekly hours project managers spend collecting hours, against the ~19-hour baseline; checked by asking project managers monthly `[ASSUMPTION: a monthly question with no tooling]`. No target is set.

**Counter-metrics (do not optimize)**
- **SM-C1**: Late marks issued. Do not minimize at the cost of accuracy; HR consequences must not push employees to submit careless sheets. Counterbalances SM-1.
- **SM-C2**: Rejection rate. Do not push it to zero by approving without checking. Counterbalances FR-16 bulk approve.

`[ASSUMPTION: the owner's "late mark" measure is read as the late-mark rate being the on-time measure; no numeric targets are set.]`

## 8. Cross-Cutting Requirements

- **Data governance:** submitted sheets, approved sheets and change history are kept at least 3 years (owner's generic rule). HR sees late marks and approved hours; learnings are private unless shared.
- **Auditability:** approved hours are immutable; every change and approval is recorded with who and when.
- **Identity and data:** identity, projects, each employee's primary project, and each project's owner and reviewer come from the HRMS; approved-leave and active status are also read from the HRMS and never maintained here. If HRMS data an action needs is unavailable or cannot be verified, the action fails closed and never completes on guessed or stale data: eligibility checks, submit, publish and copy are refused with a message to retry, and a leave-only classification stays as it is until the next HRMS event or the sweep; each failed attempt records its timestamp, the actor and the affected action; an employee is not penalized automatically for an outage-caused refusal (FR-11); retroactive HRMS changes flag records for audited resolution and never rewrite recorded decisions.
- **HRMS facts each action verifies (provisional):** submit: employee active, the primary project snapshotted at publication and each project's reviewer; publish: owner, delegate naming and publisher active; copy: each project's reviewers; decide, record or assign: the Eligible Decider facts (active, approved leave, owner, delegate, HR role); leave classification: approved leave. A verified HRMS read may be at most 5 minutes old (provisional default P14, pending the architecture step on cache invalidation, which eligibility checks are critical and failure behavior); stale data never authorizes an action when current eligibility cannot be established, and the action fails closed. Accepted cost of failing closed: one HRMS outage near a deadline can raise many automatic extension requests.
- **Experience:** the module should feel quick and forgiving; it never shames. Gamification, if ever added, is opt-in and team-level only. HR, not this module, decides any consequences of late marks, so late marks must be accurate.
- **Reminders:** scheduled in UTC, at most one reminder per person, kind and week; routing, reassignment and exception-queue notices are event notifications, not reminders, so the weekly cap does not apply to them, and they must not bypass any notification controls the product defines.
- **Fairness:** an approved sheet is never reported as incorrect; an extension records a waiver and the original late mark stays in the history.
- **Legal:** the owner confirmed 3-year retention; India's 5-year rule is not adopted. Late-mark handling and retention have had no legal review; the owner accepts this risk and has closed the question.

## 9. Open questions

Each question carries its V1 or V2 class and, where one exists, the provisional default in section 10.1 that applies until the confirmation shown is given.

- [V1, provisional default P1] Is a narrower HRMS role required for a delegate publisher (FR-10)? Until confirmed, any active employee not on approved leave when named and explicitly designated is eligible; HR or business confirms.
- [V1, proposed default P15, business approval required] Who resolves a flagged missing or conflicting HRMS primary-project, owner or reviewer assignment, or a post-publication assignment change, and how quickly (FR-2, FR-10)? HR is notified and tracks the case in the assignment-resolution list (D16, D24); proposed, not approved: the HRMS admin team corrects the source data with a one-working-day target; the business owner confirms or replaces both.
- [V1, provisional default P12] Must the employee's Project 1 block be the HRMS primary project (FR-2)? Provisional default: yes, and owner designation always uses the HRMS primary project regardless of the hours logged, except while the assignment-pending path (FR-2) applies; business confirms.
- [V1, provisional default P11] Which delivery-manager holders count for a given employee (FR-23)? Provisional default: all holders of the role; business confirms.
- [V1, provisional default P2] Is there a maximum window after a week ends within which a sheet may still be published, and what exception process applies (FR-10)? Provisional default: none; business confirms only if a limit is wanted.
- [V1, provisional default P3, accepted provisionally by the owner, HR or business confirmation required] How many waiting days may an entry stay in the HR exception queue before it escalates to the escalation contact (FR-24)? Provisional default: 3 working days, configurable.
- [V1, provisional default P8, accepted provisionally by the owner] Who is the final escalation contact for the HR exception queue (FR-24)? Provisional default: the module's business owner named in configuration; business confirms.
- [V1, provisional default P4] For an employee with approved leave for only part of the week, does the reminder rule 'employees on approved leave get none' (FR-14) apply, and at which instant? FR-14 is unchanged; provisional default: the reminder is suppressed only on a day the employee is on approved leave at the send instant; HR confirms.
- [V1, no default] Which role is authorized to resolve a flagged case when a leave change touches a sheet with blocks, a publication, a recorded decision, a late mark, a finalized decision or an issued export (FR-25), and how does the resolution appear in a later export?
- [V2 deferred] Does the 40-hour cap apply to adjustment entries (FR-17)? Also [V1, provisional default P5]: which time counts as first submission when earlier attempts were refused (FR-21)? Provisional default: a refused attempt is not a submission and the first successful submission time counts; business confirms.
- [V1, provisional default P6] Which data of other project blocks may a reviewer see (FR-15, FR-16)? Provisional default: their own block plus the sheet's total hours only; UX and business confirm.
- [V1, provisional default P7, accepted provisionally by the owner, HR or business confirmation required] What are the sweep frequency, the employee reminder offset and the reviewer reminder trigger (FR-14, FR-24)? Provisional default: sweep once a day, employee reminder 6 hours before the deadline, reviewer reminder Monday 09:00 IST once a week.
- [V1, provisional default P9; the SM-1 part stays an owner decision] When may an extension be requested, may one be requested after approval, and how do waived marks count in SM-1 (FR-12)? Provisional default: any time before the sheet is approved, not after.
- [V1, no default] How is weekend work in a leave-only week recorded, how does half-day or hourly approved leave count as covering a day or making a reviewer ineligible, and which status does a leave-only or flagged sheet show in each view (FR-25)?
- [V1, provisional default P10, accepted provisionally by the owner, HR or business confirmation required] Which notification controls must routing, reassignment and queue notices respect (FR-24)? Provisional default: no user opt-out in V1, event notices batched per recipient per hour.
- [V1, no default, unresolved] What grace period or deadline-extension applies to an outage-affected deadline (FR-11)? Until set, a held late mark is resolved through the automatically raised extension request, which the decider judges using system-recorded evidence and observed outage windows; a failed attempt recorded after the deadline is never proof by itself.
- [V1, no default] What counts as observed HRMS outage evidence (detection source, minimum duration), and is it enough on its own to waive a held late mark, or does the decider always judge (FR-11)?
- [V1, architecture step, provisional default P14] For the 5-minute verified-read window: what are the cache invalidation rules, which eligibility checks are critical and need a live HRMS read, and what is the failure behavior (section 8)?
- [V2 deferred] Is there a time limit on recording an adjustment after approval (FR-17)?
- [V2 deferred] May an employee dispute or acknowledge an adjustment, and by what route (FR-17)?

Resolved decisions are logged in `.memlog.md`.

## 10. Assumptions Index

- FR-16 — the anomaly jump threshold of 15 hours is a starting value.
- Section 7 — late mark read as the on-time measure; no targets.
- FR-12 — the Project 1 reviewer decides extensions.
- FR-17 — whether the 40-hour cap applies to adjustments is not decided; the owner decides.
- FR-23 — which delivery-manager holders count for a given employee is a provisional default of all holders; the owner confirms (P11).
- FR-21 — flat 40-hour cap, no overtime or holiday handling.
- FR-10 — whether a narrower HRMS role is required for a delegate publisher is not defined; until confirmed any active employee not on approved leave when named and explicitly designated is eligible (provisional default P1).
- FR-10 — no maximum publication window is set; none applies until the owner sets one.
- FR-24 — the days an undecided block waits before escalating from the queue, and the escalation contact, are not set; the owner supplies them before build.
- FR-24 — the periodic sweep frequency is not set; the owner specifies it.
- FR-25 — leave-only coverage counts Monday to Friday and does not recognise public holidays; this is the approved default and the owner can revisit it.
- Section 7 — SM-2 and SM-4 are checked by a monthly question; no tooling.
- FR-11, FR-2, FR-10 — inferred from owner decisions, for the owner to confirm: an observed outage window holds a late mark when it overlaps the period between publication and the deadline; when an assignment-pending flag leaves a published sheet a new snapshot is added and the earlier one kept; a sheet with missing or multiple owners is published by HR after the cut-off.

### 10.1 Provisional defaults

These are not approved requirements. Each is a safe default for build and stays listed in section 9 until the confirmation shown is given.

- **P1** Delegate: any active employee not on approved leave when named who is explicitly designated by the owner; a narrower HRMS role is pending (HR or business).
- **P2** No maximum publication window (business, only if a limit is wanted).
- **P3** HR exception queue escalation threshold: 3 working days, configurable (owner accepted as a provisional default 2026-10-11; HR or business confirmation still required).
- **P4** Partial-week leave: the employee reminder is suppressed only on a day the employee is on approved leave at the send instant (HR).
- **P5** A refused over-40 attempt is not a submission; the first successful submission time counts (business).
- **P6** A reviewer sees their own block plus the sheet's total hours only (UX and business).
- **P7** Periodic sweep once a day; employee reminder 6 hours before the deadline; reviewer reminder Monday 09:00 IST once a week (owner accepted as a provisional default 2026-10-11; HR or business confirmation still required).
- **P8** Escalation contact: the module's business owner named in configuration (owner accepted as a provisional default 2026-10-11; business confirms).
- **P9** An extension may be requested any time before the sheet is approved and not after; the SM-1 treatment of waived marks stays an owner decision (business).
- **P10** Notification policy: no user opt-out in V1; event notices batched per recipient per hour (owner accepted as a provisional default 2026-10-11; product or HR confirmation still required).
- **P11** Delivery-manager scope: all holders of the role (business).
- **P12** The Project 1 block is the employee's HRMS primary project as snapshotted at publication, and owner designation uses it regardless of the hours logged, except while the assignment-pending path applies (business).
- **P13** An HR-role holder who is also a delivery-manager holder may decide in that capacity through the chain and never through queue assignment, as for the reporting manager (owner).
- **P14** HRMS verified-read freshness: a verified read may be at most 5 minutes old; provisional until the architecture step defines cache invalidation, which eligibility checks are critical and failure behavior; stale data never authorizes an action when current eligibility cannot be established (owner accepted provisionally 2026-10-11).
- **P15** Source-data corrections for flagged HRMS assignments: PROPOSED only, not approved: the HRMS admin team corrects them with a one-working-day target; not an SLA until the business approves it.
