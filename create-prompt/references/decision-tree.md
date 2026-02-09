# Reference: Decision Tree

## Purpose
Provide post-save next-step options and the corresponding `/run-prompt` actions.

## Single Prompt
Presentation:
- "Prompt(s) created successfully!"
- "? Saved prompt to ./prompts/NNN-name.md"
- Options:
  1. Run prompt now
  2. Review/edit prompt first
  3. Save for later
  4. Other

Action:
- If user chooses #1: invoke `/run-prompt NNN`.

## Multiple Prompts (Parallel)
Presentation:
- "Prompt(s) created successfully!"
- List saved prompts.
- State: "Execution strategy: These prompts can run in PARALLEL (independent tasks, no shared files)"
- Options:
  1. Run all prompts in parallel now (launches sub-agents simultaneously)
  2. Run prompts sequentially instead
  3. Review/edit prompts first
  4. Other

Actions:
- If #1: `/run-prompt NNN NNN+1 NNN+2 --parallel`
- If #2: `/run-prompt NNN NNN+1 NNN+2 --sequential`

## Multiple Prompts (Sequential)
Presentation:
- "Prompt(s) created successfully!"
- List saved prompts.
- State: "Execution strategy: These prompts must run SEQUENTIALLY (dependencies: A ? B ? C)"
- Options:
  1. Run prompts sequentially now (one completes before next starts)
  2. Run first prompt only (NNN-name.md)
  3. Review/edit prompts first
  4. Other

Actions:
- If #1: `/run-prompt NNN NNN+1 NNN+2 --sequential`
- If #2: `/run-prompt NNN`
