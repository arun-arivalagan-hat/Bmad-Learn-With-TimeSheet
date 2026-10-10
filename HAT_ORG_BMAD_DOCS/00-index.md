# BMAD Adoption Index

Entry point for the BMAD adoption docs in this repository.

## Steps

| # | Step | BMad agent (owner of the skill) | Skill used | Status | Doc |
|---|------|------|------------|--------|-----|
| 1 | Installation and setup | BMad Agent | `bmad` (installer) | Complete | [01-bmad-installation-and-setup.md](01-bmad-installation-and-setup.md) |
| 2 | Initiative | BMad Agent | `bmad` | Complete | [02-bmad-initiative.md](02-bmad-initiative.md) |
| 3 | Spec | Skill run directly | `bmad-spec` | Complete | [03-bmad-spec.md](03-bmad-spec.md) |
| 4 | Brainstorm (feeds a spec update) | Mary (Business Analyst); `bmad-spec` run directly | `bmad-brainstorming`, `bmad-spec` | Complete | [04-bmad-brainstorm.md](04-bmad-brainstorm.md) |
| 5 | Research, three runs: engagement, domain, India labour/payroll (feeds spec updates) | Mary (Business Analyst); `bmad-spec` run directly | `bmad-deep-recon`, `bmad-spec` | Complete | [05-bmad-market-research.md](05-bmad-market-research.md) |
| 6 | Ticket plan (epics and stories) | John (Product Manager), Winston (System Architect), Amelia (Senior Software Engineer) | `bmad-ticket` | Next | Not written yet |
| 7 | Build | Amelia (Senior Software Engineer) | `bmad-build` | Not started | Not written yet |

## Generated files

| Skill | File or folder | Commit | Used for in the next step |
|-------|----------------|--------|---------------------------|
| BMAD installer | `.claude/skills/bmad*` and `.agents/skills/bmad*` | b042e23 | Provide the skills invoked in every later step. |
| (Claude Code agent) | `.claude/agents/bmad-docs-updater.md` | b042e23 | Keeps these docs current after each commit. |
| `bmad` | `_bmad-output/initiative-timesheet-management/initiative-timesheet-management.md` | b042e23 | Sets the folder where `bmad-spec` and `bmad-ticket` read and write. |
| `bmad-spec` | `_bmad-output/initiative-timesheet-management/spec-timesheet-management/spec-timesheet-management.md` | b042e23, a3b7b1d, 78fc2c0 (updated: pending) | The contract `bmad-ticket` plans stories from and `bmad-build` reads; now CAP-1 to CAP-15 (adds payroll handoff of LOP and payable days). |
| `bmad-spec` | `_bmad-output/initiative-timesheet-management/spec-timesheet-management/.memlog.md` | b042e23, a3b7b1d, 78fc2c0 (updated: pending) | Running log the spec is re-derived from; holds open questions to resolve before ticket planning. |
| `bmad-brainstorming` | `_bmad-output/initiative-timesheet-management/brainstorm-timesheet-delight/brainstorm-timesheet-delight.md` | a3b7b1d | Intent document; source of CAP-8 to CAP-13 and the spec's added constraints. |
| `bmad-brainstorming` | `_bmad-output/initiative-timesheet-management/brainstorm-timesheet-delight/brainstorm.html` | a3b7b1d | Shareable view of the brainstorm for review. |
| `bmad-brainstorming` | `_bmad-output/initiative-timesheet-management/brainstorm-timesheet-delight/.memlog.md` | a3b7b1d | Idea log the intent document is derived from. |
| `bmad-spec` | `_bmad-output/initiative-timesheet-management/spec-timesheet-management/premium-tier.md` | a3b7b1d, 78fc2c0 | Spec companion; premium candidates, not committed scope, for later sequencing. |
| `bmad-deep-recon` | `_bmad-output/initiative-timesheet-management/research-employee-engagement-in-timesheet-filling/research-employee-engagement-in-timesheet-filling.md` | 78fc2c0 | Evidence for free vs premium tiering and reminders; source of CAP-14 and new spec assumptions. |
| `bmad-deep-recon` | `_bmad-output/initiative-timesheet-management/research-employee-engagement-in-timesheet-filling/digests/` | 78fc2c0 | Per-dimension evidence behind the research report. |
| `bmad-deep-recon` | `_bmad-output/initiative-timesheet-management/research-employee-engagement-in-timesheet-filling/.memlog.md` | 78fc2c0 | Claim log with verification status; check before trusting prices. |
| `bmad-spec` | `_bmad-output/initiative-timesheet-management/spec-timesheet-management/glossary.md` | pending | Spec companion; domain terms and timesheet states (draft, submitted, rejected, approved) for ticket planning. |
| `bmad-deep-recon` | `_bmad-output/initiative-timesheet-management/research-timesheet-and-time-billing-domain-in-it/` (report, `digests/`, `.memlog.md`) | pending | Domain evidence behind the glossary, states and retention constraints; vendor-sourced, US-default. |
| `bmad-deep-recon` | `_bmad-output/initiative-timesheet-management/research-india-labour-rules-and-payroll-inputs-fo/` (report, `digests/`, `.memlog.md`) | pending | India labour and payroll evidence behind CAP-15 (LOP days, payable days, cut-off); retention figure is single-source, owner confirms. |
| (Claude Code agent) | `HAT_ORG_BMAD_DOCS/` (`00-index.md`, `01`–`03` step docs) | b042e23 | Adoption guide for the team; the index tracks step status. |
| (Claude Code agent) | `HAT_ORG_BMAD_DOCS/04-bmad-brainstorm.md` | a3b7b1d | Guide for the brainstorm step. |
| (Claude Code agent) | `HAT_ORG_BMAD_DOCS/05-bmad-market-research.md` | 78fc2c0 (updated: pending) | Guide for the research step. |
