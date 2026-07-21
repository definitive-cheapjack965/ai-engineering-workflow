# Workflow Overview

## Purpose

This document explains the overall workflow used by the `ai-engineering-workflow` Codex Skill.

The skill turns complex AI-assisted development work into a structured engineering process. It is designed for projects where a direct "write the code now" approach is risky because the task depends on multiple files, unclear requirements, grading rules, technical constraints, or step-by-step validation.

The workflow is:

```text
issue-create → issue-breakdown → issue-execute → issue-update → issue-status → issue-close
```

---

## Why This Workflow Exists

AI coding often fails in complex projects for four main reasons:

1. **Context mismatch**
   The AI does not fully understand the business background, assignment requirements, file relationships, technical constraints, or expected outputs.

2. **Task size is too large**
   The user asks the AI to complete an entire module, assignment, or system at once. This causes over-design, missing details, or incorrect implementation.

3. **Feedback loop is missing**
   The AI generates code but does not verify it, update task status, or correct the work based on testing and review.

4. **Role boundaries are unclear**
   The AI tries to act as product manager, architect, developer, tester, and document writer at the same time without clear separation.

This workflow fixes these problems by forcing Codex to work like an engineering assistant:

* first understand the context;
* then create issue documents;
* then break the work into small tasks;
* then implement one task at a time;
* then verify the work;
* then update status;
* then close the issue honestly.

---

## Workflow Stages

### 1. issue-create

`issue-create` initializes the project context.

It should create or update the main issue documents and record:

* user request;
* project background;
* input files;
* output requirements;
* technical constraints;
* acceptance criteria;
* forbidden actions;
* missing information;
* initial task direction.

No implementation should happen in this stage.

---

### 2. issue-breakdown

`issue-breakdown` converts the issue into a detailed execution plan.

It should produce:

* project phases;
* atomic tasks;
* task dependencies;
* related files;
* acceptance criteria;
* verification method;
* risk and blocker notes.

No implementation should happen in this stage.

---

### 3. issue-execute

`issue-execute` implements one bounded task from the task breakdown.

It should:

* read the selected task;
* confirm scope;
* modify only related files;
* avoid unrelated refactoring;
* run verification when possible;
* update task status;
* summarize changes and next steps.

This stage should not silently complete unrelated tasks.

---

### 4. issue-update and issue-status

`issue-update` is used when the requirement, implementation plan, or project state changes.

It should:

* update issue documents;
* update task breakdown;
* record why the change happened;
* keep the documentation and implementation synchronized.

`issue-status` is used to inspect progress.

It should report:

* completed tasks;
* pending tasks;
* in-progress tasks;
* blocked tasks;
* risks;
* next recommended action.

---

### 5. issue-close

`issue-close` creates the final handoff.

It should summarize:

* final deliverables;
* changed files;
* verification results;
* completed tasks;
* known limitations;
* unfinished or risky areas;
* next steps if the project continues.

Do not claim the project is complete unless verification has passed or the limitation is clearly stated.

---

## Default Memory Structure

When the skill creates a new issue, use this initial structure unless the existing repository has a better convention:

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

After `issue-close`, the final structure should include the close report:

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

This structure keeps the project traceable and makes it easier for Codex to understand the current issue.

---

## Task Status Vocabulary

Use these task status values consistently in workflow documents:

```text
todo
in_progress
blocked
done
done_unverified
skipped
needs_review
```

Use `done` only when the task was completed and verified. Use `done_unverified` when the work appears complete but verification could not be fully run.

---

## Operating Rules

When this workflow is active:

1. Do not jump directly into implementation for complex tasks.
2. Do not invent requirements.
3. Do not over-design.
4. Do not modify unrelated files.
5. Do not mark tasks complete without verification.
6. Do not ignore failing tests.
7. Do not hide uncertainty.
8. Do not claim final completion if checks were not run.
9. Always update documentation after meaningful changes.
10. Always recommend the next clear step.

---

## Best Use Cases

This workflow is best for:

* coursework assignments;
* data analysis projects;
* Jupyter Notebook assignments;
* multi-file coding projects;
* AI engineering projects;
* team development tasks;
* research prototypes;
* projects with strict grading requirements;
* projects that include PDFs, datasets, notebooks, starter code, or report templates.

---

## Lightweight Use

For small tasks, use a lightweight version of this workflow.

A lightweight workflow may only include:

1. brief context check;
2. small task scope;
3. implementation;
4. verification;
5. summary.

Do not create excessive documentation for a very small task unless the user explicitly asks for the full workflow.
