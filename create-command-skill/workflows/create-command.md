# Workflow: Create a Command

## Required Reading
1. references/command-frontmatter.md
2. references/command-best-practices.md

## Process

1. Gather requirements
   - Command name (filename, without extension).
   - Command purpose (one sentence).
   - Target skill or direct instruction.
   - Optional `argument-hint`.
   - Desired commands directory (`$CODEX_HOME/commands/` or `~/.codex/commands/`).

2. Create the command file

```bash
cat > {commands-dir}/{command-name}.md << 'EOF'
---
description: {brief description}
argument-hint: [optional]
---

Use the {skill-name} skill to help with: $ARGUMENTS
EOF
```

3. Validate
   - Ensure YAML frontmatter is valid.
   - Confirm the target skill exists (or will exist).
   - Ensure command content is a single clear instruction.

4. Test
   - Run a quick dry-run: "Use the {command-name} command to do X".
   - Revise wording if the command intent is ambiguous.

## Success Criteria

- Command file created with correct frontmatter
- Command invokes the intended skill or instruction
- Tested with a realistic example
