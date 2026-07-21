# Task Breakdown

## Purpose

This document breaks the issue into atomic, verifiable tasks.

It should be created or updated during `issue-breakdown`.

No implementation should happen during task breakdown.

---

## Related Issue

- **Issue ID**: {issue-id}
- **Issue Title**: {issue-title}

---

## Status Legend

- `todo`: not started
- `in_progress`: currently being worked on
- `blocked`: cannot proceed because information, files, or dependencies are missing
- `done`: completed and verified
- `done_unverified`: completed, but verification could not be fully run
- `skipped`: intentionally not done, with reason recorded
- `needs_review`: requires user, reviewer, or human confirmation

---

## Overall Plan

| Phase | Goal | Status |
|---|---|---|
| Phase 0 | Preparation and context validation | todo |
| Phase 1 | Core implementation or analysis | todo |
| Phase 2 | Integration and verification | todo |
| Phase 3 | Final documentation and closure | todo |

---

## Phase 0: Preparation

### Task 0.1: Validate Inputs

- **Status**: todo
- **Objective**: Confirm that required files, requirements, and context are available.
- **Related Files**:
  - `{file}`
- **Dependencies**: none
- **Acceptance Criteria**:
  - [ ] required files are identified;
  - [ ] missing files are recorded;
  - [ ] blockers are added to `status.md`.
- **Verification**:
  - file structure inspection;
  - requirement checklist review.

---

## Phase 1: Core Work

### Task 1.1: {task-name}

- **Status**: todo
- **Objective**: {specific objective}
- **Scope**:
  - {what is included}
- **Out of Scope**:
  - {what must not be done}
- **Related Files**:
  - `{file}`
- **Dependencies**:
  - {dependency or none}
- **Implementation Notes**:
  - {short notes}
- **Acceptance Criteria**:
  - [ ] {criterion}
  - [ ] {criterion}
- **Verification**:
  - {test command or manual check}

---

## Phase 2: Integration and Verification

### Task 2.1: Verify Project Output

- **Status**: todo
- **Objective**: Confirm that outputs match the original issue requirements.
- **Related Files**:
  - `{output-file}`
- **Dependencies**:
  - all required implementation tasks
- **Acceptance Criteria**:
  - [ ] final outputs exist;
  - [ ] outputs match requirements;
  - [ ] verification results are recorded.
- **Verification**:
  - run available tests or scripts;
  - inspect generated outputs;
  - compare against `issue.md`.

---

## Phase 3: Closure

### Task 3.1: Prepare Close Report

- **Status**: todo
- **Objective**: Summarize final deliverables, verification results, and known limitations.
- **Related Files**:
  - `close-report.md`
  - `status.md`
- **Dependencies**:
  - verification complete or limitations documented
- **Acceptance Criteria**:
  - [ ] `close-report.md` is complete;
  - [ ] final status is recorded;
  - [ ] known limitations are honest and clear.
- **Verification**:
  - manual review of close report.

---

## Execution Rules

During `issue-execute`:

- execute only one selected task or one clearly bounded task group;
- do not complete unrelated tasks silently;
- do not mark a task `done` without verification; use `done_unverified` when work is complete but verification could not be fully run;
- update `status.md` after meaningful progress;
- keep scope aligned with `issue.md`.
