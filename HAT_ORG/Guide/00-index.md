# BMAD Adoption Index

Entry point for the BMAD adoption docs in this repository. Problems shared by several steps are in [troubleshooting.md](troubleshooting.md).

Status values: Not started, Next, In progress, Draft (written, awaiting owner review), Complete.

## Steps

| # | Step | BMad agent (owner of the skill) | Skill used | Status | Doc |
|---|------|------|------------|--------|-----|
| 1 | Installation and setup | BMad Agent | `bmad` (installer) | Complete | [01-bmad-installation-and-setup.md](../CoreTools/Bmad/Bmad-Setup/01-bmad-installation-and-setup.md) |
| 2 | Initiative | BMad Agent | `bmad` | Complete | [02-bmad-initiative.md](../CoreTools/Bmad/Bmad-Initiative/02-bmad-initiative.md) |
| 3 | Spec | Skill run directly | `bmad-spec` | Complete | [03-bmad-spec.md](../BmadMethod/Bmad-spec/03-bmad-spec.md) |
| 4 | Brainstorm (feeds a spec update) | Mary (Business Analyst); `bmad-spec` run directly | `bmad-brainstorming`, `bmad-spec` | Complete | [04-bmad-brainstorm.md](../Analyst/Brainstorm-BR/04-bmad-brainstorm.md) |
| 5 | Market research (MR): employee engagement | Mary (Business Analyst); `bmad-spec` run directly | `bmad-deep-recon`, `bmad-spec` | Complete | [05-bmad-market-research.md](../Analyst/Market-Research-MR/05-bmad-market-research.md) |
| 6 | Domain research (DR): timesheet domain, India labour and payroll | Mary (Business Analyst); `bmad-spec` run directly | `bmad-deep-recon`, `bmad-spec` | Complete | [06-bmad-domain-research.md](../Analyst/Domain-Research-DR/06-bmad-domain-research.md) |
| 7 | Technical research (TR): technical approach, plus stack fit check | Mary (Business Analyst); `bmad-spec` run directly | `bmad-deep-recon`, `bmad-spec` | Complete | [07-bmad-technical-research.md](../Analyst/Technical-research-TR-TS/07-bmad-technical-research.md) |
| 8 | Competitive research (CR): BambooHR, Rippling and Keka | Mary (Business Analyst); `bmad-spec` run directly | `bmad-deep-recon`, `bmad-spec` | Complete | [08-bmad-competitive-research.md](../Analyst/Competitive-research-CR/08-bmad-competitive-research.md) |
| 9 | Product brief: for non-technical readers (awaiting owner review) | Mary (Business Analyst) | `bmad-product-brief` | Draft | [09-bmad-product-brief.md](../Analyst/Product-Brief-PB/09-bmad-product-brief.md) |
| 10 | PRFAQ: concept test (ignition stage, press release not written) | Mary (Business Analyst) | `bmad-prfaq` | In progress | [10-bmad-prfaq.md](../Analyst/Working-Backwards-PRFAQ-WB/10-bmad-prfaq.md) |
| 11 | Project context (PC): `AGENTS.md` and `CLAUDE.md` agent instructions | Mary (Business Analyst) | `bmad-project-context` | Complete | [11-bmad-project-context.md](../Analyst/Project-context-PC/11-bmad-project-context.md) |
| 12 | Architecture (records the stack and hosting decisions the spec leaves out) | Winston (System Architect) | `bmad-architecture` | Next | Not written yet |
| 13 | Ticket plan (epics and stories) | John (Product Manager), Winston (System Architect), Amelia (Senior Software Engineer) | `bmad-ticket` | Not started | Not written yet |
| 14 | Build | Amelia (Senior Software Engineer) | `bmad-build` | Not started | Not written yet |

## Generated files

