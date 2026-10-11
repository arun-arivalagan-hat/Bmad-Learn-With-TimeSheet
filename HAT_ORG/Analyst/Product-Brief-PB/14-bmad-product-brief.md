# BMAD Product Brief Guide

**SDLC role:** Analyst | **Team lead:** Not assigned yet | **BMad agent:** Mary (Business Analyst) | **Skill:** `bmad-product-brief`

## 1. Purpose

This guide explains how to write a product brief with `bmad-product-brief`. The brief is a short, plain-language page set for people who are not developers: what we are building, why, who it serves, what is in and out of the first version, and how we will know it worked. In this repository it turns the spec, brainstorm and research into one shareable document for the Timesheet Management initiative. It does not replace the spec, and it does not choose technology.

## 2. Prerequisites

* Steps 1 and 2 complete: installation and an active initiative ([02-bmad-initiative.md](../../CoreTools/Bmad/Bmad-Initiative/02-bmad-initiative.md)).
* Steps 3 to 8 recommended: the spec, brainstorm and research are the source material, so the brief can be drafted from them rather than from scratch.
* The audience and purpose of the brief (here: non-developer readers in the organisation, tracking employee work every week).

## 3. Run the Skill

Ask Mary for the product brief, or invoke the skill:

```text
Use bmad-product-brief to write a brief for Timesheet Management for non-technical readers in the organisation, drawing on the spec and research
```

The skill detects whether to create, update or validate. When you give it rich source material, it can take a fast path and draft from those files, tagging anything it had to guess as `[ASSUMPTION: ...]`. In this run the brief was written with status `draft`, then synced to the spec and PRD of 2026-10-11, polished with `bmad-review`, and set to `final` at the owner's request.

Re-run it in update mode when the spec or owner decisions change, or in validate mode to get an honest critique returned inline.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/brief-timesheet-management/brief-timesheet-management.md` | The brief: executive summary, problem, solution, what makes it different, who it serves, success criteria, scope, vision. |
| `_bmad-output/initiative-timesheet-management/brief-timesheet-management/.memlog.md` | Decisions and assumptions log the brief is derived from and updated against. |
| `_bmad-output/initiative-timesheet-management/brief-timesheet-management/addendum.md` | Detail behind the brief: retention, sizing history (160 employees, 20 projects), the unverified 19-hours-a-week figure and open decisions. |

## 5. Verify

* The brief frontmatter shows the title, `status` (this run: `final`, 2026-10-11), `created` and `updated`.
* Every guess is tagged `[ASSUMPTION: ...]` and appears in the memlog (audience, differentiator, user count, success targets, retention).
* Scope matches the spec: payroll and invoicing are out, and all capabilities are free for now.
* The brief names no technology; those choices are left to `bmad-architecture`.

## 6. Troubleshooting

* **BMad not set up, no active initiative, or the brief drifts from the spec:** See [troubleshooting.md](../../Guide/troubleshooting.md).
* **Success targets are missing:** the owner set the on-time and smiley targets aside; set targets after the first weeks of real data.

## Skill Folder Structure

Layout of the installed `bmad-product-brief` skill (`.claude/skills/bmad-product-brief/`), which mirrors its [upstream folder](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-product-brief):

* `SKILL.md`: the entry point. Frontmatter (name, description) tells the harness when to trigger; the body holds the instructions.
* `bmod.toml`: module metadata, which module the skill belongs to and where it is sourced from on GitHub.
* `customize.toml`: the override surface; team and personal overrides live in `_bmad/custom/`, never in this file.
* `assets/`: `brief-template.md`, the brief skeleton.
* No `references/` or `scripts/`: discovery, constraints and finalize are all in `SKILL.md`.


## Skill Steps

Steps the skill itself runs, in order (from its `SKILL.md`):

1. **Pick the intent:** Create, Update or Validate.
2. **Discovery:** take the user's brain dump, why the brief exists, domain and form factor; choose Fast path (batched questions, `[ASSUMPTION]` tags) or Coaching path (section by section).
3. **Draft** with a persistent workspace (`status: draft`, `.memlog.md`), aiming for 1 to 2 pages and moving overflow to `addendum.md`.
4. **Finalize:** memlog audit and addendum review, polish against the doc standards, external handoffs, then tell the user it is ready and suggest next steps via `bmad`.

## Official References

* [Product Brief](https://docs.bmad-method.org/plan/choose-a-planning-path/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad-product-brief` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-product-brief)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
