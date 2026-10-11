# Adversarial review: PRD Timesheet Management (ninth pass)

**Verdict: not ready for ticket slicing as written. 2 critical and 12 high findings. The rules mostly close their own loops now (tiered chain, snapshot, reason codes, week-bound delegate). What remains is (a) the sheet lifecycle after first submit and first approval, (b) several ways to avoid a late mark that nobody intended, (c) unbounded adjustment and publication powers, and (d) provisional or inferred items written as settled policy.**

Scope: PRD, spec and glossary, read in full; critique only, nothing edited. Rules attacked: submission, publication, approval, extension requests, adjustments, leave classification, late marks, delegate naming, HRMS outage and freshness, assignment snapshot and reason codes, the tiered alternate chain. Owner decisions D1-D26, the 20 labeled open questions, P1-P15, SM-1 and the retired CAP-15 are treated as given. Findings that touch an owner decision are phrased as open questions, never as a reversal.

Counts: Critical 2, High 12, Medium 14, Low 6.

Checked and found clean: P15 (HRMS admin team, one working day) appears only in section 9, section 10.1 and the spec equivalents, always marked proposed. It does not leak into any FR, glossary entry or constraint.

## Critical

**C1. After the first approval there is no way to add a forgotten project block or change sheet-level data.**
- Location: FR-2, FR-7, FR-15, FR-17, spec CAP-9, CAP-24, sheet-state precedence.
- Scenario: Meera submits Project 1 only and forgets Project 2. Project 1's reviewer approves within minutes. Every existing block is approved, so the sheet is Approved and locked. FR-7 reopens only rejected or undecided blocks, so there is nothing to reopen. FR-17 corrects "approved block hours", so there is no block to adjust. The Project 2 hours can never be recorded, and finance never sees them. The same applies before approval: nothing says whether an employee may add or delete a block on a Submitted sheet, or change PTO, accomplishments or learnings (sheet-level fields with no version and no reviewer). If adding a block is allowed, it is a way to add hours after the deadline with no late mark, since lateness is judged on the first submission only.
- Fix: define edits to a submitted sheet: may a block be added or removed, and until when; how sheet-level fields are versioned and locked; and whether an adjustment may create a block. As written, one fast approval permanently loses billable hours.

**C2. The deadline can be avoided by a placeholder submission.**
- Location: FR-7, FR-11 third bullet, FR-21, spec CAP-9, CAP-10.
- Scenario: lateness is judged on the first submission only, and an employee may reopen "a block no reviewer has decided yet" at any time. Submit a minimal valid sheet (one block of 0.5 hours, one-line accomplishment) before the deadline, then reopen and rewrite it days later. No late mark; the resubmission time is only history. No minimum hours exist, and the reviewer has no signal until they open it. FR-11 covers a rejected block resubmitted late, which is reviewer-driven. The employee-driven undecided-block path is not stated as an owner decision.
- Open question: is a first submission with placeholder content meant to fix lateness, or should the time of the last resubmission of an undecided block count (or a minimum content rule apply)?

## High

**H1. A never-submitted sheet earns no mark, so not submitting beats submitting late.**
- Location: FR-11, FR-19, glossary "Late mark", spec constraints.
- Note: a late mark attaches only to a sheet submitted after the deadline. A published sheet that is never submitted shows "not submitted" with no mark, no escalation and no reminder after the deadline. The rule rewards the employee who knows they will be late for skipping the sheet. The hours then never reach finance, and no rule says who chases them.
- Open question: should a not-submitted sheet past its deadline carry a recorded state HR can act on, and who is notified?

**H2. Extension requests are unlimited and a decline is not final.**
- Location: FR-12, P9, spec Assumptions.
- Note: "no limit on how many" plus routing to the Project 1 reviewer or, when ineligible, the alternate chain. An employee whose request is declined can re-request, for example after the reviewer goes on leave and the decider changes (forum shopping). Two requests can be pending at once, and an automatic request can coincide with one the employee made. The "request as stored" binding does not say which wins. A pending request at the moment the sheet becomes Approved is not covered either (P9 says none after approval).
- Open question: one open request per sheet; is a decline final for that sheet; what happens to a pending request when the sheet is approved?

