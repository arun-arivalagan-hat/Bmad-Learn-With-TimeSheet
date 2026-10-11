# BMAD Spec Guide

**BMad agent:** Skill run directly | **Skill:** `bmad-spec`

## 1. Purpose

This guide explains how to use `bmad-spec`, the hub skill that distills any input (a form, notes, an objective) into the **spec**: the contract that later planning and build steps read. It does not slice work into stories; that is `bmad-ticket`.

## 2. Prerequisites

* Step 2 complete: an active initiative exists ([02-bmad-initiative.md](../../CoreTools/Bmad/Bmad-Initiative/02-bmad-initiative.md)).
* Source input: for this repository, the HAT timesheet form plus the objective "capture actual work effort and link it to billing/utilization".

## 3. Run the Skill

Invoke `bmad-spec` and supply the input, for example:

```text
Use bmad-spec to create a spec for Timesheet Management from this form and objective: ...
```

The skill appends findings to a running log (`.memlog.md`) and re-derives the spec from it, so you can re-run it later with new material (PRD, UX, architecture, prototype notes) and the spec is updated rather than hand-merged.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/spec-timesheet-management/spec-timesheet-management.md` | The spec: Why, Capabilities (see the spec for the current CAP list), Constraints, Non-goals, Success signal, Assumptions. |
| `_bmad-output/initiative-timesheet-management/spec-timesheet-management/.memlog.md` | Running log of decisions, capabilities, constraints, assumptions and open questions the spec is derived from. |
| `_bmad-output/initiative-timesheet-management/spec-timesheet-management/premium-tier.md` | Companion added after the brainstorm ([04-bmad-brainstorm.md](../../Analyst/Brainstorm-BR/04-bmad-brainstorm.md)): premium tier candidates, not committed scope. |
| `_bmad-output/initiative-timesheet-management/spec-timesheet-management/glossary.md` | Companion added after the domain research ([06-bmad-domain-research.md](../../Analyst/Domain-Research-DR/06-bmad-domain-research.md)): domain terms and timesheet states. |
| `_bmad-output/initiative-timesheet-management/prd-timesheet-management/prd-timesheet-management.md` | The PRD, listed in the spec's `companions`: its journeys, metrics and FR detail stay reachable for UX, architecture and tickets. Written by `bmad-prd`, not by this skill. |

After the brainstorm re-run the spec has CAP-1 to CAP-13 (CAP-8 to CAP-13 added), and the billable-flag and identity-source questions below are answered as constraints. The research re-runs then added CAP-14 (reminders) and CAP-15 (payroll handoff). The owner later retired CAP-15 and put the payroll handoff out of scope; its ID is never reused. Later updates added CAP-16 and above (the PRD run added CAP-19, reporting manager read-only view, and CAP-20, Project 1 owner status view); the spec holds the current list.

The spec was then validated (critique) and five findings applied: late-mark visibility stated once, consistent 'employee' and 'project reviewers' wording, CAP-6 and CAP-16 without HOW wording, and the PRD moved from sources to companions (see [12-bmad-prd.md](../../ProductOwner/Product-Requirements-PRD/12-bmad-prd.md)). The owner then closed the legal question (3-year retention accepted, no legal review), so the spec's Open Questions section was removed.

## 5. Review the Spec

* Each capability has an **intent** and a **success** condition.
* Capabilities marked `proposed, unconfirmed` need your confirmation or removal. CAP-6, CAP-7, CAP-11 and CAP-13 were confirmed for v1 during the PRD run (2026-10-11).
* Read **Assumptions** (for example: only Project 1 required, 0.5-hour steps, 40-hour weekly cap) and correct any that are wrong.
* The spec now has no Open Questions section: none remain (the legal question was closed by the owner, 2026-10-11). Log any new question in `.memlog.md` and re-derive through `bmad-spec`.

## 6. Troubleshooting

* **Spec is too thin:** `bmad-spec` distills and does not coach. For vague input use `bmad-product-brief` or `bmad-prd` first, then feed the result to `bmad-spec`.
* **Memlog fails to parse:** Frontmatter values containing a colon must be quoted.
* **Requirements changed later, or another document needs to reach the spec:** See [troubleshooting.md](../../Guide/troubleshooting.md).

## Skill Folder Structure

Layout of the installed `bmad-spec` skill (`.claude/skills/bmad-spec/`), which mirrors its [upstream folder](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-spec):

* `SKILL.md`: the entry point. Frontmatter (name, description) tells the harness when to trigger; the body holds the instructions.
* `bmod.toml`: module metadata, which module the skill belongs to and where it is sourced from on GitHub.
* `customize.toml`: the override surface; team and personal overrides live in `_bmad/custom/`, never in this file.
* `assets/`: `spec-template.md` (the kernel skeleton) and `headless-schemas.md` (output shapes for headless runs).
* No `references/` or `scripts/`: the whole operation lives in `SKILL.md`; the memlog script comes from the shared `_bmad/scripts/`.


## Skill Steps

Steps the skill itself runs, in order (from its `SKILL.md`):

1. **Read the input** and its linked materials; if a `.memlog.md` exists, the run becomes an update and the memlog is the authority on decisions and capability IDs.
2. **Sort the content:** trust pre-sorted input (brief, PRD); sort mixed input yourself into the kernel and companions.
3. **Distill** into the five-field kernel, either express (every gap becomes an open question) or guided (walk the fields with you).
4. **Log** each decision, capability and constraint to `.memlog.md` as it is made.
5. **Self-validate** against the Spec Law (intent and success per capability, stable IDs, explicit non-goals).
6. **Output** `spec-<slug>.md` and companions; optionally hand off to `bmad-ticket`.

## Official References

* [Spec](https://docs.bmad-method.org/plan/define-requirements-and-a-specification/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad-spec` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-spec)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
