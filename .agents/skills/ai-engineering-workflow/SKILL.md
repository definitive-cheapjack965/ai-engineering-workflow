---
name: ai-engineering-workflow
description: Use this skill for complex coding, coursework, data analysis, notebook, research, or multi-file projects that need structured issue creation, context analysis, task breakdown, atomic execution, verification, status tracking, and final closure.
---

# ai-engineering-workflow

## Purpose

Use this Skill to manage complex project work through a controlled engineering workflow instead of jumping directly into implementation.

```text
issue-create → issue-breakdown → issue-execute → issue-update → issue-status → issue-close
```

The workflow helps Codex understand context, control scope, execute bounded tasks, verify honestly, synchronize documentation, and produce a clear final handoff.

---

## When To Use

Use this Skill when the user invokes:

```text
$ai-engineering-workflow
```

It is appropriate for:

- coursework and research projects;
- multi-file coding or AI engineering work;
- data analysis and notebook projects;
- projects with starter code, datasets, PDFs, templates, or grading rules;
- requests to create an issue, plan tasks, implement one task, revise the plan, report progress, or close a project.

Do not force the full workflow onto a simple one-step task unless the user explicitly invokes the Skill.

---

## Core Rules

### 1. Understand Before Implementing

Before editing files, identify:

- user goal and project background;
- available files and current repository state;
- expected deliverables;
- constraints and acceptance criteria;
- missing or unclear information.

Load context in layers when available: project instructions, repository guidance, current issue documents, architecture documents, relevant source files, and tests.

Do not silently invent missing requirements. Record uncertainty and its impact.

### 2. Keep Scope Controlled

Only perform work that is requested, required by the active issue, required by the selected task, or necessary for verification.

Suggest optional improvements separately. Do not implement them automatically.

### 3. Execute Atomic Tasks

Every implementation task should define:

- task ID and objective;
- scope and related files;
- dependencies;
- acceptance criteria;
- verification method;
- status.

During `issue-execute`, complete only one selected task or one clearly bounded task group.

### 4. Verify Honestly

Use available checks such as tests, scripts, notebook execution, output inspection, Markdown checks, file-structure checks, and requirement matching.

Never claim a check passed when it was not run. When verification cannot be performed, record:

```text
Verification not run
```

and explain why.

### 5. Keep Documents Synchronized

After meaningful work, update the relevant workflow documents:

```text
issue.md
status.md
docs/system-analysis.md
docs/architecture.md
docs/task-breakdown.md
close-report.md
```

Documentation must reflect the actual project state.

### 6. Protect User Work

When working in a Git repository:

- inspect the current branch and working tree before editing;
- avoid overwriting user changes;
- do not commit secrets, credentials, private datasets, or private assignment answers;
- do not publish before local testing and privacy checks.

---

## Mode Selection

Supported conceptual modes:

```text
issue-create
issue-breakdown
issue-execute
issue-update
issue-status
issue-close
```

These are Skill modes, not operating-system commands. Natural-language requests may invoke them.

When the user does not name a mode, choose the safest next step from the current project state:

- new complex project → `issue-create`;
- context exists but no executable plan → `issue-breakdown`;
- a bounded task is ready → `issue-execute`;
- requirements, files, scope, or blockers changed → `issue-update`;
- progress summary requested → `issue-status`;
- work is ready for handoff → `issue-close`.

---

## Task Status Vocabulary

Use these values consistently for individual tasks:

```text
todo
in_progress
blocked
done
done_unverified
skipped
needs_review
```

- `todo`: not started;
- `in_progress`: currently being worked on;
- `blocked`: cannot proceed because required information, files, or dependencies are missing;
- `done`: completed and verified;
- `done_unverified`: appears complete, but verification could not be fully run;
- `skipped`: intentionally omitted, with the reason recorded;
- `needs_review`: requires human confirmation.

Use these values only for the overall issue at closure:

```text
complete
partially_complete
blocked
canceled
```

Do not mix task status and issue closure status.

---

## Mode Behavior

### `issue-create`

Goal: establish project context before implementation.

Required actions:

1. Read the request and inspect available files.
2. Identify goal, scope, deliverables, constraints, risks, and acceptance criteria.
3. Create the issue memory directory and initial workflow documents.
4. Record missing information and assumptions.
5. Do not implement unless the user explicitly requests combined planning and implementation.

Expected files:

```text
memories/YYYYMM/CHANGEID/issue.md
memories/YYYYMM/CHANGEID/status.md
memories/YYYYMM/CHANGEID/docs/system-analysis.md
memories/YYYYMM/CHANGEID/docs/architecture.md
memories/YYYYMM/CHANGEID/docs/task-breakdown.md
```

### `issue-breakdown`

Goal: convert established context into atomic executable tasks.

Required actions:

