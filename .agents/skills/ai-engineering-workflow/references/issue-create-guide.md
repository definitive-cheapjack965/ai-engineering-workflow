# issue-create Guide

## Purpose

`issue-create` is the first stage of the AI engineering workflow.

Its purpose is to turn a vague or broad user request into a structured issue with enough context for later planning and implementation.

This stage is about understanding and documentation, not coding.

---

## When To Use

Use `issue-create` when:

* the user gives a new assignment;
* the user gives a new coding project;
* the user uploads multiple files;
* the user asks Codex to start a complex task;
* there is no existing issue document;
* the task requires planning before implementation;
* the project has unclear requirements or multiple deliverables.

---

## Main Rule

Do not implement code during `issue-create`.

This command should only:

* inspect context;
* create documents;
* summarize requirements;
* identify missing information;
* prepare the project for task breakdown.

---

## Inputs

Possible inputs include:

* user request;
* assignment instructions;
* project README;
* PDFs;
* CSV files;
* notebooks;
* starter code;
* existing source files;
* grading rubrics;
* report templates;
* design documents;
* previous issue documents.

---

## Required Actions

When running `issue-create`, follow this order:

1. Inspect the repository structure.
2. Check whether Git is available.
3. Check current branch and working tree status.
4. Create a feature branch only when the repository workflow requires it or the user approves it.
5. Identify the issue ID or create one.
6. Create the issue memory directory.
7. Create initial issue documents.
8. Fill in all known information.
9. Mark unclear or missing information.
10. Stop before implementation.

---

## Recommended Branch Naming

If Git is available and branch creation is required by the repository workflow or approved by the user, use:

```text
feature/YYYYMMDD_CHANGEID_short-description
```

Example:

```text
feature/20260618_AEW001_assignment-workflow-test
```

If Git is unavailable, continue without branch creation and record this in the issue document.

---

## Memory Directory

Create the issue under:

```text
memories/YYYYMM/CHANGEID/
```

Example:

```text
memories/202606/AEW001/
```

Required files:

```text
memories/YYYYMM/CHANGEID/
├── issue.md
├── status.md
└── docs/
    ├── system-analysis.md
    ├── architecture.md
    └── task-breakdown.md
```

---

## issue.md Content

The issue document should include:

```text
# Issue: {issue-title}

## Basic Information

- Issue ID:
- Created At:
- Branch:
- User Request:
- Current Mode: issue-create

## Project Background

Describe the assignment or project background.

## Objective

Describe what the final result should achieve.

## Input Files

List all known input files and their purposes.

## Expected Outputs

List final deliverables.

## Technical Constraints

List required tools, languages, libraries, frameworks, or formats.

## Forbidden Actions

List actions Codex must not do.

## Acceptance Criteria

List conditions for success.

## Open Questions

List missing or unclear information.

## Next Step

Recommend issue-breakdown as the next step.
```

---

## status.md Content

The status document should include:

```text
# Issue Status

## Current Stage

issue-create

## Completed

- Initial issue created.
- Known requirements summarized.

## todo

- Task breakdown.
- Implementation.
- Verification.
- Final closure.

## Blocked

- List missing information or files.

## Next Action

Run issue-breakdown.
```

---

## system-analysis.md Content

The system analysis document should explain:

* business or assignment scenario;
* major modules or sections;
* user-facing goals;
* grading or evaluation logic;
* input-output relationship;
* high-level data or code flow;
* important constraints.

For coursework assignments, focus on:

* assignment parts;
* scoring weights;
* required analyses;
* required outputs;
* report or notebook structure.

---

## architecture.md Content

The architecture document should explain the technical structure.

For coding projects, include:

* project directories;
* main modules;
* data flow;
* dependencies;
* configuration;
* testing structure.

For data analysis assignments, include:

* data files;
* notebook structure;
* analysis sections;
* visualization outputs;
* final report export process.

---

## task-breakdown.md Initial Content

During `issue-create`, create only a placeholder task breakdown.

Example:

```text
# Task Breakdown

## Current Status

Task breakdown has not been completed yet.

## Initial Phases

- Phase 1: Requirement understanding
- Phase 2: Task breakdown
- Phase 3: Implementation
- Phase 4: Verification
- Phase 5: Final closure

## Next Action

Run issue-breakdown to create atomic tasks.
```

---

## Completion Criteria

`issue-create` is complete when:

* memory directory exists;
* issue document exists;
* status document exists;
* system analysis document exists;
* architecture document exists;
* initial task-breakdown document exists;
* missing information is clearly listed;
* no implementation code has been written.

---

## Response Format

After completing `issue-create`, respond with:

```text
## Completed

- Created issue memory directory.
- Created initial issue documents.
- Summarized known requirements.

## Files Created or Updated

- memories/YYYYMM/CHANGEID/issue.md
- memories/YYYYMM/CHANGEID/status.md
- memories/YYYYMM/CHANGEID/docs/system-analysis.md
- memories/YYYYMM/CHANGEID/docs/architecture.md
- memories/YYYYMM/CHANGEID/docs/task-breakdown.md

## Planning Notes

- Missing information:
- Risks:
- Assumptions:

## Current Status

- done:
- todo:
- blocked:

## Next Step

Run issue-breakdown.
```
