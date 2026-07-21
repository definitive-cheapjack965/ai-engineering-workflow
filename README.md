# AI Engineering Workflow Skill

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
![Version](https://img.shields.io/badge/version-v1.0.0-blue)
![Type](https://img.shields.io/badge/type-Codex%20Skill-green)

`ai-engineering-workflow` is a reusable Codex Skill for managing complex AI-assisted coursework, coding tasks, data analysis projects, notebook projects, research prototypes, and multi-file development work.

Instead of jumping directly into implementation, the Skill guides Codex through a structured engineering workflow:

1. understand the request;
2. create issue context;
3. analyze requirements;
4. break the work into atomic tasks;
5. execute one bounded task at a time;
6. verify results honestly;
7. update project status;
8. close the issue with a clear handoff report.

---

## Why This Skill Exists

AI tools are useful for simple coding and explanation tasks, but complex assignments and project work often fail when the model lacks context.

Common problems include:

- unclear project requirements;
- missing datasets or files;
- tasks that are too large;
- code generated before requirements are understood;
- missing verification;
- undocumented assumptions;
- inconsistent project status;
- untracked changes.

This Skill addresses those problems with a lightweight, issue-based engineering workflow.

---

## Best Use Cases

Use this Skill for:

- coursework projects;
- data analysis assignments;
- Jupyter Notebook projects;
- research report projects;
- multi-file coding tasks;
- project scaffolding;
- debugging and incremental implementation;
- tasks that require documentation and verification.

Do not use the full workflow for very small one-step questions unless it is explicitly requested.

---

## Workflow

```text
issue-create
    ↓
issue-breakdown
    ↓
issue-execute
    ↓
issue-update
    ↓
issue-status
    ↓
issue-close
```

### `issue-create`

Creates a structured issue folder and records project context.

Initial outputs:

```text
memories/YYYYMM/CHANGEID/
├── issue.md
├── status.md
└── docs/
    ├── system-analysis.md
    ├── architecture.md
    └── task-breakdown.md
```

### `issue-breakdown`

Creates or completes `docs/task-breakdown.md` and divides the issue into atomic, verifiable tasks.

### `issue-execute`

Executes one selected task or one clearly bounded next task. The Skill should not silently complete unrelated work.

### `issue-update` and `issue-status`

Updates or checks task progress, blockers, changed files, and verification status.

### `issue-close`

Creates a final close report with deliverables, verification results, limitations, and handoff notes.

Final outputs after closure:

```text
memories/YYYYMM/CHANGEID/
├── issue.md
├── status.md
├── close-report.md
└── docs/
    ├── system-analysis.md
    ├── architecture.md
    └── task-breakdown.md
```

> [!NOTE]
> `issue-create`, `issue-breakdown`, `issue-execute`, `issue-update`, `issue-status`, and `issue-close` are conceptual workflow modes used by the Skill. They are not operating-system shell commands and do not require separate command-line scripts.

---

## Status Vocabulary

### Task status

| Status | Meaning |
|---|---|
| `todo` | Not started. |
| `in_progress` | Currently being worked on. |
| `blocked` | Cannot proceed because required information, files, or dependencies are missing. |
| `done` | Completed and verified. |
| `done_unverified` | Work is complete, but verification could not be fully run. |
| `skipped` | Intentionally not done, with the reason recorded. |
| `needs_review` | Requires user, reviewer, or human confirmation. |

### Issue closure status

Use these values only for the overall issue:

```text
complete
partially_complete
blocked
canceled
```

Do not use issue closure values for individual tasks.

---

## Repository Structure

```text
ai-engineering-workflow/
├── AGENTS.md
├── README.md
├── CHANGELOG.md
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

---

## Installation

### Project-level installation

Clone the repository:

```bash
git clone https://github.com/Jared13PG/ai-engineering-workflow.git
```

Copy the Skill folder from:

```text
ai-engineering-workflow/.agents/skills/ai-engineering-workflow/
```

into the target project:

```text
your-project/.agents/skills/ai-engineering-workflow/
```

Windows PowerShell example:

```powershell
Copy-Item `
  -Recurse `
  ".\ai-engineering-workflow\.agents\skills\ai-engineering-workflow" `
  ".\your-project\.agents\skills\"
```

You may also download the repository as a ZIP file and copy only:

```text
.agents/skills/ai-engineering-workflow/
```

into the corresponding `.agents/skills/` directory of your project.

### Global installation

Copy the Skill folder to the user-level Codex Skill directory:

```text
$HOME/.agents/skills/ai-engineering-workflow/
```

Linux or macOS example:

```bash
mkdir -p "$HOME/.agents/skills"
cp -R .agents/skills/ai-engineering-workflow "$HOME/.agents/skills/"
```

Windows PowerShell example:

```powershell
New-Item -ItemType Directory -Force "$HOME\.agents\skills" | Out-Null
Copy-Item -Recurse ".\.agents\skills\ai-engineering-workflow" "$HOME\.agents\skills\"
```

GitHub hosting makes the Skill easy to download, but it does not install the Skill automatically. Restart or reload the Codex session after installation when necessary.

---

## Example Usage

Start a complex assignment or project with:

```text
Use $ai-engineering-workflow.
Start with issue-create. Analyze the project and create the initial workflow documents, but do not implement anything yet.
```

Continue with task breakdown:

```text
Continue with issue-breakdown and create atomic tasks with dependencies, acceptance criteria, and verification steps.
```

Execute one bounded task:

```text
Continue with issue-execute and complete Task 1.1 only.
```

Check progress:

```text
Use issue-status to summarize what is done, pending, blocked, and what should happen next.
```

Close the issue:

```text
Use issue-close to create the final handoff report.
```

---

## Quality Principles

The Skill follows these principles:

- do not implement before understanding requirements;
- do not invent missing requirements;
- do not add unrequested features;
- do not modify unrelated files;
- execute one bounded task at a time;
- record blockers honestly;
- verify before marking work complete;
- keep status and documentation synchronized;
- protect private information and credentials.

---

## What This Skill Does Not Do

This Skill does not:

- replace project-specific tests or manual review;
- guarantee correctness when verification cannot be run;
- automatically publish, commit, or release changes;
- remove the need to check private data before pushing to GitHub;
- become globally available unless it is installed in the appropriate global Skill directory.

---

## Validation Status

A local workflow validation test is recorded in:

```text
examples/local-validation-result.md
```

The recorded runtime validation covers:

- `issue-create`;
- `issue-breakdown`;
- `issue-execute`;
- `issue-status`;
- `issue-close`.

A controlled `issue-update` regression scenario is included in `examples/homework-test-plan.md` and is marked pending a fresh Codex runtime test in the validation record.

The example test plan is available at:

```text
examples/homework-test-plan.md
```

---

## Project Status

The first public version, v1.0.0, has been released.

Current completed components:

- core Skill instructions;
- workflow reference guides;
- reusable issue and project templates;
- local validation example;
- installation and usage documentation;
- privacy and verification safeguards.

The Skill will continue to be improved through real project testing and user feedback.

See [CHANGELOG.md](CHANGELOG.md) for release history.

---

## License

This project is released under the [MIT License](LICENSE).
