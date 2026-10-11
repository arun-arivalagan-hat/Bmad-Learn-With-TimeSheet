# BMAD Domain Research Guide

**SDLC role:** Analyst | **Team lead:** Not assigned yet | **BMad agent:** Mary (Business Analyst), menu option DR; skill run directly for `bmad-spec` | **Skill:** `bmad-deep-recon` (domain type), `bmad-spec`

## 1. Purpose

This guide explains how to run domain research (Mary's **DR** option) with `bmad-deep-recon`. It builds shared vocabulary, rules and value-chain knowledge for a field. For this repository there were two runs: timesheets and time billing in IT services (terms, states, rules), and India labour rules and payroll inputs for IT timesheets (retention and payroll). It produces cited reports. It is not legal advice and it does not edit the spec; `bmad-spec` merges the findings.

## 2. Prerequisites

* Step 3 complete: a spec exists ([03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)).
* No earlier research step is needed. Market research (MR) follows in [06-bmad-market-research.md](../Market-Research-MR/06-bmad-market-research.md).
* A domain topic and the decision it serves.

## 3. Run the Skill

Ask Mary for **DR**, or invoke `bmad-deep-recon` with the domain type, for example:

```text
Use bmad-deep-recon for domain research: timesheet and time billing domain in IT services, to define terms, states and rules
```

Then re-run `bmad-spec` so the findings are merged into the spec and its glossary.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/research-timesheet-and-time-billing-domain-in-it/` | Report, `digests/` (glossary, rules, value-chain) and `.memlog.md`; domain evidence, vendor-sourced and US-default. |
| `_bmad-output/initiative-timesheet-management/research-india-labour-rules-and-payroll-inputs-domain/` | Report, `digests/` (labour-rules, payroll-inputs) and `.memlog.md`; India labour and payroll evidence, medium confidence at most, secondary sources. |
| `_bmad-output/initiative-timesheet-management/spec-timesheet-management/glossary.md` | Written by `bmad-spec` after the first run: domain terms and timesheet states. |

The India run first shaped CAP-15 (payroll handoff), but the owner later retired CAP-15 and put the payroll handoff out of scope, so treat that run as background. Its retention figure (5 years) is single-source; the spec uses 3 years by owner decision.

## 5. Verify

* Each research folder holds the report, `digests/` and `.memlog.md`, and the report frontmatter shows `type: domain` and `status: complete`.
* The spec frontmatter lists the research paths under `sources:`.
* Legal points are treated as needing confirmation by legal or compliance.

## 6. Troubleshooting

* **Legal claims look unconfirmed:** The report states no official source was read; confirm with legal or compliance before relying on them.
* **Spec unchanged after the research, or files in the wrong folder:** See [troubleshooting.md](../../Guide/troubleshooting.md).

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

`bmad-deep-recon` picks the research type from the ask (here: domain) and routes on the intent:

1. **Draft:** compose a deep-research prompt for your own tool.
2. **Process:** file a finished report, extract its claims and distill the downstream summary.
3. **Run:** native research. Resolve effort, hold the plan gate (the one hard stop), run the search loop, then verify and synthesize.
4. **Refresh / Deepen:** update or extend an existing run folder.

Every intent ends by finalizing the run folder (`brief.md`, `imports/`, `digests/`, report, `.memlog.md`). Then `bmad-spec` folds the findings into the spec (see [03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)).

## Official References

* [Domain Research](https://docs.bmad-method.org/plan/research-a-decision/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad-deep-recon` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-deep-recon)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
