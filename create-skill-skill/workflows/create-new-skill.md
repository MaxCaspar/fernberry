# Workflow: Create a New Skill

## Required Reading
1. references/recommended-structure.md
2. references/skill-structure.md
3. references/core-principles.md
4. references/use-structured-sections.md

## Process

0. Detect non-Codex input
   - If the user provides a non-Codex skill/agent/command, run workflows/convert-external-input.md first.

1. Gather requirements
   - Ask what the skill should do and who it serves.
   - Clarify inputs, outputs, and constraints.

2. Decide structure
   - Simple single-file skill for small scope.
   - Router pattern for multiple workflows or large domains.

3. Create directories

```bash
mkdir -p $CODEX_HOME/skills/{skill-name}
mkdir -p $CODEX_HOME/skills/{skill-name}/workflows
mkdir -p $CODEX_HOME/skills/{skill-name}/references
mkdir -p $CODEX_HOME/skills/{skill-name}/templates
mkdir -p $CODEX_HOME/skills/{skill-name}/scripts
```

4. Write SKILL.md
   - Add YAML frontmatter.
   - Use Markdown headings: Objective, Steps, Success Criteria.
   - Add routing sections if using the router pattern.

5. Add workflows and references
   - Keep procedures in workflows/.
   - Put reusable knowledge in references/.

6. Add a slash command (optional)

```bash
cat > $CODEX_HOME/commands/{skill-name}.md << 'EOF'
---
description: {brief description}
argument-hint: [optional]
---

Use the {skill-name} skill to help with: $ARGUMENTS
EOF
```

7. Validate and test
   - Check frontmatter and file paths.
   - Run a real task through the skill and iterate.

## Success Criteria

- Skill directory exists with expected structure
- SKILL.md is concise and valid
- Workflows and references are linked correctly
- Slash command works if created
- Tested on a real example