**H3. The P9 window closes on approval, which a fast reviewer triggers before a late employee can ask.**
- Location: FR-12, UJ-3, P9, FR-16.
- Note: UJ-3 has Anita submit late and then request an extension. Bulk approve (FR-16) can approve all blocks within minutes. Under P9, "not after the sheet is approved", the window can shut before she acts, while the late mark stays and is the only mark that can attach to an approved sheet. Written in section 9 and 10.1 only, so FR-12 reads as unbounded while the default is bounded.
- Fix: state in FR-12 which rule applies, and whether the employee is told of a late mark and the window at submit time.

**H4. The hold on a late mark has a very low trigger and is overbroad.**
- Location: FR-11 fifth and sixth bullets, section 8, glossary "Held late mark".
- Note: (1) Any HRMS-caused refused submit recorded before the successful one holds the mark, "even one recorded after the deadline". An employee two days late with a one-second HRMS error at submit gets a held mark and an automatic extension request. (2) Any observed outage window overlapping the 24-hour period holds every late mark for every sheet published then, whether or not the outage touched that employee. No minimum duration (open question) means a 30-second blip does it, and section 8 accepts "many automatic extension requests" as cost. (3) The module only observes HRMS when it calls it, so an unobserved overnight outage creates no window. (4) The module's own downtime near a deadline has no rule at all; only HRMS outages are covered.
- Fix: until the open questions close, state a minimum evidence bar in FR-11 (for example an outage must overlap the employee's own attempt or last hours before the deadline), and say what happens when the module itself is down.

**H5. Publication is unbounded in time and irrevocable, so it can be mistaken or weaponised.**
- Location: FR-10, P2, glossary "Published sheet".
- Note: a past week of any age can be published (no window), the deadline then runs 24 hours from that moment, and "a published sheet is never published again" with no withdrawal. An owner or HR clicking the wrong employee or week starts a 24-hour clock on a sheet the employee cannot have expected, and a late mark follows. The same power can be used deliberately against one employee. Reminders and notices are the only protection, and notice delivery is not part of the deadline.
- Open question: is there a withdraw or correct-publication action, and should publishing a week older than some age need HR-only or an acknowledgement? Future-week publication is not stated as refused.

**H6. Adjustments bypass the 40-hour cap and have no upper bound.**
- Location: FR-17 last bullet, FR-18, FR-21, spec CAP-24.
- Note: the submit path refuses over 40 hours, but adjustments have "no cap rule" and no time limit. A reviewer or any eligible alternate (including all delivery-manager holders under P11) can raise approved hours well above 40 a week, years later, and the net roll-up reports it. This defeats the cap exactly where finance reads. The V2 deferral is listed, but adjustments ship in V1.
- Open question: ship V1 with a provisional ceiling (the cap, or a configurable one) on net block or sheet hours, or accept unbounded net hours knowingly?

**H7. No route exists to start a correction, and the HR flag is hard to use.**
- Location: FR-17, FR-24, glossary "HR exception queue", section 9 V2 items.
- Note: there is no request object and the dispute route is V2 (and that route is about disputing an adjustment, not asking for one). The employee cannot reopen an approved block. The reviewer only learns of an error out of band. HR may raise an adjustment-needed flag only when neither the reviewer nor any alternate is eligible, but the reporting manager is nearly always an eligible alternate, and nothing says whether HR can see that or whether a flag with an eligible recorder is refused.
- Fix: state who can ask for a correction and how it reaches a recorder, and the HR flag precondition.

**H8. An employee can log hours to any project, so the reviewer can be chosen and billable hours inflated.**
- Location: FR-2, FR-15, FR-16, FR-18.
- Note: projects come from the HRMS, but no rule says the employee must be assigned to a project they log against; only Project 1 is tied to them. The reviewer comes from the chosen project, so an employee can pick a project with a lenient reviewer, or a billable one, and the project reviewer sees only their own block plus the total (P6) so cannot easily tell. Closed projects are flagged but not refused, and copy-last-week carries them forward.
- Open question: is a block refused or flagged when the employee has no HRMS assignment to the project?

**H9. Who counts as "the reviewer" is unbound in time and cardinality.**
- Location: FR-2, FR-15, FR-24, Eligible Decider rule, glossary "Project reviewer".
- Note: the owner is judged at decision time and snapshotted, but the reviewer is not. Scenario: the HRMS replaces reviewer A with B after the block is submitted. Is the block B's, or can A still approve it? The Eligible Decider rule never requires the named reviewer to still be the project's reviewer. A project with two reviewers is also undefined (owner has "multiple owners" as a reason code, reviewer has no equivalent). Block routing, reminders and approved-by audit all depend on this.
- Fix: say whether the reviewer is snapshotted per block version or read live, and handle zero, one and several reviewers.

**H10. Naming a delegate lets the owner steer who decides.**
- Location: FR-10, FR-24, spec constraints, P1.
- Note: a delegate is excluded from deciding every sheet of that owner's team that week, and persistently for sheets they published (D26). If the delegate is a block's named reviewer or an employee's reporting manager, those blocks move down the chain, and a block is never routed back. The owner who "never approves" can therefore choose the reporting manager or delivery manager as the decider by naming the strict reviewer as delegate, and P1 allows any active employee.
- Open question: should naming a current reviewer or reporting manager as delegate be warned, restricted or audited as the cause of the reroute? Designation independence (D14) is not challenged.

**H11. The escalation has no end state.**
- Location: FR-24 last bullet, P3, P8.
- Note: after 3 working days a queue entry "escalates to an escalation contact", the module's business owner. What the contact may do is never stated: decide, assign, or only be notified. They may themselves be an HR-role holder or an owner or delegate for that sheet, in which case the Eligible Decider rule bars them. If nobody eligible exists (small org, all conflicted), the item has no exit and the sheet stays unapproved.
- Fix: define the contact's action and what happens when the contact is also ineligible. "Working days" is also undefined, since public holidays are not recognised in v1.

**H12. Provisional and inferred items are written as settled policy, and the document says "final".**
- Location: PRD front matter, FR-2, FR-10, FR-11, FR-21, section 8; spec CAP-2, CAP-10, CAP-16, constraints.
- Note:
  1. `status: final` with 20 open questions, six with no default and the outage grace unresolved.
  2. FR-11, the glossary "Held late mark", spec CAP-10 and CAP-2 state flatly that an observed outage overlapping publication-to-deadline holds the mark, and that a missing or multiple owners sheet is published by HR. Only the section 10 index line and the spec "inferred from D21, D23, D24" assumption say these are inferred for owner confirmation. No inline tag.
  3. FR-21 and the spec constraint state the P5 outcome (a refused over-40 attempt never changes lateness) as fixed; it is provisional.
  4. FR-2 states "Project 1 is the HRMS primary project and is required" with no tag while P12 awaits business confirmation.
  5. Section 8 calls failing closed with many automatic extensions an "accepted cost" without saying by whom, and it depends on the unresolved grace policy.
  6. The spec line "provisional, owner decision D22" labels the same item both ways; P14 is provisional.
- Fix: tag each inline, or move the wording behind the P-number, and set the status to draft or conditional.

## Medium

**M1. P14 (5-minute read) contradicts "at the instant".** The Eligible Decider rule and FR-24 say eligibility is judged at the instant on authoritative data; P14 allows a read up to 5 minutes old. A reviewer who went on leave 3 minutes ago can still approve. State which governs, or mark the instant rule as "within the freshness window".

**M2. Stale "not set" wording contradicts P3, P7, P8.** FR-24 last bullet, the sweep assumption, the section 10 index, spec CAP-22 and the spec assumption ("days not set, owner confirmed") say the waiting days, contact and sweep frequency are unset and "supplied before build". P3, P7 and P8 give values the owner accepted provisionally. Update the wording to point at the P-numbers.

**M3. Sheet-level fields have no lifecycle or reader.** Accomplishments are mandatory but P6 shows reviewers neither them nor learnings; FR-9 says learnings stay private "unless shared", with no sharing mechanism or audience. PTO is typed by the employee on a normal sheet with no check against HRMS leave (it can be claimed with no leave, or omitted while on leave), and "total available hours", the utilization denominator, is not defined in the glossary.

**M4. Tier flapping.** Eligibility is checked at decision time, but "a block is never automatically routed back". When a reporting manager returns from leave, are delivery managers still eligible for an item they were handling, and does a stale-action refusal hit a manager mid-review? "Current tier" needs a time reference.

**M5. Outage versus queue and clock.** "Cannot verify" fails closed, yet "none eligible" sends to the HR queue, whose assignment also needs HRMS, and the P3 escalation clock may run through the outage. FR-14 reminders (they need leave status) are not in the fail-closed list.

**M6. Anomaly baseline is undefined.** The 15-hour jump compares to the prior week: does total include PTO, what is the baseline after a leave-only or unsubmitted prior week, and for a first sheet? A returning employee may be flagged every time or never.

**M7. Three resolution paths have no named resolver.** Assignment cases (P15 proposed only), leave changes touching a sheet with history (no default) and retroactive HRMS changes touching a recorded decision (no open question at all) each end in "audited resolution" by nobody. Flagged items will accumulate.

**M8. Departed or inactive employees.** An employee made inactive in HRMS cannot submit ("employee active" is a submit check), and a rejected block can never be resubmitted, so the sheet stays Changes required forever and the hours are never billable. Last-week sheets at exit are unspecified.

**M9. Publication notice versus the deadline.** The deadline starts at publication, not at delivery; routing and queue notices may be batched up to an hour (P10), and employees on partial leave get a 24-hour wall-clock deadline across a weekend. The late mark can follow a notice the employee never received.

**M10. Self-published sheets set their own deadline.** An owner, delegate or HR-role employee may publish their own sheet at a time of their choosing, so a late mark can hardly bind them. D14 is not challenged; open question: should a self-published sheet use the cut-off or a different rule?

**M11. Snapshots after the flag clears.** "A new snapshot is added and the earlier kept": are both snapshotted owners excluded from deciding that sheet, and which one routes status and extensions? The rule excludes the snapshotted and the current owner, but a second snapshot is not mentioned in it.

**M12. Late-mark display by state.** Counted, pending-extension, held and waived marks are not mapped to what the owner, delegate, reviewer, reporting manager and HR see. The owner "sees only on time or late"; a waived or held mark in that view is undefined. A table is needed.

**M13. Leave-flagged published sheets.** A published sheet later fully covered by approved leave is flagged, not converted. The employee's submission duty, late marks and reminders while it is flagged are undefined, as is a publish racing a leave approval or an unverifiable classification at the cut-off.

**M14. The flat 40 cap conflicts with "real effort".** An honest 45-hour week is refused, so it is either under-reported or moved between weeks, against the vision of real hours. Together with H6, hours above 40 can enter only through an adjustment. An owner would need to say whether that is intended.

## Low

- **L1.** FR numbering is out of sequence in the document (FR-21 sits after FR-3, FR-22 in 4.2, FR-23 to FR-25 at the end).
- **L2.** The PRD glossary entries "Authorized delivery manager" and "Alternate approver" omit the provisional note (P11) the spec glossary carries.
- **L3.** P13 is listed as a provisional default but has no section 9 entry, though section 10.1 says each stays listed there; P5 (V1) sits inside a V2-deferred bullet; P14 lacks the "accepted provisionally by the owner" tag that P3, P7, P8 and P10 carry in section 9.
- **L4.** A late mark is visible to "the project reviewer", so every reviewer on a sheet sees it, against P6's minimization of what other reviewers see.
- **L5.** Reviewer reminder "Monday 09:00 IST once a week" and the weekly cap mean a sheet submitted after that Monday reminder gets none until the next week.
- **L6.** FR-12 does not require a reason or comment on a declined extension, though a block rejection does; the employee is not told why.

## Open questions for the owner

1. Should first submission with placeholder content fix lateness, or does the last resubmission of an undecided block count (C2)?
2. May blocks and sheet-level fields be added or edited after first submit, and can an adjustment add a missing block (C1)?
3. Should a published sheet that is never submitted carry a recorded state HR can act on (H1)?
4. Is there one open extension request per sheet, is a decline final, and what happens to a pending request when the sheet is approved or when P9 closes the window (H2, H3)?
5. What minimum evidence should hold a late mark, and what applies when the module itself is down (H4)?
6. Can a publication be withdrawn, and is there an age limit or extra step for old weeks (H5)?
7. Should net adjusted hours have a provisional ceiling in V1 (H6, M14)?
8. Who can request a correction to approved hours, and when may HR raise the flag (H7)?
9. Must an employee be assigned to a project to log hours against it (H8)?
10. Is a block's reviewer snapshotted or live, and what if a project has several (H9)?
11. Should naming a reviewer or reporting manager as delegate be warned or restricted (H10)?
12. What may the escalation contact do, and what if they are ineligible (H11)?
13. Who resolves leave-touching and retroactive HRMS cases while P15 is only proposed (M7)?
