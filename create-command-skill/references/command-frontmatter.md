# Command Frontmatter

Commands are lightweight Markdown files with YAML frontmatter:

```yaml
---
description: Brief purpose of the command.
argument-hint: [optional hint]
---
```

- Keep `description` under 100 characters.
- Use `argument-hint` only when the command expects arguments.
