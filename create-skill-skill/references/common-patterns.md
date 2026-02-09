# Common Patterns

## Pattern: Objective + Steps + Success Criteria

Use this for almost every skill. It creates a predictable, testable structure.

## Pattern: Context Then Action

If the task depends on state, add a Context section that lists commands to run or files to inspect before steps.

## Pattern: Output + Verification

When a task creates files or changes code, include Output and Verification sections to reduce ambiguity.

## Anti-Patterns

- Vague descriptions in YAML frontmatter.
- Large SKILL.md files that mix every workflow and reference.
- Deeply nested references.
- Unclear or missing success criteria.

## Example

```markdown
---
name: audit-foo
description: Audit foo config and report issues
---

## Objective
Audit foo configuration files and report risks.

## Context
Run `foo status` and inspect `foo.yaml`.

## Steps
1. Identify missing required keys.
2. Check for deprecated settings.
3. Summarize risks and fixes.

## Success Criteria
- All required keys evaluated
- Deprecated settings reported with fixes
```
