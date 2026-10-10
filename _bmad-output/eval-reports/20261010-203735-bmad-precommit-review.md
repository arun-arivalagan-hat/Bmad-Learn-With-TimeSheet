# Review: bmad-precommit

Target: `.agents/skills/bmad-precommit` (765 tokens, plain skill, description 456 chars). Advice only; nothing applied.

## Lens verdicts
- architecture: pass, no findings
- customization: pass, no findings
- determinism: 1 medium, 1 low
- leanness: 2 medium, 3 low
- trigger: 3 low

## Findings, most severe first

1. **medium, determinism**: Path classification of `git status --porcelain -uall` is done in prose on every run, and again in step 3. It has one right answer per input (renames, quoted paths, exclusion globs). Fix: add `scripts/classify.py` (stdlib, `-z` parsing, JSON out: planning_inputs, bmad_outputs, hat_org_only, all_changed, action) with a unit test; steps 1 and 3 become "run it and read its JSON". Mirror the hook's exclusion list so the two cannot drift.
2. **medium, leanness**: The "spec is derived and must not feed itself" rule appears in three places. Keep one clause beside the row 1 exclusion; drop the never-hand-edit sentence (AGENTS.md holds it).
3. **medium, leanness**: Table and steps 1-2 encode the same branching. Keep the order; delete the "Nothing BMad-related" row and shorten step 2. Keep the HAT_ORG-only and `.claude/skills`/`_bmad` rows (non-inferable wiring).
4. **low, leanness**: End state of the report is not checkable. Close on: nothing staged, and each agent reported as changed files, failure message, or skipped.
5. **low, determinism**: "What each agent changed" is left to recall. Optional: snapshot `git status` before and after each agent and diff.
6. **low, leanness**: "Stage nothing, commit nothing" repeats the description and the briefing. Keep it once, in the agent briefing.
7. **low, leanness**: Closing paragraph on failed agents repeats step 5. Fold into step 4 as one clause.
8. **low, trigger**: Eval has no near misses for running one agent only, or HAT_ORG alone. Needs an owner decision on whether those should fire.
9. **low, trigger**: "Use when" has two near-duplicate phrases. Collapse and add a context (planning inputs edited, spec and HAT_ORG to be refreshed before committing). Confirm with the trigger eval first.
10. **low, trigger**: Description repeats procedure the body owns. Optional shortening; keep the agent names as anchors.

## Notes
- Leanness' smaller version is a hypothesis, saving about 150-200 tokens. Measure with a variant eval before cutting.
- Validate: init check and path scan clean. Judgment finding: the name carries `bmad-` outside BMAD-METHOD (collision risk with a future core skill; `hat-precommit` avoids it).
- Packaging: not applied; kept as a plain skill.
