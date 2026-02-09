# Workflow: Verify a Command

## Process

1. Locate the command file
   - Confirm path and filename.

2. Validate frontmatter
   - `description` present and concise.
   - `argument-hint` present only if needed.

3. Validate behavior
   - Command content calls the intended skill or instruction.
   - No extra prompts or multi-step instructions inside the command file.

4. Test
   - Run a dry-run with a sample argument and confirm expected behavior.

## Success Criteria

- Command frontmatter is valid
- Command intent matches user goal
- Dry-run passes
