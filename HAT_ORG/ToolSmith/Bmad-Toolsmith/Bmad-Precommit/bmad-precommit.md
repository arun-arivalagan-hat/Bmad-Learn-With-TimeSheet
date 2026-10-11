# BMAD Pre-commit Guide

**SDLC role:** ToolSmith | **Team lead:** Not assigned yet | **BMad agent:** Skill run directly | **Skill:** `bmad-precommit` (custom skill built with `bmad-toolsmith`; not part of an installed BMad module)

## 1. Purpose

`bmad-precommit` brings everything connected to your uncommitted work up to date, so you can review one clean working tree and then commit it yourself. It is the manual twin of the pre-commit hook: same two agents, same order. It differs in one way: the hook reads the staged diff, while the skill reads the working tree, so it can run before anything is staged.

It is a tool you run when you want it, not a numbered step, and it does not replace the hook. It was built with Smithy and `bmad-toolsmith`; see [bmad-toolsmith.md](../bmad-toolsmith.md).

## 2. Prerequisites

* Step 1 complete: BMAD installed ([01-bmad-installation-and-setup.md](../../../CoreTools/Bmad/Bmad-Setup/01-bmad-installation-and-setup.md)).
* The two agents exist in `.claude/agents/`: `bmad-spec-sync` and `bmad-docs-updater`.
* The skill exists at `.agents/skills/bmad-precommit/`, with a link in `.claude/skills/`.

## 3. Run it

Invoke the skill in Claude Code:

```text
/bmad-precommit
```

It sorts each changed or untracked file (`git status --porcelain -uall`) and updates what each kind connects to:

| Changed file | Connected artifacts | Updated by |
|---|---|---|
| Planning input: anything under `_bmad-output/` outside `spec-*/`, `digests/`, `*.memlog.md` and `brainstorm.html` (research, brainstorm, brief, PRFAQ, PRD, UX, architecture) | The spec folder: spec, glossary, premium tier, through its memlog | `bmad-spec-sync` |
| Any BMad output, including spec files the previous row regenerated; changes under `.claude/skills/` or `_bmad/` | `HAT_ORG/` step docs, the index tables, shared troubleshooting | `bmad-docs-updater` |
| Only `HAT_ORG/` | The index | `bmad-docs-updater` |
| Nothing BMad-related | Nothing | none |

Order: spec sync first (only when there are planning inputs), then a second read of the tree, then the docs update. The docs step runs second because it records the spec as it then stands.

It stages nothing, commits nothing and pushes nothing. It ends with a report of what each agent changed, any failure, and that nothing is staged. Review the changes, stage the paths you mean to, and commit.

## 4. Files Generated

The skill itself generates no document. The agents edit the working tree only.

| File | Purpose |
|------|---------|
| `.agents/skills/bmad-precommit/SKILL.md` | The skill. |
| `.agents/skills/bmad-precommit/evals/triggers.json` | 18 test queries for checking that the description fires on the right requests. |
| `.claude/skills/bmad-precommit` | Link that makes the skill available to Claude Code. |
| `_bmad-output/eval-reports/<timestamp>-bmad-precommit-review.md` | Review report from `bmad-toolsmith`; advice on the skill, not a planning input. |

## 5. Verify

* `git status --short` before and after: the changes the agents made appear as modified or new files, none staged (`git diff --cached --name-only` prints nothing).
* After a planning input changes, the spec and `.memlog.md` changed with it, and the index's Generated files table lists the new file.
* A run with nothing BMad-related changed says so and stops.

## 6. Troubleshooting

* **Spec, index or `HAT_ORG/` not updated:** see [troubleshooting.md](../../../Guide/troubleshooting.md).
* **An agent did not pick up the uncommitted change:** both agents are written for the hook, where their input is `git diff --cached`. The skill tells them to read the working tree instead. If an agent still reports nothing to do, run it again with the changed paths named, or stage the files and let the hook do the work.
* **`__pycache__` files show as untracked:** build cache from skill scripts. Do not commit them.
* **A tool-generated file under `_bmad-output/` outside the spec (for example `eval-reports/`) matches the planning-input rule:** it is not a planning input. The skill's rule does not yet exclude it, so skip spec sync for such files.
* **Hook not running on commit:** `.git/hooks/pre-commit` is not tracked and is per clone. This skill is the way to run the same routine without it.

## 7. Open items

* A review of the skill (see the report above) recommends a small classify script and a checkable end state for the report. Neither is applied yet.
* The skill has not yet been run on a real planning-input change; the first real run was on tooling files only.

## 8. Next Step

Use it before each commit. It does not change the next planning step: run `bmad-architecture` ([00-index.md](../../../Guide/00-index.md), step 13).

## Skill Folder Structure

A custom skill in this repository (`.agents/skills/bmad-precommit/`, linked from `.claude/skills/`), not from upstream. It is the minimal skill shape:

* `SKILL.md`: the whole routine (classify, spec sync, docs update, report).
* `evals/triggers.json`: cases that check when the skill should and should not trigger.
* No `bmod.toml`, `customize.toml`, `references/` or `scripts/`, because it belongs to no module and loads no extra files.

## Skill Steps

`bmad-precommit` is a custom skill in this repository, so it has no upstream page. Its steps (from its `SKILL.md`):

1. **Classify** the uncommitted changes; stop if none are BMad-related.
2. **Spec sync:** launch `bmad-spec-sync` when planning inputs changed.
3. **Re-read the tree** with `git status` because the spec step may have added files.
4. **Docs update:** launch `bmad-docs-updater` with every changed path.
5. **Report** what each agent changed; nothing is staged.

## Official References

* [Pre-commit (built with Toolsmith)](https://docs.bmad-method.org/toolsmith/toolsmith/)
* [Official documentation: Eval Runner](https://docs.bmad-method.org/toolsmith/bmad-eval/)
* [GitHub: `bmad-toolsmith` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-toolsmith)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
