# PRD Quality Review — Timesheet Management

## Overall verdict
The PRD is lean and honest for a 160-person internal tool. It has a clear thesis (approved hours that billing can read without re-keying), a real Non-Goals list, contiguous IDs and mostly testable FR consequences. The risk sits in the approval and late-mark mechanics. Multi-reviewer sheets, resubmission after the deadline and the publish dependency are all unspecified, and these are the places where stories will diverge. The success metrics are also mostly unmeasurable as written.

## Decision-readiness — adequate
Decisions are stated as decisions. Section 9 lists what the owner resolved: the 40-hour cap, project reviewer only, 3-year retention, unlimited extensions. The open list is short and real: legal review and the memlog entry. The "Legal" bullet in §8 does name a risk and says it is "not a launch condition", while Open Question 1 says "Before launch, ask HR or legal". Those two statements pull in different directions.

Trade-offs are named only thinly. "There is no limit on how many extensions an employee can request" (FR-12) removes the late mark as a control. The PRD does not say what was given up, and the reviewer, not HR, decides. The 40-hour hard refusal (§4.1 Notes) is stated with no mention of overtime or holiday weeks. No `[NOTE FOR PM]` callouts are used anywhere, although several real tensions exist.

### Findings
- **high** Multi-reviewer approval semantics undefined (FR-2, FR-15, §3) — A sheet has up to 5 blocks, each with its own reviewer, and the Sheet has one state. FR-15 says a reviewer "sees only sheets with hours against their project" but not whether each reviewer approves only their block, whether one rejection rejects the whole sheet, or when the sheet becomes "Approved means locked". FR-18 rolls up approved hours "by project", which implies block-level approval. *Fix:* define approval granularity (per block or per sheet), the rule for the sheet state when reviewers disagree, and which reviewer decides extensions (FR-12).
- **high** Late-mark rules for reject, reopen and resubmit are missing (FR-7, FR-11, UJ-2) — If a sheet is submitted on time, rejected, and resubmitted after the deadline, is it late? The same question applies to a reopen after the deadline. FR-11 only covers first submission. Combined with "the late mark is the only mark that can attach to an approved sheet", this decides whether HR sees accurate marks. *Fix:* state that lateness is judged on first submission (or the last), and add a consequence to FR-7 and FR-11.
- **medium** Self-review and reviewer SLA (FR-15, §2.1) — A project reviewer's own sheet has no stated approver. Nothing bounds how long a sheet can wait for review, although finance reads only approved hours (FR-18). *Fix:* add a self-review rule and a reviewer reminder or escalation consequence.

## Substance over theater — strong
There is no persona theater: the four UJs each drive a rule (the Project 1 owner cannot approve, anomaly-first review, late and extension). The Vision is specific and not swappable. It names the 19-hour baseline and flags it as "owner figure, unverified". There is no NFR boilerplate, because §8 holds product-specific rules. One small piece of furniture is "Fairness: an approved sheet is never reported as incorrect", which is not testable and not tied to any FR.

### Findings
- **low** Vague "Fairness" bullet (§8) — It reads as a principle with no consequence. *Fix:* either tie it to FR-17 and FR-18 (adjustments are shown, not rewritten) or drop it.

## Strategic coherence — adequate
The thesis is clear: capture real effort per project, route it to the reviewer, lock it, and let finance read it. Scope follows it, and FR-18 and FR-19 serve the finance and HR sides. Counter-metrics are present, which is good. The weak point is measurement. The metrics do not yet prove the thesis.

### Findings
- **medium** SM-2 and SM-4 are not measurable (§7) — SM-2 ("completes a full sheet in one sitting... without re-keying") has no instrument, threshold or timeframe. SM-4 has a baseline but "After-target not set", and SM-3 has no target. The thesis claim is about billing without re-keying, and no metric tests it beyond SM-2. *Fix:* give SM-2 a proxy (for example median time to submit, or finance re-key incidents per month) and set a review date for the targets.
- **medium** SM-C1 duplicates SM-1 (§7) — SM-1 is "one minus the late-mark rate", and SM-C1 is "Late marks issued". They are the same quantity read in opposite directions, so SM-C1 is not an independent guard. Extension waivers (FR-12, unlimited) also inflate SM-1. *Fix:* measure SM-1 before waivers, or make SM-C1 something else, such as the share of waived marks or the share of resubmissions after rejection.

## Done-ness clarity — adequate
Most FRs carry specific consequences that are testable (FR-2 four-field refusal and sixth-block refusal, FR-3 multiples of 8, FR-16 15-hour threshold). Gaps appear where behaviour depends on undefined terms, and the 40-hour rule has no FR of its own.

