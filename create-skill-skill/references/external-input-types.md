# External Input Types

Use these heuristics to classify non-Codex input.

## External Skill / Prompt
Signals:
- Large system prompt or instruction block.
- Descriptive goal with steps or constraints.
- Mentions of "system", "assistant", "instructions".
- Often a single file with prose and bullet points.

## External Agent Spec
Signals:
- Structured roles/goals/tools fields.
- JSON/YAML with keys like `role`, `tools`, `policies`, `capabilities`.
- Multi-section configuration with explicit tool definitions.

## External Command
Signals:
- Short file focused on a single action.
- Command name or alias in frontmatter or title.
- References to "slash command" or invocation format.

## Frontmatter and Schema Hints
- YAML/JSON fields like `name`, `description`, `instructions`, `tools` typically indicate skill/agent.
- If command-like frontmatter exists (name + short description + argument hint), treat as command.

## Ambiguous Cases
If multiple signals match, ask the user to confirm the input type.
