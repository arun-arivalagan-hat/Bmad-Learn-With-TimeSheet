# Roles and Commands

Which SDLC role runs which command, and where the result is documented. Index of all steps: [00-index.md](00-index.md).

## How it works

1. A role runs its command, for example `/bmad-architecture`. The skill writes files under `_bmad-output/`.
2. The same role runs `/bmad-precommit`. It updates the spec first, then calls the docs updater.
3. The docs updater creates the role's folder in `HAT_ORG/` if missing, and writes the numbered step doc inside it. Example: after `/bmad-architecture`, `HAT_ORG/Architect/Architecture-AR/13-bmad-architecture.md` appears, and the index links it.
4. Nothing is staged or committed. The role reviews the working tree and commits.

## Roles

The team lead column is filled in by the team. The docs updater never invents a name and never overwrites one.

| Role folder | Persona | Team lead | Commands | Run it when | Step docs |
|---|---|---|---|---|---|
| `Analyst/` | Mary (Business Analyst) | Not assigned yet | `/bmad-brainstorming`, `/bmad-deep-recon`, `/bmad-product-brief`, `/bmad-prfaq`, `/bmad-project-context` | Exploring an idea, researching, writing a brief or PRFAQ, setting agent rules | [Analyst](../Analyst/) |
| `ProductOwner/` | John (Product Manager) | Not assigned yet | `/bmad-prd`, `/bmad-correct-course`, `/bmad-ticket` | Defining requirements, handling a mid-build change, slicing stories | [ProductOwner](../ProductOwner/) |
| `Architect/` | Winston (System Architect) | Not assigned yet | `/bmad-architecture` | Recording stack, hosting and the decisions that keep parts consistent | [Architect](../Architect/) |
| `UXDesigner/` | Sally (UX Designer) | Not assigned yet | `/bmad-ux` | Capturing how the product looks and behaves | Created by the first run |
| `Developer/` | Amelia (Senior Software Engineer) | Not assigned yet | `/bmad-build`, `/bmad-qa-generate-e2e-tests`, `/bmad-code-review`, `/bmad-retrospective` | Building a story, testing, reviewing, closing an epic | Created by the first run |
| `ScrumMaster/` | No persona | Not assigned yet | Uses `/bmad-ticket` (status, what is ready), `/bmad-retrospective`, `/bmad-correct-course` | Running the board, closing an epic, handling a mid-sprint change | Docs stay with the owning role: [ProductOwner](../ProductOwner/), [Developer](../Developer/) |
| `TeamLead/` | No persona | Not assigned yet | Uses `/bmad-code-review`, `/bmad-walkthrough`, `/bmad-review`, `/bmad-precommit` | Reviewing changes before they are committed | Docs stay with the owning role: [Developer](../Developer/), [CoreTools](../CoreTools/) |
| `BmadMethod/` | No agent | Not assigned yet | `/bmad-spec` | Folding any result into the spec | [BmadMethod](../BmadMethod/) |
| `CoreTools/` | BMad Agent, Smithy | Not assigned yet | `/bmad`, `/bmad-toolsmith`, `/bmad-precommit` | Setup, initiative, building skills, the pre-commit routine | [CoreTools](../CoreTools/) |

`/bmad-ticket` is shared by John, Winston and Amelia; its doc lives under `ProductOwner/`.

## Adding another role

Any SDLC role (QA, DevOps, Tech Writer) works the same way. Add a row to the table above with its role folder and commands. The next `/bmad-precommit` creates the folder and the numbered step doc from it. No change to the agent is needed.

## GitHub references

- [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
- [Skills and Agents (all skills)](https://docs.bmad-method.org/)
- [GitHub: bmad-architecture skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-architecture)
- [GitHub: bmad-ux skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-ux)
- [GitHub: bmad-prd skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-prd)
- [GitHub: bmad-ticket skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-ticket)
- [GitHub: bmad-build skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-build)
- [GitHub: bmad-spec skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-spec)

Each step doc lists the skill source for its own skill, plus its steps and official pages.
