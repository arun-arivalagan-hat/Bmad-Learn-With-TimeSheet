# BMAD Technical Research Guide

**BMad agent:** Mary (Business Analyst), menu option TR | **Skill:** `bmad-deep-recon` (technical type), then `bmad-spec`

## 1. Purpose

This guide explains how to run technical research (Mary's **TR** option) with `bmad-deep-recon`. It surveys how a feature is built in practice: integration patterns, architecture patterns, and implementation options. For this repository the topic is the technical approach for a timesheet module inside an HRMS, and the decision is which integration, approval and audit, and notification approaches to use. It produces a cited report with options and trade-offs. It does not pick a stack (that is the architecture step) and it does not edit the spec.

## 2. Prerequisites

* Steps 1 to 3 complete: installation, an active initiative and a spec ([03-bmad-spec.md](03-bmad-spec.md)).
* Steps 5 and 6 helpful: the market and domain research set the scope ([05-bmad-market-research.md](05-bmad-market-research.md), [06-bmad-domain-research.md](06-bmad-domain-research.md)).
* A topic, the decision it serves, and any known constraints (here: the existing HRMS stack was unknown, so options are general).

## 3. Run the Skill

Ask Mary for **TR**, or invoke `bmad-deep-recon` with the technical type:

```text
Use bmad-deep-recon for technical research: technical approach for a timesheet module inside an HRMS, to decide integration, approval and audit, and notification patterns
```

The skill proposes a plan (dimensions, number of assistants, depth, freshness and two-source rules), waits for approval, runs parallel web searches, writes a digest per assistant, and assembles the report. In this run the dimensions were integration, architecture patterns, and implementation reality, with one assistant each.

Then re-run `bmad-spec` so the module-relevant findings merge into the spec. Findings about infrastructure (stack, hosting, observability, backups, CI/CD) were declared out of scope for the spec and belong to `bmad-architecture`.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/research-timesheet-module-technical-approach-insi/research-timesheet-module-technical-approach-insi.md` | The report: executive summary, options per dimension, recommendations for the architecture step, numbered sources and a staleness map. |
| `_bmad-output/initiative-timesheet-management/research-timesheet-module-technical-approach-insi/digests/` | One digest per assistant: `integration-r1-1.md`, `patterns-r1-1.md`, `stack-deployment-r1-1.md`. |
| `_bmad-output/initiative-timesheet-management/research-timesheet-module-technical-approach-insi/.memlog.md` | Decisions and claims, each with a verification status. |

What reached the spec: a reminder constraint (UTC, at most once per employee, reminder kind and week) and a Teams note in `premium-tier.md`. The report also records the owner decisions that infrastructure and the payroll handoff are out of scope.

## 5. Verify

* The report frontmatter shows `status: complete` and the decision it serves.
* Version and compatibility claims carry a re-check date in the staleness map (about one month), so re-check them before building.
* Gaps are listed (email provider limits, observability, backups, CI/CD, hiring data), not hidden.
* The spec lists the report under `sources:`.

## 6. Troubleshooting

* **The report names no winner:** that is intended. It gives options with trade-offs; decide in `bmad-architecture`.
* **Claims look weak:** most are vendor docs or search summaries. Treat low-confidence claims as leads.
* **The spec did not change:** research does not edit the spec. Re-run `bmad-spec` with the report as input.
