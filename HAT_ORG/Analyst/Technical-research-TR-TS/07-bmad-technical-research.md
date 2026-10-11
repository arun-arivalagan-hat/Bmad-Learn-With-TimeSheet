# BMAD Technical Research Guide

**BMad agent:** Mary (Business Analyst), menu option TR | **Skill:** `bmad-deep-recon` (technical type), then `bmad-spec`

## 1. Purpose

This guide explains how to run technical research (Mary's **TR** option) with `bmad-deep-recon`. It surveys how a feature is built in practice: integration patterns, architecture patterns, and implementation options. For this repository the topic is the technical approach for a timesheet module inside an HRMS, and the decision is which integration, approval and audit, and notification approaches to use. It produces a cited report with options and trade-offs. It does not pick a stack (that is the architecture step) and it does not edit the spec.

## 2. Prerequisites

* Steps 1 to 3 complete: installation, an active initiative and a spec ([03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)).
* Steps 5 and 6 helpful: the market and domain research set the scope ([05-bmad-market-research.md](../Market-Research-MR/05-bmad-market-research.md), [06-bmad-domain-research.md](../Domain-Research-DR/06-bmad-domain-research.md)).
* A topic, the decision it serves, and any known constraints (here: the existing HRMS stack was unknown, so options are general).

## 3. Run the Skill

Ask Mary for **TR**, or invoke `bmad-deep-recon` with the technical type:

```text
Use bmad-deep-recon for technical research: technical approach for a timesheet module inside an HRMS, to decide integration, approval and audit, and notification patterns
```

The skill proposes a plan (dimensions, number of assistants, depth, freshness and two-source rules), waits for approval, runs parallel web searches, writes a digest per assistant, and assembles the report. In this run the dimensions were integration, architecture patterns, and implementation reality, with one assistant each.

A second TR run, a stack fit check, used the select mode to confirm or challenge the owner's chosen stack (React with TypeScript, NestJS, PostgreSQL, a status column plus audit table, SendGrid, AWS) against alternatives, with three assistants and a two-source rule. It shares this doc because it is the same research type. It feeds `bmad-architecture` and left the spec unchanged.

Then re-run `bmad-spec` so the module-relevant findings merge into the spec. Findings about infrastructure (stack, hosting, observability, backups, CI/CD) were declared out of scope for the spec and belong to `bmad-architecture`.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/research-timesheet-module-technical-approach-insi/research-timesheet-module-technical-approach-insi.md` | The report: executive summary, options per dimension, recommendations for the architecture step, numbered sources and a staleness map. |
| `_bmad-output/initiative-timesheet-management/research-timesheet-module-technical-approach-insi/digests/` | One digest per assistant: `integration-r1-1.md`, `patterns-r1-1.md`, `stack-deployment-r1-1.md`. |
| `_bmad-output/initiative-timesheet-management/research-timesheet-module-technical-approach-insi/.memlog.md` | Decisions and claims, each with a verification status. |

Stack fit check files, under `_bmad-output/initiative-timesheet-management/research-stack-fit-check-react-nestjs-postgresql/`: the report `research-stack-fit-check-react-nestjs-postgresql.md` (verdict per pick: five hold, SendGrid challenged), `digests/` (`backend-db-r1-1.md`, `cloud-r1-1.md`, `workflow-email-r1-1.md`, `backend-cloud-r2-1.md`, `email-workflow-r2-1.md`) and `.memlog.md`. Evidence gaps: React barely researched, no official AWS cost figures, no team retrospectives.

What reached the spec: a reminder constraint (UTC, at most once per employee, reminder kind and week) and a Teams note in `premium-tier.md`. The report also records the owner decisions that infrastructure and the payroll handoff are out of scope.

## 5. Verify

* The report frontmatter shows `status: complete` and the decision it serves.
* Version and compatibility claims carry a re-check date in the staleness map (about one month), so re-check them before building.
* Gaps are listed (email provider limits, observability, backups, CI/CD, hiring data), not hidden.
* The spec lists the report under `sources:`.

## 6. Troubleshooting

* **The report names no winner:** that is intended. It gives options with trade-offs; decide in `bmad-architecture`.
* **Weak claims, or the spec did not change:** See [troubleshooting.md](../../Guide/troubleshooting.md).

## Skill Folder Structure

Layout of the installed `bmad-deep-recon` skill (`.claude/skills/bmad-deep-recon/`), which mirrors its [upstream folder](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-deep-recon):

* `SKILL.md`: the entry point. Frontmatter (name, description) tells the harness when to trigger; the body holds the instructions.
* `bmod.toml`: module metadata, which module the skill belongs to and where it is sourced from on GitHub.
* `customize.toml`: the override surface; team and personal overrides live in `_bmad/custom/`, never in this file.
* `references/`: one file per intent (`draft`, `process`, `run`, `lifecycle`) plus `verification`, `synthesis`, `selection` and `finalize`; loaded only when that step is reached.
* `types/`: one research pack per type (`market`, `domain`, `technical`, `competitive`, `user-voice`, `academic-lit`).
* `assets/`: `research.template.md`, the report skeleton.
* `scripts/`: `recon_kit.py`, helper for run folders and claim logs.


## Skill Steps

Steps the skill itself runs, in order (from its `SKILL.md`):

`bmad-deep-recon` picks the research type from the ask (here: technical) and routes on the intent:

1. **Draft:** compose a deep-research prompt for your own tool.
2. **Process:** file a finished report, extract its claims and distill the downstream summary.
3. **Run:** native research. Resolve effort, hold the plan gate (the one hard stop), run the search loop, then verify and synthesize.
4. **Refresh / Deepen:** update or extend an existing run folder.

Every intent ends by finalizing the run folder (`brief.md`, `imports/`, `digests/`, report, `.memlog.md`). Then `bmad-spec` folds the findings into the spec (see [03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)).

## Official References

* [Technical Research](https://docs.bmad-method.org/plan/research-a-decision/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad-deep-recon` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-deep-recon)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
