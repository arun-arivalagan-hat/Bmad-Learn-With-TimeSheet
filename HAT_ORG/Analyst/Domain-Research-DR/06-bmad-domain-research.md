# BMAD Domain Research Guide

**BMad agent:** Mary (Business Analyst), menu option DR; skill run directly for `bmad-spec` | **Skill:** `bmad-deep-recon` (domain type), `bmad-spec`

## 1. Purpose

This guide explains how to run domain research (Mary's **DR** option) with `bmad-deep-recon`. It builds shared vocabulary, rules and value-chain knowledge for a field. For this repository there were two runs: timesheets and time billing in IT services (terms, states, rules), and India labour rules and payroll inputs for IT timesheets (retention and payroll). It produces cited reports. It is not legal advice and it does not edit the spec; `bmad-spec` merges the findings.

## 2. Prerequisites

* Step 3 complete: a spec exists ([03-bmad-spec.md](../../BmadMethod/Bmad-spec/03-bmad-spec.md)).
* Step 5 recommended: the market research ran first ([05-bmad-market-research.md](../Market-Research-MR/05-bmad-market-research.md)).
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
| `_bmad-output/initiative-timesheet-management/research-india-labour-rules-and-payroll-inputs-fo/` | Report, `digests/` (labour-rules, payroll-inputs) and `.memlog.md`; India labour and payroll evidence, medium confidence at most, secondary sources. |
| `_bmad-output/initiative-timesheet-management/spec-timesheet-management/glossary.md` | Written by `bmad-spec` after the first run: domain terms and timesheet states. |

The India run first shaped CAP-15 (payroll handoff), but the owner later retired CAP-15 and put the payroll handoff out of scope, so treat that run as background. Its retention figure (5 years) is single-source; the spec uses 3 years by owner decision.

## 5. Verify

* Each research folder holds the report, `digests/` and `.memlog.md`, and the report frontmatter shows `type: domain` and `status: complete`.
* The spec frontmatter lists the research paths under `sources:`.
* Legal points are treated as needing confirmation by legal or compliance.

## 6. Troubleshooting

* **Legal claims look unconfirmed:** The report states no official source was read; confirm with legal or compliance before relying on them.
* **Spec unchanged after the research, or files in the wrong folder:** See [troubleshooting.md](../../Guide/troubleshooting.md).
