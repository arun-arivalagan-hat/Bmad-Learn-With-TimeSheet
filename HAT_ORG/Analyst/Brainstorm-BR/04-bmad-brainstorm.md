# BMAD Brainstorm Guide

**BMad agent:** Mary (Business Analyst) for `bmad-brainstorming`; skill run directly for `bmad-spec` | **Skill:** `bmad-brainstorming`, `bmad-spec`

## 1. Purpose

This guide explains how to use `bmad-brainstorming` to generate and converge ideas for an initiative, then feed the result back into the spec through `bmad-spec`. It produces an intent document and a premium-tier companion; it does not slice work into stories (that is `bmad-ticket`).

## 2. Prerequisites

* Step 2 complete: an active initiative exists ([02-bmad-initiative.md](../../CoreTools/Bmad/Bmad-Initiative/02-bmad-initiative.md)).
* Step 3 complete: a first spec exists ([03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)), so the brainstorm can answer its open questions.
* A topic and goal, for example: "a timesheet people finish on time and enjoy, plus approval and billing flows".

## 3. Run the Skill

Invoke `bmad-brainstorming` with the topic and goal, for example:

```text
Use bmad-brainstorming for Timesheet Management: make timesheets delightful so users submit on time, include premium-tier ideas
```

The skill runs techniques (for example Anti-Solution), logs every idea to `.memlog.md`, converges on chosen directions, and writes the intent document and an HTML view.

Then re-run `bmad-spec` so the chosen directions are merged into the spec (the spec lists the brainstorm under `sources:` and `premium-tier.md` under `companions:`).

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/brainstorm-timesheet-delight/brainstorm-timesheet-delight.md` | Intent document: goal, core insight, six chosen directions, premium tier candidates, open decisions, out of scope. |
| `_bmad-output/initiative-timesheet-management/brainstorm-timesheet-delight/brainstorm.html` | HTML view of the brainstorm for sharing. |
| `_bmad-output/initiative-timesheet-management/brainstorm-timesheet-delight/.memlog.md` | Running log of every idea and technique the document is derived from. |
| `_bmad-output/initiative-timesheet-management/spec-timesheet-management/premium-tier.md` | Spec companion: premium tier candidates (not committed scope). |

The re-run of `bmad-spec` also updates `spec-timesheet-management.md` (now CAP-1 to CAP-13) and its `.memlog.md`.

## 5. Verify

* The brainstorm folder exists under the initiative and holds the three files above.
* The spec frontmatter has `companions: [premium-tier.md]` and the brainstorm path under `sources:`.
* Each "Open decision" in the intent document is either answered in the spec (for example the billable flag lives on the project) or left as a recorded open question.
* New capabilities (CAP-8 to CAP-13) have an intent and a success condition; those marked `proposed` need confirmation.

## 6. Troubleshooting

* **Ideas feel too broad:** Treat `premium-tier.md` as candidates only; keep committed scope in the spec's capabilities and non-goals.
* **Spec unchanged after the brainstorm, or files in the wrong folder:** See [troubleshooting.md](../../Guide/troubleshooting.md).

## Skill Folder Structure

Layout of the installed `bmad-brainstorming` skill (`.claude/skills/bmad-brainstorming/`), which mirrors its [upstream folder](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-brainstorming):

* `SKILL.md`: the entry point. Frontmatter (name, description) tells the harness when to trigger; the body holds the instructions.
* `bmod.toml`: module metadata, which module the skill belongs to and where it is sourced from on GitHub.
* `customize.toml`: the override surface; team and personal overrides live in `_bmad/custom/`, never in this file.
* `references/`: one file per stance (`mode-facilitator`, `mode-partner`, `mode-autonomous`) plus `converge`, `finalize`, `resume`, `headless` and `in-chat-techniques`.
* `assets/`: `brain-methods.csv` (technique catalog), `brain-selector.html` (composer page) and icons.
* `scripts/`: `brain.py`, lists and shows techniques without loading the whole catalog.


## Skill Steps

Steps the skill itself runs, in order (from its `SKILL.md`):

1. **Frame:** ask what is being brainstormed and why, and whether there are inputs or special requests.
2. **Choose a stance and techniques:** pick Facilitator, Creative Partner or Ideate for me, and a batch of techniques (composer page or in chat).
3. **Run techniques:** run each until it stops producing, logging every idea to `.memlog.md`.
4. **Converge (optional):** narrow and decide on the chosen directions.
5. **Wrap up:** synthesis, `status: complete`, intent document and HTML view.
6. **Resume:** pick up an earlier session from its memlog.

Then `bmad-spec` merges the result into the spec (see its steps in [03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)).

## Official References

* [Brainstorming](https://docs.bmad-method.org/plan/explore-and-validate-an-idea/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad-brainstorming` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-brainstorming)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
