# PRD Quality Review — Timesheet Management

Scope: critique only, after D18-D26 were applied. Owner decisions D1-D26, provisional defaults P1-P15 (P15 is a proposal only), the 20 section-9 open questions, SM-1 and the retired CAP-15 are treated as given. Any finding that touches an owner decision is phrased as an open question.

## Overall verdict
The PRD is coherent on its main paths. The sheet and block state derivation, publication and deadline, late-mark and waiver, and the Eligible Decider rule agree across the PRD, spec and glossary. The remaining risk is in three places. First, wording left behind by D18-D26 contradicts the accepted provisional defaults (P3, P7, P8, P14). Second, some inferred rules are written as settled policy with no assumption tag (the outage-overlap hold, the second snapshot). Third, a number of gaps would force a ticket author to invent rules: who may be assigned from the HR queue, what a reopened block looks like to a reviewer, what an extension request means before a submission, and who consumes accomplishments.

## Decision-readiness — adequate
Decisions are mostly stated as decisions and each open question carries a class and a default. The accepted cost of failing closed is now named in section 8, which fixes a gap in the earlier review. The weak points are where provisional values and approved rules are not separated.

### Findings
- **[high]** Stale "not set" wording contradicts accepted provisional defaults (§FR-24 last bullet, §10 assumptions, P3, P7, P8) — FR-24 says "the owner supplies the waiting days and the escalation contact before build" and "the escalation has no time limit until they are". The sweep frequency is likewise "not set; the owner specifies it". P3 (3 working days), P8 (the business owner) and P7 (daily sweep) are now accepted provisionally by the owner. A ticket author reading FR-24 literally builds an escalation with no timer, while section 10.1 says 3 days. *Fix:* rewrite the FR-24 bullet and the two §10 lines to "provisional default P3/P8/P7 applies until HR or business confirms", and remove "before build" unless that gate is intended.
- **[high]** Eligible Decider has no positive qualification, so HR may assign anyone (§3 "Eligible decider", FR-24, FR-17) — the rule is purely exclusionary: not the employee, owner, delegate, inactive, on leave, and for assignment no HR role. Any other active employee, including a peer or a junior colleague, passes. HR can assign such a person to approve or adjust hours that become finance-visible and locked. Open question for the owner: must a queue assignee hold a management or delivery role, belong to the employee's reporting chain, or hold some reviewer capacity? State the pool, or state explicitly that none is intended.
- **[medium]** "Decision-time on authoritative data" conflicts with the 5-minute freshness window (§3 "Eligible decider", FR-24 first bullet, §8, P14) — the FRs say eligibility is judged "at the instant" on "authoritative HRMS data". Section 8 and P14 allow a verified read up to 5 minutes old. A reviewer put on leave 3 minutes ago can still decide, and the FR text does not admit that. P14 is provisional and Q18 is open, but the FRs present the strict rule as approved. *Fix:* qualify the FR-24 and glossary wording with "within the P14 freshness window, provisional".
- **[medium]** Open question for the owner on D14: may an employee who is their own sheet's owner or delegate publish it whenever they choose (§FR-10)? That lets them set their own deadline start, so they can never be late, which weakens late-mark fairness. Is any control intended, for example the HR cut-off applying to self-published sheets?

## Substance over theater — adequate
Personas drive distinct rules and there is no boilerplate. One required field has no reader. See Done-ness.

### Findings
- **[medium]** Accomplishments and learnings are mandatory but no role may read them (§FR-4, FR-9, P6, FR-15) — FR-4 refuses a sheet without accomplishments. P6 limits a reviewer to their own block plus total hours, FR-9 keeps learnings private, and the reporting manager and HR views list hours, marks and status only. A ticket author cannot decide who sees accomplishments, or why they are required. *Fix:* name the audience (reviewer, reporting manager, HR, or the employee only) or state that they are stored for the employee alone.

## Strategic coherence — adequate
The thesis (real effort per project, reviewed, locked and read by finance) is clear. The governance machinery is large relative to the metrics.

### Findings
- **[medium]** Open question: a flat 40-hour refusal against "captures real effort" (§1, FR-21, P5) — a refused over-40 attempt never changes lateness, so an employee who worked 45 hours must under-report to submit on time or accept a late mark. That conflicts with the vision and with SM-C1 ("do not push careless sheets"). It is tagged an assumption, but the tension is not named. Is a flat cap acceptable for exempt IT staff, or should the owner confirm it explicitly?
- **[low]** No metric covers the new governance load (§7) — HR queue age, held-mark count and assignment-pending count have no signal. *Fix:* add a no-target secondary metric.
- **[low]** All FRs are In Scope with no priority (§6.1).

