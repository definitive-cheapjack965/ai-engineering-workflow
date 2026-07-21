# issue-execute Guide

## Purpose

`issue-execute` is the implementation stage of the `ai-engineering-workflow` skill.

Its purpose is to execute one atomic task from the task breakdown, verify the result, and update project status.

This stage should turn a planned task into real project changes without expanding the scope.

---

## When To Use

Use `issue-execute` when:

* `issue-create` has already created the issue context;
* `issue-breakdown` has already created atomic tasks;
* the user asks to implement a specific task;
* the user asks to continue with the next task;
* the selected task has clear acceptance criteria and verification steps.

Do not use `issue-execute` when:

* no issue document exists;
* no task breakdown exists;
* the task scope is unclear;
* the selected task has unresolved blockers;
* the user only wants planning or explanation.

---

## Main Rule

Only execute one selected task or one clearly bounded task group.

Do not silently complete unrelated tasks.

Do not perform broad refactoring unless the selected task explicitly requires it.

---

## Required Inputs

Before implementing, read:

```text
memories/YYYYMM/CHANGEID/issue.md
memories/YYYYMM/CHANGEID/status.md
memories/YYYYMM/CHANGEID/docs/task-breakdown.md
```

Also read any related source files, notebooks, datasets, or configuration files listed in the selected task.

If these documents are missing, stop and recommend running `issue-create` and `issue-breakdown`.

---

## Execution Procedure

Follow this sequence every time.

### Step 1: Identify Current Issue

Find the current issue by:

1. reading the active branch name;
2. checking the latest `memories/YYYYMM/CHANGEID/` directory;
3. using a user-provided issue path if available.

If the current issue cannot be identified, ask the user to provide the issue path.

---

### Step 2: Select Task

Select the task from `task-breakdown.md`.

The task must include:

* task ID;
* task name;
* goal;
* scope;
* related files;
* dependencies;
* acceptance criteria;
* verification method;
* status.

If the user says "execute the next task", choose the first pending task whose dependencies are complete.

---

### Step 3: Check Dependencies

Before coding, verify that:

* required previous tasks are complete;
* required files exist;
* required data is available;
* required environment is available;
* acceptance criteria are clear.

If a dependency is missing, stop and report the blocker.

Do not guess missing files or fabricate outputs.

---

### Step 4: Confirm Scope Internally

Restate the task scope before editing.

Example:

```text
Executing Task 1.1 only:
- Load CSV files.
- Verify shapes and columns.
- Do not perform analysis or visualization yet.
```

This keeps implementation bounded.

---

### Step 5: Implement

Implement only the selected task.

Rules:

* modify only related files;
* keep code simple;
* follow existing project style;
* avoid unnecessary abstractions;
* avoid unrelated cleanup;
* avoid adding new dependencies unless required;
* preserve user work;
* do not delete files without confirmation.

For notebooks:

* edit only the relevant cells;
* keep outputs clear;
* do not remove assignment instructions;
* do not fake execution results.

For data analysis:

* verify data loading;
* check column names;
* document assumptions;
* keep charts readable;
* ensure conclusions are supported by data.

---

### Step 6: Verify

Run the verification method listed in the task.

Verification may include:

* running unit tests;
* running a script;
* running notebook cells;
* checking generated files;
* checking CSV loading;
* checking figure output;
* checking formatting;
* manually reviewing the modified file.

If verification cannot be run, state why.

Do not claim that verification passed if it was not actually run.

---

### Step 7: Update Documentation

After implementation, update:

```text
memories/YYYYMM/CHANGEID/docs/task-breakdown.md
memories/YYYYMM/CHANGEID/status.md
```

Update task status using one of:

```text
todo
in_progress
blocked
done
done_unverified
skipped
needs_review
```

If the task changed the project design or requirements, also update:

```text
memories/YYYYMM/CHANGEID/issue.md
memories/YYYYMM/CHANGEID/docs/architecture.md
memories/YYYYMM/CHANGEID/docs/system-analysis.md
```

---

## Task Completion Criteria

A task can be marked `done` only when:

* the selected task scope was implemented;
* acceptance criteria were satisfied;
* verification was run and passed;
* related documentation was updated.

A task should be marked `done_unverified` when:

* implementation is complete;
* verification could not be fully run;
* the reason is documented.

A task should be marked `blocked` when:

* required information is missing;
* required files are missing;
* dependencies are incomplete;
* the task cannot be safely implemented.

---

## Response Format

After running `issue-execute`, respond with:

```text
## Completed

- Executed Task {task-id}: {task-name}.
- Briefly explain what was implemented.

## Files Created or Updated

- path/to/file1
- path/to/file2

## Verification

- Check performed:
- Result:
- If not run, reason:

## Current Status

- done:
- todo:
- blocked:

## Next Step

- Recommended next task or command.
```

---

## What Not To Do

During `issue-execute`, do not:

* implement multiple unrelated tasks;
* rewrite the entire project;
* modify files not listed in the task unless necessary;
* add unrequested features;
* skip verification;
* claim success without checking;
* hide errors;
* change task status without actual work;
* delete or overwrite user files without confirmation;
* commit changes unless the user requested a commit or the project workflow requires it.

---

## Example

User request:

```text
Run issue-execute for Task 1.1 only.
```

Correct behavior:

1. Read the issue documents.
2. Find Task 1.1.
3. Check dependencies.
4. Implement only Task 1.1.
5. Run the listed verification.
6. Update task status.
7. Report changed files and next step.

Incorrect behavior:

```text
I completed Task 1.1, Task 1.2, Task 2.1, and wrote the final report.
```

That violates atomic task execution.