| Skill | File or folder | Commit | Used for in the next step |
|-------|----------------|--------|---------------------------|
| BMAD installer | `.claude/skills/bmad*` and `.agents/skills/bmad*` | b042e23 | Provide the skills invoked in every later step. |
| (Claude Code agent) | `.claude/agents/bmad-docs-updater.md` | b042e23, 78fc2c0, e448b7f, 191ebe6 (updated: pending) | Keeps these docs current after each commit. |
| `bmad` | `_bmad-output/initiative-timesheet-management/initiative-timesheet-management.md` | b042e23 | Sets the folder where `bmad-spec` and `bmad-ticket` read and write. |
| `bmad-spec` | `_bmad-output/initiative-timesheet-management/spec-timesheet-management/spec-timesheet-management.md` | b042e23, a3b7b1d, 78fc2c0, 3441043 (updated: 4973556) | The contract `bmad-ticket` plans stories from and `bmad-build` reads; HR constraints CAP-17 and CAP-18 added (HR decides consequences of late timesheets); CAP-15 (payroll handoff) is retired and out of scope, CAP-16 adds weekly sheet publication by the Project 1 owner, and CAP-14 now carries the 11:59 pm UTC deadline and late mark. |
| `bmad-spec` | `_bmad-output/initiative-timesheet-management/spec-timesheet-management/.memlog.md` | b042e23, a3b7b1d, 78fc2c0, 3441043, e448b7f, 7a16381 | Running log the spec is re-derived from; the 7a16381 update records the owner decisions and a review of the stack fit check, which needed no spec change. |
| `bmad-brainstorming` | `_bmad-output/initiative-timesheet-management/brainstorm-timesheet-delight/brainstorm-timesheet-delight.md` | a3b7b1d (updated: 4973556) | Intent document; source of CAP-8 to CAP-13 and the spec's added constraints; now also records the owner decisions of 2026-10-10. |
| `bmad-brainstorming` | `_bmad-output/initiative-timesheet-management/brainstorm-timesheet-delight/brainstorm.html` | a3b7b1d | Shareable view of the brainstorm for review. |
| `bmad-brainstorming` | `_bmad-output/initiative-timesheet-management/brainstorm-timesheet-delight/.memlog.md` | a3b7b1d | Idea log the intent document is derived from. |
| `bmad-spec` | `_bmad-output/initiative-timesheet-management/spec-timesheet-management/premium-tier.md` | a3b7b1d, 78fc2c0 | Spec companion; premium candidates, not committed scope, for later sequencing. |
| `bmad-deep-recon` | `_bmad-output/initiative-timesheet-management/research-employee-engagement-in-timesheet-filling/research-employee-engagement-in-timesheet-filling.md` | 78fc2c0 (updated: 4973556) | Evidence for free vs premium tiering and reminders; source of CAP-14 and new spec assumptions. |
| `bmad-deep-recon` | `_bmad-output/initiative-timesheet-management/research-employee-engagement-in-timesheet-filling/digests/` | 78fc2c0 | Per-dimension evidence behind the research report. |
| `bmad-deep-recon` | `_bmad-output/initiative-timesheet-management/research-employee-engagement-in-timesheet-filling/.memlog.md` | 78fc2c0 | Claim log with verification status; check before trusting prices. |
| `bmad-spec` | `_bmad-output/initiative-timesheet-management/spec-timesheet-management/glossary.md` | 3441043 (updated: 4973556) | Spec companion; domain terms and timesheet states (draft, submitted, rejected, approved) for ticket planning. |
| `bmad-deep-recon` | `_bmad-output/initiative-timesheet-management/research-timesheet-and-time-billing-domain-in-it/` (report, `digests/`, `.memlog.md`) | 3441043 (updated: 4973556) | Domain evidence behind the glossary, states and retention constraints; vendor-sourced, US-default. |
| `bmad-deep-recon` | `_bmad-output/initiative-timesheet-management/research-india-labour-rules-and-payroll-inputs-fo/` (report, `digests/`, `.memlog.md`) | 3441043 | India labour and payroll evidence; CAP-15, which it informed, is now retired, so treat it as background. Retention figure is single-source. |
| `bmad-deep-recon` | `_bmad-output/initiative-timesheet-management/research-bamboohr-rippling-keka-timesheet-teardow/` (report, `digests/`, `.memlog.md`) | e448b7f | Competitive evidence on which timesheet engagement features BambooHR, Rippling and Keka include and at which tier; input to spec and `premium-tier.md`. |
| `bmad-deep-recon` | `_bmad-output/initiative-timesheet-management/research-timesheet-module-technical-approach-insi/` (report, `digests/`, `.memlog.md`) | e448b7f | Technical evidence (integration, approval and audit, notification patterns, stack and deployment options) for the architecture step; the spec leaves stack choice to it. |
| `bmad-deep-recon` | `_bmad-output/initiative-timesheet-management/research-stack-fit-check-react-nestjs-postgresql/` (report, `digests/`, `.memlog.md`) | 7a16381 | Technical (select) fit check of the owner's stack (React TypeScript, NestJS, PostgreSQL, status column plus audit table, SendGrid, AWS) against alternatives; challenges SendGrid. Input to `bmad-architecture`; the spec is unchanged. Evidence is thin on React, AWS cost and team retrospectives. |
| (Claude Code agent) | `.claude/agents/bmad-spec-sync.md` | 7a16381 | Keeps the spec in sync with changed research and brainstorm files before each commit; leaves infrastructure and stack findings to `bmad-architecture`. |
| `bmad-product-brief` | `_bmad-output/initiative-timesheet-management/brief-timesheet-management/brief-timesheet-management.md` | 8b31b6b (updated: 4973556) | Plain-language summary of problem, scope and success criteria for non-developer readers; draft awaiting owner review. Now says HR sees late marks and decides consequences. Input to `bmad-ticket` and `bmad-architecture` alongside the spec. |
| `bmad-product-brief` | `_bmad-output/initiative-timesheet-management/brief-timesheet-management/.memlog.md` | 8b31b6b (updated: 4973556) | Decision and assumption log the brief is updated against. |
| `bmad-prfaq` | `_bmad-output/initiative-timesheet-management/prfaq-timesheet-management/prfaq-timesheet-management.md` | 4973556 | Concept test at ignition stage: customer (project manager), the owner's pain numbers (unverified) and decision A (HR decides consequences of late timesheets). Press release, FAQs and verdict still to come; address its gaps before `bmad-ticket`. |
| (Claude Code agent) | `HAT_ORG/` (this index, `troubleshooting.md` and one step doc per skill or research type, in `Analyst/`, `BmadMethod/` and `CoreTools/`) | b042e23, a3b7b1d, 78fc2c0, e448b7f, 7a16381, 8b31b6b, 4973556, 191ebe6 (moved from `HAT_ORG_BMAD_DOCS/`: pending) | Adoption guide for the team; the index tracks step status. Each step doc lists the files its step generated. |
| `bmad-project-context` | `AGENTS.md` | 191ebe6 (updated: pending) | The rules every coding agent loads at session start; now points to `HAT_ORG/`; refresh after architecture and after the first code. |
| `bmad-project-context` | `CLAUDE.md` | 191ebe6 | One line, `@AGENTS.md`, so Claude Code loads the same rules. |
