# Validation Report — Timesheet Management

- **PRD:** `_bmad-output/initiative-timesheet-management/prd-timesheet-management/prd-timesheet-management.md`
- **Rubric:** `_bmad-output/initiative-timesheet-management/prd-timesheet-management/review-rubric.md`
- **Run at:** 2026-10-11T18:40:03+05:30
- **Grade:** Fair

## Overall verdict

The PRD is decision-ready and well argued. D14 to D17 are applied consistently across the FRs, glossary, section 8, section 9, section 10 and the spec. I found no contradiction among the submission, publication, approval, extension, adjustment, leave-classification and late-mark rules. The remaining risk is precision at the edges of the new rules. The held late mark has no bound on when the failed attempt happened. The D16 assignment-pending flag's trigger and exit cover only the primary project, and its waiver permits a sheet with no blocks. The "alternate" chain can be read as ordered or concurrent. Several FRs, FR-24 above all, are too dense to slice into stories as written.

No owner decision is questioned. The 18 section-9 open questions, P1-P13, SM-1 and the reopen-lateness interaction are treated as intentional.

This is the eighth review, run once after the D14 to D17 correction pass. The rubric walker rates the PRD sound and decision-ready, finds D14 to D17 applied consistently across the FRs, glossary, section 8, section 9 and the spec, and reports one high finding (the held late mark does not bound when the failed attempt happened). The adversarial reviewer (20 findings: 0 critical, 8 high) says the PRD is not ready for ticket slicing as written and questions no owner decision. Its highs: whether the alternate chain is ordered-exclusive or pooled; no trigger or scope bound for who may record an adjustment under D17; extension routing 'fixed when made' against the block reroute rules; no defined qualifying attempt for a held late mark; no freshness bound or fact list for 'cannot be verified' HRMS data; whether the primary project and owner are a snapshot at publication or read live; the assignment-pending trigger covering only the primary project in some sections and a missing owner in others; and delegate naming not tied to a sheet week. The four highs from the seventh pass are closed. There are no critical findings, so the grade is Fair, driven by the high findings.

## Dimension verdicts
- Decision-readiness — strong
- Substance over theater — strong
- Strategic coherence — adequate
- Done-ness clarity — adequate
- Scope honesty — strong
- Downstream usability — adequate
- Shape fit — adequate

Finding counts across both reviewers: critical 0, high 9, medium 20, low 8 (rubric walker alone: critical 0, high 1, medium 8, low 8).

## Findings by severity

### Critical (0)

### High (9)

**[Decision-readiness]** — Held late mark does not say when the failed attempt must have happened (§FR-11, glossary "Held late mark")
FR-11 holds the mark "if the first successful submission then falls after the deadline and such an attempt was recorded earlier". "Earlier" is relative to the successful submission only. An employee who is already past the deadline and then hits one recorded HRMS refusal, or who hits one at any time during the week, converts a plain late mark into a held mark plus an automatic extension request. Late-mark accuracy is the PRD's stated fairness goal ("late marks must be accurate", §8). Open question 16 asks whether a recorded attempt is enough proof of an outage, but not whether the attempt must fall before the deadline.
Fix: add to open question 16 (do not change D15) whether the refused attempt must be recorded at or before the deadline, and whether it must concern that sheet and week. Record a provisional default.

**[Adversarial review]** — H1. Alternate chain: ordered-exclusive or pooled? (PRD FR-23, FR-24 (shared decision rules), FR-17; glossary "Alternate approver"; spec constraints.)
FR-23 says the block goes to the "first eligible decider in order": reporting manager, then delivery-manager holders. The same text says "any eligible holder" of the DM role may decide, and the shared rules say "an eligible alternate may [act]" with the first valid decision winning. Scenario: a self-review block; the reporting manager is eligible and a DM holder is also eligible. Does the DM see approve and reject, and can the DM win the race? Three readings are possible: only the RM until the RM is ineligible; the RM or any DM at once; or the RM plus all DMs, with the first recording winning. The same ambiguity applies to extension requests and adjustments. This decides who sees the approve button and who gets routing notices, so it blocks the approval stories.
Fix: state whether the chain is ordered-exclusive (a DM acts only when the RM is ineligible) or pooled, and apply the same rule to blocks, extension requests and adjustments.

