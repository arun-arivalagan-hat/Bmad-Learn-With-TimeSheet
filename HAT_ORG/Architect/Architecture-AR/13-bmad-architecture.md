# BMAD Architecture Guide

**SDLC role:** Architect | **Team lead:** Not assigned yet | **BMad agent:** Winston (System Architect) | **Skill:** `bmad-architecture`

## 1. Purpose

This guide explains how to record architecture decisions with `bmad-architecture`. The skill produces an architecture spine: a short contract that fixes only the decisions that keep separately built parts consistent (design paradigm, boundaries, how state changes, who owns shared data). In this repository it is where the stack, hosting and similar choices that the spec and PRD leave out are recorded.

## 2. Prerequisites

* Steps 1 and 2 complete: installation and an active initiative ([02-bmad-initiative.md](../../CoreTools/Bmad/Bmad-Initiative/02-bmad-initiative.md)).
* The spec ([03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)) and the PRD ([12-bmad-prd.md](../../ProductOwner/Product-Requirements-PRD/12-bmad-prd.md)) as inputs. The technical research (step 7) holds the stack fit check of the owner's intended stack.

## 3. Run the Skill

Ask Winston for the architecture, or run:

```text
/bmad-architecture
```

The skill offers a Coaching path (default) or a Fast path before it drafts, and asks whether the spine is the only deliverable. It can create, update or validate a spine, and resumes a run from its memlog.

In this run: Coaching path, audience is the development team, altitude is the whole initiative. Afterwards run `/bmad-precommit` so this doc and the index are refreshed.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/architecture-timesheet-management/.memlog.md` | Run log. So far: the owner-adopted paradigm (modular monolith, one deployable; the sheet is the single consistency boundary; PostgreSQL status column plus append-only audit log; every state change goes through one domain method that writes the audit row in the same transaction), constraints inherited from the spec, the team constraint, and one open question (team headcount). |
| `_bmad-output/initiative-timesheet-management/architecture-timesheet-management/architecture-timesheet-management.md` | The architecture spine. At the time of writing it is still the unfilled template (`status: draft`, placeholders such as `{name}`); the spine is distilled from the memlog at the end of the run. |

## 5. Verify

* The spine's frontmatter `status` is `final` only after the reviewer gate and owner review. Until then step 13 stays In progress.
* No `{placeholder}` or template `<!-- -->` comment remains in the spine.
* Each decision (`AD-n`) has Binds, Prevents and Rule, and the owner-adopted ones are tagged `[ADOPTED]`.
* The spec is not changed by hand. Stack and hosting stay in the architecture, not in the spec (see [troubleshooting.md](../../Guide/troubleshooting.md)).

## 6. Troubleshooting

* **BMad not set up, no active initiative, or the spec not updated after another skill ran:** See [troubleshooting.md](../../Guide/troubleshooting.md).
* **The spine still shows `{name}` and empty sections:** the run was started but not finalized. Resume it; the skill offers to continue from the memlog.
* **Research disagrees with an owner decision (for example the email vendor):** the owner decision stands; log the conflict as an open question in the memlog, do not reverse it.

## Skill Folder Structure

Layout of the installed `bmad-architecture` skill (`.claude/skills/bmad-architecture/`), which mirrors its [upstream folder](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-architecture):

* `SKILL.md`: the entry point; the coaching flow, memlog rules and finalize sequence.
* `bmod.toml`: module metadata.
* `customize.toml`: the override surface (spine output path, run folder pattern, finalize reviewers); team overrides live in `_bmad/custom/`.
* `references/`: `headless.md` (unattended runs) and `reviewer-gate.md` (pre-handoff review).
* `assets/`: `spine-template.md`, the template the spine is seeded from.
* `scripts/`: `lint_spine.py` (deterministic spine check) and its `tests/`.
* No `evals/` folder.

## Skill Steps

Steps the skill itself runs, in order (from its `SKILL.md`):

1. **Activation:** resolve customization and config, find the active initiative, detect create, update or validate, and offer to resume.
2. **Choose the working mode:** Coaching path (default) or Fast path, then ask about purpose and audience.
3. **Seed the run:** create the run folder, copy the spine template, run `memlog.py init`.
4. **Elicit and log:** decisions, constraints, versions, assumptions and questions go to the memlog.
5. **Finalize:** distill the spine from the memlog, reconcile inputs, run the reviewer gate, triage open questions, then produce any extra renderings.

## Official References

* [Architecture](https://docs.bmad-method.org/plan/design-ux-and-architecture/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad-architecture` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-architecture)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
