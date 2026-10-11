# BMAD User-Voice Research Guide

**SDLC role:** Analyst | **Team lead:** Not assigned yet | **BMad agent:** Mary (Business Analyst), menu option UV | **Skill:** `bmad-deep-recon` (user-voice type), then `bmad-spec`

## 1. Purpose

This guide explains how to run user-voice research (Mary's **UV** option) with `bmad-deep-recon`. It collects what real users say in public places (forums, communities, comment threads) about a task or product: who they are, what they complain about, how they work around it, and the words they use. For this repository the question is whether the pain claims behind the timesheet module hold up outside one organisation. It produces a cited report. It does not survey your own staff, and it does not edit the spec.

## 2. Prerequisites

* Steps 1 to 3 complete: installation, an active initiative and a spec ([03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)).
* Recommended: the market and competitive research, so this run adds the users' own words to the vendor view ([06-bmad-market-research.md](../Market-Research-MR/06-bmad-market-research.md), [08-bmad-competitive-research.md](../Competitive-research-CR/08-bmad-competitive-research.md)).
* The user groups and the decision the research serves.

## 3. Run the Skill

Ask Mary for **UV**, or invoke `bmad-deep-recon` with the user-voice type:

```text
Use bmad-deep-recon for user-voice research: what employees, project managers and HR say about weekly timesheets
```

The skill proposes a plan, waits for approval, runs one assistant per user group in parallel (in this run: employees, project managers and approvers, HR and appraisal), and assembles a report. A second round (depth 2) can follow up gaps; this run added one round-2 digest on open APIs.

Then re-run `bmad-spec` so findings that change a decision reach the spec. In this run the research found a self-approval gap (a project manager approving their own timesheet). The owner decided that no one approves their own timesheet, and the spec gained CAP-21 (see [03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)). The other findings (reminders, copy-hours, softer late marks) needed no spec change.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/research-user-voice-timesheets-employees-managers/research-user-voice-timesheets-employees-managers.md` | The report: who the users are, complaints and workarounds, appraisal and penalty talk, their language, recommendations, owner decisions, sources and staleness map. |
| `_bmad-output/initiative-timesheet-management/research-user-voice-timesheets-employees-managers/digests/` | One digest per user group and round: `employees-r1-1.md`, `project-managers-r1-1.md`, `hr-appraisal-r1-1.md`, `open-apis-r2-1.md`. |
| `_bmad-output/initiative-timesheet-management/research-user-voice-timesheets-employees-managers/.memlog.md` | Decisions and claims, each with a verification status. |

## 5. Verify

* The report frontmatter shows `type: user-voice` and `status: complete`, and the decision it serves.
* Quotes are short and redacted: no usernames, handles or identifying links.
* Prevalence claims rest on two independent communities; single-community claims are marked.
* The report says what did not hold up (here, the 19-hours-a-week figure is neither supported nor contradicted) and which sources were blocked.
* Sentiment is at most about 18 months old, or marked stale in the staleness map.

## 6. Troubleshooting

* **Sources were blocked or empty:** several review and community sites block automated reads. The report says so and marks the evidence thin; do not read absence as agreement.
* **Evidence is small or single-community:** treat it as a lead. Measure inside your organisation before quoting a number in a press release.
* **Vendor marketing mixed in:** the run excludes it from user voice; check that quoted words come from users, not vendors.
* **Spec unchanged after the research:** See [troubleshooting.md](../../Guide/troubleshooting.md).

## Skill Folder Structure

Layout of the installed `bmad-deep-recon` skill (`.claude/skills/bmad-deep-recon/`), which mirrors its [upstream folder](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-deep-recon):

* `SKILL.md`: the entry point. Frontmatter (name, description) tells the harness when to trigger; the body holds the instructions.
* `bmod.toml`: module metadata, which module the skill belongs to and where it is sourced from on GitHub.
* `customize.toml`: the override surface; team and personal overrides live in `_bmad/custom/`, never in this file.
* `references/`: one file per intent (`draft`, `process`, `run`, `lifecycle`) plus `verification`, `synthesis`, `selection`, `finalize` and `html-briefing`; loaded only when that step is reached.
* `types/`: one research pack per type; this guide uses `user-voice.md` (dimensions: jobs, complaints and workarounds, delight and switching, unmet needs, their language).
* `assets/`: `research.template.md`, the report skeleton.
* `scripts/`: `recon_kit.py`, helper for run folders and claim logs.

## Skill Steps

Steps the skill itself runs, in order (from its `SKILL.md`):

`bmad-deep-recon` picks the research type from the ask (here: user-voice) and routes on the intent:

1. **Draft:** compose a deep-research prompt for your own tool.
2. **Process:** file a finished report, extract its claims and distill the downstream summary.
3. **Run:** native research. Resolve effort, hold the plan gate (the one hard stop), run the search loop, then verify and synthesize.
4. **Refresh / Deepen:** update or extend an existing run folder.

Every intent ends by finalizing the run folder. Then `bmad-spec` folds the findings into the spec (see [03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)).

## Official References

* [User Voice Research](https://docs.bmad-method.org/plan/research-a-decision/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad-deep-recon` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad-deep-recon)
* [GitHub: BMAD-METHOD repository](https://github.com/bmad-code-org/BMAD-METHOD)
