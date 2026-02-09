---
name: create-prompt
description: Create Codex prompts with structured XML, save to ./prompts, and optionally run them.
---

# Create Prompt

## Objective
Turn a user task description into one or more high-quality Codex prompts using XML tags, save them under `./prompts/` with sequential numbering, and present the correct next-step decision tree.

## Steps
1. Run `workflows/intake-gate.md` to gather requirements, resolve gaps, and confirm readiness.
2. Run `workflows/generate-and-save.md` to build prompt files, save them, and present next-step options.

## References
- `references/question-templates.md`
- `references/intelligence-rules.md`
- `references/prompt-patterns.md`
- `references/glob-and-numbering.md`
- `references/decision-tree.md`

## Success Criteria
- Intake gate completed and user selected "Proceed".
- Prompt(s) generated with XML structure and explicit context, requirements, and verification.
- Files saved to `./prompts/[number]-[name].md` with correct sequential numbering.
- Decision tree presented inline and correct `/run-prompt` action chosen if requested.
