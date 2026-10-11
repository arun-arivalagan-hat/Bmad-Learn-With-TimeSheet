# BMAD Market Research Guide

**BMad agent:** Mary (Business Analyst), menu option MR; skill run directly for `bmad-spec` | **Skill:** `bmad-deep-recon` (market type), `bmad-spec`

## 1. Purpose

This guide explains how to use `bmad-deep-recon` to research a topic that supports a decision, then feed the findings back into the spec through `bmad-spec`. For this repository the topic is how timesheet products engage employees to fill timesheets on time, and the decision is which engagement features go in the free vs premium tier. It produces a cited research report; it does not slice work into stories (that is `bmad-ticket`).

## 2. Prerequisites

* Step 2 complete: an active initiative exists ([02-bmad-initiative.md](../../CoreTools/Bmad/Bmad-Initiative/02-bmad-initiative.md)).
* Step 3 complete: a spec exists ([03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)).
* Step 4 recommended: the brainstorm raised the premium-tier and reminder questions the research answers ([04-bmad-brainstorm.md](../Brainstorm-BR/04-bmad-brainstorm.md)).
* A topic, a research type (here `market`) and the decision the research serves.

## 3. Run the Skill

Invoke `bmad-deep-recon` with the topic and decision, for example:

```text
Use bmad-deep-recon for market research: how timesheet products engage employees to fill timesheets on time, to decide which features go in the free vs premium tier
```

The skill proposes a plan (dimensions, number of assistants, depth, validation level), runs parallel web searches, writes a digest per search round, logs every claim to `.memlog.md`, and assembles the report. In this run the dimensions were pain points, segments and behavior, competitive landscape, and pricing.

Then re-run `bmad-spec` so the findings are merged into the spec (the spec lists the research under `sources:`).

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/research-employee-engagement-in-timesheet-filling/research-employee-engagement-in-timesheet-filling.md` | The research report: executive summary, recommendation, caveats, findings per dimension, numbered sources. |
| `_bmad-output/initiative-timesheet-management/research-employee-engagement-in-timesheet-filling/digests/` | One digest per dimension and round (competitive, pain-and-behavior, pricing); the evidence behind the report. |
| `_bmad-output/initiative-timesheet-management/research-employee-engagement-in-timesheet-filling/.memlog.md` | Running log of decisions and claims, each with a verification status. |

The re-run of `bmad-spec` also updates `spec-timesheet-management.md` (adds CAP-14 reminders, new assumptions and open questions), its `.memlog.md`, and `premium-tier.md`.

### Other research types

Each research type has its own step doc: domain research (DR) in [06-bmad-domain-research.md](../Domain-Research-DR/06-bmad-domain-research.md), technical research (TR) in [07-bmad-technical-research.md](../Technical-research-TR-TS/07-bmad-technical-research.md), and competitive research (CR) in [08-bmad-competitive-research.md](../Competitive-research-CR/08-bmad-competitive-research.md).

Market evidence is mostly vendor-sourced. Owner decisions made after the research are recorded in the spec, not here.

## 5. Verify

* The research folder exists under the initiative and holds the report, `digests/` and `.memlog.md`.
* The report frontmatter shows `status: complete` and states the decision it serves.
* The spec frontmatter lists the research path under `sources:`.
* Claims marked `unverified` in `.memlog.md` are treated as low confidence in the spec (for example competitor prices are recorded as unvalidated).
* Evidence gaps appear as spec open questions (for example whether reminders raise on-time submission needs a pilot).

## 6. Troubleshooting

* **Shared problems:** See [troubleshooting.md](../../Guide/troubleshooting.md) for an unchanged spec, thin or vendor-biased findings, or files in the wrong folder.

## Skill Folder Structure

Layout of the installed `bmad-deep-recon` skill (`.claude/skills/bmad-deep-recon/`), which mirrors its [upstream folder](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-deep-recon):

* `SKILL.md`: the entry point. Frontmatter (name, description) tells the harness when to trigger; the body holds the instructions.
* `bmod.toml`: module metadata, which module the skill belongs to and where it is sourced from on GitHub.
* `customize.toml`: the override surface; team and personal overrides live in `_bmad/custom/`, never in this file.
* `references/`: one file per intent (`draft`, `process`, `run`, `lifecycle`) plus `verification`, `synthesis`, `selection` and `finalize`; loaded only when that step is reached.
* `types/`: one research pack per type (`market`, `domain`, `technical`, `competitive`, `user-voice`, `academic-lit`).
* `assets/`: `research.template.md`, the report skeleton.
* `scripts/`: `recon_kit.py`, helper for run folders and claim logs.


## Skill Steps

Steps the skill itself runs, in order (from its `SKILL.md`):

`bmad-deep-recon` picks the research type from the ask (here: market) and routes on the intent:

1. **Draft:** compose a deep-research prompt for your own tool.
2. **Process:** file a finished report, extract its claims and distill the downstream summary.
3. **Run:** native research. Resolve effort, hold the plan gate (the one hard stop), run the search loop, then verify and synthesize.
4. **Refresh / Deepen:** update or extend an existing run folder.

Every intent ends by finalizing the run folder (`brief.md`, `imports/`, `digests/`, report, `.memlog.md`). Then `bmad-spec` folds the findings into the spec (see [03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)).

## Official References

* [Market Research](https://docs.bmad-method.org/plan/research-a-decision/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad-deep-recon` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-deep-recon)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
