# Recommended Skill Structure

Use a simple single-file skill for small tasks. Use a router pattern for larger skills with multiple workflows.

## Router Pattern

```
skill-name/
+-- SKILL.md              # router + essential principles
+-- workflows/            # step-by-step procedures
+-- references/           # reusable knowledge
+-- templates/            # output structures
+-- scripts/              # executable code
```

## Why This Works

- Keeps SKILL.md small and always relevant.
- Lets workflows load only the references they need.
- Separates procedures from knowledge.

## SKILL.md Template (Router)

```markdown
---
name: skill-name
description: What it does and when to use it.
---

## Essential Principles
Short guidance that applies to every workflow.

## Intake
Ask the user what they want to do.

## Routing
Map intent to workflows.

## References
List key reference files.

## Workflows
List available workflows.
```

## Workflow Template

```markdown
# Workflow: Name

## Required Reading
1. references/example.md

## Process
1. Step one
2. Step two

## Success Criteria
- [ ] Done when...
```

## When To Use Router Pattern

- More than one distinct user intent
- Shared domain knowledge across workflows
- Expected growth beyond ~200 lines
