---
name: create-command-skill
description: Create Codex command files (slash command hooks) with correct structure, validation, and testing.
---

# Create Codex Commands

## Objective
Create a Codex command file that invokes a skill or executes a structured instruction with correct frontmatter and safe defaults.

## Essential Principles
- Commands are lightweight entry points; keep them concise.
- Use YAML frontmatter with `description` and optional `argument-hint`.
- Prefer clear routing to a skill (single responsibility).
- Minimize questions; only ask when required data is missing.

## Intake
Ask for:
- Command name (filename) and target skill (or direct instruction).
- Command purpose (one sentence) and optional argument hint.
- Where the command should live if `$CODEX_HOME` is not set.

## Routing
| Response | Next Action | Workflow |
| --- | --- | --- |
| Create a new command | Gather requirements | workflows/create-command.md |
| Modify or audit a command | Ask for command path | workflows/verify-command.md |

If the user states intent directly ("create a command for X"), route immediately.

## References
- references/command-frontmatter.md
- references/command-best-practices.md

## Workflows
- create-command.md
- verify-command.md

## YAML Requirements

```yaml
---
description: Brief purpose of the command.
argument-hint: [optional hint]
---
```

## Success Criteria
- Command file created in the correct commands directory
- Frontmatter valid and concise
- Command content invokes the intended skill or instruction
- Quick dry-run walkthrough documented
