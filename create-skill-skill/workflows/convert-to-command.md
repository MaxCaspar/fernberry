# Workflow: Convert To Command

## Required Reading
1. references/mapping-table.md
2. templates/command-template.md

## Process
1. Extract command intent
   - Identify command name, purpose, and arguments.
   - Capture any aliasing or triggers.

2. Create Codex command file
   - Use `templates/command-template.md`.
   - Place in `$CODEX_HOME/commands/` or `~/.codex/commands/`.

3. Link to skill if needed
   - If the command should invoke a skill, reference the skill name in the body.

## Success Criteria
- Command file created with correct frontmatter.
- Command behavior matches intent of the source command.
