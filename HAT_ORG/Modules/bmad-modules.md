# BMAD Modules

BMAD in this repository has three modules. Each one has a different job.

| Module | Plain name | What it is for | Example skills |
|---|---|---|---|
| `method` | Workflow framework | Takes an idea to working software, in order: analysis, planning, build, validation. | `bmad-spec`, `bmad-prd`, `bmad-product-brief`, `bmad-architecture`, `bmad-ticket`, `bmad-build` |
| `core-tools` | Utility library | General helpers you can use at any time, in any order. | `bmad`, `bmad-brainstorming`, `bmad-deep-recon`, `bmad-review` |
| `toolsmith` | Skill-building kit | Builds and tests new skills, agents and modules. | `bmad-toolsmith`, `bmad-eval` |

## Why they differ

* **`method`** works on the product. Its outputs feed each other: the spec, PRD and tickets.
* **`core-tools`** has no order and no dependencies. Use a skill whenever it helps.
* **`toolsmith`** works on the tools, not the product. You need it only to make a skill.

## Where the docs are

| Module | Docs |
|---|---|
| `method` | `Analyst/`, `ProductOwner/`, `Architect/`, `BmadMethod/`, grouped by role |
| `core-tools` | `CoreTools/Bmad/` (Setup, Initiative, Review) |
| `toolsmith` | `ToolSmith/Bmad-Toolsmith/` |

`bmad-precommit` is a custom skill built with Toolsmith. It belongs to no module, but its doc sits in `ToolSmith/Bmad-Toolsmith/`.

Only these three modules are installed. The `bmm` name in `_bmad/config.toml` is an older name still left in the config.
