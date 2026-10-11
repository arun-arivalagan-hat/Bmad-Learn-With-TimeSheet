# Reconciliation: PRD vs spec (plus glossary, premium-tier, brief, PRFAQ)

Inputs compared: spec-timesheet-management.md, glossary.md, premium-tier.md, brief-timesheet-management.md, prfaq-timesheet-management.md. Known and intended differences (scale, reporting manager view FR-20, 15h jump anomaly with 40h cap, reviewer only approves) are excluded.

Checked and fine: CAP-1 to CAP-14, CAP-16 to CAP-18 all map to FRs; CAP-15 retired and not reused; 3-year retention matches memlog (generic rule, no country follow-up); non-goals, UTC deadline, one sheet per week, pay never touched, immutability and adjustments all carried.

## Gaps

1. **Rejection feedback is thinner than CAP-6.** The spec says a rejection "shows the employee what changed", returns the rejected line with a reason, and offers "a one-click fix and resubmit". FR-15 keeps only "comment required, returned to employee". The what-changed view and one-click fix are gone, and it is unclear whether rejection is per project line or whole sheet. This is the main feel-of-the-product loss for the rejected path (brief: "clear reason when they reject").

2. **Submission-status view for the Project 1 owner has no FR of its own.** The brief and PRFAQ both say the owner opens the sheet and sees who has submitted. The PRD has it only as UJ-4 and one consequence line inside FR-15 (view status, cannot approve). Visibility scope (which employees, which states) is undefined, and FR-10 (publish) does not mention it.

3. **Tone and delight qualities have no requirement behind them.** Brief and spec Why: "quick and pleasant", "forgiving", "not used against them", "no shaming", delight as the adoption lever (brainstorm-derived premium-tier note: gamification only opt-in and team level, with backfire risk). The PRD keeps the smiley and the no-public-rankings non-goal, but the "forgiving, never feels like busywork" intent is reduced to SM-2 (one sitting). Nothing states a feel or effort bar for the sheet, the rejection message tone, or the reminder tone. Gamification-stays-opt-in-team-level is not recorded as a constraint, so it could be added later by default.

3b. (Minor, same theme) PRFAQ fairness rules ("employee is not penalised for a sheet the reviewer approved", "never published means never late") are in FR-11 and section 8, but PRFAQ context that HR currently cuts hike percentage and score from late or wrong sheets is absent. SM-C1 hints at it, but the PRD never says why accuracy of the late mark matters.

4. **Dropped spec constraint wording: weekly effort for every employee, "including exempt IT staff".** The glossary term "weekly effort" is kept, but the explicit rule that no one, exempt or not, enters daily hours or a different mode is not in an FR or section 8. FR-2 covers "never per day" only per block.

5. **Spec assumptions not carried or flagged.** (a) "Reopening only by the original employee": present in FR-7 as owner of the sheet, fine. (b) The spec assumption that a late sheet published on a non-Friday still gets next-day 11:59 pm: covered by FR-10 notification line only, no FR consequence. (c) The spec states approvals stay in core (not gated) because competitors charge for them; PRD does not record this positioning, though section 6.2 refers to premium-tier.md. (d) PRD tags CAP-6, CAP-7, CAP-11, CAP-13 as "treated as in v1 scope" but the spec still marks them "proposed, unconfirmed"; the PRD does not raise this as an open question, so the unconfirmed status is silently dropped (spec memlog should record the confirmation).

## Update 2026-10-11: CAP-21

CAP-21 (no one approves their own timesheet; alternate approver) maps to FR-23. CAP-6 and CAP-19 were reconciled with the spec: the reporting manager reads direct reports' data (FR-20) and approves or rejects only as the alternate approver (FR-23); the Project 1 owner still never approves. FR-15, FR-17, UJ-2 and the glossary reference FR-23. No new gap.