1. Read the issue, system analysis, architecture, status, and relevant project instructions.
2. Break the work into phases and atomic tasks.
3. Add dependencies, related files, acceptance criteria, and verification methods.
4. Update `docs/task-breakdown.md` and `status.md`.
5. Do not implement code.

### `issue-execute`

Goal: complete one selected task without scope expansion.

Required actions:

1. Identify the selected task and confirm its dependencies.
2. Inspect relevant files before editing.
3. Modify only the files necessary for that task.
4. Run available verification.
5. Update task status and `status.md`.
6. Report changed files, verification results, blockers, and the next step.

### `issue-update`

Goal: synchronize the workflow after requirements, files, blockers, assumptions, or scope change.

Required actions:

1. Identify and classify the change.
2. Update all affected issue, analysis, architecture, task, risk, and status documents.
3. Revise dependencies or acceptance criteria when needed.
4. Mark invalidated work or verification honestly.
5. Do not continue implementation using outdated assumptions.
6. Do not implement code unless explicitly requested.

### `issue-status`

Goal: report the current state without implementation.

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

Do not modify project code during a status-only request.

### `issue-close`

Goal: create an honest final handoff.

Required actions:

1. Check task completion and deliverables.
2. Review changed and created files.
3. Review verification results.
4. Record unresolved risks, limitations, or manual checks.
5. Create or update `close-report.md`.
6. Mark the issue `complete`, `partially_complete`, `blocked`, or `canceled`.

Do not claim full completion unless all required tasks are complete and verified.

---

## Project Memory Structure

Create this structure during `issue-create`:

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

Add `close-report.md` during `issue-close`.

Use English filenames by default unless the user explicitly requests otherwise.

---

## Templates

Load reusable templates relative to this Skill directory from:

```text
assets/templates/
```

Mapping:

```text
assets/templates/issue-template.md           → issue.md
assets/templates/system-analysis-template.md → docs/system-analysis.md
assets/templates/architecture-template.md    → docs/architecture.md
assets/templates/task-breakdown-template.md  → docs/task-breakdown.md
assets/templates/status-template.md          → status.md
assets/templates/close-report-template.md    → close-report.md
```

If a template is unavailable, create the document manually using the same structure and note the missing template.

---

## Reference Loading Rules

Load detailed guidance relative to this Skill directory only when relevant:

- for overall workflow selection or an unclear project state, read `references/workflow-overview.md`;
- for `issue-create`, read `references/issue-create-guide.md`;
- for `issue-breakdown`, read `references/issue-breakdown-guide.md`;
- for `issue-execute`, read `references/issue-execute-guide.md`;
- for `issue-update` or `issue-status`, read `references/issue-update-status-guide.md`;
- for `issue-close`, read `references/issue-close-guide.md`;
- before final completion, release, or when verification is important, read `references/quality-control.md`.

Do not load every reference automatically when one focused guide is sufficient.

---

## Quality Gates

Before marking work complete, check:

- **Requirement Gate**: goals, deliverables, constraints, and uncertainties are clear.
- **Scope Gate**: no unrelated work was added.
- **Implementation Gate**: only necessary files were changed.
- **Verification Gate**: checks were run or skipped with an explanation.
- **Documentation Gate**: issue, task, and status documents match reality.
- **Git Gate**: no secrets, private data, or unrelated changes are included.
- **Handoff Gate**: the user knows what changed, what remains, and what to do next.

---

## Forbidden Actions

Do not:

- jump directly into implementation for a complex task without context;
- invent requirements, files, datasets, test results, or command output;
- implement unrelated features or broad refactors;
- overwrite user changes silently;
- mark work verified when checks were not run;
- publish secrets or private data;
- use inconsistent workflow filenames or status labels.

---

## Progress Response Format

Use a compact structure such as:

```text
Done
- ...

Files Created or Updated
- ...

Verification
- ...

Current Status
- done: ...
- todo: ...
- blocked: ...
- done_unverified: ...

Next Step
- ...
```

When blocked or unverified, state the reason explicitly.

---

## Example Invocations

```text
Use $ai-engineering-workflow in issue-create mode. Analyze the project and create the initial workflow documents, but do not implement yet.
```

```text
Continue in issue-breakdown mode and create atomic tasks with dependencies, acceptance criteria, and verification steps.
```

```text
Continue in issue-execute mode and complete Task 1.1 only.
```

```text
Use issue-update mode. The input file and requirement changed; revise the workflow documents before further implementation.
```

```text
Use issue-status mode to summarize completed, pending, blocked, and unverified work.
```

```text
Use issue-close mode to create the final handoff report.
```

---

## Final Rule

Always prefer:

```text
understand → document → break down → execute one task → verify → update → close
```

over:

```text
guess → code everything → skip checks → claim completion
```
