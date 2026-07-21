# Quality Control Guide

## Purpose

This document defines the quality gates for the `ai-engineering-workflow` skill.

Quality control ensures that Codex does not simply generate output, but produces work that is scoped, verifiable, documented, and aligned with requirements.

---

## Quality Gate Overview

Every task should pass these gates:

```text
Requirement Gate
Scope Gate
Implementation Gate
Verification Gate
Documentation Gate
Git Gate
Handoff Gate
```

For data analysis and notebook tasks, also apply:

```text
Data Analysis Gate
Notebook Gate
```

---

## 1. Requirement Gate

Before implementation, check:

* Is the task supported by the user request?
* Is the task listed in `task-breakdown.md`?
* Are the expected inputs known?
* Are the expected outputs known?
* Are acceptance criteria defined?
* Are forbidden actions clear?
* Are missing details documented?

Fail this gate when:

* the task depends on guessed requirements;
* the task is not in the issue;
* the expected output is unclear;
* the task requires unavailable files.

Action if failed:

```text
Stop and run issue-update or ask for clarification.
```

---

## 2. Scope Gate

Before editing, check:

* Is the selected task atomic?
* Are related files listed?
* Are unrelated files excluded?
* Is the task small enough to verify independently?
* Are dependencies complete?

Fail this gate when:

* the task is too broad;
* the task mixes unrelated goals;
* the task requires large refactoring without approval;
* the task would change many unrelated files.

Action if failed:

```text
Run issue-breakdown again and split the task further.
```

---

## 3. Implementation Gate

During implementation, check:

* Is the code simple?
* Does it follow project style?
* Are variable and function names clear?
* Are comments useful but not excessive?
* Are new dependencies necessary?
* Are errors handled reasonably?
* Are existing user changes preserved?

Fail this gate when:

* implementation is over-engineered;
* unrelated features are added;
* code style conflicts with the project;
* new dependencies are added without reason;
* existing functionality is broken.

Action if failed:

```text
Refine only within the task scope or run issue-update if the plan must change.
```

---

## 4. Verification Gate

After implementation, check:

* Was the planned verification run?
* Did it pass?
* Are failures documented?
* Are skipped checks explained?
* Are generated outputs inspected?
* Are edge cases considered when relevant?

Fail this gate when:

* no verification was attempted;
* tests failed;
* output files are missing;
* the task is marked complete without evidence.

Action if failed:

```text
Fix the task if the failure is in scope.
Otherwise mark the task `blocked` or `done_unverified`.
```

---

## 5. Documentation Gate

After implementation, check:

* Was `task-breakdown.md` updated?
* Was `status.md` updated?
* Was the issue updated if scope changed?
* Was the architecture updated if design changed?
* Were blockers recorded?
* Were verification results recorded?

Fail this gate when:

* code changes but task status does not change;
* task status claims completion without notes;
* requirements changed but documents stayed outdated.

Action if failed:

```text
Update the relevant documents before continuing.
```

---

## 6. Git Gate

When Git is available, check:

```text
git status
```

Confirm:

* modified files are expected;
* untracked files are understood;
* no secrets are staged;
* no temporary junk files are staged;
* commit messages are meaningful when committing.

Fail this gate when:

* unexpected files changed;
* private files are staged;
* generated junk is staged;
* repository state is unclear.

Action if failed:

```text
Review file changes before committing.
```

---

## 7. Data Analysis Gate

For data analysis projects, check:

* data files exist;
* data loads successfully;
* required columns are present;
* missing values are handled or discussed;
* transformations are explained;
* charts have titles and labels;
* statistics are appropriate;
* conclusions are supported by data;
* final outputs match assignment requirements.

Fail this gate when:

* analysis uses the wrong file;
* column names are guessed;
* charts are unlabeled;
* conclusions are not supported;
* outputs are missing.

Action if failed:

```text
Fix the analysis or document the blocker.
```

---

## 8. Notebook Gate

For Jupyter Notebook projects, check:

* notebook opens successfully;
* cells run in order when possible;
* required outputs are visible;
* markdown explanations are clear;
* code cells are not overly complex;
* assignment instructions are not deleted;
* final notebook is saved;
* export format is produced if required.

Fail this gate when:

* cells are out of order;
* code depends on hidden state;
* outputs are missing;
* final export fails;
* notebook contains fake results.

Action if failed:

```text
Run or repair the relevant cells, then update verification notes.
```

---

## 9. Handoff Gate

Before closing, check:

* final deliverables exist;
* final limitations are listed;
* verification results are summarized;
* user knows how to use the output;
* next steps are clear;
* public release risks are reviewed.

Fail this gate when:

* final output path is unclear;
* limitations are hidden;
* private data might be included;
* release readiness is not checked.

Action if failed:

```text
Do not publish or close until handoff is clear.
```

---

## Public Repository Gate

Use this gate before publishing the skill or generated workflow records to GitHub.

Ask:

* Is the public author name and email correct?
* Are `LICENSE`, `README.md`, and installation notes ready for public readers?
* Are runtime `memories/` folders excluded unless intentionally published?
* Are private coursework answers, datasets, credentials, API keys, and personal paths absent?
* Is at least one local validation result recorded?

Fail the gate if private information is present or the release status is unclear.

---

## Final Quality Checklist

Use this checklist before marking a task complete:

```text
[ ] Requirement is clear.
[ ] Task scope is atomic.
[ ] Related files were inspected.
[ ] Only expected files were modified.
[ ] Implementation is simple and readable.
[ ] Verification was run, or the task was marked `done_unverified` / `skipped` with a clear reason.
[ ] Verification result is documented.
[ ] Task status was updated.
[ ] Git status was checked when available.
[ ] Next step is clear.
```

Use this checklist before publishing the skill:

```text
[ ] Skill name is consistent: ai-engineering-workflow.
[ ] SKILL.md has correct frontmatter.
[ ] AGENTS.md describes the repository rules.
[ ] Reference guides exist.
[ ] Templates exist.
[ ] README explains installation and usage.
[ ] Local test plan exists.
[ ] Local test result is recorded.
[ ] No private data is included.
[ ] Git history is clean enough for public release.
```
