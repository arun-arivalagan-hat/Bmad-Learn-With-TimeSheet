# BMAD Review Guide

**SDLC role:** CoreTools (used by TeamLead, Product Owner and Analyst) | **Team lead:** Not assigned yet | **BMad agent:** Skill run directly | **Skill:** `bmad-review` (`core-tools` module)

## 1. Purpose

`bmad-review` reviews a diff, a pull request or a document through one or more lenses and reports the findings in one shape. It is a tool you run when you ask for a review, not a numbered step. It never runs on its own, and it does not review edits you just made unless you say "review".

Use `bmad-code-review` for agent review of a code change. Use `bmad-review` when you want specific lenses, or when the content is a document such as a brief, PRD or spec.

## 2. Prerequisites

* Step 1 complete: BMAD installed ([01-bmad-installation-and-setup.md](../Bmad-Setup/01-bmad-installation-and-setup.md)).
* The skill exists at `.claude/skills/bmad-review/`, with `customize.toml` and a `references/` folder holding one file per lens.
* `_bmad/scripts/resolve_customization.py` exists. The skill uses it to read its settings.

## 3. Run it

```text
/bmad-review <path>
```

You can also say what to review, for example "review the PRD" or "review my uncommitted changes". Name lenses to run only those: `/bmad-review <path> lenses=structure,prose`.

| Lens code | What it checks | Applies to | Runs when |
|---|---|---|---|
| `adversarial` | Critique that must find at least ten concrete issues | Any content | Always |
| `edge-case-hunter` | Unhandled paths in code, diffs, and specs, requirements, plans and stories | Any content with behavior | Not for prose with no behavior |
| `verification-gap` | Behavior the tests do not cover | Code | Inside a repo where tests can be read |
| `structure` | How a document is organized | Documents | The author may change the shape |
| `prose` | Copy edit; runs after `structure` and uses its findings | Documents | The document is being copy-edited |

With no lens named, it runs every lens that applies to the content. It first says in one line which lenses it will run. Each lens works alone, so overlapping findings are kept, not merged.

Settings you can change in `customize.toml` (use `bmad-customize` for an override): `output_format` (now `both`, JSON plus a markdown report), `report_path` (now empty, so the report appears in chat), `style_guide` (now Microsoft Writing Style Guide) and `reader_type` (now `humans`).

## 4. Files Generated

The skill generates no file by default. With `report_path` empty, the findings appear in chat only.

| File | Purpose |
|------|---------|
| `.claude/skills/bmad-review/` | The installed skill: `SKILL.md`, `customize.toml`, `bmod.toml`, `scripts/` and `references/` (one `lens-*.md` file per lens, plus `editorial-common.md` and `structure-models.md`). |

Each finding carries `lens`, `location`, `trigger_condition`, `guard_snippet` and `potential_consequence`. The editorial lenses show a findings table instead. There is no severity or ranking.

## 5. Where it was used in this project

| Step | Use | Result |
|---|---|---|
| 12, PRD ([12-bmad-prd.md](../../../ProductOwner/Product-Requirements-PRD/12-bmad-prd.md)) | Structure and prose lenses polished the PRD. | The owner accepted the fixes: approval per project block, lateness judged on first submission, FR-21 and FR-22. |
| 14, product brief ([14-bmad-product-brief.md](../../../Analyst/Product-Brief-PB/14-bmad-product-brief.md)) | Polished the brief before it was set to `final`. | Brief status `final` on 2026-10-11. |

The review files beside the PRD (`review-rubric.md`, `review-adversarial-general.md`, validation reports) come from the PRD run and are listed in the index's Generated files table. They are advice, not planning inputs.

## 6. Verify

* The reply starts with one line naming the content class and the lenses that will run.
* The report groups findings by lens, and a lens with nothing to report gets one line.
* `git status --short` shows no change to the reviewed content. A review reports; it does not edit.

## 7. Troubleshooting

* **"Script not found" or BMad not set up:** the skill offers to run setup; see [troubleshooting.md](../../../Guide/troubleshooting.md).
* **It did not run:** it runs only when you ask for a review. A request to apply earlier feedback is a change, not a review.
* **A lens is missing:** an override may have disabled it (empty `instruction`) or replaced it. Check `customize.toml` and any override.
* **Review findings contradict an owner decision:** record the conflict as an open question; never reverse the decision (see `AGENTS.md` policy).

## 8. Open items

* `report_path` is empty, so findings exist only in chat. Set it with `bmad-customize` if the team wants reports kept in `_bmad-output/`. If so, add the path to the index's Generated files table.
* The skill has not been run on code in this project, since there is no application code yet.

## 9. Next Step

After a review, apply the accepted changes through the owning skill (for the PRD, `bmad-prd`; for the spec, a memlog entry first, then `bmad-spec`). The next planning step stays `bmad-architecture` ([00-index.md](../../../Guide/00-index.md), step 13).

## Official References

* [Official documentation: bmad-review](https://docs.bmad-method.org/)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
