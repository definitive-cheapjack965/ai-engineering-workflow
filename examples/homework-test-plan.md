# Homework Test Plan

## Purpose

This example describes how to test the `ai-engineering-workflow` skill on a typical coursework or data analysis project.

The goal is not to provide a complete assignment solution.
The goal is to verify that Codex follows the engineering workflow:

1. understand the request;
2. create structured project context;
3. break the work into atomic tasks;
4. execute one bounded task at a time;
5. update status and verification records;
6. close the issue with an honest handoff report.

---

## Test Scenario

Use a small coursework-style data analysis task.

Example task:

> Given one CSV file and one assignment instruction document, create a short data analysis notebook and a final report. The analysis should include basic descriptive statistics, at least one chart, and a short written conclusion.

This scenario is intentionally simple, but it tests the same workflow needed for larger assignments.

---

## Suggested Test Files

Create a temporary test project with files such as:

```text
test-homework-project/
├── data/
│   └── sample_data.csv
├── instructions/
│   └── assignment-instructions.md
└── README.md
```

Example `sample_data.csv` can contain simple columns such as:

```csv
student_id,group,score,hours_studied
1,A,82,5
2,A,91,7
3,B,75,3
4,B,88,6
5,A,79,4
6,B,93,8
```

Example assignment requirement:

```text
Use the dataset to compare score differences between groups A and B.
Create one table, one chart, and a short conclusion.
Use Python with pandas and matplotlib.
Do not add extra features beyond the assignment requirements.
```

---

## Skill Invocation Flow

In Codex, run the workflow step by step.

### Step 1: Create Issue

```text
/issue-create Analyze the sample homework dataset and generate a short notebook-style analysis with one chart and one conclusion.
```

Expected behavior:

* Codex identifies the current working context and creates a feature branch only when the workflow or repository rules require it.
* Codex creates a new memory folder:

```text
memories/YYYYMM/CHANGEID/
├── issue.md
├── status.md
└── docs/
    ├── system-analysis.md
    ├── architecture.md
    └── task-breakdown.md
```

Expected checks:

* `issue.md` records the user request.
* `docs/system-analysis.md` explains the assignment context.
* `docs/architecture.md` explains the technical approach.
* `status.md` records the current stage.
* `docs/task-breakdown.md` may be only an initial placeholder during this step. It is formally completed during `issue-breakdown`.

Codex should not start coding during this step.

---

### Step 2: Break Down Tasks

```text
/issue-breakdown
```

Expected behavior:

* Codex reads the issue context.
* Codex creates or formally completes `docs/task-breakdown.md`.
* Codex breaks the assignment into small tasks.

Example task breakdown:

```text
Task 0.1: Confirm input files
Task 1.1: Load CSV data
Task 1.2: Compute descriptive statistics
Task 1.3: Generate one chart
Task 1.4: Write short conclusion
Task 2.1: Verify outputs
Task 3.1: Prepare close report
```

Expected checks:

* each task has a clear objective;
* each task has related files;
* each task has acceptance criteria;
* each task has verification instructions;
* no implementation happens during breakdown.

---

### Step 3: Execute One Task

```text
/issue-execute next
```

Expected behavior:

* Codex executes only the next atomic task.
* Codex updates task status.
* Codex updates `status.md`.

Expected checks:

* Codex does not complete unrelated tasks silently;
* changed files match the selected task;
* verification is recorded honestly.

---

### Step 4: Update After a Requirement Change

Introduce a controlled change, for example:

```text
Use issue-update mode. Replace the original chart requirement with a bar chart and record that the input filename changed from sample_data.csv to revised_sample_data.csv. Update the workflow documents only; do not continue implementation.
```

Expected behavior:

* Codex identifies the changed requirement and input file.
* Codex updates affected assumptions, related files, acceptance criteria, dependencies, and status.
* Codex does not perform unrelated implementation.
* Previously completed work is marked for review or re-verification when the change invalidates it.

Expected checks:

* `issue.md`, `docs/task-breakdown.md`, and `status.md` reflect the new requirement;
* outdated filenames or acceptance criteria are removed or clearly superseded;
* the change is traceable and no unrelated task is completed.

---

### Step 5: Check Status

```text
Use issue-status mode.
```

Expected behavior:

* Codex summarizes current progress.
* Codex lists completed, pending, blocked, and unverified tasks.
* Codex reports verification status and the effect of the requirement change.

Expected checks:

* `status.md` is up to date;
* blockers are clearly recorded if any exist;
* unfinished or invalidated tasks are not marked complete.

---

### Step 6: Close Issue

```text
/issue-close
```

Expected behavior:

* Codex creates or updates `close-report.md`.
* Codex summarizes final deliverables.
* Codex records changed files and verification results.
* Codex clearly states known limitations.

Expected checks:

* `close-report.md` exists;
* deliverables are listed;
* verification results are honest;
* no private information is included.

---

## Expected Final Memory Structure

After the full test, the memory folder should look like:

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

## Pass Criteria

The skill passes this test if:

* [ ] Codex does not jump directly into implementation during `issue-create`.
* [ ] Codex creates the correct memory folder structure.
* [ ] Codex fills the required workflow documents.
* [ ] Codex breaks the work into atomic tasks.
* [ ] Codex executes only one bounded task at a time.
* [ ] Codex handles a controlled requirement change through `issue-update` before further implementation.
* [ ] Codex updates affected issue, task, and status documents consistently.
* [ ] Codex updates `status.md` after meaningful progress.
* [ ] Codex records verification results honestly.
* [ ] Codex creates `close-report.md` before closing.
* [ ] Codex does not invent missing files or requirements.
* [ ] Codex does not include private data, secrets, or unrelated changes.

---

## Failure Cases to Watch

The test should be considered failed or partially failed if Codex:

* starts coding before issue creation and task breakdown;
* creates old split runtime folders instead of using the unified `docs/` structure;
* marks tasks complete without verification;
* adds unrequested features;
* modifies unrelated files;
* hides missing input files;
* continues implementation using outdated requirements instead of running `issue-update`;
* fails to update `status.md`;
* closes the issue without a final report.

---

## Notes

This example is intentionally lightweight.
For real coursework or project work, the same workflow should be applied with richer requirements, more input files, and stricter verification.
