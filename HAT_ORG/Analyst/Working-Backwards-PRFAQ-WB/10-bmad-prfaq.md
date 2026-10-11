# BMAD PRFAQ Guide

**SDLC role:** Analyst | **Team lead:** Not assigned yet | **BMad agent:** Mary (Business Analyst) | **Skill:** `bmad-prfaq`

## 1. Purpose

This guide explains how to test a concept with `bmad-prfaq`. A PRFAQ is a press release plus hard FAQs, with researched claims and a verdict, written before anything is built. It tests whether the idea survives scrutiny. In this repository it challenges the Timesheet Management brief and spec: who the real customer is, how big the pain is, and what the organisation expects from the tool. It does not replace the brief or the spec, and it does not choose technology.

## 2. Prerequisites

* Steps 1 and 2 complete: installation and an active initiative ([02-bmad-initiative.md](../../CoreTools/Bmad/Bmad-Initiative/02-bmad-initiative.md)).
* Steps 3 to 9 and 14 recommended: the spec and research (steps 3 to 9) and the brief (step 14) are its inputs ([14-bmad-product-brief.md](../Product-Brief-PB/14-bmad-product-brief.md)).
* Time to answer the coach's questions. The skill asks about the customer, the pain and the numbers, and it records the owner's answers.

## 3. Run the Skill

Ask Mary for a PRFAQ, or invoke the skill:

```text
Use bmad-prfaq to test the Timesheet Management concept, drawing on the brief, spec and research
```

The skill works in stages. It begins with an ignition stage that fixes the concept type and the primary customer, and records the owner's numbers as unverified. Later stages draft the press release, the FAQs and the verdict. In this run the document is still at stage 1 (`status: ignition`), with the press release not yet written.

Re-run it to continue from the saved stage.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/prfaq-timesheet-management/prfaq-timesheet-management.md` | The PRFAQ: frontmatter with status and stage, plus coaching notes (customer, pain, owner decisions, open questions). Later stages add the press release, FAQs and verdict. |

The skill can also write a `-distillate.md` beside it. None exists yet.

## 5. Verify

* The frontmatter shows `status`, `stage` and the `inputs` list (brief, spec, market and competitive research).
* Numbers supplied by the owner are marked as not independently verified.
* Owner decisions that change earlier documents (here, decision A: HR decides the consequences of late and wrong timesheets) are also reflected in the spec and brief. Check that they agree.
* Open questions are listed before the press release is written.

## 6. Troubleshooting

* **BMad not set up, no active initiative, or the PRFAQ contradicts the spec or brief:** See [troubleshooting.md](../../Guide/troubleshooting.md).
* **The status stays at `ignition`:** the open questions are unanswered. Answer them and re-run.

## Skill Folder Structure

Layout of the installed `bmad-prfaq` skill (`.claude/skills/bmad-prfaq/`), which mirrors its [upstream folder](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-prfaq):

* `SKILL.md`: the entry point. Frontmatter (name, description) tells the harness when to trigger; the body holds the instructions.
* `bmod.toml`: module metadata, which module the skill belongs to and where it is sourced from on GitHub.
* `customize.toml`: the override surface; team and personal overrides live in `_bmad/custom/`, never in this file.
* `references/`: one file per later stage (`press-release`, `customer-faq`, `internal-faq`, `verdict`); Ignition lives in `SKILL.md`.
* `agents/`: subagent briefs (`artifact-analyzer`, `web-researcher`) for the parallel scans.
* `assets/`: `prfaq-template.md`; `bmad-manifest.json`: manifest kept from the older skill format.


## Skill Steps

Steps the skill itself runs, in order (from its `SKILL.md`):

1. **Ignition:** raw concept, customer-first framing.
2. **The Press Release:** iterative drafting with hard coaching.
3. **Customer FAQ:** devil's-advocate customer questions.
4. **Internal FAQ:** skeptical stakeholder questions.
5. **The Verdict:** synthesis, strength assessment and the final PRFAQ.

Each stage stops for the user; the run resumes from the existing `prfaq-*.md`.

## Official References

* [PRFAQ (Working Backwards)](https://docs.bmad-method.org/plan/explore-and-validate-an-idea/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad-prfaq` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-prfaq)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
