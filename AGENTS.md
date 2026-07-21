# AGENTS.md

## Project Identity

This repository contains a Codex Skill named:

```text
ai-engineering-workflow
```

The purpose of this project is to provide a reusable AI engineering workflow for Codex. The skill helps Codex handle complex assignments, coding projects, data analysis tasks, research prototypes, and multi-file development work using a structured engineering process.

The workflow is:

```text
issue-create → issue-breakdown → issue-execute → issue-update → issue-status → issue-close
```

This project should make AI-assisted development more reliable by enforcing context gathering, requirement clarification, task decomposition, atomic execution, verification, documentation updates, and final handoff.

---

## Main Skill Location

The main skill files are located at:

```text
.agents/skills/ai-engineering-workflow/
```

The core file is:

```text
.agents/skills/ai-engineering-workflow/SKILL.md
```

Do not rename the skill directory unless the user explicitly asks.

Do not change the skill name unless the user explicitly asks.

The skill name must remain:

```text
ai-engineering-workflow
```

---

## Repository Structure

Expected repository structure:

```text
ai-engineering-workflow/
├── README.md
├── AGENTS.md
├── LICENSE
├── .gitignore
├── .gitattributes
├── examples/
│   ├── homework-test-plan.md
│   └── local-validation-result.md
└── .agents/
    └── skills/
        └── ai-engineering-workflow/
            ├── SKILL.md
            ├── references/
            │   ├── workflow-overview.md
            │   ├── issue-create-guide.md
            │   ├── issue-breakdown-guide.md
            │   ├── issue-execute-guide.md
            │   ├── issue-update-status-guide.md
            │   ├── issue-close-guide.md
            │   └── quality-control.md
            └── assets/
                └── templates/
                    ├── issue-template.md
                    ├── system-analysis-template.md
                    ├── architecture-template.md
                    ├── task-breakdown-template.md
                    ├── status-template.md
                    └── close-report-template.md
```

When adding or editing files, keep this structure stable.

---

## Development Priorities

When working in this repository, follow these priorities:

1. Keep the skill clear, reusable, and easy to understand.
2. Prefer simple Markdown instructions over unnecessary scripts.
3. Keep `SKILL.md` concise enough to act as the main instruction file.
4. Put longer explanations in `references/`.
5. Put reusable document formats in `assets/templates/`.
6. Keep examples realistic and useful for testing.
7. Do not add unrelated tools, frameworks, or dependencies unless the user requests them.

---

## Editing Rules

When modifying this project:

* Preserve the skill name `ai-engineering-workflow`.
* Preserve the main workflow order.
* Do not remove the issue-based development process.
* Do not make the skill too broad or vague.
* Do not add features that are not related to AI engineering workflow management.
* Do not add private user data, credentials, API keys, or assignment answers into the public repository.
* Do not commit generated junk files, temporary files, caches, or local environment files.
* Keep all instructions in clear English because Codex will read these files directly.

---

## Skill Design Rules

The skill should always enforce these behaviors:

1. Codex should not jump directly into code for complex tasks.
2. Codex should first create or load project context.
3. Codex should convert vague requirements into structured issue documents.
4. Codex should break large work into atomic tasks.
5. Codex should execute one bounded task at a time.
6. Codex should verify results before marking a task complete.
7. Codex should update status and documentation after meaningful changes.
8. Codex should close the issue with a final handoff report.
9. Codex should be honest about missing files, failed checks, or incomplete verification.

---

## Command Model

The skill supports these command-style workflows:

```text
/issue-create
/issue-breakdown
/issue-execute
/issue-update
/issue-status
/issue-close
```

These are conceptual workflow modes inside the skill. They do not require actual shell commands unless scripts are added later.

When users invoke the skill with natural language, infer the correct mode:

* New project or assignment → `/issue-create`
* Need detailed task plan → `/issue-breakdown`
* Need implementation → `/issue-execute`
* Requirement changed → `/issue-update`
* Need progress summary → `/issue-status`
* Work finished → `/issue-close`

---

## Testing Strategy

Before considering this skill ready for publishing, test it locally with a real assignment or project.

The minimum test should confirm that Codex can:

1. Recognize and explain the skill.
2. Run `issue-create` without writing implementation code.
3. Generate initial issue documents.
4. Run `issue-breakdown` and produce atomic tasks.
5. Run `issue-execute` for only one task at a time.
6. Run verification or clearly explain why verification cannot be run.
7. Update status documents.
8. Run `issue-close` and produce a final close report.

Do not publish the project until the local test is successful.

---

## Git Rules

Use Git to track meaningful project changes.

Recommended commit style:

```text
Add initial skill instructions
Add project-level AGENTS guidance
Add workflow reference guides
Add reusable issue templates
Add local assignment test plan
Update README with installation guide
```

Before committing, check:

```text
git status
```

Do not commit:

* local cache files;
* `.env` files;
* private credentials;
* large assignment datasets unless intentionally included as public examples;
* user-private homework files;
* generated temporary outputs.

---

## Public Release Rules

Before publishing to GitHub:

1. Review all files for private information.
2. Make sure the skill name is consistent.
3. Make sure the README explains installation and usage.
4. Make sure examples do not include private homework answers.
5. Make sure the license is included.
6. Run a final local test.
7. Confirm that the repository history does not contain secrets.

---

## Current Project Goal

The current goal is to maintain the public version of the `ai-engineering-workflow` Codex Skill, keep the workflow clear and reusable, improve it based on real project tests, and ensure that public examples do not contain private user data.
