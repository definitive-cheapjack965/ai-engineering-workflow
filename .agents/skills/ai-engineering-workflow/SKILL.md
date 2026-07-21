---
name: ai-engineering-workflow
description: Use this skill for complex coding, coursework, data analysis, notebook, research, or multi-file projects that need a structured engineering workflow. It enforces issue creation, context analysis, task breakdown, atomic execution, verification, status tracking, and final closure.
---

# ai-engineering-workflow

## Purpose

`ai-engineering-workflow` is a Codex skill for handling complex project work through a structured engineering process.

Use it when a task should not jump directly into coding.

Core workflow:

```text
issue-create → issue-breakdown → issue-execute → issue-update → issue-status → issue-close
```

This skill helps Codex:

* understand project context before implementation;
* avoid inventing requirements;
* break large work into atomic tasks;
* execute one task at a time;
* verify changes honestly;
* update project status after each step;
* close the issue with a clear final report.

---

## When To Use

Use this skill when the user invokes:

```text
$ai-engineering-workflow
```

Also use it for:

* coursework projects;
* multi-file coding projects;
* data analysis projects;
* Jupyter Notebook projects;
* research prototypes;
* AI engineering projects;
* projects with starter code, PDFs, datasets, templates, or grading requirements;
* requests to create issues, break down tasks, execute one task, update status, or close a project.

For simple one-step tasks, do not force the full workflow unless the user explicitly invokes this skill.

---

## Core Rules

### 1. Understand Before Implementing

Before writing code or modifying files, identify:

* user goal;
* project background;
* available files;
* expected deliverables;
* constraints;
* acceptance criteria;
* missing or unclear information.

When available, load context in layers:

* user or project-level memory;
* project overview and constraints;
* architecture and module documents;
* current issue documents;
* related source files and tests.

Do not guess missing requirements. Record uncertainty clearly.

---

### 2. Keep Scope Controlled

Do not implement extra features, broad refactors, or unrelated changes.

Only do work that is:

* requested by the user;
* required by the issue;
* required by the selected task;
* needed for verification.

Optional improvements should be suggested, not implemented automatically.

---

### 3. Execute Atomic Tasks

Large work must be broken into small tasks.

Each task should include:

* task ID;
* objective;
* related files;
* scope;
* dependencies;
* acceptance criteria;
* verification method;
* status.

During `/issue-execute`, complete only one selected task or one clearly bounded task group.

---

### 4. Verify Honestly

After implementation, run available checks when possible.

Verification may include:

* tests;
* scripts;
* notebook execution;
* output inspection;
* Markdown rendering;
* file structure checks;
* requirement matching.

Never claim a test passed if it was not run.

If verification cannot be performed, write:

```text
Verification not run
```

and explain why.

---

### 5. Keep Documents Updated

After meaningful work, update the workflow documents:

```text
issue.md
status.md
docs/system-analysis.md
docs/architecture.md
docs/task-breakdown.md
close-report.md
```

The project state in documentation must match the actual work.

---

### 6. Protect User Work

When working in a Git repository:

* check branch and working tree status before editing;
* avoid overwriting user changes;
* do not commit secrets, API keys, credentials, private datasets, or private assignment answers;
* do not publish to GitHub before local testing and privacy checks.

---

## Command Modes

Supported modes:

```text
/issue-create
/issue-breakdown
/issue-execute
/issue-update
/issue-status
/issue-close
```

If the user does not specify a mode, choose the safest next step based on project state.

---

## Task Status Vocabulary

Use these task status values consistently in `docs/task-breakdown.md`, `status.md`, and `close-report.md`:

```text
todo
in_progress
blocked
done
done_unverified
skipped
needs_review
```

Definitions:

- `todo`: not started;
- `in_progress`: currently being worked on;
- `blocked`: cannot proceed because required information, files, or dependencies are missing;
- `done`: completed and verified;
- `done_unverified`: work appears complete, but verification could not be fully run;
- `skipped`: intentionally not done, with reason recorded;
- `needs_review`: requires human confirmation before it can be considered done.

Do not mix these status values with alternate labels such as `Pending`, `Completed`, or `Completed but not fully verified` inside workflow documents.

---

## Mode Behavior

### `/issue-create`

Use when starting a new project issue.

Goal: create project context before implementation.

Required actions:

1. Read the request and inspect available files.
2. Identify goal, scope, deliverables, constraints, and acceptance criteria.
3. Create the issue memory directory.
4. Create initial workflow documents.
5. Do not implement code unless explicitly requested.

Expected files:

```text
memories/YYYYMM/CHANGEID/issue.md
memories/YYYYMM/CHANGEID/status.md
memories/YYYYMM/CHANGEID/docs/system-analysis.md
memories/YYYYMM/CHANGEID/docs/architecture.md
memories/YYYYMM/CHANGEID/docs/task-breakdown.md
```

---

### `/issue-breakdown`

Use after issue context exists.

Goal: convert the project into atomic tasks.

Required actions:

1. Read `issue.md`, `docs/system-analysis.md`, and `docs/architecture.md` if available.
2. Break work into phases and atomic tasks.
3. Add dependencies, acceptance criteria, and verification methods.
4. Update `docs/task-breakdown.md`.
5. Update `status.md`.
6. Do not implement code.

---

### `/issue-execute`

