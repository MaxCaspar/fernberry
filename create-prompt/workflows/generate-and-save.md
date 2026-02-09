# Workflow: Generate And Save

## Required Reading
1. references/prompt-patterns.md
2. references/glob-and-numbering.md
3. references/intelligence-rules.md
4. references/decision-tree.md

## Process
1. Pre-generation analysis
   - Determine single vs multiple prompts.
   - If multiple, decide parallel vs sequential execution.
   - Select reasoning depth (standard vs extended thinking triggers).
   - Identify required tools, file references, and output locations.
   - Decide whether "go beyond basics", WHY explanations, examples, research/validation tags are needed.

2. Determine next prompt number
   - Use Glob `./prompts/*.md`.
   - If the directory does not exist, create it on first Write.
   - Choose the next sequential number using `references/glob-and-numbering.md`.

3. Generate prompt content
   - Use XML structures from references/prompt-patterns.md.
   - Always include objective, context, requirements, output, verification, and success criteria.
   - Include conditional tags and language based on analysis and rules.

4. Save prompt files
   - Single prompt: `./prompts/[number]-[name].md`.
   - Multiple prompts: sequential filenames for each prompt.
   - File contents must be ONLY the prompt XML, no extra commentary.

5. Post-save decision tree
   - Present the decision tree as inline text (not a special tool or UI).
   - Follow the actions in references/decision-tree.md.
   - If user chooses a run option, invoke `/run-prompt` with the correct arguments.

## Success Criteria
- Prompt(s) generated with correct XML structure and explicit instructions.
- Files saved with correct numbering and naming.
- Decision tree shown and correct `/run-prompt` action taken when requested.
