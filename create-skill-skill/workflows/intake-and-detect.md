# Workflow: Intake And Detect

## Required Reading
1. references/external-input-types.md
2. references/conversion-checklist.md

## Process
1. Gather input
   - Ask for one of: file path, repo path, URL, or pasted text.
   - If a repo or URL is provided, locate the relevant file(s).
   - Capture the intended output: skill directory only or skill + command hook.

2. Extract metadata
   - Identify name, description, and any tool definitions.
   - Note any system prompt or instruction blocks.
   - Record any command aliases or slash-command indicators.

3. Heuristic detection
   - Apply the rules in references/external-input-types.md.
   - If a single type is clear, proceed with that route.

4. Fallback questions
   - If ambiguous, ask the user to confirm one of:
     - External skill/prompt
     - External agent spec
     - External command

## Success Criteria
- Input source is captured and accessible.
- Basic metadata extracted.
- Input type determined or explicitly confirmed by the user.
