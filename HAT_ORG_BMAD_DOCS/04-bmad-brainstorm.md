# BMAD Brainstorm Guide

**BMad agent:** Mary (Business Analyst) for `bmad-brainstorming`; skill run directly for `bmad-spec` | **Skill:** `bmad-brainstorming`, `bmad-spec`

## 1. Purpose

This guide explains how to use `bmad-brainstorming` to generate and converge ideas for an initiative, then feed the result back into the spec through `bmad-spec`. It produces an intent document and a premium-tier companion; it does not slice work into stories (that is `bmad-ticket`).

## 2. Prerequisites

* Step 2 complete: an active initiative exists ([02-bmad-initiative.md](02-bmad-initiative.md)).
* Step 3 complete: a first spec exists ([03-bmad-spec.md](03-bmad-spec.md)), so the brainstorm can answer its open questions.
* A topic and goal, for example: "a timesheet people finish on time and enjoy, plus approval and billing flows".

## 3. Run the Skill

Invoke `bmad-brainstorming` with the topic and goal, for example:

```text
Use bmad-brainstorming for Timesheet Management: make timesheets delightful so users submit on time, include premium-tier ideas
```

The skill runs techniques (for example Anti-Solution), logs every idea to `.memlog.md`, converges on chosen directions, and writes the intent document and an HTML view.

Then re-run `bmad-spec` so the chosen directions are merged into the spec (the spec lists the brainstorm under `sources:` and `premium-tier.md` under `companions:`).

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/brainstorm-timesheet-delight/brainstorm-timesheet-delight.md` | Intent document: goal, core insight, six chosen directions, premium tier candidates, open decisions, out of scope. |
| `_bmad-output/initiative-timesheet-management/brainstorm-timesheet-delight/brainstorm.html` | HTML view of the brainstorm for sharing. |
| `_bmad-output/initiative-timesheet-management/brainstorm-timesheet-delight/.memlog.md` | Running log of every idea and technique the document is derived from. |
| `_bmad-output/initiative-timesheet-management/spec-timesheet-management/premium-tier.md` | Spec companion: premium tier candidates (not committed scope). |

The re-run of `bmad-spec` also updates `spec-timesheet-management.md` (now CAP-1 to CAP-13) and its `.memlog.md`.

## 5. Verify

* The brainstorm folder exists under the initiative and holds the three files above.
* The spec frontmatter has `companions: [premium-tier.md]` and the brainstorm path under `sources:`.
* Each "Open decision" in the intent document is either answered in the spec (for example the billable flag lives on the project) or left as a recorded open question.
* New capabilities (CAP-8 to CAP-13) have an intent and a success condition; those marked `proposed` need confirmation.

## 6. Troubleshooting

* **Spec did not change after the brainstorm:** Brainstorming does not edit the spec. Re-run `bmad-spec` with the brainstorm as input.
* **Ideas feel too broad:** Treat `premium-tier.md` as candidates only; keep committed scope in the spec's capabilities and non-goals.
* **Skills write to `_bmad-output/` root:** No initiative is active. Ask `bmad` to set it.
