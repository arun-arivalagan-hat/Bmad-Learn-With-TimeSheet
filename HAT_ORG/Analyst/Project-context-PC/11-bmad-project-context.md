# BMAD Project Context Guide

**SDLC role:** Analyst | **Team lead:** Not assigned yet | **BMad agent:** Mary (Business Analyst), menu option PC | **Skill:** `bmad-project-context`

## 1. Purpose

This guide explains how to create the repository's agent instructions with `bmad-project-context`. It writes a small, verified block of rules into `AGENTS.md`, plus a `CLAUDE.md` that imports it, so every AI assistant that opens the repository starts with the same rules and does not need them repeated each session. It records policy, where things are, how to run and verify the project, and pitfalls that agents have actually hit. It does not describe the whole repository, list the stack, or replace the team docs in `HAT_ORG/`.

## 2. Prerequisites

* Step 1 complete: BMad is installed ([01-bmad-installation-and-setup.md](../../CoreTools/Bmad/Bmad-Setup/01-bmad-installation-and-setup.md)).
* Steps 2 and 3 recommended: an active initiative and a spec give the skill real rules to record ([03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)).
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

## Skill Folder Structure

Layout of the installed `bmad-project-context` skill (`.claude/skills/bmad-project-context/`), which mirrors its [upstream folder](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-project-context):

* `SKILL.md`: the entry point. Frontmatter (name, description) tells the harness when to trigger; the body holds the instructions.
* `bmod.toml`: module metadata, which module the skill belongs to and where it is sourced from on GitHub.
* `customize.toml`: the override surface; team and personal overrides live in `_bmad/custom/`, never in this file.
* `references/`: `best-practices.md` (what makes agent instructions good) and `template.md` (the `AGENTS.md` block); both are loaded first on every run.
* No `scripts/`: it reads and writes the repo's own files.


## Skill Steps

Steps the skill itself runs, in order (from its `SKILL.md`):

No files are written until step 5.

1. **Assess and report** what instruction files exist and how they measure up.
2. **Ask what you bring:** rules, standards and outside documents no scan reaches.
3. **Discover and verify** with parallel scans of config, CI, source and history.
4. **Interview the gaps:** only what no scan can answer.
5. **Show the block, then write it** (`AGENTS.md`, plus `CLAUDE.md` pointing at it).
6. **Close:** what went in, what stayed out and why, and how to maintain it.

Variants: Refresh (step 1 as a diff), Adoption, Greenfield, Migration, plus `record` for pitfalls and an audit.

## Official References

* [Project Context](https://docs.bmad-method.org/existing-codebases/set-and-maintain-project-context/)
* [Official documentation: The Theory of Project Context](https://docs.bmad-method.org/existing-codebases/theory-of-project-context/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad-project-context` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-project-context)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