**[Adversarial review]** — H2. Adjustment authority has no trigger or scope bound (FR-17, FR-20, FR-23, FR-24, spec CAP-24, assumptions (D17).)
D17 lets the named reviewer "or an eligible alternate" record an adjustment, and "both may act". FR-20 lists "or an adjustment" next to triggers that mean the reviewer is ineligible, but D17 allows alternates when the reviewer is eligible. As written, the employee's reporting manager and every eligible DM holder (P11 is all holders) can change approved, billable hours on any block for any project at any time. There is no precondition, no time limit (V2) and no request object. Scenario: a DM adjusts a block on a project they have nothing to do with, with the named reviewer eligible and unaware. Only an audit row is left. Finance reads the net roll-up.
Fix: say when an alternate may record (for example only when the named reviewer is ineligible or has not acted within a set time), or state explicitly that any chain member may record at any time. If the latter, record it as a conscious owner decision with a notification to the named reviewer.

**[Adversarial review]** — H3. Extension routing "fixed when the request is made" conflicts with eligibility re-check and rerouting (FR-12, FR-24 (shared rules), spec CAP-10.)
FR-12 says routing is fixed at request time and eligibility is re-checked at decision time. FR-24 says blocks are rerouted promptly when the decider becomes ineligible, and re-checked on HRMS change events and by the sweep. Scenario: Meera requests an extension on Monday and it routes to the Project 1 reviewer R. R goes on approved leave Tuesday, or HRMS reassigns the reviewer. Does the request stay with R, reroute to the chain, or enter the HR queue? Is the queue entry triggered when R becomes ineligible, or only when someone tries to decide? "Fixed" can mean the decider identity or only the chain type. Meanwhile the late mark sits unresolved.
Fix: define "fixed" (chain type versus person) and state that a pending extension reroutes under the same events as a block. The extension-specific wording should not contradict the shared rules.

**[Adversarial review]** — H4. A held late mark has no defined qualifying attempt (FR-11 fifth bullet, FR-21, section 8; spec CAP-10; glossary "Held late mark".)
the hold applies when "such an attempt was recorded earlier", meaning an HRMS-caused refused attempt at submit. Undefined are:
Fix: define the qualifying attempt: submit action, same sheet, made at or before the deadline (or a stated window), refusal classified by a fixed validation order. Add an owner-confirmed way to cover an outage where no attempt could be recorded (for example a module-observed outage window). Related open question below.

**[Adversarial review]** — H5. "Cannot be verified" and "stale" are undefined, and so is which actions need HRMS data (section 8, FR-5, FR-6, FR-10, FR-24, spec outage constraint.)
every fail-closed rule depends on "unavailable or cannot be verified" and "never stale data". No freshness bound is given. Scenario: a read made 30 seconds ago is a stale read, or not? Which submit checks need HRMS: reviewer assignment, primary project, leave status, active status? Copy takes reviewers "at the time of copying", yet a submitted block's reviewer snapshot is never said to be fixed or refreshed. Whether the Submit button depends on a live HRMS call or on the stored block reviewer decides whether outages are rare or constant. Fail-closed behavior is also the trigger for the held mark, so this feeds H4.
Fix: for each action (submit, publish, copy, decide, record, name delegate, classify leave) list the HRMS facts it verifies. Give a freshness rule, even a provisional default (P-number) such as a maximum age for a verified read.

