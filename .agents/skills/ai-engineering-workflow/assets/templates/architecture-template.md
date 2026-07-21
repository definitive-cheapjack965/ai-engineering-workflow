# Architecture

## Purpose

This document describes the technical structure and implementation plan for the issue.

It should guide implementation without adding unnecessary complexity.

---

## Related Issue

- **Issue ID**: {issue-id}
- **Issue Title**: {issue-title}

---

## Architecture Summary

{briefly describe how the project should be structured or completed}

---

## Project Structure

Record the expected or current file structure.

    {project-root}/
    ├── {folder-or-file}
    ├── {folder-or-file}
    └── {folder-or-file}

---

## Important Files

| File | Role | Expected Change |
|---|---|---|
| {file} | {what it does} | {create/modify/read only} |

---

## Data Flow / Work Flow

Describe how inputs become outputs.

1. {input or starting step}
2. {processing or implementation step}
3. {verification step}
4. {final output}

---

## Module / Component Plan

Use this section for coding, notebook, data analysis, document, slide, or research projects when the work can be divided into components.

| Component | Responsibility | Related Files |
|---|---|---|
| {component} | {what it handles} | {files} |

---

## Implementation Boundaries

### Allowed

- {what implementation may do}

### Not Allowed

- Do not add unrequested features.
- Do not introduce unnecessary frameworks.
- Do not modify unrelated files.
- Do not hide uncertainty or failed checks.

---

## Dependencies

| Dependency | Purpose | Required? | Notes |
|---|---|---|---|
| {dependency} | {why needed} | Yes/No | {notes} |

---

## Verification Plan

| Check | Command / Method | Expected Result |
|---|---|---|
| {test/check} | {command or manual method} | {expected result} |

If verification cannot be run, record the reason in `status.md`.

---

## Output Plan

| Output | Location | Verification |
|---|---|---|
| {output file} | {path} | {how to confirm it is correct} |

---

## Open Technical Questions

| Question | Impact | Decision |
|---|---|---|
| {question} | {impact} | {decision or pending} |
