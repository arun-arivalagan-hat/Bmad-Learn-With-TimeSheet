# BMAD Installation Guide

**BMad agent:** BMad Agent (`bmad`) | **Skill:** `bmad` (installer)

## 1. Purpose

This guide explains how to install BMAD, initialize it in a project, and verify that the installation is working.

## 2. Prerequisites

* Node.js and npm
* Git
* Claude Code, if using the plugin installation method
* Access to the official BMAD repository

## 3. Choose an Installation Method

Choose **one primary installation method** to avoid duplicate skills and conflicting configurations.

### Method A: Install Through Claude Code Plugins

**Step 1 — Register the marketplace**

Run inside Claude Code:

```text
/plugin marketplace add bmad-code-org/bmad-plugins
```

**Step 2 — Install BMAD Method**

Run in the terminal:

```bash
claude plugin install bmad-method@bmad
```

**Purpose:** Installs the BMAD Method plugin through Claude Code.

### Method B: Install Through the Skills CLI

Run from your project root:

```bash
npx skills add bmad-code-org/BMAD-METHOD
```

Follow the prompts to select your coding tool and the skills you need.

To install selected skills explicitly:

```bash
npx skills add bmad-code-org/BMAD-METHOD \
  --skill bmad \
  --skill bmod-core-tools \
  --skill bmod-method \
  --skill bmad-ticket
```

Verify that these skill names are available in the repository version you are installing.

### Method C: Install Using the BMAD Installer

Follow the current official installation instructions:

https://docs.bmad-method.org/start/install-bmad/

Use the installer command documented for your BMAD version. Do not assume that `npx bmad-method install` is supported by every release.

## 4. Initialize the Project

After installing BMAD, open your coding tool from the project root.

Invoke the installed `bmad` skill and request:

```text
bmad setup
```

Follow the setup prompts to configure the project and required modules.

## 5. Verify the Installation

Invoke the BMAD skill and request:

```text
bmad status
```

Confirm that:

* BMAD setup completed successfully.
* Required skills and modules are available.
* The `_bmad/` configuration and runtime files exist.
* The `_bmad-output/` directory is available when required by your setup.
* No unexpected duplicate installations or configuration conflicts exist.

**Note:** `bmad setup` and `bmad status` are skill instructions in supported coding tools, not universal terminal commands.

## 6. Update the Installation

For installations managed through the Skills CLI:

```bash
npx skills update
```

For plugin installations, update the relevant plugins through Claude Code's plugin management workflow.

After updating, verify the setup and status again.

## 7. Troubleshooting

* **Skill not found:** Check that the skill is installed and enabled in the selected coding tool - /skills and /reload-skills ,manage plugins
* **Setup incomplete:** Recheck the installation output and follow the official setup instructions.
* **Duplicate skills:** Check whether the same skill was installed through both plugins and the Skills CLI.
* **Missing modules:** Verify the selected modules and installed version.
* **Version mismatch:** Confirm that the plugin and project installations are using the intended versions.

## Skill Folder Structure

Layout of the installed `bmad` skill (`.claude/skills/bmad/`), which mirrors its [upstream folder](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad):

* `SKILL.md`: the entry point. Frontmatter (name, description) tells the harness when to trigger; the body holds the instructions.
* `bmod.toml`: module metadata, which module the skill belongs to and where it is sourced from on GitHub.
* `customize.toml`: the override surface; team and personal overrides live in `_bmad/custom/`, never in this file.
* `references/`: `setup`, `initiative`, `migrate` and `help`, one per action the skill routes to.
* `scripts/`: `setup.py` and `setup_check.py` (install and check), `resolve_config.py` (reads config), `knowledge.py` (module help), `memlog.py`, `roster.py` and others.
* `assets/`: `config.template.toml`, the starting config.


## Skill Steps

Steps the `bmad` skill runs for setup (from `references/setup.md`):

1. **Check:** run the setup check to see whether BMad, its modules and the config are in place.
2. **Fix:** repair or complete what the check reports missing, add a module, or change a config answer.
3. **Verify** with the check again; for help and next-step advice `bmad` reads each installed module's own help.

## 8. Official References

* [BMAD Installation Guide](https://docs.bmad-method.org/start/install-bmad/)
* [BMAD Method Repository](https://github.com/bmad-code-org/BMAD-METHOD)
* [BMAD Plugin Marketplace](https://github.com/bmad-code-org/bmad-plugins)
* [Skills CLI Repository](https://github.com/vercel-labs/skills)
* [Get Answers About BMad](https://docs.bmad-method.org/start/get-answers-about-bmad/)
* [Add Modules](https://docs.bmad-method.org/customize/add-modules/)
* [Skills and Agents (all skills)](https://docs.bmad-method.org/reference/skills-and-agents/)
* [GitHub: `bmad` skill source](https://github.com/bmad-code-org/BMAD-METHOD/tree/main/skills/bmad)

---

**Installation complete:** Proceed to project workflows only after the installation and verification steps succeed.