**[Adversarial review]** — H6. Owner and primary project: snapshot at publication, or live? (FR-2, FR-10, FR-22, glossary "Project 1 owner"; spec constraints (owner status judged at decision instant); P12.)
Project 1 must be the HRMS primary project. Scenario: owner A publishes Friday. On Saturday HRMS moves the employee to a single new primary project owned by B; no flag is raised because the assignment was never missing or conflicting. The employee's draft names Project 1 = old project. Does submit refuse (HRMS-caused refusal, held mark) or accept? Which owner (A or B) sees the sheet in FR-22 and sees the on-time or late status? Under the decision-instant rule, A stops being excluded from deciding and B becomes excluded. The delegate named by A may no longer be a delegate for a B-owned sheet, yet A's publish record stays. FR-2 only calls out the "assignment changed" refusal inside the pending-flag paragraph.
Fix: say whether the primary project and owner are snapshotted at publication or read live at each use (publish, submit, status view, exclusion, extension routing), and how a transfer between publication and submission is handled.

**[Adversarial review]** — H7. Assignment-pending trigger disagrees across sections (FR-10 fifth bullet, spec CAP-16, versus FR-2, D16, glossary "Assignment-pending flag".)
FR-10 and CAP-16 send an employee with a missing or conflicting primary-project **or owner** assignment through the pending path. FR-2, D16 and the glossary define the flag only for a missing or conflicting **primary-project** assignment. Scenario: the employee has exactly one primary project, but that project has no owner in HRMS. Is the flag raised? If yes, the "Project 1 requirement waived" rule makes no sense, because Project 1 is known. If no, nobody can publish before the cut-off and after it only HR, with no flag, no HR notification and no assignment-resolution list entry. A conflicting assignment (two primary projects) also leaves "that sheet's Project 1 owner" for the exclusion rule undefined: both owners, neither, or fail closed?
Fix: list the exact flag triggers (missing primary, conflicting primary, missing owner, multiple owners) and what each waives. State the exclusion set for a conflicting assignment.

**[Adversarial review]** — H8. Delegate naming week and expiry are not tied to a sheet week (FR-10 (delegate bullet and past-week bullet), spec CAP-16, glossary "Delegate publisher".)
"one week", "expires at the next Monday 00:00 IST" and "named after the cut-off" are all anchored to the naming time, not to a timesheet week. Scenarios:
Fix: define a naming as owner plus timesheet week (or plus a start and end instant), what sheet weeks it can publish, and whether it is per owner or per employee.

### Medium (20)

**[Decision-readiness]** — Outage volume is not surfaced as a consequence (§8 Identity and data, FR-11, FR-12)
fail-closed submit plus an automatically raised extension request per affected sheet means one HRMS outage near a deadline creates up to one request per employee. Each goes to a Project 1 reviewer or the HR queue, and the escalation clock is unset. This trade-off is not named.
Fix: add an open question on bulk or outage-wide handling of auto-raised requests, and note it in §8 as an accepted cost. Do not reverse D15.

**[Strategic coherence]** — No metric or signal covers the governance machinery (§7)
SM-1 to SM-4 and the counters cover on-time rate, effort, smiley and rejection rate. Nothing tracks the HR exception queue, held marks, assignment-pending cases or review turnaround. These are the parts D14 to D17 added and the likeliest to create operational load.
Fix: add a secondary or counter-metric such as queue age and held-mark count, with no target, in the same style as SM-3.

**[Done-ness clarity]** — The D16 waiver permits a sheet with no blocks (§FR-2, FR-15, §3 "Sheet states")
"The Project 1 requirement is waived while the flag is open... the employee may submit otherwise valid blocks" and "Projects 2 through 5 optional". Nothing requires at least one block. A submitted zero-block sheet has no reviewer and no block to approve, and "Approved when every block is approved" is vacuously true or never reached. A leave-only sheet is the only documented zero-block case.
Fix: state "at least one block" while the flag is open, or state the outcome for a zero-block submit.

