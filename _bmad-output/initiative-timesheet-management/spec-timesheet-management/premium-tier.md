# Premium Tier Candidates

Sources: brainstorm-timesheet-delight; research-employee-engagement-in-timesheet-filling. Not committed scope. Owner decision 2026-10-10: everything ships free for now with no pricing; this file lists future candidates only. Evidence is mostly vendor pages, low to medium confidence.

## Free vs premium split

| Tier | Candidate | Value | Market evidence |
|---|---|---|---|
| Free | Core weekly sheet, copy-last-week, basic reminders (CAP-14), mobile, simple reports | The base contract in `spec-timesheet-management.md` | Harvest, Clockify and TimeCamp keep sheet, timer, mobile and basic reports free |
| Automation | AI week drafting from calendar, tickets and commits | Employee confirms instead of typing | TimeCamp bills AI usage (about $6 per user per month estimated cost); Deltek bundles it |
| Automation | Integrations: Jira, GitHub, Google and Outlook calendars, Slack, Teams | Log and remind where people already work; Teams uses Workflows (Power Automate) because Office 365 connector webhooks were retired in 2026 | Gated by tier or count at Toggl, TimeCamp, Harvest |
| Intelligence | Anomaly detection, forecasting, natural-language reports, scheduled manager dashboards | Catches billing leakage, plans capacity | No competitor anomaly flags found; scheduled reports sit at TimeCamp Premium |
| Intelligence | Budget alerts at 80% of a project's hours | Early warning for project leads | Not researched |
| Transparency | Audit-grade export | Finance and audit trail | Audit log is top-tier at Harvest, Clockify and TimeCamp |
| Transparency | Client portal with approved-hours statements | Fewer billing disputes | No pricing precedent found |
| Transparency | Role-based rate cards, white-label branding | Finance and client-facing polish | Billable and cost rates are mid-tier at Harvest and Toggl |

## Notes

- Competitors gate approvals at $5.49 to $16 per user per month. This spec keeps approvals (CAP-6) in the core product.
- Gamification stays opt-in and team-level; the evidence is one small study with backfire risk.
