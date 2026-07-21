# issue-close Guide

## Purpose

`issue-close` is the final stage of the `ai-engineering-workflow` skill.

Its purpose is to close the issue honestly by collecting final deliverables, verification results, changed files, known limitations, and handoff notes.

This stage prevents unfinished or unverified work from being presented as fully complete.

---

## When To Use

Use `issue-close` when:

* all required tasks are completed;
* the user says the project is finished;
* the user asks for final delivery;
* the user asks to summarize the project;
* the user asks to prepare for submission or release;
* the user asks to publish after local testing.

Do not use `issue-close` when:

* required tasks are still pending;
* blockers remain unresolved;
* major verification has not been attempted;
* final deliverables do not exist;
* the user is still changing requirements.

---

## Main Rule

Do not claim full completion unless the required work has been verified.

Use honest status language:

```text
done
done_unverified
partially complete
blocked
not complete
```

---

## Required Inputs

Before closing, read:

```text
memories/YYYYMM/CHANGEID/issue.md
memories/YYYYMM/CHANGEID/status.md
memories/YYYYMM/CHANGEID/docs/task-breakdown.md
memories/YYYYMM/CHANGEID/docs/system-analysis.md
memories/YYYYMM/CHANGEID/docs/architecture.md
```

Also inspect:

```text
git status
```

If the project generated outputs, inspect whether those outputs exist.

Examples:

```text
output/*.pdf
output/*.html
output/*.ipynb
figures/*.png
reports/*.md
dist/
build/
```

---

## Close Procedure

### Step 1: Check Task Completion

Review `task-breakdown.md`.

Confirm:

* all required tasks are complete;
* no required tasks are still pending;
* no blockers remain unresolved;
* each completed task has verification notes.

If required tasks are incomplete, do not close. Recommend the next task.

---

### Step 2: Run or Review Final Verification

Run available final checks.

Examples:

```text
pytest
npm test
python script.py
jupyter nbconvert --execute
ruff check
mypy
notebook cell execution
manual file inspection
```

For data analysis assignments, check:

* datasets load correctly;
* analysis sections are complete;
* charts are generated;
* conclusions match data;
* final notebook/report exists;
* export format is correct.

For documentation-only skill projects, check:

* required Markdown files exist;
* skill name is consistent;
* paths are correct;
* README usage instructions are accurate;
* no private data is included.

---

### Step 3: Create Close Report

Create or update:

```text
memories/YYYYMM/CHANGEID/close-report.md
```

If the project is closing the skill development itself and no issue memory exists, create:

```text
examples/local-test-close-report.md
```

---

## Close Report Structure

Use this structure:

```text
# Close Report

## Issue Information

- Issue ID:
- Issue Title:
- Closed At:
- Final Status:

## Final Deliverables

- Deliverable 1:
- Deliverable 2:

## Completed Tasks

- Task 1:
- Task 2:

## Files Created or Updated

- path/to/file1
- path/to/file2

## Verification Results

- Check:
- Result:
- Notes:

## Git Summary

- Branch:
- Latest commit:
- Working tree status:

## Known Limitations

- Limitation 1:
- Limitation 2:

## Risks

- Risk 1:
- Risk 2:

## Handoff Notes

- How to use the result:
- What the user should check:
- Recommended next step:
```

---

## Final Response Format

After running `issue-close`, respond with:

```text
## Completed

- Closed the issue and created the final handoff report.

## Final Deliverables

- path/to/deliverable1
- path/to/deliverable2

## Files Created or Updated

- path/to/file1
- path/to/file2

## Verification

- Check performed:
- Result:
- Missing checks:

## Known Limitations

- Limitation:

## Current Status

- Final status:

## Next Step

- Recommended next action.
```

---

## What Not To Do

During `issue-close`, do not:

* claim completion without checking tasks;
* hide pending work;
* hide failed tests;
* delete temporary files unless safe and expected;
* publish to GitHub without reviewing private information;
* include private homework data or answers in public examples;
* create a final report that contradicts task status.

---

## GitHub Release Check

Before publishing a skill repository to GitHub, check:

```text
git status
git log --oneline
```

Review:

* README is complete;
* LICENSE exists;
* `.gitignore` is appropriate;
* skill name is consistent;
* examples contain no private data;
* no API keys or credentials exist;
* test plan is documented;
* local test result is recorded.