**[Done-ness clarity]** — The assignment-pending trigger and exit cover the primary project only (§FR-2, FR-10, FR-12, glossary "Assignment-pending flag")
FR-10 routes a "missing or conflicting HRMS primary-project or owner assignment" through the flag, and FR-2 says a project with no HRMS reviewer is "flagged for resolution". The glossary and spec trigger is only a missing or conflicting primary project, and the flag leaves when the HRMS "shows exactly one primary project". A missing owner with a valid primary project, or a missing reviewer, has no defined trigger, no defined listing in the assignment-resolution list, and no defined exit. FR-12 names "no primary-project or reviewer assignment" but not "conflicting".
Fix: state in FR-2 whether a missing owner or reviewer raises the same flag or a different one, with its exit condition. If that is undecided, add it to open question 2.

**[Done-ness clarity]** — "Alternate" is ambiguous between ordered and concurrent (§FR-17, FR-23, FR-24, glossary "Alternate approver")
the glossary says "first eligible decider in order, the employee's designated reporting manager and then any eligible holder of the delivery-manager role". FR-24 and D17 say the named reviewer "and an eligible alternate may both act" and "the first valid recording wins". It is unclear whether a delivery manager may act while the reporting manager is eligible. For adjustments nothing routes to anyone, so "in order" has no meaning.
Fix: one sentence stating whether all eligible chain members may act, or only the first eligible one, for blocks, extension requests and adjustments.

**[Done-ness clarity]** — Unbounded or undefined terms (§FR-24, §8, FR-18, FR-16, FR-9)
"the block is rerouted promptly" sits beside a daily sweep default (P7) and event triggers, so no bound is given. §8 "quick and forgiving" has no threshold. FR-18 uses a "total available hours" denominator that is not defined for part-leave or leave-only weeks. FR-16 "closed project" has no named source. FR-9 "learnings stay private unless shared" gives no sharing action or audience.
Fix: give "promptly" a bound or point it at the HRMS-event trigger. Set a UI response bound or drop the adjective. Define available hours. Name the system of record for closed projects. Define sharing or drop the clause.

**[Downstream usability]** — FR-24 is epic-sized (§FR-24)
its ~13 bullets mix absent-reviewer routing, eligibility timing, the queue, HR assignment limits, shared decision rules, notification policy and escalation. Stories would span several FRs, and FR-23 repeats the "decides only that block" bullet.
Fix: split FR-24 into routing and eligibility, HR queue and assignment, and shared decision rules, keeping the IDs by adding new ones rather than renumbering.

**[Downstream usability]** — The PRD restates the spec near-verbatim although §0 says it "does not duplicate" it (FR-2, FR-10, FR-11, FR-17, FR-24, FR-25, §3)
each owner decision must now be kept in step across the spec, glossary and PRD, which creates drift risk. D14 to D17 are in sync today.
Fix: soften the §0 claim, or have the FRs reference the CAP success text for the detailed rules.

**[Adversarial review]** — M1. Non-draft sheet when the pending flag clears (FR-2 last bullet, D16.)
only "a draft sheet then follows the normal Project 1 rule". A Submitted or Changes-required sheet that was submitted with no Project 1 block, when the flag clears, is undefined: valid, invalid, or needs a Project 1 block added? A rejected block that is resubmitted after the clear faces the normal rule. FR-12's routing for an extension raised under the flag stays fixed, which is probably intended but not stated.
Fix: say that submitted sheets stay valid as recorded, and what a reopen or resubmit after the clear must contain.

**[Adversarial review]** — M2. Pre-deadline and pre-submission extension requests (FR-12, UJ-3, P9, CAP-10 intent.)
the intent says "request an extension". The only effect defined is waiving an existing late mark. Scenarios: an extension requested before the deadline, or before any submission. Is a request on an on-time sheet allowed, and what does an approval waive? Does approval pre-authorize a later mark? A request pending when the sheet becomes Approved: is it still decidable under P9 ("not after approved")? Unlimited requests allow two pending requests on one sheet, or a declined request followed by an identical one, and an automatically raised request may coincide with an employee-raised one. The "request as stored" binding does not say which one wins.
Fix: state that a request attaches to a sheet, whether one may exist before a mark does, the maximum one pending per sheet, and what happens to a pending request at approval.

