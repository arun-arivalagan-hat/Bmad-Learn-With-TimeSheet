---
name: bmad-precommit
description: Runs the TimeSheet pre-commit routine on demand against uncommitted working-tree changes: reads which files were generated or edited, then updates everything connected to them, the spec (via bmad-spec-sync) and the HAT_ORG docs and index (via bmad-docs-updater). Use when the user says "precommit", "run the pre-commit routine", or "update the connected docs before I commit". Not for staging, committing or pushing, and not a replacement for the git hook.
---

# Pre-commit routine

Bring everything connected to your uncommitted work up to date, so the user reviews one clean working tree and commits it themselves. This is the manual twin of `.git/hooks/pre-commit`: same two agents, same order, but it reads the working tree where the hook reads the staged diff.

Stage nothing, commit nothing, push nothing; that belongs to the user and the hook.

## What is connected to what

Classify each changed or untracked file from `git status --porcelain -uall`, then update what its class connects to:

| Changed file | Connected artifacts | Updated by |
|---|---|---|
| Planning input: anything under `_bmad-output/` outside `spec-*/`, `digests/`, `*.memlog.md` and `brainstorm.html` (research, brainstorm, brief, PRFAQ, PRD, UX, architecture) | The spec folder: spec, glossary, premium tier, via its memlog | `bmad-spec-sync` |
| Any BMad output, including the spec files the previous row just regenerated; changes under `.claude/skills/` or `_bmad/` | `HAT_ORG/` step docs, the index's step table and Generated files table, shared troubleshooting | `bmad-docs-updater` |
| Only `HAT_ORG/` | The index | `bmad-docs-updater` |
| Nothing BMad-related | Nothing | none |

The spec is derived from the planning inputs and must not feed itself, which is why spec files, memlogs and digests are not inputs. The spec is also derived from its memlog, so it is never hand-edited; that is the agent's job.

## Steps

1. **Classify.** With no changes, or none of them BMad-related, say so and stop.
2. **Spec sync.** With planning inputs, launch `bmad-spec-sync`, pass it the input paths, and wait. Otherwise skip and say so.
3. **Re-read the tree.** Run `git status --porcelain -uall` again: the spec step may have generated files the docs step must now record.
4. **Docs update.** Launch `bmad-docs-updater` with the full list of changed paths from step 3. It runs second because it records the spec as it then stands.
5. **Report.** List what each agent changed, any agent failure with its message, and that nothing is staged.

## Briefing the agents

Both agents are written for the hook, where their input is `git diff --cached`. In a manual run that diff is empty, so say in each prompt: "This is a manual pre-commit run. The changes are uncommitted in the working tree, not staged. Read them with `git diff HEAD -- <path>` and `git status --porcelain -uall` wherever your instructions say `git diff --cached`; read untracked files directly. Do not stage, commit or push."

A failed agent does not stop the routine: carry on to the next step and report the failure, as the hook does.