## Done-ness clarity — adequate
Most consequences are testable. The gaps below are in the edges added by D18-D26 and in a few unbounded areas.

### Findings
- **[high]** Inferred rules are written as settled policy without an inline tag (§FR-11 outage overlap bullet, FR-2 and FR-10 snapshot behaviour, §10 last bullet, glossary "Held late mark") — section 10 lists as "inferred, for the owner to confirm": an observed outage window holds a late mark when it overlaps the publication-to-deadline period; a second snapshot is added when a flag leaves a published sheet; a sheet with missing or multiple owners is published by HR after the cut-off. In the FRs these appear as fact with no `[ASSUMPTION]`, and the second-snapshot rule appears nowhere in FR-2 or FR-10. FR-2 says the sheet "keeps that Project 1 and owner", so which snapshot governs routing after the flag leaves is unstated. The overlap rule has no minimum duration (Q17 has no default), so a one-minute overnight blip could hold every late mark in the window and raise one automatic extension request per employee. *Fix:* tag these inline, state which snapshot governs, and either add a provisional minimum overlap or put the question on Q17 explicitly.
- **[medium]** A zero-block submit is possible and reaches Approved with no decision (§FR-2, §3 "Sheet states") — while a missing or conflicting primary project flag is open, Project 1 is waived and Projects 2-5 are optional, and nothing requires at least one block. "Approved when every block is approved" is vacuously true. *Fix:* state at least one block, or the outcome of a zero-block submit.
- **[medium]** A reopened undecided block has no defined sheet state or reviewer view (§FR-7, §3 "Sheet states", FR-15) — precedence says "Submitted after submit" and the block goes back to Draft, so the sheet can be Submitted while a block is Draft. Can the reviewer still decide that block, is it hidden from the reviewer's list, and does the sheet need to be resubmitted as a whole?
- **[medium]** Open question: is there any limit on reopening undecided blocks (§FR-7, FR-11)? An employee can submit on time and edit freely until a reviewer decides, with no new late mark. That keeps lateness unaffected but leaves the timing and content of the first submission unbounded.
- **[medium]** Extension request semantics are unclear before a submission and after approval (§FR-12, P9, FR-11) — "no submitted block is needed" implies a request can precede submission, but an approved request then has no mark to waive. Does approval pre-waive a later mark, and what if the employee submits on time? An automatically raised request for a held mark can also be pending when the sheet is approved (P9 forbids requests after approval); is that request still decidable?
- **[medium]** Block validity rules are missing (§FR-2) — whether a block may carry 0 hours, whether the same project may appear in two blocks, whether an employee may choose any HRMS project or only an assigned one, and whether a closed project is selectable (FR-16 only flags it) are all unstated.
- **[medium]** Copy-last-week edge cases (§FR-6) — "hours left editable" is ambiguous (copied or blank). The rule is unstated for a prior leave-only week, a project the employee has left or that is closed, a changed primary project and an open assignment-pending flag.
- **[medium]** PTO entered by the employee is never reconciled with HRMS leave (§FR-3, FR-25) — a normal sheet accepts any multiple of 8, even when HRMS shows no leave or more or fewer days. State whether it is validated, flagged or only informational. This feeds utilization.
- **[medium]** "Total available hours" is used as a denominator but is never defined (§FR-18, §3) — leave, PTO and part-leave weeks are not covered, so a utilization test case cannot be written.
- **[medium]** HR queue lifecycle is incomplete (§FR-24, FR-17) — what happens when an assignee later becomes ineligible, declines, or never acts; whether reassignment is allowed; and the queue states other than the adjustment-needed flag's open, assigned or recorded. Also: who tells HR that an adjustment is needed, since HR is otherwise read-only?
- **[medium]** "Rerouted promptly" is unbounded and depends on an HRMS capability that is not stated (§FR-24) — event-driven routing assumes the HRMS emits active and leave change events, while the only default is a daily sweep (P7), so the worst lag is a day. Add the event dependency to the assumptions and state the bound or drop "promptly".
- **[low]** Held marks are not specified in the employee, owner and delegate views (§FR-13, FR-22) — does the owner or delegate see "late" or "on time" for a held mark, and does the employee see it?
- **[low]** Bulk approve outcome is unspecified for partial failure and for ineligible sheets (§FR-16) — stale versions are covered, but eligibility rechecks and a per-sheet result report are not.
- **[low]** Bulk publish is not stated (§FR-10, UJ-4) — publication is per employee per week, yet UJ-4 has the owner publish for the team. Is there a one-action bulk publish with per-employee deadlines?
- **[low]** A mis-publication cannot be undone (§FR-10) — "never published again" has no correction path for a wrong employee or week once the deadline has started.
- **[low]** An employee who leaves or turns inactive mid-week (§FR-5, §8) — submit verifies "employee active" and fails closed, so their last hours cannot be submitted. State the offboarding behaviour.
- **[low]** Billable flag history (§FR-18) — whether a later change to a project's billable flag rewrites the roll-up of approved hours, or is snapshotted at approval.
- **[low]** Reviewer reminder is once per week (§FR-14, P7) — sheets published later in the week, or for past weeks, never trigger a reminder because of the cap.

