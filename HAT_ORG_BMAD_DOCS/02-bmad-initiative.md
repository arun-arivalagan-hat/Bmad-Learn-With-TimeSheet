# BMAD Initiative Guide

## 1. Purpose

This guide explains how to create a BMAD **initiative**: the named folder under `_bmad-output/` that groups every document for one body of work (spec, tickets, and later UX or architecture files). Later skills (`bmad-spec`, `bmad-ticket`, `bmad-build`) read and write inside the active initiative.

Example in this repository: `timesheet-management` (weekly effort capture linked to billing and utilization).

## 2. Prerequisites

* Step 1 complete: BMAD installed and `bmad status` succeeds ([01-bmad-installation-and-setup.md](01-bmad-installation-and-setup.md)).
* A short description of the work (name and objective).

## 3. Create the Initiative

Invoke the `bmad` skill and request, for example:

```text
Create a new initiative called Timesheet Management
```

The skill creates the initiative folder and marks it as the active initiative. Showing, switching, creating or clearing the active initiative are all `bmad` requests.

## 4. Files Generated

| File | Purpose |
|------|---------|
| `_bmad-output/initiative-timesheet-management/initiative-timesheet-management.md` | Initiative document. Frontmatter holds `type: initiative`, `title` and `parent: none`. |

Documents follow the layout `<type>-<slug>/<type>-<slug>.md`. Here the initiative folder is the parent of every later document.

## 5. Verify

* The folder `_bmad-output/initiative-timesheet-management/` exists.
* The initiative file has `type: initiative` and the expected title.
* Ask `bmad` to show the active initiative and confirm it is the one you created.

## 6. Troubleshooting

* **Skills write to `_bmad-output/` root instead of the initiative:** No initiative is active. Ask `bmad` to set the active initiative.
* **Wrong initiative receives new files:** Ask `bmad` to switch the active initiative before running the next skill.
* **Skill hands off to `bmad` when you run `bmad-spec`:** This is expected when no initiative is active; set one first.

## 7. Next Step

Run `bmad-spec` (guide to be added once the spec files are staged).
