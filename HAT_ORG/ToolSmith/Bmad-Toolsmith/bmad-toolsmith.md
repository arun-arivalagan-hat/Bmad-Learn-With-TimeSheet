# BMAD Toolsmith Guide

**SDLC role:** ToolSmith | **Team lead:** Not assigned yet | **BMad agent:** Smithy (the Toolsmith), `toolsmith` module | **Skill:** `bmad-toolsmith`, with its companion `bmad-eval`

## 1. Purpose

Toolsmith is for people who author skills, agents and modules, not for people who only use them. Smithy builds and changes BMad content from a conversation; `bmad-eval` measures whether the result works.

Smithy:

* **Builds** a skill, agent or module from a conversation about what it is for, who uses it and what it produces. He picks the shape (plain skill, agent, module and so on) as a conclusion of that conversation, never as a menu.
* **Reviews** an existing skill against five lenses (architecture, determinism, leanness, customization, trigger) and writes the findings to chat and to a markdown report. Nothing fails or blocks; you decide what to act on.
* **Validates** a skill or module: manifests, file references, frontmatter, and a trigger eval when a case suite exists. Pass or fail, each failure named.
* **Packages** one skill or several into a module.

He also edits, converts and migrates skills that exist. After a build the quality lenses run on their own and Smithy fixes what they find before handing over.

It is a tool you use when you want to make or judge a skill, not a numbered step.

## 2. Prerequisites

* Step 1 complete: BMAD installed and set up, so `_bmad/` exists ([01-bmad-installation-and-setup.md](../../CoreTools/Bmad/Bmad-Setup/01-bmad-installation-and-setup.md)). Without it Smithy offers setup first.
* `uv` installed; every script runs as `uv run`.
* For `bmad-eval`: a harness recorded once (see section 4).

## 3. Run it

Ask for Smithy by name, or describe the thing you want ("make me a skill", "review this skill"). The `bmad-toolsmith` skill opens his menu:

| Code | Mode | What it does |
|---|---|---|
| BUILD | Build | A new skill, agent or module from a conversation. |
| SCAFFOLD | Scaffold | Lays out the folder, frontmatter and `bmod.toml` for a skill you will write yourself. |
| LOGS | Logs | Proposes a skill from your session logs or transcripts, then builds it. |
| EDIT | Edit | Changes, fixes or extends a skill that exists. |
| CONVERT | Convert | Rebuilds a skill, prompt, rule or command from another tool as a BMad skill, listing what did not carry over. |
| REVIEW | Review | Findings in chat and a report in the reports folder. |
| PACKAGE | Package | Wraps one skill or several as a module. |
| VALIDATE | Validate | Checks manifests, file references, frontmatter and triggers. |
| MIGRATE | Migrate | Converts an old-format module (`module.yaml`, setup skill, help CSV) in place; shows the plan and waits for approval. |
| EVAL | Eval | Runs, benchmarks or trigger-tests a skill with `bmad-eval`. |

**Nothing is written until you approve a read-back.** Before any build, Smithy shows name, description, shape, registration, approach, location and files. Every line can be changed. At the end he says where the skill is, whether it is already live and how it is registered.

### bmad-eval

`bmad-eval` runs a skill's evals and reports what they show. Smithy offers one at the end of every build and reaches it from his menu, so you rarely call it directly. It has four modes:

| Mode | Answers |
|---|---|
| Baseline | Does the skill beat the bare model on the same input? |
| Variant | Does a stripped or prior version do as well? |
| Quality | Does the output meet the case's rubric? |
| Trigger | Does the description fire on the right requests and stay quiet on the rest? |

It needs a harness, recorded once. The first time it runs in a project, the agent works out four facts about its own CLI (the command for one non-interactive run, the folder it reads skills from, the env vars the run needs, and the files that keep it logged in) and records them in `bmad-eval`'s customization through `bmad-customize`. Each case then runs in a clean working directory with a fresh HOME. The run bypasses the CLI's permission prompts, because nobody is there to answer them; wrap the recorded command in a sandbox if you want it contained. Three runs per case is the floor.

## 4. Files Generated

Smithy writes where the read-back says. Common places:

