# issue-breakdown Guide

## Purpose

`issue-breakdown` is the planning stage of the AI engineering workflow.

Its purpose is to convert a broad issue into small, clear, executable tasks.

This stage prevents Codex from trying to complete an entire project in one uncontrolled step.

---

## When To Use

Use `issue-breakdown` when:

* issue documents already exist;
* the user asks for a detailed plan;
* the task is too large to implement directly;
* the project has multiple deliverables;
* the project requires staged implementation;
* the user wants Codex to plan before coding.

---

## Main Rule

Do not implement code during `issue-breakdown`.

This stage only creates the execution plan.

---

## Required Inputs

Before starting, read:

* `issue.md`
* `status.md`
* `docs/system-analysis.md`
* `docs/architecture.md`
* any assignment instructions or README files
* any relevant source files or data file names

If these documents are missing, stop and recommend running `issue-create`.

---

## Breakdown Principles

When breaking down tasks, follow these principles:

### 1. Atomicity

Each task should be small enough to execute independently.

A good task usually has one clear goal.

Bad task:

```text
Complete the whole assignment.
```

Good task:

```text
Load the provided CSV files and verify row/column structure.
```

### 2. Clear Scope

Each task must define:

* what to do;
* what not to do;
* related files;
* expected output.

### 3. Dependency Awareness

If one task depends on another, write it clearly.

Example:

```text
Task 2.2 depends on Task 2.1 because charts cannot be generated before data cleaning is complete.
```

### 4. Acceptance Criteria

Each task must have a measurable completion condition.

Example:

```text
Acceptance criteria:
- CSV files load without errors.
- Data shape is printed or documented.
- Missing values are summarized.
```

### 5. Verification Method

Each task must say how it will be checked.

Example:

```text
Verification:
- Run notebook cells for data loading.
- Confirm no FileNotFoundError.
- Confirm expected columns exist.
```

---

## Recommended Structure

Use this structure:

```text
# Task Breakdown

## Issue Information

- Issue ID:
- Issue Title:
- Current Stage: issue-breakdown

## Overall Plan

- Phase 1:
- Phase 2:
- Phase 3:
- Phase 4:
- Phase 5:

## Task List

### Phase 1: Requirement and Data Preparation

#### Task 1.1: {task-name}

- Goal:
- Scope:
- Related files:
- Dependencies:
- Acceptance criteria:
- Verification:
- Status: `todo`

#### Task 1.2: {task-name}

- Goal:
- Scope:
- Related files:
- Dependencies:
- Acceptance criteria:
- Verification:
- Status: `todo`

## Execution Order

1. Task 1.1
2. Task 1.2
3. Task 2.1

## Risks and Blockers

- Risk:
- Blocker:

## Next Action

Run issue-execute for Task 1.1.
```

---

## Recommended Phases

For coding projects, use:

```text
Phase 1: Requirement and environment preparation
Phase 2: Core implementation
Phase 3: Integration
Phase 4: Testing and quality control
Phase 5: Documentation and closure
```

For data analysis assignments, use:

```text
Phase 1: Data preparation
Phase 2: Exploratory analysis
Phase 3: Required analysis sections
Phase 4: Visualization and interpretation
Phase 5: Final notebook/report validation
```

For research prototype projects, use:

```text
Phase 1: Baseline setup
Phase 2: Core method implementation
Phase 3: Experiment design
Phase 4: Result analysis
Phase 5: Final report and reproducibility check
```

---

## Task Size Rules

A task is too large if:

* it modifies many unrelated files;
* it requires several unrelated decisions;
* it cannot be verified independently;
* it mixes planning, coding, testing, and writing;
* it would take more than one clear implementation step.

When a task is too large, split it further.

---

## What Not To Do

During `issue-breakdown`, do not:

* write implementation code;
* generate final report content;
* run large experiments;
* modify source files;
* edit notebooks;
* mark tasks complete without execution;
* invent requirements;
* ignore missing information.

---

## Completion Criteria

`issue-breakdown` is complete when:

* all major deliverables are represented;
* tasks are atomic;
* each task has acceptance criteria;
* each task has verification method;
* dependencies are clear;
* risks and blockers are listed;
* the next executable task is identified.

---

## Response Format

After completing `issue-breakdown`, respond with:

```text
## Completed

- Created detailed task breakdown.
- Split the project into phases and atomic tasks.
- Added dependencies, acceptance criteria, and verification methods.

## Files Created or Updated

- memories/YYYYMM/CHANGEID/docs/task-breakdown.md
- memories/YYYYMM/CHANGEID/status.md

## Planning Notes

- Total phases:
- Total tasks:
- Main risks:
- Blockers:

## Current Status

- done:
- todo:
- blocked:

## Next Step

Run issue-execute for Task 1.1.
```
