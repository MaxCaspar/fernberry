---
name: create-skill-skill
description: Expert guidance for creating, writing, building, and refining Codex skills and related / slash commands. Use when working with SKILL.md files, authoring new skills, improving existing skills, or standardizing skill structure and workflows.
---

# Create Codex Skills

## Essential Principles

- Skills are modular, filesystem-based guides for Codex.
- SKILL.md is always loaded when a skill triggers; keep it concise and decisive.
- Use Markdown headings (not XML tags). Favor clear section titles like Objective, Steps, and Success Criteria.
- Apply progressive disclosure: keep SKILL.md small and push deep details into references/.

## Intake

Ask the user what they want to do:

1. Create a new skill
2. Audit or modify an existing skill
3. Add a component (workflow, reference, template, script)
4. Get general guidance

Wait for the response before proceeding.

## Routing

| Response | Next Action | Workflow |
| --- | --- | --- |
| Non-Codex input (skill/agent/command) | Convert to Codex-native format | workflows/convert-external-input.md |
| 1, "create", "new", "build" | Ask if task-execution or domain-expertise skill | workflows/create-new-skill.md or workflows/create-domain-expertise-skill.md |
| 2, "audit", "modify", "existing" | Ask for skill path | workflows/audit-skill.md or workflows/verify-skill.md |
| 3, "add", "component" | Ask what to add | workflows/add-workflow.md, add-reference.md, add-template.md, add-script.md |
| 4, "guidance", "help" | Provide guidance | workflows/get-guidance.md |

If the user states intent directly ("add a workflow", "create skill for X"), route immediately.
After reading a workflow, follow it exactly.

## Quick Reference

Simple skill:

```markdown
---
name: skill-name
description: What it does and when to use it.
---

## Objective
What this skill does.

## Steps
1. Step one
2. Step two

## Success Criteria
- Done when...
```

Complex skill (router pattern):

- SKILL.md contains principles, intake, routing, and indexes.
- workflows/ contains step-by-step procedures.
- references/ contains domain knowledge.
- templates/ contains reusable output structures.
- scripts/ contains executable code.

## Slash Command Hook

If the user wants a slash command to invoke this skill, create a command file in `$CODEX_HOME/commands/` (or `~/.codex/commands/` if `$CODEX_HOME` is unset). Example:

```markdown
---
description: Create or modify Codex skills
argument-hint: [goal]
---

Use the create-skill-skill skill to help with: $ARGUMENTS
```

## References

- Structure: references/recommended-structure.md, references/skill-structure.md
- Principles: references/core-principles.md, references/be-clear-and-direct.md, references/use-structured-sections.md
- Patterns: references/common-patterns.md, references/workflows-and-validation.md
- Assets: references/using-templates.md, references/using-scripts.md
- Advanced: references/executable-code.md, references/api-security.md, references/iteration-and-testing.md
- Conversion: references/external-input-types.md, references/mapping-table.md, references/conversion-checklist.md, references/codex-skill-best-practices.md

## Templates

- templates/skill-skeleton.md
- templates/workflow-template.md
- templates/reference-template.md
- templates/command-template.md

## Workflows

- convert-external-input.md
- intake-and-detect.md
- convert-to-codex-skill.md
- convert-to-command.md
- convert-to-agent.md
- finalize-and-verify.md
- create-new-skill.md
- create-domain-expertise-skill.md
- audit-skill.md
- verify-skill.md
- add-workflow.md
- add-reference.md
- add-template.md
- add-script.md
- upgrade-to-router.md
- get-guidance.md

## YAML Requirements

```yaml
---
name: skill-name          # lowercase-with-hyphens, matches directory
description: ...          # What it does AND when to use it (third person)
---
```

## Success Criteria

A well-structured skill:

- Has valid YAML frontmatter
- Uses Markdown headings for structure
- Keeps SKILL.md under 500 lines
- Routes cleanly to workflows and references
- Minimizes unnecessary questions
- Has been tested with real usage