**[Adversarial review]** — M3. Late-mark display while a request is pending, waived or held (FR-11, FR-13, FR-19, FR-22, glossary "Late mark".)
the owner "sees only whether on time or late"; the employee sees "each late mark"; HR sees held marks. Undefined: is the mark counted and visible to HR, the reporting manager and the owner as "late" while a human-raised extension is pending? Does the owner and delegate view show "late" for a waived or held mark? Does the employee see held marks? SM-1 counting is an owner decision, but the per-view display is not.
Fix: a small table of mark state (counted, pending-extension, held, waived) by viewer.

**[Adversarial review]** — M4. Leave-flagged sheet behavior and the publish-versus-leave race (FR-25, FR-14, FR-10.)
a published sheet whose week later becomes fully covered by leave is flagged, never converted, and the resolver role has no default (an intentional open question). The part not covered: does the employee owe a submission, do lateness and the reminder rules still apply (FR-14 suppresses reminders for "employees on approved leave")? FR-25 says a submission races a leave approval with "the submission wins" but gives no rule for a publish racing the same leave approval; HR's publish at the cut-off minute on a sheet that is leave-only at that instant is undefined, and so is the case where classification cannot be verified (the sheet keeps its type while HR publishes).
Fix: say whether a flagged sheet is subject to late marks and reminders until resolved. Give a precedence rule for publish versus leave approval.

**[Adversarial review]** — M5. Sheet entity before publication (FR-1, FR-6, FR-10, FR-25, sheet-state definitions.)
an employee "cannot start the week's sheet until it is published", yet the unpublished sheet carries leave-only type and the pending flag, appears in HR's unpublished list, and is "exactly one per employee per week". Copy-last-week "is a new sheet", so a copy attempted before publication is not addressed. Derived state for an unpublished sheet is "Draft", which the glossary defines as "Started".
Fix: say whether the sheet record exists from week start, what "start" blocks (edit, copy), and what state it shows before publication.

**[Adversarial review]** — M6. Outage versus "nobody eligible" (FR-24, section 8, FR-14.)
during an outage the eligibility check "fails closed: refused with retry". The same text sends an item to the HR exception queue "when no decider is eligible". Which applies when eligibility cannot be verified? Scenario: a 6-hour outage and 40 pending blocks. If they all enter the queue, HR's assignment is itself refused (the assignee check needs HRMS). The escalation clock (P3) may run during an outage. Reminders need leave status: sent or suppressed when leave cannot be read? FR-14 is not listed among fail-closed actions.
Fix: say that "cannot verify" never creates a queue entry and does not start the escalation clock. Give the reminder behavior during an outage.

**[Adversarial review]** — M7. Delegate or owner changes after naming (FR-10, spec constraints.)
the delegate must be active and not on leave "when named" only. A delegate who goes on leave or becomes inactive on Tuesday keeps the naming. The owner may be replaced in HRMS the same week; does the old owner's naming survive for a project now owned by someone else? Audit rows are specified, behavior is not.
Fix: say what happens to a naming when either party changes status or the owner changes.

**[Adversarial review]** — M8. Resolver for retroactive HRMS changes (section 8, FR-24, spec outage constraint.)
"retroactive HRMS changes flag records for audited resolution". Open question 2 covers assignment resolution and question 9 covers leave. Nothing names who resolves a retroactive reviewer, active-status or ownership change that touches a recorded decision, or what a resolution may do given "never rewrite".
Fix: add an open question (with a default such as the module owner) or a stated rule.

