# BMAD Competitive Research Guide

**SDLC role:** Analyst | **Team lead:** Not assigned yet | **BMad agent:** Mary (Business Analyst), menu option CR | **Skill:** `bmad-deep-recon` (competitive type), then `bmad-spec`

## 1. Purpose

This guide explains how to run competitive research (Mary's **CR** option) with `bmad-deep-recon`. It is a teardown of specific, named competitors: what they ship, how they price it, and what their users say. Surveying an unnamed market is the market type (MR). For this repository the competitors are BambooHR, Rippling and Keka, and the decision is which timesheet engagement features HRMS suites include and at which tier. It produces a cited comparison. It does not choose your pricing, and it does not edit the spec.

## 2. Prerequisites

* Steps 1 to 3 complete: installation, an active initiative and a spec ([03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)).
* Step 6 recommended: the market research covered standalone trackers, so this run compares HRMS suites against it ([06-bmad-market-research.md](../Market-Research-MR/06-bmad-market-research.md)).
* The named competitors and the decision the teardown serves.

## 3. Run the Skill

Ask Mary for **CR**, or invoke `bmad-deep-recon` with the competitive type:

```text
Use bmad-deep-recon for competitive research: timesheet capabilities of BambooHR, Rippling and Keka, to see which engagement features they include and at which tier
```

The skill proposes a plan, waits for approval, runs one assistant per competitor in parallel, and assembles a report with a feature comparison table. In this run the dimensions were feature teardown, pricing and packaging, and customer voice.

Then re-run `bmad-spec` so findings that change a decision reach the spec. In this run it informed the late penalty: Keka lists late-submission penalties, and the owner chose to add a late mark that never affects pay.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/research-bamboohr-rippling-keka-timesheet-teardow-competitive/research-bamboohr-rippling-keka-timesheet-teardow.md` | The report: feature table per competitor, pricing and packaging, customer voice, recommendations, numbered sources. |
| `_bmad-output/initiative-timesheet-management/research-bamboohr-rippling-keka-timesheet-teardow-competitive/digests/` | One digest per competitor: `bamboohr-r1-1.md`, `rippling-r1-1.md`, `keka-r1-1.md`. |
| `_bmad-output/initiative-timesheet-management/research-bamboohr-rippling-keka-timesheet-teardow-competitive/.memlog.md` | Decisions and claims, each with a verification status. |

## 5. Verify

* The report frontmatter shows `status: complete` and the decision it serves.
* Each capability claim shows its sources and confidence; single-source claims are marked.
* Pricing and feature claims carry a re-check date (about three months).
* The spec lists the report under `sources:`, and the competitor open question is closed.

## 6. Troubleshooting

* **Help pages were behind a login:** the report marks such claims medium or low confidence. Treat them as leads and check with a trial account if a decision depends on them.
* **All prices are quote-only:** that is a finding, not a failure. Do not anchor a price on estimates from third parties.
* **Vendor comparison pages overclaim:** the run checks capabilities against help documentation where it can.

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

`bmad-deep-recon` picks the research type from the ask (here: competitive) and routes on the intent:

1. **Draft:** compose a deep-research prompt for your own tool.
2. **Process:** file a finished report, extract its claims and distill the downstream summary.
3. **Run:** native research. Resolve effort, hold the plan gate (the one hard stop), run the search loop, then verify and synthesize.
4. **Refresh / Deepen:** update or extend an existing run folder.

Every intent ends by finalizing the run folder (`brief.md`, `imports/`, `digests/`, report, `.memlog.md`). Then `bmad-spec` folds the findings into the spec (see [03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)).

## Official References

* [Competitive Research](https://docs.bmad-method.org/plan/research-a-decision/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad-deep-recon` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-deep-recon)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