### Findings
- **medium** The 40-hour cap is an orphan (§4.1 "Notes") — "project hours plus PTO total at most 40 per week; a sheet above 40 is refused" sits under FR-9 with no FR ID and no CAP. It also has no handling for overtime or public-holiday weeks, and no minimum. *Fix:* promote it to its own FR with a CAP and state the overtime and holiday cases.
- **medium** Week and deadline definitions (FR-1, FR-11, UJ-1) — The week's start day and boundaries are not defined. The deadline is "11:59 pm UTC on the day after publication", while UJ-1 says "before Saturday ends". For an India-based workforce, 11:59 pm UTC is early morning local time the next day, so the two statements can disagree. *Fix:* define the week, and state the deadline in the local time that matters or show the UTC-to-local conversion.
- **medium** Adjustment entry workflow (FR-17, §3) — "a recorded adjustment entry" does not say who can create it, who approves it, whether it passes through the reviewer, or how the roll-up (FR-18) includes it. *Fix:* add actor, approval and roll-up consequences.
- **medium** Reminders and leave dependency (FR-14, §5) — "before the deadline" has no lead time, and the reviewer reminder has no cadence. "Employees on approved leave get none" needs leave data, while leave is a Non-Goal. *Fix:* give lead times and name the HRMS source of approved leave.
- **medium** Learnings visibility (FR-4, FR-9, §8) — "learnings stay private unless shared" does not say who shares or with whom. It is also unclear whether the reviewer sees learnings when reviewing the sheet. *Fix:* state the sharing actor and audience and what the reviewer sees.
- **low** FR-11 wording — "accepted, marked late, and carries a late mark" says the same thing twice. FR-18 does not name the export format, and FR-4 and FR-5 have no description line.

## Scope honesty — adequate
The Non-Goals section does real work (payroll, loss-of-pay, CAP-15 retired, pay consequences). The open-items density is low and fits the stakes, but it is partly low because gaps are left unflagged.

### Findings
- **high** The Project 1 owner is a single point of failure (FR-10, UJ-4) — "an employee cannot start the week's sheet until it is published", and the deadline counts from publication. If the owner is on leave or forgets, there is no delegate, fallback or escalation, and the deadline could start late. This is neither a Non-Goal nor an open question. *Fix:* add a delegate or HR-publish rule, or record it as an open question with a `[NOTE FOR PM]`.
- **medium** Assumptions not tagged inline (§0, §10) — §0 says assumptions are tagged `[ASSUMPTION]`, but only one inline tag exists (§7). The 15-hour threshold in FR-16 and "CAP-6, CAP-7, CAP-11 and CAP-13 are treated as in v1 scope" appear only in the index. §9 says the threshold is "tagged as an assumption", which it is not. *Fix:* tag them inline at FR-16 and in §6.1.

## Downstream usability — adequate
FR-1 to FR-20, UJ-1 to UJ-4 and SM-1 to SM-4 plus SM-C1 and SM-C2 are contiguous. UJs have named protagonists. The Glossary is partial and defers to the spec's `glossary.md`, which is acceptable for a PRD that sits next to the spec. Several role terms drift.

### Findings
- **medium** UJ-4 has no matching FR (§2.3, FR-15) — Priya "watches who has and has not submitted", but the only FR content is a clause in FR-15 ("can view submission status"). §4.2 says it realizes UJ-4, yet nothing there describes the status view. *Fix:* add an FR for the owner's submission-status view and its scope.
- **medium** Role vocabulary drift (§2.1, §3) — "Project manager", "Project owner (Project 1 owner)", "Project reviewer", "Reporting manager", "Finance" and "HR" appear, but only "Project reviewer" and "Published sheet" are in the Glossary. The Project manager's job ("stop spending hours collecting") has no FR. Finance has no access FR either. Terms like "extension" and "anomaly" are used as nouns without definitions. *Fix:* add role and term definitions and say whether the project manager and reviewer can be the same person.

## Shape fit — strong
A capability spec with four short UJs fits an internal tool with six roles. The UJs justify themselves because each exposes a rule. UJ-4 is two sentences and does not feel padded. There are no consumer-style sections (no pricing, market or innovation) and no over-formalization.

## Mechanical notes
- **Broken cross-ref:** §0 says assumptions are "indexed in section 9", but the Assumptions Index is §10 (§9 is Open Questions).
- **Assumptions roundtrip:** the index has 3 entries. Only the §7 entry appears inline. The 15-hour threshold and the CAP-6/7/11/13 scope assumption are not tagged inline (see the Scope honesty finding).
- **ID continuity:** FR-1 to FR-20, UJ-1 to UJ-4, SM-1 to SM-4 and SM-C1/C2 have no gaps or duplicates. CAP-15 is not used, consistent with the retirement policy. I did not verify CAP numbers against the spec file.
- **FR-to-CAP mapping:** CAP-10 is used by both FR-11 and FR-12, and CAP-7 and CAP-9 appear in several FRs. This is fine. The 40-hour rule has no CAP (see Done-ness).
- **Glossary:** "Project block — one project's project, tasks/activities, hours and reviewer" is awkwardly worded. "Published sheet" is defined, but FR-10 says the owner publishes "the weekly sheet", so the term is used loosely.
- **Sections:** all sections needed for this product type are present. There is no Addendum, as expected.