## Scope honesty — adequate
Non-goals are explicit, CAP-15 stays retired and V2 items are labelled. Provisional and proposed items are labelled in sections 9 and 10.1, and P15 is not presented as approved anywhere. Weaknesses are the unflagged inferences and stale wording above.

### Findings
- **[low]** Front matter says `status: final` while §0 lists items still to confirm and the title line says "confirm" (front matter, §0, title). *Fix:* align the status.
- **[low]** P13 has no entry in section 9 although §10.1 says each default stays listed there until confirmed (§9, §10.1). The FRs also state the P13 rule (an HR-role holder decides only in a separate capacity) as firm text. *Fix:* add a question or mark P13 as confirmed by the owner.
- **[low]** Section 9 Q2 cites "D16, D24" but the PRD never defines those identifiers (§9). *Fix:* describe or link them to the memlog.
- **[low]** Section 9 Q10 bundles a V2 question (40-hour cap on adjustments) with a V1 question (P5) (§9).

## Downstream usability — adequate
Cross-references resolve, every FR names a CAP and CAP-15 is not reused. Sliceability is the concern.

### Findings
- **[medium]** Finance has no access scope and the export has no issuance rule (§3 "Finance", "Issued export", FR-18) — who can read which projects, who or what issues an export and when, and the format and scope per issue are all unstated, although "issued export is never rewritten" depends on them. *Fix:* add a finance access rule and the issue trigger.
- **[low]** FR-24 remains epic-sized, and FR-23's title ("for self-review") understates its tiered chain scope (§FR-23, FR-24).
- **[low]** Term drift: "alternate chain", "eligible alternate", "alternate decider" and "Alternate approver"; "decider", "approver" and "recorder" (§3, §4).
- **[low]** The PRD copy of P6 omits the spec's clause "with no other block content, accomplishments or learnings" (§10.1 against the spec).
- **[low]** Retention (§8) names sheets and change history only; failed-attempt records, naming audits, outage windows, held marks and queue history have no stated retention.
- **[low]** Section 8 has no access-control, performance, availability or accessibility statements, and "quick and forgiving" has no threshold (§8). Stack choices stay with architecture, but testable targets can be stated.

## Shape fit — adequate
Named-protagonist journeys suit a multi-stakeholder module. No journey exists for HR (queue, held-mark resolution) or finance (export), although D18-D26 added most of the new behaviour there.

### Findings
- **[low]** Add one short-form journey for HR resolving a queue entry or an assignment-pending case (§2.3), and one for finance issuing an export.
- **[low]** Open question: when the Project 1 owner is also the named reviewer of that Project 1 block, the block always routes down the alternate chain (§FR-24, Eligible decider). Is that frequency expected, and does it overload reporting managers?

## Mechanical notes
- **ID continuity:** FR-1 to FR-25 and CAP-1 to CAP-24 are present and unique; FR-21 sits between FR-3 and FR-4 and FR-22 inside §4.2.
- **Assumptions roundtrip:** all inline `[ASSUMPTION]` tags are indexed, but the last index line (outage overlap, second snapshot, HR publication of missing or multiple owners) has no inline tag. See the high finding above.
- **P-list drift:** P1-P5 and P7-P15 match the spec; P6 differs (low finding above).
- **Open-question count:** 20 questions, as stated.
- **Policy check:** no stack, hosting or vendor content found in the PRD; CAP-15 is not reused; P15 appears only as proposed.
- **Spec and glossary agreement:** the Delegate publisher PRD entry omits "must be in effect when publishing", which the spec and glossary carry; otherwise D18-D26 are in step across the three files.

## Counts
- critical: 0
- high: 3
- medium: 15
- low: 20
