---
name: heal-skill
description: Heal skill documentation by applying corrections discovered during execution with approval workflow.
---

# Heal Skill Documentation

## Objective
Update a skill's SKILL.md and related files based on corrections discovered during execution.

Analyze the conversation to detect which skill is running, reflect on what went wrong, propose fixes, get approval, then apply changes with optional commit.

## Steps
1. Detect the target skill from conversation context; if unclear, ask.
2. Inspect the skill directory and related files; capture evidence of the issue.
3. Draft proposed changes using the reference templates.
4. Request approval before making edits.
5. Apply edits with `apply_patch` or shell tools, then verify and optionally commit.

## Workflows
- workflows/heal-skill.md

## References
- references/scan-commands.md
- references/proposed-changes-template.md
- references/approval-prompt.md

## Success Criteria
- Target skill identified and scoped.
- Proposed fixes documented with before/after text.
- Edits applied only after approval.
- Modified sections verified and consistent.
- Optional commit created if requested.
