<!-- bmad:context -->
<!-- Verified 2026-10-10 against 4973556. Managed by bmad-project-context; edits inside this block are replaced on refresh. Keep anything you want preserved outside the markers. -->

## TimeSheet_OneHrms

Weekly timesheet module for an HRMS. Planning only so far, no application code yet. Owner's intended stack, not yet recorded in an architecture document: React with TypeScript, NestJS, PostgreSQL, AWS. Planning lives in `_bmad-output/initiative-timesheet-management/`.

## Policy

- Never hand-edit `spec-timesheet-management.md` or `glossary.md`. They are derived from `.memlog.md`; log the change with `uv run _bmad/scripts/memlog.py append --workspace <spec folder> --type <type> --text "..."` first, then re-derive.
- Never reuse or renumber a capability ID. CAP-15 is retired; payroll, loss-of-pay days and the payroll cut-off stay out of scope.
- Owner decisions in the spec memlog and in any "Owner decisions" section outrank research findings. Record a conflict as an open question; never reverse the decision.
- Keep stack, hosting, observability, backups, CI/CD and email vendor out of the spec. They belong to the architecture step.
- Never commit, push or stage; the pre-commit hook stages only the spec folder and `HAT_ORG/`.

## Where things are

- Spec and its companions: `_bmad-output/initiative-timesheet-management/spec-timesheet-management/`. Research, brainstorm, brief and PRFAQ folders sit beside it.
- Active initiative: `_bmad/custom/config.user.toml`.
- Step docs for the team: `HAT_ORG/`, indexed in `HAT_ORG/Guide/00-index.md`; one doc per research type, grouped in `Analyst/`, `BmadMethod/` and `CoreTools/`. Problems shared by several steps live in `HAT_ORG/Guide/troubleshooting.md`.
- Commit-time automation: `.git/hooks/pre-commit`, which is not tracked and is per clone. It runs `bmad-spec-sync` then `bmad-docs-updater` (`.claude/agents/`) and takes about a minute.

## Running and verifying

- TODO: no build, test or run commands exist yet. Add them after the first story is built, and verify them against the code.

## Known pitfalls

- In zsh, never store a command in a variable and expand it (`M="uv run ..."; $M ...`); it fails with "no such file or directory". Use a function or write the command out.
- `git add` stages unrelated work too; before committing, check `git status` and commit only the paths you mean to.
<!-- /bmad:context -->
