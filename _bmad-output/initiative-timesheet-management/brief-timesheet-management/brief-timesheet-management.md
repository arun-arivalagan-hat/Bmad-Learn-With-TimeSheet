---
title: Product Brief: Timesheet Management
status: draft
created: 2026-10-10
updated: 2026-10-10
---

# Product Brief: Timesheet Management

*Written for people in the organisation who are not developers. It explains what we are building and why, in plain words.*

## Executive Summary

Every week, employees report what they worked on using the HAT timesheet form. Today that form is not connected to billing or to how busy each person is, so decisions about billing clients and planning people's time rest on plans, not on the hours actually worked.

Timesheet Management is a weekly timesheet inside our HR system. Each week the sheet is opened for employees, they record the hours they spent on each of their projects, the project reviewer approves or sends it back, and finance and managers can then read the approved hours per project without anyone re-typing them.

The aim is simple: **track the work of every employee every week, accurately and with little effort, and tie those hours to billing and to how people's time is used.** The tool should also be quick and pleasant enough that people submit on time without being chased.

## The Problem

- Employees fill in the weekly form, but the hours are not tied to billing or utilisation (how much of people's time goes to billable work). Billing and resourcing decisions rest on plans, not on real hours.
- Reviewing and approving hours is slow and unclear. When approval is late, billing is late, and money can be lost between work done and work billed.
- Timesheets are widely disliked as busywork. People forget them, enter them late, or fill them from memory.
- Corrections after the fact are risky: if approved hours can be changed quietly, billed numbers stop being trustworthy.

## The Solution

A weekly timesheet that works like this:

1. **The sheet is opened.** The owner of an employee's main project (Project 1) opens the week's sheet in the app, usually on Friday.
2. **The employee fills it in.** They log hours on up to five projects, with what they worked on and who reviews it, plus time off (8 hours per day), their key accomplishments, and what they learned (marked Beginner, Intermediate or Advanced). Their name and email fill in automatically.
3. **Deadline.** The sheet is due by 11:59 pm UTC the day after it opens (Saturday for a Friday opening). A late sheet is still accepted but gets a **late mark**, which the employee, the reviewer and HR can see. A sheet that was never opened cannot be marked late.
4. **Review.** The named project reviewer approves the hours or rejects them with a reason. A rejected sheet returns to the employee to fix and resubmit.
5. **Locked.** Once approved, the hours are locked. If a mistake is found later, it is fixed with a recorded correction, never a silent edit.
6. **Used.** Approved hours roll up by project, person and week into billable and non-billable time, so billing and managers read the same numbers.

Small things make it easy to finish: copy last week's sheet, reminders for employees and for reviewers, and a quick smiley rating after submitting so we learn how it feels.

## What Makes This Different

We looked at products such as Harvest, Clockify, Toggl, BambooHR, Rippling and Keka. Our version is not a new idea; it is built to fit our own process. What is distinctive:

- It sits **inside our HR system**, so names, projects and reviewers come from the data we already have.
- Approvals, locking and corrections are part of the basic product, where many competitors charge extra for approvals.
- Late marks and approved hours are visible to **HR, who decides any consequences**, so the record has to be accurate and fair. The tool itself never changes anyone's pay, and there are no public rankings or shaming lists.

We are not claiming a technical advantage. The advantage is fit and simplicity. [ASSUMPTION: no further differentiator beyond fit to our process.]

## Who This Serves

- **Employees** (the people who fill it in): want it quick, forgiving, and not used against them.
- **Project reviewers**: want to see only the sheets for their projects, understand them at a glance, and give a clear reason when they reject one.
- **Project owners**: open each week's sheet and see who has submitted.
- **Finance and managers**: need trusted, approved hours per project for billing and planning.
- **HR**: reads approved hours and late marks, read-only, and decides any consequences for employees.

[ASSUMPTION: the number of employees and projects is not known. The tool is sized for hundreds to a few thousand users.]

## Success Criteria

- An employee can complete and submit a full weekly sheet in **one sitting**.
- Billing can read a week's **approved hours per project without re-typing anything**.
- Most sheets are submitted by the deadline. [ASSUMPTION: no target yet. We will measure the on-time rate from launch and set a target after the first weeks.]
- Employees report that the process feels fine, measured by the smiley rating after submit. [ASSUMPTION: no target yet.]
- Approved hours never change silently after approval.

## Scope

**In the first version**
- Weekly sheet with up to five projects, time off, accomplishments and learnings.
- Opening of the sheet by the Project 1 owner, a deadline, and late marks.
- Approval or rejection with a reason by the project reviewer, locking after approval, and recorded corrections.
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
- Records are kept at least three years. [ASSUMPTION: a generic rule; confirm for our country.]

## Vision

If this works, timesheets stop being a chore and become the single trusted record of where our people's time goes. Later versions could draft the week automatically from calendars and tickets, connect to tools people already use, offer manager dashboards and a client view of approved hours, and show each person a private summary of their work and what they learned. These are options for later, not promises.
