# BMAD Product Brief Guide

**BMad agent:** Mary (Business Analyst) | **Skill:** `bmad-product-brief`

## 1. Purpose

This guide explains how to write a product brief with `bmad-product-brief`. The brief is a short, plain-language page set for people who are not developers: what we are building, why, who it serves, what is in and out of the first version, and how we will know it worked. In this repository it turns the spec, brainstorm and research into one shareable document for the Timesheet Management initiative. It does not replace the spec, and it does not choose technology.

## 2. Prerequisites

* Steps 1 and 2 complete: installation and an active initiative ([02-bmad-initiative.md](02-bmad-initiative.md)).
* Steps 3 to 8 recommended: the spec, brainstorm and research are the source material, so the brief can be drafted from them rather than from scratch.
* The audience and purpose of the brief (here: non-developer readers in the organisation, tracking employee work every week).

## 3. Run the Skill

Ask Mary for the product brief, or invoke the skill:

```text
Use bmad-product-brief to write a brief for Timesheet Management for non-technical readers in the organisation, drawing on the spec and research
```

The skill detects whether to create, update or validate. When you give it rich source material, it can take a fast path and draft from those files, tagging anything it had to guess as `[ASSUMPTION: ...]`. In this run the brief was written with status `draft`, awaiting owner review before polish and finalise.

Re-run it in update mode when the spec or owner decisions change, or in validate mode to get an honest critique returned inline.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/brief-timesheet-management/brief-timesheet-management.md` | The brief: executive summary, problem, solution, what makes it different, who it serves, success criteria, scope, vision. |
| `_bmad-output/initiative-timesheet-management/brief-timesheet-management/.memlog.md` | Decisions and assumptions log the brief is derived from and updated against. |

## 5. Verify

* The brief frontmatter shows the title, `status`, `created` and `updated`.
* Every guess is tagged `[ASSUMPTION: ...]` and appears in the memlog (audience, differentiator, user count, success targets, retention).
* Scope matches the spec: payroll and invoicing are out, and all capabilities are free for now.
* The brief names no technology; those choices are left to `bmad-architecture`.

## 6. Troubleshooting

* **The skill reports BMad is not set up:** run the `bmad` skill's setup, then run the skill again.
* **No active initiative:** set one with the `bmad` skill ([02-bmad-initiative.md](02-bmad-initiative.md)).
* **The brief drifts from the spec:** run it in update mode against the spec; do not patch it by hand.
* **Success targets are missing:** they are marked as assumptions on purpose; set them after the first weeks of real data.
