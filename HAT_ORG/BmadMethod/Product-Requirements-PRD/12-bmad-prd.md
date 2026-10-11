# BMAD PRD Guide

**BMad agent:** John (Product Manager) | **Skill:** `bmad-prd`

## 1. Purpose

This guide explains how to write a product requirements document (PRD) with `bmad-prd`. The skill coaches detailed requirements out of the owner, sized to the stakes, and can also update or validate an existing PRD. In this repository it follows the analyst steps (brainstorm, research, brief, PRFAQ) and feeds `bmad-spec`, `bmad-ux`, `bmad-architecture` and `bmad-ticket`. The PRD does not replace the spec; the spec stays the contract that builds read.

## 2. Prerequisites

* Steps 1 and 2 complete: installation and an active initiative ([02-bmad-initiative.md](../../CoreTools/Bmad/Bmad-Initiative/02-bmad-initiative.md)).
* Steps 3 to 11 recommended: the spec, research, brief, PRFAQ and project context are the inputs. In this run the owner confirmed the analyst phase was complete.
* The stakes of the work (here: internal tool) and the working mode (here: Fast path).

## 3. Run the Skill

Ask John for the PRD, or invoke the skill:

```text
Use bmad-prd to write a PRD for Timesheet Management from the spec, brief, PRFAQ, brainstorm and research
```

The skill detects whether to create, update or validate, and offers to resume an in-progress PRD before starting a new one. Re-run it in update mode when requirements change, or in validate mode for a critique.

After the run, use `bmad-spec` with the PRD as input so the spec absorbs it. Do not edit the spec by hand; see [troubleshooting.md](../../Guide/troubleshooting.md).

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/prd-timesheet-management/.memlog.md` | Decision log for the run (stakes, working mode, inputs). Present so far. |
| `_bmad-output/initiative-timesheet-management/prd-timesheet-management/prd-timesheet-management.md` | The PRD itself. Not present yet at the time of writing; it appears when the draft is written. |

## 5. Verify

* The PRD file exists and its frontmatter `status` is `final` only after the owner has reviewed it.
* Every `[ASSUMPTION]`, open question and `[NOTE FOR PM]` is resolved or logged in the memlog.
* Owner decisions in the spec memlog are kept: payroll, loss-of-pay and the payroll cut-off stay out of scope, and CAP-15 stays retired.
* No stack, hosting, observability, backup, CI/CD or email vendor choice appears; those belong to `bmad-architecture`.

## 6. Troubleshooting

* **BMad not set up, no active initiative, or the spec not updated after the PRD:** See [troubleshooting.md](../../Guide/troubleshooting.md).
* **A PRD run is stuck at draft:** finalizing sets `status: final` only after the memlog audit, input reconciliation and reviewer pass; resume the run instead of starting a new one.

## Skill Folder Structure

Layout of the installed `bmad-prd` skill (`.claude/skills/bmad-prd/`), which mirrors its [upstream folder](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-prd):

* `SKILL.md`: the entry point. Frontmatter (name, description) tells the harness when to trigger; the body holds the instructions.
* `bmod.toml`: module metadata, which module the skill belongs to and where it is sourced from on GitHub.
* `customize.toml`: the override surface; team and personal overrides live in `_bmad/custom/`, never in this file.
* `references/`: `validate.md` (validation run) and `headless.md` (unattended runs).
* `assets/`: `prd-template.md`, `prd-validation-checklist.md`, `headless-schemas.md` and `validation-report-template.html`.
* No `scripts/`: the PRD flow is in `SKILL.md`.


## Skill Steps

Steps the skill itself runs, in order (from its `SKILL.md`):

1. **Detect intent:** Create, Update or Validate; offer to resume an in-progress run.
2. **Discovery:** gather inputs, set stakes and working mode (Fast path or coaching), research where needed.
3. **Draft** in a persistent workspace with `.memlog.md`, under the PRD discipline and a reviewer gate.
4. **Finalize:** memlog audit, input reconciliation, reviewer pass, triage of open items, polish, external handoffs, then set `status: final`.

## Official References

* [PRD](https://docs.bmad-method.org/plan/define-requirements-and-a-specification/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad-prd` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-prd)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
