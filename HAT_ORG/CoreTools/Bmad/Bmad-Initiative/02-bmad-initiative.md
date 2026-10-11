# BMAD Initiative Guide

**BMad agent:** BMad Agent (`bmad`) | **Skill:** `bmad`

## 1. Purpose

This guide explains how to create a BMAD **initiative**: the named folder under `_bmad-output/` that groups every document for one body of work (spec, tickets, and later UX or architecture files). Later skills (`bmad-spec`, `bmad-ticket`, `bmad-build`) read and write inside the active initiative.

Example in this repository: `initiative-timesheet-management` (weekly effort capture linked to billing and utilization).

## 2. Prerequisites

* Step 1 complete: BMAD installed and `bmad status` succeeds ([01-bmad-installation-and-setup.md](../Bmad-Setup/01-bmad-installation-and-setup.md)).
* A short description of the work (name and objective).

## 3. Create the Initiative

Invoke the `bmad` skill and request, for example:

```text
Create a new initiative called Timesheet Management
```

The skill creates the initiative folder and marks it as the active initiative. Showing, switching, creating or clearing the active initiative are all `bmad` requests.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/initiative-timesheet-management.md` | Initiative document. Frontmatter holds `type: initiative`, `title` and `parent: none`. |

Documents follow the layout `<type>-<slug>/<type>-<slug>.md`. Here the initiative folder is the parent of every later document.

## 5. Verify

* The folder `_bmad-output/initiative-timesheet-management/` exists.
* The initiative file has `type: initiative` and the expected title.
* Ask `bmad` to show the active initiative and confirm it is the one you created.

## 6. Troubleshooting

* **Files in the wrong folder, wrong initiative, or a hand-off to `bmad`:** See [troubleshooting.md](../../../Guide/troubleshooting.md).

## 7. Next Step

Run `bmad-spec` ([03-bmad-spec.md](../../../BmadMethod/Bmad-spec/03-bmad-spec.md)).

## Skill Folder Structure

Layout of the installed `bmad` skill (`.claude/skills/bmad/`), which mirrors its [upstream folder](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad):

* `SKILL.md`: the entry point. Frontmatter (name, description) tells the harness when to trigger; the body holds the instructions.
* `bmod.toml`: module metadata, which module the skill belongs to and where it is sourced from on GitHub.
* `customize.toml`: the override surface; team and personal overrides live in `_bmad/custom/`, never in this file.
* `references/initiative.md`: the steps for this doc; the other references (`setup`, `migrate`, `help`) cover other actions.
* `scripts/resolve_config.py`: reads `core.active_initiative` and `core.output_folder`.
* `assets/`: `config.template.toml`, the starting config.


## Skill Steps

Steps the skill itself runs, in order (from its `SKILL.md`):

1. **Resolve config:** read `core.output_folder` and `core.active_initiative` through `resolve_config.py`; if the script is missing, BMad is not set up.
2. **Report** the active initiative and list the `initiative-*` folders.
3. **Choose:** pick one, create a new one, or clear it. A new one gets `initiative-<slug>/initiative-<slug>.md`.
4. **Write** `active_initiative` under `[core]` in `_bmad/custom/config.user.toml`.
5. **Confirm** the change in one line.

## Official References

* [Initiative (via BMad setup)](https://docs.bmad-method.org/start/install-bmad/)
* [Get Answers About BMad](https://docs.bmad-method.org/start/get-answers-about-bmad/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
