---
title: Product Brief: Timesheet Management
status: final
created: 2026-10-10
updated: 2026-10-11
---

# Product Brief: Timesheet Management

*Written for people in the organisation who are not developers. It explains what we are building and why, in plain words.*

## Executive Summary

Every week, employees report what they worked on using the HAT timesheet form (our current weekly form). Today that form is not connected to billing or to how busy each person is, so decisions about billing clients and planning people's time rest on plans, not on the hours actually worked.

Timesheet Management is a weekly timesheet inside our HR system. Each week the sheet is published for employees, they record the hours they spent on each of their projects, the project reviewer approves or sends it back, and finance and managers can then read the approved hours per project without anyone re-typing them.

The aim is simple: **track the work of every employee every week, accurately and with little effort, and tie those hours to billing and to how people's time is used.** The tool should also be quick and pleasant enough that people submit on time without being chased.

## The Problem

- Employees fill in the weekly form, but the hours are not tied to billing or utilisation (how much of people's time goes to billable work). Billing and resourcing decisions rest on plans, not on real hours.
- Reviewing and approving hours is slow and unclear, and project managers spend about 19 hours a week chasing and collecting hours (owner's figure, not yet verified). When approval is late, billing is late, and money can be lost between work done and work billed.
- Timesheets are widely disliked as busywork. People forget them, enter them late, or fill them from memory.
- Corrections after the fact are risky: if approved hours can be changed quietly, billed numbers stop being trustworthy.

## The Solution

A weekly timesheet that works like this:

1. **The sheet is published.** Each week runs Monday to Monday, India time. After the Friday 12:00 PM IST cut-off, the owner of the employee's main project (Project 1, taken from the HR system) or a delegate named for that week publishes it. If they have not, HR can publish it, and the owner, any delegate and HR are reminded.
2. **The employee fills it in.** They log hours on up to five projects (only Project 1 is required), in half-hour steps, with what they worked on, plus time off, key accomplishments, and what they learned (Beginner, Intermediate or Advanced). Project hours plus time off cannot exceed 40 hours a week. Name, email and each project's reviewer fill in from the HR system.
3. **Deadline.** The sheet is due 24 hours after it is published, and that is never shortened. A late sheet is still accepted but gets a **late mark**, based only on the first submission. The employee, their reviewer, their reporting manager and HR can see it; the project owner sees only "on time" or "late". An approved extension request removes the mark, and the original stays in the history.
4. **Review.** Each project's reviewer approves or rejects the hours for their own project, giving a reason when rejecting. Only the rejected project returns to the employee, and the sheet is approved when every project is approved. Nobody approves their own hours: the reporting manager steps in first, then a delivery manager.
5. **Locked.** Once approved, the hours are locked. A later mistake is fixed by a dated correction with a reason, recorded by the reviewer (or an eligible alternate) on top of the original, which stays visible. HR never records a correction.
6. **Used.** Approved hours roll up by project, person and week into billable and non-billable time, so billing and managers read the same numbers.

**Special cases**
- A week fully covered by approved leave needs no sheet: no submission, no late mark, no reminder.
- A sheet that was never published cannot be marked late.
- If a reviewer is inactive or on leave, an alternate is used. If nobody is eligible, the review goes to an HR queue, where HR assigns an alternate but never decides.
- Reviewers see only their own project's hours plus the total.
- If the HR system's data cannot be checked at that moment, the tool refuses the action and asks the person to try again, rather than guessing.

**Small things that make it easy to finish**
- Copy last week's sheet.
- Reminders: at most one of each kind per person per week, none for people on approved leave.
- A check that flags unusual sheets, so reviewers can approve clean ones in bulk.
- A short smiley rating after submitting, so we learn how it feels.

## What Makes This Different

We looked at products such as Harvest, Clockify, Toggl, BambooHR, Rippling and Keka. Our version is not a new idea; it is built to fit our own process. What is distinctive:

- It sits **inside our HR system**, so names, projects and reviewers come from the data we already have.
- Approvals, locking and corrections are part of the basic product, where many competitors charge extra for approvals.
- Late marks and approved hours are visible to **HR, who decides any consequences**, so the record has to be accurate and fair. The tool itself never changes anyone's pay, and there are no public rankings or shaming lists.

We are not claiming a technical advantage. The advantage is fit and simplicity. [ASSUMPTION: no further differentiator beyond fit to our process.]

## Who This Serves

- **Employees** (the people who fill it in): want it quick, forgiving, and not used against them.
- **Project reviewers**: want to see only the sheets for their projects, understand them at a glance, and give a clear reason when they reject one.
- **Project owners**: publish each week's sheet and see who has submitted.
- **Reporting managers and delivery managers**: see their direct reports' sheets read-only, and step in to approve when a reviewer cannot.
- **Finance and managers**: need trusted, approved hours per project for billing and planning.
- **HR**: reads approved hours and late marks, read-only, decides any consequences for employees, publishes a sheet when the owner has not, and assigns an alternate when no reviewer is available.

## Success Criteria

- An employee can complete and submit a full weekly sheet in **one sitting**.
- Billing can read a week's **approved hours per project without re-typing anything**.
- Most sheets are submitted by the deadline. The owner has set no target for now; we measure the on-time share from launch.
- Employees report that the process feels fine, measured by the trend in the smiley rating. No target for now.
- Project managers spend far less time collecting hours than today.
- Approved hours never change silently after approval.

**Watch-outs:** the late-mark rate and the rejection rate, so the tool does not push people to rush or reviewers to reject by habit.

## Scope

**In the first version**
- Weekly sheet with up to five projects, time off, accomplishments and learnings.
- Publishing of the sheet by the Project 1 owner or a delegate (or HR after the cut-off), a 24-hour deadline, late marks, and extension requests.
- Approval or rejection per project by the project reviewer, a fallback chain and HR queue when no reviewer is available, locking after approval, and recorded corrections.
- Copy last week, reminders, the smiley rating, and a private weekly view of your own hours by project.
- Roll-up of approved hours by project, person and week into billable and non-billable time.
- Free to use: all capabilities ship free for now, with no pricing.

**Not in the first version**
- Payroll: pay calculation, loss-of-pay days, and any handover to payroll.
- Invoicing: we supply billable hours, not invoices.
- Attendance and clock-in tracking.
- Automatic drafting of the sheet from calendar or tickets (a possible later addition).
- Technology choices such as hosting and email service: these are decided separately by the technical team.

**Rules to know**
- One sheet per employee per week.
- Sized for 160 employees and 20 projects (confirmed by the owner).
- Records are kept for three years. This is a generic rule with no legal review for our country; the owner accepts the risk.

## Still Open

Decisions not yet made: whether a waived late mark counts as on time in the on-time measure, how long a grace period lasts after an HR system outage, and whether the 40-hour cap applies to later corrections. Reminder timing, the escalation wait and the "unusual sheet" threshold are working defaults, not final. The addendum lists them with values, and the spec and PRD track the full list.

## Vision

If this works, timesheets stop being a chore and become the single trusted record of where our people's time goes. Later versions could draft the week automatically from calendars and tickets, connect to tools people already use, offer manager dashboards and a client view of approved hours, and show each person a private summary of their work and what they learned. These are options for later, not promises.
