# AI Engineering Workflow Skill

`ai-engineering-workflow` is a Codex skill for managing complex AI-assisted coursework, coding tasks, data analysis projects, notebook projects, research prototypes, and multi-file development work.

The skill helps Codex avoid jumping directly into implementation. Instead, it guides Codex through a structured engineering workflow:

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

This skill solves these problems by introducing a lightweight engineering workflow for Codex.

---

## Best Use Cases

Use this skill for:

- coursework projects;
- data analysis assignments;
- Jupyter notebook projects;
- research report projects;
- multi-file coding tasks;
- project scaffolding;
- debugging and incremental implementation;
- tasks that require documentation and verification.

Do not use this skill for very small one-step questions where a normal answer is enough.

---

## Workflow

The main workflow is:

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

### issue-create

Creates a structured issue folder and records the project context.

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

### issue-breakdown

Creates or formally completes `docs/task-breakdown.md` and breaks the issue into atomic, verifiable tasks.

### issue-execute

Executes one selected task or one clearly bounded next task. The skill should not silently complete unrelated work.

### issue-update and issue-status

Updates or checks task progress, blockers, changed files, and verification status.

### issue-close

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

---

## Task Status Vocabulary

Use the following task status values consistently across generated workflow documents:

| Status | Meaning |
|---|---|
| `todo` | Not started. |
| `in_progress` | Currently being worked on. |
| `blocked` | Cannot proceed because required information, files, or dependencies are missing. |
| `done` | Completed and verified. |
| `done_unverified` | Implementation or work is complete, but verification could not be fully run. |
| `skipped` | Intentionally not done, with the reason recorded. |
| `needs_review` | Requires user, reviewer, or human confirmation before it can be considered done. |

---

## Repository Structure

```text
ai-engineering-workflow/
├── AGENTS.md
├── README.md
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

For project-level use, copy the skill folder into the project repository:

```text
.agents/skills/ai-engineering-workflow/
```

For global use, copy the same skill folder into the global or shared Codex skills directory supported by your local Codex setup. GitHub hosting makes the skill easy to download, but it does not automatically make the skill globally available on your machine.

Then use the skill in a project where Codex can read and write files.

---

## Example Usage

Start with a complex assignment or project request:

```text
Use ai-engineering-workflow to analyze this assignment, create an issue, break it into tasks, and implement it step by step.
```

A typical command flow is:

```text
/issue-create [project or assignment request]
/issue-breakdown
/issue-execute next
/issue-status
/issue-close
```

---

## Quality Principles

The skill follows these principles:

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

This skill does not:

- replace project-specific tests or manual review;
- guarantee correctness when verification cannot be run;
- automatically publish, commit, or release changes;
- remove the need to check private data before pushing to GitHub;
- make the skill globally available unless it is installed in the appropriate global skill directory.

---

## Validation Status

A local workflow validation test has been recorded in:

```text
examples/local-validation-result.md
```

The recorded validation covers the expected workflow stages:

- `issue-create`;
- `issue-breakdown`;
- `issue-execute`;
- `issue-status`;
- `issue-close`.

The example test plan is available at:

```text
examples/homework-test-plan.md
```

---

## Development Status

Current completed parts:

- core skill file;
- workflow references;
- runtime document templates;
- example homework test plan;
- local validation result note;
- repository guidance.

Before publishing publicly, review the remaining release checks:

- confirm the public author name and email in Git history and `LICENSE`;
- confirm no private coursework, datasets, credentials, or personal paths are included;
- run one final local test after any edits;
- decide whether to publish a clean source archive or a Git repository with preserved history.

---

## License

This project is released under the MIT License.
