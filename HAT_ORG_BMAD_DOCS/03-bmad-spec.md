# BMAD Spec Guide

**BMad agent:** Skill run directly | **Skill:** `bmad-spec`

## 1. Purpose

This guide explains how to use `bmad-spec`, the hub skill that distills any input (a form, notes, an objective) into the **spec**: the contract that later planning and build steps read. It does not slice work into stories; that is `bmad-ticket`.

## 2. Prerequisites

* Step 2 complete: an active initiative exists ([02-bmad-initiative.md](02-bmad-initiative.md)).
* Source input: for this repository, the HAT timesheet form plus the objective "capture actual work effort and link it to billing/utilization".

## 3. Run the Skill

Invoke `bmad-spec` and supply the input, for example:

```text
Use bmad-spec to create a spec for Timesheet Management from this form and objective: ...
```

The skill appends findings to a running log (`.memlog.md`) and re-derives the spec from it, so you can re-run it later with new material (PRD, UX, architecture, prototype notes) and the spec is updated rather than hand-merged.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/spec-timesheet-management/spec-timesheet-management.md` | The spec: Why, Capabilities (CAP-1 to CAP-13), Constraints, Non-goals, Success signal, Assumptions. |
| `_bmad-output/initiative-timesheet-management/spec-timesheet-management/.memlog.md` | Running log of decisions, capabilities, constraints, assumptions and open questions the spec is derived from. |
| `_bmad-output/initiative-timesheet-management/spec-timesheet-management/premium-tier.md` | Companion added after the brainstorm ([04-bmad-brainstorm.md](04-bmad-brainstorm.md)): premium tier candidates, not committed scope. |

After the brainstorm re-run the spec has CAP-1 to CAP-13 (CAP-8 to CAP-13 added), and the billable-flag and identity-source questions below are answered as constraints.

## 5. Review the Spec

* Each capability has an **intent** and a **success** condition.
* Capabilities marked `proposed, unconfirmed` (CAP-6 reviewer approval, CAP-7 billing and utilization roll-up) need your confirmation or removal.
* Read **Assumptions** (for example: only Project 1 required, 0.5-hour steps, 40-hour weekly cap) and correct any that are wrong.
* Open questions in `.memlog.md` (source of project and reviewer lists, tech stack, where the billable flag lives, resubmission rules) should be answered and fed back through `bmad-spec`.

## 6. Troubleshooting

* **Spec is too thin:** `bmad-spec` distills and does not coach. For vague input use `bmad-product-brief` or `bmad-prd` first, then feed the result to `bmad-spec`.
* **Memlog fails to parse:** Frontmatter values containing a colon must be quoted.
* **Requirements changed later:** Re-run `bmad-spec` with the new input instead of editing the spec by hand.

