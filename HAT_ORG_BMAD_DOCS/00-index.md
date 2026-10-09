# BMAD Adoption Index

Entry point for the BMAD adoption docs in this repository.

## Steps

| # | Step | Skill used | Status | Doc |
|---|------|------------|--------|-----|
| 1 | Installation and setup | `bmad` (installer) | Complete | [01-bmad-installation-and-setup.md](01-bmad-installation-and-setup.md) |
| 2 | Initiative | `bmad` | Complete | [02-bmad-initiative.md](02-bmad-initiative.md) |
| 3 | Spec | `bmad-spec` | Complete | [03-bmad-spec.md](03-bmad-spec.md) |
| 4 | Ticket plan (epics and stories) | `bmad-ticket` | Next | Not written yet |
| 5 | Build | `bmad-build` | Not started | Not written yet |

## Generated files

| Skill | File or folder | Commit | Used for in the next step |
|-------|----------------|--------|---------------------------|
| BMAD installer | `.claude/skills/bmad*` and `.agents/skills/bmad*` | pending | Provide the skills invoked in every later step. |
| (Claude Code agent) | `.claude/agents/bmad-docs-updater.md` | pending | Keeps these docs current after each commit. |
| `bmad` | `_bmad-output/initiative-timesheet-management/initiative-timesheet-management.md` | pending | Sets the folder where `bmad-spec` and `bmad-ticket` read and write. |
| `bmad-spec` | `_bmad-output/initiative-timesheet-management/spec-timesheet-management/spec-timesheet-management.md` | pending | The contract `bmad-ticket` plans stories from and `bmad-build` reads. |
| `bmad-spec` | `_bmad-output/initiative-timesheet-management/spec-timesheet-management/.memlog.md` | pending | Running log the spec is re-derived from; holds open questions to resolve before ticket planning. |
| (Claude Code agent) | `HAT_ORG_BMAD_DOCS/` (`00-index.md`, `01`–`03` step docs) | pending | Adoption guide for the team; the index tracks step status. |
