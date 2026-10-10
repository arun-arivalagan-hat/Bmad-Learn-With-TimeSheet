# Intent: A Timesheet People Finish On Time and Enjoy

Source: brainstorm session of 159 ideas (`.memlog.md` in this folder). Initiative: Timesheet Management.

## Goal

Make the weekly timesheet quick and pleasant enough that people submit on time without being chased, and make approval and billing fast and trusted. Offer a premium tier that sells automation, not extra form fields.

## Core insight

Removing effort beats reminding people. Reviewer speed and clarity drive an on-time culture. Hours are for billing and resourcing, never a performance score.

## Chosen directions

1. **Auto-drafted week.** The system prefills the sheet from last week, calendar, tickets and commits. The employee reviews and confirms. Also: copy last week, autosave drafts, live validation in plain words.
2. **Kind deadline recovery.** A Friday wrap-up screen, a panic mode showing only what is missing, a grace window, and a one-tap late submit or extension request with a reason. No shaming.
3. **Exceptions-based approval (extends CAP-6).** Reviewers see flagged sheets first (for example a 60-hour week, hours on a closed project, a big jump from last week). Clean sheets are approved in bulk. A rejection requires a reason and shows what changed, with a one-click fix and resubmit.
4. **Locked approved snapshots (extends CAP-7).** Approved hours are frozen so billed numbers never change silently. Finance gets a live billable vs non-billable view and an audit-ready billing feed.
5. **Team kudos, not leaderboards.** Private nudges, quiet on-time streaks, opt-in milestones, and a team-level on-time rate. No public individual rankings.
6. **Personal value.** A weekly insight card, and learnings (Beginner, Intermediate, Advanced) that build a personal skill log and a quarter-end highlights summary. Learnings stay private unless shared.

## Premium tier candidates

- **Free:** the core sheet, reminders, simple reports.
- **Automation:** AI week drafting, integrations (Jira, GitHub, Google and Outlook calendars, Slack, Teams).
- **Intelligence:** anomaly detection, forecasting, natural-language reports, scheduled manager dashboards, budget alerts at 80% of project hours.
- **Transparency:** client portal with approved-hours statements, role-based rate cards, white-label branding.

## Open decisions for the spec

- Is auto-drafting in scope, and which sources feed it?
- Where does the billable flag live: project, employee or timesheet line?
- Can a submitted sheet be reopened or resubmitted, and how is the change history kept?
- Where do identity, project lists and reviewer lists come from?
- How is "happy" measured beyond on-time rate?

## Out of scope for now

Ambient time capture, an hours marketplace, and a continuous rolling week. These are interesting but premature.

## Owner decisions (2026-10-10)

- Auto-drafting is out of v1; copy-last-week is in. All capabilities ship free for now, so the premium tier is future only.
- The billable flag lives on the project. A submitted sheet can be reopened before approval, with a change history. One sheet per employee per week.
- The owner of the employee's Project 1 publishes the weekly sheet in the app, usually on Friday. It must be submitted by 11:59 pm UTC on the day after publication (Saturday); later sheets are accepted and marked late. The project reviewer then approves or rejects.
- Identity, project and reviewer lists come from the existing HRMS. A one-tap smiley after submit measures happiness.
- The owner holds that reminders and copy-last-week raise on-time submission. This is a belief to measure.
- The payroll handoff and ambient time capture are out of scope.
- Late sheets are accepted but carry a late penalty (a recorded late mark visible to the project reviewer, never affecting pay). This replaces the earlier no-penalty idea in direction 2, while keeping the kind recovery path.