**[Adversarial review]** — M9. No entry point for an adjustment, and an unenforceable HR flag condition (FR-17, FR-24, glossary "HR exception queue".)
there is no request object and no employee route (the dispute route is V2, but the request route is not mentioned there). The named reviewer must discover the error. HR "raises the flag when neither the reviewer nor any alternate is eligible". With D17 a reporting manager is nearly always an eligible alternate, so the flag almost never applies, and nothing says it is refused when someone is eligible. The queue definition says items are in the queue with "no eligible recorder", but a flag raised by HR is the entry mechanism.
Fix: state who can ask for a correction (even informally outside the module) and whether an HR flag on a block with an eligible recorder is refused.

**[Adversarial review]** — M10. Delegate naming changes who decides (FR-10, FR-24, spec constraints.)
naming a block's reviewer (or an RM) as delegate makes them conflicted for every sheet of that owner's team, which reroutes blocks to the alternate chain, and a block is "never automatically routed back". The owner is excluded from deciding but can change who decides by choosing the delegate. The naming expiry does not restore the reviewer. P1 allows any active employee as delegate.
Fix: either narrow the exclusion for a delegate (owner's call, so record it as an open question) or say that naming a current block reviewer as delegate triggers a warning. The rerouting should at least be audited as caused by the naming.

**[Adversarial review]** — M11. Self-owner or self-delegate controls its own deadline (FR-10 (D14), FR-11.)
an employee who owns their own primary project, or is HR, can publish their own sheet at a time of their choosing. With no publication window, a later publish gives a later deadline, so late marks never apply to them in practice, while FR-10 says the owner is "never from what the employee types to influence late status". See open question 2.
Fix: owner decision needed; see below.

**[Adversarial review]** — M12. Bulk publish partial failure (FR-10, UJ-4.)
publication is "per employee per week" and fails closed "when HRMS data cannot be verified". An owner publishing for a team of 12 and hitting an outage after 7 gets partial success, each deadline stamped at its own success time. Is a partial publish allowed, which employees were left out, and does the owner see it? "The attempt is recorded" says nothing on this.
Fix: say that publication is per employee with per-employee results shown to the actor.

### Low (8)

**[Decision-readiness]** — Front matter says `status: final` while §0 says "*To confirm:* the working title, the open questions in section 9, and the assumptions in section 10" and the title line says "Working title: confirm". *Fix:* align the status with the confirmations still pending.

Fix: 

**[Strategic coherence]** — All of FR-1 to FR-25 are "In Scope" with no priority (§6.1), so FR-8 (smiley) and FR-24 (queue and escalation) carry equal weight. *Fix:* add a must/should marker for slicing, or state that none is intended.

Fix: 

**[Strategic coherence]** — SM-3 (smiley trend) validates only FR-8 and measures activity rather than the thesis. *Fix:* keep it as a secondary signal or tie it to SM-2.

Fix: 

**[Done-ness clarity]** — The fail-closed list omits some actions (§8, FR-12, FR-7)
it names eligibility checks, submit, publish and copy. Creating an extension request needs routing and eligibility, and a resubmission after reopen needs the HRMS. Neither is stated as fail-closed or as recording its attempt.
Fix: add them to the list, or state that "eligibility checks" covers them.

**[Done-ness clarity]** — Delegate validity is checked only "when named" (§FR-10)
a delegate who later goes inactive or on leave can still publish while the naming is in effect. "For one week" and "named for that week" (FR-22, UJ-4) is also unclear against the "next Monday 00:00 IST" expiry when the sheet published is for a past week.
Fix: say whether this is intended and whether naming binds to a timesheet week or to calendar time.

**[Done-ness clarity]** — Visibility of a held mark to the employee is unstated (FR-13, FR-19)
FR-19 shows held marks to HR, and FR-13 says the employee sees "each late mark".
Fix: state whether held and waived marks appear in the employee's view.

**[Downstream usability]** — Terms drift across the document
"alternate chain", "eligible alternate", "alternate decider" and "Alternate approver"; "decider", "approver" and "recorder"; "exception queue" and "HR exception queue". The "Extension request" glossary entry says "an employee's request" but FR-12 also covers an automatically raised one.
Fix: pick one term per concept and update the glossary entry.

**[Shape fit]** — No journey for HR or finance (§2.3)
the HR exception queue, held-mark resolution and the finance export are exercised only as edge cases.
Fix: add one short-form UJ for HR resolving a queue entry or held mark, so UX and story slicing have a protagonist.

## Open questions for the owner (from the adversarial review)

1. Is the reporting manager and delivery-manager chain ordered-exclusive or pooled, for blocks, extension requests and adjustments (H1)?
2. D14 lets an employee who is their own sheet's owner or delegate (including an HR-role employee) publish their own sheet and set their own deadline. With no publication window, the late mark can then never bind them. Is that intended, or should a published-by-self sheet use the HR cut-off or another rule (M11)? This is raised as a question only; D14 is not challenged.
3. D17 lets the reporting manager and any DM holder record adjustments with the named reviewer eligible. Should an alternate need a precondition, or is open authority intended (H2)?
4. For an outage where no attempt could be recorded (identity outage, HRMS down at sign-in), may the module itself mark the outage window and apply the hold to all submissions in it (H4)? This sits next to the open grace-period question.
5. Are the primary project and owner snapshotted at publication or read live (H6)? Which owner sees the sheet after a mid-week transfer?
6. Does a missing project owner (primary project known) raise the assignment-pending flag, and does it waive the Project 1 requirement (H7)?
7. Which week does a delegate naming cover, and may it publish past weeks (H8)?
8. What freshness limit applies to "verified" HRMS data, as a provisional default (H5)?
9. May an extension be requested before a mark exists, and is more than one pending request allowed per sheet (M2)?
10. Who resolves flagged cases from retroactive HRMS changes (M8)?
11. Should naming a block's reviewer or reporting manager as delegate reroute that person's blocks, given D14's independence rule (M10)? Raised as a question, not a reversal.
12. Does a leave-flagged sheet (published, then fully covered by approved leave) carry late marks and reminders until resolved (M4)?

## Mechanical notes
- **D14 to D17 consistency:** D14 matches in FR-10, FR-22, glossary ("Delegate publisher", "Eligible decider"), spec CAP-16 and the constraints. D15 matches in FR-5, FR-6, FR-10, FR-11, §8, glossary ("Held late mark"), open question 16 and spec CAP-10 and the outage constraint. D16 matches in FR-2, FR-10, FR-12, FR-19, glossary, open questions 2 and 3, P12 and spec CAP-2 and the assumptions. D17 matches in FR-17, FR-20, FR-24, glossary ("Adjustment entry"), spec CAP-24 and the assumptions. The gaps found are listed above.
- **ID continuity:** FR-1 to FR-25 are all present and unique. FR-21 sits between FR-3 and FR-4 and FR-22 inside §4.2, so the order is non-sequential. *Fix:* optional; reorder or note it.
- **Assumptions Index roundtrip:** all inline `[ASSUMPTION]` tags are indexed and all index entries appear inline. SM-2 and SM-4 share one index line.
- **P-list drift:** P1 to P13 match the spec, except that P6 in the spec adds "with no other block content, accomplishments or learnings". *Fix:* copy it into the PRD.
- **Section 9 bullet 10** bundles a V2 question (40-hour cap on adjustments) with a V1 question (P5, first-submission time). Split it for cleaner tracking.
- **Glossary gaps:** "outage-affected" (a sheet flag used in FR-11) and "assignment-resolution list" are used in the FRs but are not standalone glossary terms.
- **Cross-references:** all section and FR references checked resolve. Open question 10 cites FR-21 for P5 correctly.
- **Policy check:** no stack, hosting or vendor content in the PRD. CAP-15 is not reused.

## Reviewer files
- `review-rubric.md`
- `review-adversarial-general.md`
