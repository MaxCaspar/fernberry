# Skill Structure

Skills have three parts:

1. YAML frontmatter (metadata)
2. Markdown body (instructions)
3. File layout (progressive disclosure)

## YAML Frontmatter

Required fields:

```yaml
---
name: skill-name
description: What it does and when to use it.
---
```

- `name` must match the directory name (lowercase, hyphens).
- `description` is the primary trigger. Be explicit.

## Markdown Body

Use clear headings like Objective, Steps, and Success Criteria. Avoid XML tags.

## File Layout

- `SKILL.md` for routing and essentials.
- `workflows/` for procedures.
- `references/` for reusable knowledge.
- `templates/` for output structures.
- `scripts/` for executable code.

Keep references one level deep from SKILL.md.
