# BMAD Troubleshooting (shared)

Problems that occur in more than one step. Step docs link here and list only the problems specific to their own step. Back to the [index](00-index.md).

## BMad not set up

**Symptom:** A BMad skill is not found, or `bmad status` fails.

* Complete step 1 ([01-bmad-installation-and-setup.md](../CoreTools/Bmad/Bmad-Setup/01-bmad-installation-and-setup.md)) and confirm `.claude/skills/bmad*` exists.
* Restart the Claude Code session so the skills load.

## No active initiative, wrong initiative, or files in the wrong folder

**Symptom:** A skill asks which initiative to use, or its output lands outside `_bmad-output/initiative-timesheet-management/`.

* Check the active initiative in `_bmad/custom/config.user.toml`.
* If it is wrong or empty, ask the `bmad` agent to show or set the active initiative ([02-bmad-initiative.md](../CoreTools/Bmad/Bmad-Initiative/02-bmad-initiative.md)), then run the skill again.
* Move misplaced documents into the initiative folder, one folder per document (`<type>-<slug>/<type>-<slug>.md`).

## Spec not updated after another skill ran

**Symptom:** A research, brainstorm, brief or PRFAQ document changed, but the spec did not.

* Run `bmad-spec` so it logs the change in `.memlog.md` and re-derives the spec ([03-bmad-spec.md](../BmadMethod/Bmad-spec/03-bmad-spec.md)).
* Findings on stack, hosting or vendors are not spec changes. They belong to the architecture step.
* If a finding conflicts with an owner decision, record it as an open question. Never reverse the decision.

## Derived documents edited by hand

**Symptom:** `spec-timesheet-management.md` or `glossary.md` has a manual edit that a later re-derive removed.

* Never hand-edit these files. They are derived from `.memlog.md`.
* Log the change first: `uv run _bmad/scripts/memlog.py append --workspace <spec folder> --type <type> --text "..."`, then re-derive with `bmad-spec`.

## Thin or vendor-biased research findings

**Symptom:** A research report relies on vendor pages or a single source.

* Check the claim log in the research folder's `.memlog.md` for verification status before relying on a figure.
* Treat unverified numbers as assumptions, not decisions.

## Drift between the brief, PRFAQ and spec

**Symptom:** The brief or PRFAQ says something the spec does not.

* The spec and the owner decisions outrank the brief and PRFAQ. Update the brief or PRFAQ to match, or record the conflict as an open question.
