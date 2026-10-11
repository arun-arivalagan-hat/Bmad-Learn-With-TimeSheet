# Pricing digest r1-1 (timesheet / time-tracking pricing and packaging)
Accessed 2026-10-10 for all sources. All prices USD as shown on vendor pages. Vendor pages carry no visible pub_date (live pages; treat as current at access). Fetches were summarised by a fetch tool, so numbers are single-source (vendor page only) unless stated; no corroborating second source was retrieved. Class = vendor-primary unless noted.

## Findings

1. Harvest: Free $0 (1 seat, 2 projects; time tracking, invoicing, expenses, estimates, basic reporting, Mac/iOS apps). Teams $9/seat/mo annual ($11 monthly): team reporting, billable and cost rates, accounting/payment integrations, up to 4 custom reports. Enterprise $14/seat/mo annual ($17.50 monthly): unlimited custom reports, profitability reporting, TIMESHEET APPROVAL, ACTIVITY LOG, SSO, required notes. Enterprise Plus custom. Source: https://www.getharvest.com/pricing | Harvest | pub_date n/a | conf high | vendor-primary. Note: invoicing is free; approvals and audit/activity log are top-tier gated. Reminders and client portal not mentioned on page.
2. Clockify: Free (up to 5 users per table; FAQ says 4 invited, internal conflict) includes unlimited tracking, timesheets, reports, mobile/desktop. Annual per seat/mo: Basic $3.99 ($4.99 mo), Standard $5.49 ($6.99), Pro $7.99 ($9.99), Enterprise $11.99 ($14.99), CAKE.com Bundle $12.99 ($15.99). Standard adds invoicing, time off, approvals, manager roles, QuickBooks. Pro adds scheduling, forecasting, expenses, budgets, GPS tracking. Enterprise adds SSO, SCIM, AUDIT LOG. 20% annual discount; 7-day Pro trial. Source: https://clockify.me/pricing | Clockify (CAKE.com) | n/a | conf high | vendor-primary. Note: approvals sit at the second paid rung (about $5.49); audit log top tier; bundle model.
3. Toggl Track: Free (up to ~3 users per page; tracking, calendar integrations, boards, tasks, personal reports). Starter $9 / $12 (annual vs monthly, page does not label explicitly): billable rates, team reports. Premium $16 / $24: profitability reports, TIMESHEET APPROVALS, Jira/Asana integrations, SSO. Enterprise contact sales. Add-ons per user/mo: Time Off Pro $2, Capacity Management $5 or $6. Desktop auto-tracker (Win/Mac), iOS/Android apps. Source: https://toggl.com/track/pricing/ | Toggl | n/a | conf med (billing labels ambiguous) | vendor-primary. Reminders, audit log, invoicing not clearly mapped.
4. TimeCamp: Free $0 with UNLIMITED users and projects: timesheets, timers, auto tracking, idle time, 10+ reports, mobile on all tiers. Starter $3.99 annual ($5.49 mo): invoicing, attendance/time off, overtime. Premium $6.99 ($9.99): billable time, budgets, apps/website tracking, resource planner, ONE integration, scheduled email reports. Ultimate $9.99 ($13.99): TIMESHEET APPROVALS, screenshots, expenses, billing rates, SSO, unlimited integrations. Enterprise contact sales: geofencing, kiosk, AUDIT LOG, custom reports. AI Time Tracker listed on all tiers, usage-billed (est. ~$6/user/mo token cost; $10 trial credit). Reminders not listed on any tier. Source: https://www.timecamp.com/pricing | TimeCamp | n/a | conf med-high (page structured data shows a stray "Basic $7" plan) | vendor-primary. Notable: AI auto-tracking sold as usage-based add-on; integrations gated by count.
5. Replicon (Deltek): pricing page redirects (301) to Deltek product page, which lists NO tiers or prices (demo/contact). Describes web/mobile/CloudClock capture, integrations (SAP, ADP, Jira, Costpoint), reports/dashboards, Tableau/Power BI, compliance rules (DCAA, FAR, FedRAMP, NIST). Source: https://www.deltek.com/products/replicon/ | Deltek | n/a | conf high that price is not public | vendor-primary.
6. Zoho People (HRMS): tiers Free (up to 53 users per page), Essential HR, Professional, Premium, Enterprise; paid tiers 5-user minimum; monthly vs yearly (yearly saves >20%); per-user prices not extracted by fetch. Timesheets appear at a mid-upper tier (with attendance/roster) and "Timesheets with OT compliance" under Workforce in People Plus; exact tier mapping unclear. Search snippet said plans start at $3/user (US page). Source: https://www.zoho.com/people/zohopeople-pricing.html | Zoho | n/a | conf low | vendor-primary (+ search snippet, unfetched). Timesheets treated as HRMS add-on-like upper-tier feature, not free.
7. Reviews (weak): a search returned only TimeCamp review pages (Capterra/GetApp, unfetched snippets). Summary claims: users value auto+manual tracking, reporting, integrations (Asana/Jira/Trello), client/project billing analysis; complaints: pricing high for teams, features locked behind paid, free plan restrictive. Source: https://www.capterra.com/p/129847/TimeCamp/reviews/?page=5 | Capterra | 2026 (per title) | conf low (snippet only, not read) | third-party review.

## Cross-vendor pattern (synthesis of 1-4, all vendor pages)
- Free tier always includes basic timer/timesheet/mobile; Clockify and TimeCamp give timesheets and reports free to multiple users (TimeCamp unlimited).
- Approvals gated: Clockify ~$5.49, TimeCamp $9.99, Harvest $14, Toggl $16 (annual-ish). Mid-to-top tier everywhere.
- Audit log gated to top/enterprise tier in Harvest (activity log), Clockify, TimeCamp.
- Billable/cost rates: paid mid tier (Harvest $9, Toggl $9, TimeCamp Ultimate).
- Invoicing: free in Harvest, Starter in TimeCamp, Standard in Clockify.
- Integrations: count-gated (TimeCamp) or tier-gated (Toggl Jira/Asana at Premium; Harvest accounting at Teams).
- Models seen: per seat per month with annual discount (20-33%), free tier, add-ons per user (Toggl), usage-billed AI (TimeCamp), bundle (Clockify), sales-quoted enterprise (Replicon).

## Leads worth chasing
- Zoho People per-user prices (regional pages, e.g. /in/people or pricing PDF) and Keka/Darwinbox/BambooHR timesheet module pricing.
- Reminders / nudges: verify in vendor help docs (Clockify, Toggl, Harvest "timesheet reminders") for which plan includes them.
- Client portal: Harvest/others; check help centre.
- Read Capterra/G2 reviews for Clockify, Toggl, Harvest, and Replicon for what users pay for; corroborate prices via Wayback or second source.
- Toggl exact annual vs monthly labelling; Replicon pricing via G2/Capterra listings.

## Looked for and could not find
- Reminders pricing tier on any vendor pricing page (not listed on Harvest, TimeCamp, Toggl pages as fetched).
- Client portal tier on any vendor page.
- Replicon public prices.
- Zoho People per-user prices and exact timesheet tier (the pricing page 404'd on two URLs; third was ambiguous).
- Independent (non-vendor) analyses of willingness to pay; only a thin TimeCamp-centric review snippet.
- Second corroborating source for any price (not done within budget; ~13 calls used).
