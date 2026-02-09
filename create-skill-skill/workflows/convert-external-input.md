# Workflow: Convert External Input to Codex-Native

## Objective
Detect non-Codex skill/agent/command inputs and convert them to Codex-native format using best practices before proceeding with create-skill-skill workflows.

## Process

1. Detect non-Codex input
   - Look for cues like third-party model mentions, "system prompt", "tool use", agent specs, or non-Codex command formats.
   - If uncertain, ask the user to confirm whether the input was built for a non-Codex system.

2. Route to conversion
   - Run workflows/intake-and-detect.md to classify the input type.
   - Ask for the desired output (skill directory only or skill + command hook).

3. Complete conversion
   - Run the matching conversion workflow:
     - workflows/convert-to-codex-skill.md
     - workflows/convert-to-command.md
     - workflows/convert-to-agent.md
   - Always finish with workflows/finalize-and-verify.md.
   - Ensure the converted SKILL.md uses Objective, Steps, Success Criteria.
   - Ensure workflows, references, templates, and scripts follow progressive disclosure.

4. Return to create-skill-skill
   - If the user wants additional changes, continue with the relevant create-skill-skill workflow.

## Success Criteria

- Non-Codex input detected or confirmed.
- Codex-native skill directory produced using best practices.
- User guided to next appropriate create-skill-skill workflow if needed.
