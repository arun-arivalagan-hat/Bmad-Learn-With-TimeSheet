# BMAD Project Context Guide

**BMad agent:** Mary (Business Analyst), menu option PC | **Skill:** `bmad-project-context`

## 1. Purpose

This guide explains how to create the repository's agent instructions with `bmad-project-context`. It writes a small, verified block of rules into `AGENTS.md`, plus a `CLAUDE.md` that imports it, so every AI assistant that opens the repository starts with the same rules and does not need them repeated each session. It records policy, where things are, how to run and verify the project, and pitfalls that agents have actually hit. It does not describe the whole repository, list the stack, or replace the team docs in `HAT_ORG_BMAD_DOCS/`.

## 2. Prerequisites

* Step 1 complete: BMad is installed ([01-bmad-installation-and-setup.md](01-bmad-installation-and-setup.md)).
* Steps 2 and 3 recommended: an active initiative and a spec give the skill real rules to record ([03-bmad-spec.md](03-bmad-spec.md)).
* A repository with no `AGENTS.md` or `CLAUDE.md` (setup), or an existing one (adopt, refresh).

## 3. Run the Skill

Ask Mary for **PC**, or invoke `bmad-project-context`. The skill works in six steps and writes nothing until the fifth:

1. **Assess:** it reads what exists and decides the intent: setup, adopt, refresh, record or audit. Here it was setup on a greenfield repository (planning only, no code).
2. **Ask what you bring:** rules no scan can find. Five questions: who can change main and how; security and secrets; coding standards; outside documents; mistakes agents have made. You can answer "none" to each. In this repository all five were "none".
3. **Verify:** it path-checks every claim and reads the scripts that commands run.
4. **Interview the gaps:** only what no scan reaches. Observed mistakes from the session are offered as candidate lines.
5. **Show the block, then write it:** you see the complete block and what was left out, and approve before anything is written.
6. **Close:** it reports what went in and why, and how to keep it current.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `AGENTS.md` | The managed block between `<!-- bmad:context -->` markers: orientation, policy, where things are, running and verifying, known pitfalls. The provenance line records the date and commit it was verified against. |
| `CLAUDE.md` | One line, `@AGENTS.md`, so Claude Code loads the same rules. Other agent tools read `AGENTS.md` directly. |

What went into this repository's block: never hand-edit the spec or glossary (log to `.memlog.md` first), never reuse a capability ID, owner decisions outrank research, keep stack and hosting out of the spec, never commit, the file map, the commit-time hook, a TODO for run commands (no code exists yet), and two observed pitfalls (zsh command variables, `git add` staging unrelated work).

## 5. Verify

* The block's paths all exist, and the provenance line names a real commit.
* Start a fresh Claude Code session and ask what the repository rules say about the spec. It should answer from `AGENTS.md` without reading files. This was checked and passed.
* The block stays small. Run commands, tool versions and coding conventions are added only from real evidence.

## 6. Maintain and Troubleshoot

* **Refresh** after significant change: after `bmad-architecture` records the stack, and after the first code exists so the TODO becomes verified commands.
* **Record** the moment an agent gets something wrong, so a recurring mistake earns a line. Prefer a check (hook, linter, CI) over a new line.
* **Rules do not load:** confirm `CLAUDE.md` contains `@AGENTS.md` and start a new session; instruction chains are built at session start.
* **The file grew long:** instruction-following degrades as the loaded set grows. Cut the weakest lines or move them behind a trigger.
* **Hooks enforce, files guide:** `AGENTS.md` does not block anything. If a rule must hold, enforce it with a hook such as the pre-commit hook.
