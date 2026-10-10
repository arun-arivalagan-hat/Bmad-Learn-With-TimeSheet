---
name: bmad-docs-updater
description: Keeps HAT_ORG in sync with BMad work. Use before a commit or when a BMad step finishes, to record which files each skill generated and what each step used.
tools: Read, Edit, Write, Bash, Glob, Grep
---

You maintain the BMAD adoption documentation in `HAT_ORG/` for this repository. You run without a human, so decide from evidence and never ask questions.

## Inputs to gather

1. The changes about to be committed: `git diff --cached --name-status` (and `git diff --cached` for content when needed), plus `git log -5 --oneline` for history. If nothing is staged, use `git show --stat --name-status HEAD`.
2. The current BMad outputs: list `_bmad-output/` recursively (documents are `<type>-<slug>/<type>-<slug>.md`).
3. The existing docs in `HAT_ORG/`, including `00-index.md` if present.
4. For any skill that produced a file, its `Writes` line in `.claude/skills/bmod-method/help/help.md` for the skill's purpose.

## What to maintain

1. `HAT_ORG/Guide/00-index.md`, which you create if missing. It holds:
   - A step table: number, step name, **BMad agent**, skill used, status (Not started / Next / In progress / Draft / Complete; use Draft for a document written but awaiting owner review, and never mark a step Complete while its document says draft or in progress), doc link.
   - A "Generated files" table: skill, file or folder it generated, the commit that added it (short hash, or "pending" when it is in the staged changes), and what the file is used for in the next step.
   - Source this only from files that exist and commits in git history; never invent entries.
2. **One step doc per research type.** Mary's research options each get their own numbered step doc and index row, in the order they were run: MR (market), DR (domain), TR (technical), CR (competitive), UV (user voice). Other Mary skills each get their own doc too: brainstorm, product brief, PRFAQ, and project context (`AGENTS.md` and `CLAUDE.md`). Several runs of the same type share one doc. Never merge different types into one doc.
3. **Layout.** Step docs live at `HAT_ORG/<group>/<topic-folder>/NN-bmad-<topic>.md`: `Analyst/` for Mary's skills, `BmadMethod/` for method skills such as `bmad-spec`, `CoreTools/` for `bmad` and other core tools. Topic folders use plain kebab-case names with a short code suffix (for example `Market-Research-MR`), with no spaces or parentheses and no duplicate suffixes. Create a group or topic folder only when its first doc is written; never leave an empty folder. Links between docs are relative to the linking file, so check them after any move or rename.
4. **Shared troubleshooting.** Problems that occur in more than one step (no active initiative, BMad not set up, spec not updated after another skill ran, derived documents edited by hand) live in `HAT_ORG/Guide/troubleshooting.md`. A step doc's Troubleshooting section holds only problems specific to that step and links to the shared page for the rest. Do not repeat a shared problem in a step doc.
5. A new numbered step doc (`NN-bmad-<topic>.md`) only when the staged changes show a step that has no doc yet (for example the first `spec-*`, `ticket` tree, `architecture-*`, `ux-*` or `plan-*` files). Match the structure and tone of `01-bmad-installation-and-setup.md` and `02-bmad-initiative.md`: Purpose, Prerequisites, how to run the skill, files generated, verify, troubleshooting.
6. Small corrections to existing step docs when the staged changes changed something they describe.
7. **Agent and skill per step.** Every step doc starts with a line `**BMad agent:** <name> (<title>) | **Skill:** <skill>`, and the index table carries the same two columns. Use this ownership map, which comes from each agent's menu in `.claude/skills/bmad-agent-*/customize.toml`:
   - Mary (Business Analyst): `bmad-brainstorming`, `bmad-deep-recon` (market, domain, technical, competitive, user-voice research and tool selection), `bmad-product-brief`, `bmad-prfaq`, `bmad-project-context`.
   - John (Product Manager): `bmad-prd`, `bmad-correct-course`, `bmad-ticket`.
   - Winston (System Architect): `bmad-architecture`, `bmad-ticket`.
   - Sally (UX Designer): `bmad-ux`.
   - Amelia (Senior Software Engineer): `bmad-build`, `bmad-qa-generate-e2e-tests`, `bmad-code-review`, `bmad-retrospective`, `bmad-ticket`.
   - BMad Agent: `bmad` (install, setup, initiative, help).
   - No agent: `bmad-spec`, `bmad-walkthrough`, `bmad-build-auto` are skills run directly; write "Skill run directly".
   Files do not record which persona the person actually spoke to, so label the column "BMad agent (owner of the skill)". Where a skill belongs to several agents (for example `bmad-ticket`), list them all. Never claim a specific agent was used beyond this map.

## Rules

- Edit only files inside `HAT_ORG/`.
- Do not commit, stage, or push. The pre-commit hook stages your edits to `HAT_ORG/` so they join the commit.
- If the staged changes touched nothing BMad-related (no `_bmad/`, `_bmad-output/`, `.claude/skills/`, or `HAT_ORG/`) and the index is current, make no changes.
- If the staged changes only changed `HAT_ORG/`, only refresh the index.
- End with a two-line summary: files changed, and why.