| File | Purpose |
|------|---------|
| The new skill folder (the folder your agent reads skills from, or the project `skills/` folder) | The skill, live at once; skills written this way are not tracked by the skills CLI, so updates are yours. |
| `<skill>/evals/` | The skill's test cases, for example `triggers.json`. |
| `_bmad-output/eval-reports/<timestamp>-<skill>-review.md` | A review report; advice, not a planning input. |
| `_bmad-output/eval-reports/<timestamp>/` | One folder per eval run, a subfolder per case; never overwritten. |

In this repo it built `bmad-precommit` and its review report; see [bmad-precommit.md](Bmad-Precommit/bmad-precommit.md) and the Generated files table in [00-index.md](../../Guide/00-index.md). The eval has not been run yet and no harness is recorded here (there is no `bmad-eval` customization under `_bmad/custom/`).

## 5. Verify

* The read-back was shown and approved before files appeared; the skill is where Smithy said it would be.
* `.claude/skills/<skill>` resolves (a link or folder), so Claude Code can load it.
* Validate mode passes, or names each failure.
* After an eval, a timestamped folder exists under `_bmad-output/eval-reports/`.

## 6. Troubleshooting

* **BMad not set up:** see [troubleshooting.md](../../Guide/troubleshooting.md).
* **`uv` not found:** install `uv`; Smithy's scripts will not run without it.
* **`bmad-eval` asks about the harness:** expected on the first run; the answers are saved through `bmad-customize` and can be edited there.
* **A skill does not trigger, or fires on the wrong things:** run a trigger eval, then let Smithy revise the description from the failures. Do not tune it by feel.
* **A new tool-generated folder shows as untracked or as a planning input:** see the `__pycache__` and `eval-reports/` notes in [bmad-precommit.md](Bmad-Precommit/bmad-precommit.md).

## 7. Next Step

After a build, run the trigger eval Smithy offers, then try one real request. After an edit or package of a skill you own, run a review. After a review, use edit mode for the findings you accept. This does not change the next planning step: run `bmad-architecture` ([00-index.md](../../Guide/00-index.md), step 13).

## Skill Folder Structure

Layout of the installed `bmad-toolsmith` skill (`.claude/skills/bmad-toolsmith/`), which mirrors its [upstream folder](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-toolsmith):

* `SKILL.md`: the entry point. Frontmatter (name, description) tells the harness when to trigger; the body holds the instructions.
* `bmod.toml`: module metadata, which module the skill belongs to and where it is sourced from on GitHub.
* `customize.toml`: the override surface; team and personal overrides live in `_bmad/custom/`, never in this file.
* Route files at the root: `discover.md` (every build starts here), `ship.md` (lenses run before hand-over), `canon.md` and `ecosystem.md`.
* `approaches/`, `shapes/`, `modes/`: how to build (eval-first, lean, scaffold...), what shape to build (plain skill, agent, module...), and what to do to an existing skill (convert, edit, review, validate, package, migrate).
* `lenses/`: the review checks (architecture, contract, customization, determinism, leanness, trigger).
* `scripts/`: scaffolding and scanning helpers (`init_skill.py`, `prepass.py`, `count_tokens.py`...); `evals/triggers.json`: its own trigger eval.
* Companion `bmad-eval` has `references/` (eval and grader format), `scripts/` (`run_evals.py`, `run_triggers.py`) and `evals/`.


## Skill Steps

Steps the skill itself runs, in order (from its `SKILL.md`):

1. **Discover:** every new skill starts in a conversation that ends with an approved read-back; nothing is written before that.
2. **Choose an approach and shape:** for example eval-first, lean or scaffold; plain skill, agent or module. Only the route file reached is loaded.
3. **Build, or work on an existing skill** with a mode: convert, edit, review, validate, package or migrate.
4. **Ship:** the lenses (architecture, contract, customization, determinism, leanness, trigger) run over what was written and Smithy fixes what they find.
5. **Measure:** hand the skill to `bmad-eval` (baseline, variant, quality and trigger evals).

## Official References

* [Toolsmith](https://docs.bmad-method.org/toolsmith/toolsmith/)
* [Official documentation: Eval Runner (`bmad-eval`)](https://docs.bmad-method.org/toolsmith/bmad-eval/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad-toolsmith` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-toolsmith)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
