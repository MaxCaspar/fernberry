# Workflow: Convert To Codex Skill

## Required Reading
1. references/mapping-table.md
2. references/codex-skill-best-practices.md
3. templates/skill-skeleton.md
4. templates/workflow-template.md
5. templates/reference-template.md

## Process
1. Define the target skill
   - Choose the Codex skill name (lowercase, hyphens).
   - Draft a concise description that includes what it does and when to use it.

2. Map core content
   - Convert external system prompt/instructions into Codex SKILL.md Objective and Essential Principles.
   - Convert any tool usage or safety constraints into references or workflow steps.

3. Build directory structure
   - Create `workflows/`, `references/`, `templates/` as needed.
   - Keep SKILL.md under 500 lines; move depth into references.

4. Create workflows
   - Break large procedures into named workflows.
   - Use `templates/workflow-template.md` as the base.

5. Add references
   - Extract reusable knowledge into reference files.
   - Use `templates/reference-template.md` for consistency.

6. Finalize SKILL.md
   - Ensure YAML frontmatter matches directory name.
   - Link workflows and references.

## Success Criteria
- Codex skill directory created with correct structure.
- SKILL.md contains valid YAML frontmatter and routing as needed.
- Workflows and references are linked and loadable.
