# issue-update and issue-status Guide

## Purpose

This document explains two related workflow modes:

```text
issue-update
issue-status
```

`issue-update` is used when requirements, plans, implementation details, or blockers change.

`issue-status` is used to inspect the current project progress.

Together, they create the feedback loop of the AI engineering workflow.

---

# Part 1: issue-update

## Purpose

`issue-update` keeps project documents synchronized with the latest requirement, implementation, or review feedback.

It prevents the project from drifting away from the user's actual needs.

---

## When To Use issue-update

Use `issue-update` when:

* the user changes requirements;
* assignment instructions are clarified;
* a task is found to be too large;
* a task must be split further;
* implementation reveals a new constraint;
* verification fails;
* data files are missing or inconsistent;
* the user asks to adjust the plan;
* the project scope changes;
* new deliverables are added or removed.

---

## Main Rule

Update the documents before continuing implementation.

Do not keep coding with outdated assumptions.

---

## Required Inputs

Before updating, read:

```text
memories/YYYYMM/CHANGEID/issue.md
memories/YYYYMM/CHANGEID/status.md
memories/YYYYMM/CHANGEID/docs/task-breakdown.md
```

Depending on the change, also read:

```text
memories/YYYYMM/CHANGEID/docs/system-analysis.md
memories/YYYYMM/CHANGEID/docs/architecture.md
```

---

## Update Procedure

### Step 1: Identify Change Type

Classify the change as one or more of:

```text
Requirement change
Scope change
Task breakdown change
Technical design change
Data or file change
Verification change
Blocker update
User feedback update
```

---

### Step 2: Locate Affected Documents

Use this mapping:

```text
Requirement changed          → issue.md, system-analysis.md
Technical structure changed  → architecture.md
Task plan changed            → task-breakdown.md
Progress changed             → status.md
Verification changed         → task-breakdown.md, status.md
Blocker discovered           → status.md, task-breakdown.md
Deliverable changed          → issue.md, task-breakdown.md, close-report.md if closing
```

---

### Step 3: Update Documents

Make the smallest necessary documentation change.

Do not rewrite all documents unless required.

Preserve useful history when the change affects traceability.

Recommended update note:

```text
## Update Log

### YYYY-MM-DD HH:MM

- Change type:
- Reason:
- Updated files:
- Impact:
- Next action:
```

---

### Step 4: Re-check Task Plan

After an update, check whether:

* any task should be split;
* any task should be removed;
* any dependency changed;
* any acceptance criteria changed;
* any verification method changed;
* any completed task needs review.

---

### Step 5: Report Update

Use this response format:

```text
## Completed

- Updated project documents based on the latest change.

## Files Created or Updated

- path/to/file1
- path/to/file2

## Update Notes

- Change type:
- Reason:
- Impact:

## Current Status

- done:
- todo:
- blocked:

## Next Step

- Recommended next command or task.
```

---

## What Not To Do During issue-update

Do not:

* implement code unless the user explicitly asks;
* hide the old requirement if it matters;
* silently change acceptance criteria;
* mark tasks complete without execution;
* remove blockers without solving them;
* rewrite unrelated documents.

---

# Part 2: issue-status

## Purpose

`issue-status` gives a clear view of current project progress.

It answers:

```text
What is done?
What is pending?
What is blocked?
What should happen next?
```

---

## When To Use issue-status

Use `issue-status` when:

* the user asks for progress;
* the user asks what remains;
* the user asks what to do next;
* a long task has been running;
* after several `issue-execute` operations;
* before `issue-close`;
* when the project state feels unclear.

---

## Required Inputs

Read:

```text
memories/YYYYMM/CHANGEID/status.md
memories/YYYYMM/CHANGEID/docs/task-breakdown.md
```

If available, also inspect:

```text
git status
```

For data or notebook projects, inspect whether required outputs exist.

---

## Status Categories

Use these task status categories:

```text
todo
in_progress
blocked
done
done_unverified
skipped
needs_review
```

---

## Status Procedure

### Step 1: Read Current Issue

Identify the current issue and read its status documents.

### Step 2: Inspect Task Breakdown

Count:

* total tasks;
* completed tasks;
* pending tasks;
* blocked tasks;
* tasks needing review.

### Step 3: Inspect Verification

Check whether completed tasks have verification notes.

If a completed task has no verification, mark it as needing review.

### Step 4: Inspect Git State

If Git is available, run or consider:

```text
git status
```

Report:

* clean working tree;
* modified files;
* untracked files;
* staged files.

Do not treat untracked generated files as final deliverables unless the project says so.

### Step 5: Recommend Next Action

Recommend one next step only.

Examples:

```text
Run issue-execute for Task 2.1.
Run issue-update because the data file name changed.
Run final verification before issue-close.
```

---

## Response Format

After running `issue-status`, respond with:

```text
## Current Status Summary

- Issue:
- Current stage:
- Overall progress:

## done

- Task list.

## in_progress

- Task list.

## todo

- Task list.

## blocked

- Task list and reason.

## Verification Notes

- Passed checks:
- Missing checks:
- Failed checks:

## Git Status

- Summary of working tree.

## Next Step

- Recommended next command or task.
```

---

## What Not To Do During issue-status

Do not:

* implement code;
* change files unless the user asks;
* mark tasks complete without evidence;
* ignore verification gaps;
* claim the working tree is clean without checking when Git is available.
