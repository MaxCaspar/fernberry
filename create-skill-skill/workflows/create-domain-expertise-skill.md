# Workflow: Create a Domain Expertise Skill

## Required Reading
1. references/recommended-structure.md
2. references/skill-structure.md
3. references/core-principles.md

## Process

0. Detect non-Codex input
   - If the user provides a non-Codex skill/agent/command, run workflows/convert-external-input.md first.

1. Define the domain and scope
   - Identify the domain boundaries and the intended use cases.

2. Design the router
   - Create SKILL.md with intake and routing.

3. Build the reference library
   - Organize references by sub-domain.
   - Keep files one level deep from SKILL.md.

4. Add workflows
   - Create workflows for common tasks in the domain.

5. Validate and test
   - Ensure all referenced files exist.
   - Test each workflow on a real question.

## Success Criteria

- Domain scope is clear and bounded
- Router correctly maps intents to workflows
- References are organized and reachable
- Workflows are complete and tested