Use when implementing one selected task.

Goal: complete exactly one atomic task.

Required actions:

1. Identify the selected task.
2. Confirm dependencies and blockers.
3. Read relevant files before editing.
4. Modify only necessary files.
5. Run available verification.
6. Update `docs/task-breakdown.md`.
7. Update `status.md`.
8. Summarize changed files and verification results.

Do not complete unrelated tasks.

---

### `/issue-update`

Use when requirements, files, blockers, or scope change.

Goal: keep workflow documents accurate.

Required actions:

1. Identify what changed.
2. Update affected documents.
3. Update assumptions, constraints, risks, or task dependencies.
4. Update `status.md`.
5. Do not implement code unless explicitly requested.

---

### `/issue-status`

Use when the user asks for current progress.

Goal: summarize state without implementation.

Include:

```text
done
in_progress
todo
blocked
done_unverified
needs_review
Verification Notes
Next Step
```

Do not modify code during `/issue-status`.

---

### `/issue-close`

Use when the issue is complete or ready for handoff.

Goal: create the final closure report.

Required actions:

1. Check task completion.
2. Review changed and created files.
3. Review verification results.
4. Record unresolved risks or limitations.
5. Create or update `close-report.md`.
6. Mark the issue as `Complete`, `Partially Complete`, `Blocked`, or `Canceled`.

Do not claim full completion unless all required tasks are completed and verified.

---

## Default Project Memory Structure

Create this initial structure during `/issue-create`:

```text
memories/
└── YYYYMM/
    └── CHANGEID/
        ├── issue.md
        ├── status.md
        └── docs/
            ├── system-analysis.md
            ├── architecture.md
            └── task-breakdown.md
```

Create or update this final structure during `/issue-close`:

```text
memories/
└── YYYYMM/
    └── CHANGEID/
        ├── issue.md
        ├── status.md
        ├── close-report.md
        └── docs/
            ├── system-analysis.md
            ├── architecture.md
            └── task-breakdown.md
```

Use English filenames by default.

Do not use Chinese filenames unless the user explicitly requests them.

---

## Templates

Use templates from:

```text
.agents/skills/ai-engineering-workflow/assets/templates/
```

Expected templates:

```text
issue-template.md
system-analysis-template.md
architecture-template.md
task-breakdown-template.md
status-template.md
close-report-template.md
```

Template mapping:

```text
issue-template.md              → issue.md
system-analysis-template.md    → docs/system-analysis.md
architecture-template.md       → docs/architecture.md
task-breakdown-template.md     → docs/task-breakdown.md
status-template.md             → status.md
close-report-template.md       → close-report.md
```

If a template is missing, create the document manually using the same structure and note that the template was unavailable.

---

## References

Detailed guidance is stored in:

```text
.agents/skills/ai-engineering-workflow/references/
```

Reference files:

```text
workflow-overview.md
issue-create-guide.md
issue-breakdown-guide.md
issue-execute-guide.md
issue-update-status-guide.md
issue-close-guide.md
quality-control.md
```

`SKILL.md` defines the core workflow. Reference files provide detailed behavior.

---

## Quality Gates

Before marking work complete, check:

* Requirement Gate: goal, deliverables, constraints, and missing information are clear.
* Scope Gate: no unrelated work was added.
* Implementation Gate: only necessary files were changed.
* Verification Gate: checks were run or skipped with explanation.
* Documentation Gate: status and task documents were updated.
* Git Gate: no secrets, private data, or unrelated changes are included.
* Handoff Gate: the user knows what changed, what remains, and what to do next.

---

## Forbidden Actions

Do not:

* jump directly into implementation for complex tasks;
* invent requirements;
* implement unrelated features;
* silently modify unrelated files;
* overwrite user changes;
* mark tasks complete without verification or explanation;
* fabricate test results, citations, datasets, or command outputs;
* commit secrets or private data;
* publish to GitHub before local testing and privacy checks;
* mix the old capitalized skill name with `ai-engineering-workflow`;
* use Chinese workflow filenames by default.

---

## User Response Format

When reporting progress, use this structure:

```text
done
- ...

Files Created or Updated
- ...

Verification
- ...

Current Status
- done:
- todo:
- blocked:
- done_unverified:

Next Step
- ...
```

If blocked, include:

```text
Blocked
- ...
```

If verification was not run, include:

```text
Verification Not Run
- Reason: ...
```

---

## Example Invocations

Create issue context:

```text
$ai-engineering-workflow
/issue-create
Create an issue context for this project. Do not write code yet.
```

Break down tasks:

```text
$ai-engineering-workflow
/issue-breakdown
Break this project into atomic tasks with acceptance criteria and verification steps.
```

Execute one task:

```text
$ai-engineering-workflow
/issue-execute
Execute Task 1.1 only.
```

Update workflow documents:

```text
$ai-engineering-workflow
/issue-update
The requirement has changed. Update the workflow documents first.
```

Check status:

```text
$ai-engineering-workflow
/issue-status
Summarize what is complete, pending, blocked, and what to do next.
```

Close issue:

```text
$ai-engineering-workflow
/issue-close
Generate the final close report.
```

---

## Final Rule

Always prefer:

```text
understand → document → break down → execute one task → verify → update status → close
```

over:

```text
guess → code everything → skip checks → claim completion
```
