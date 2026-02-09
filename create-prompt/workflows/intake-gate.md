# Workflow: Intake Gate

## Required Reading
1. references/question-templates.md
2. references/intelligence-rules.md

## Process
1. Check arguments
   - If the user provided no task description or it is vague, immediately ask the user in chat with a multiple-choice question:
     - header: "Task type"
     - question: "What kind of prompt do you need?"
     - options:
       - "Coding task" - Build, fix, or refactor code
       - "Analysis task" - Analyze code, data, or patterns
       - "Research task" - Gather information or explore options
   - Then ask: "Describe what you want to accomplish" (user can select "Other" for free text).

2. Adaptive analysis
   - Infer task type, complexity, prompt structure (single vs multiple), execution strategy (parallel vs sequential), and depth needed.
   - Use the rules in references/intelligence-rules.md.

3. Contextual questioning
   - Ask 2-4 questions based only on genuine gaps using the templates in references/question-templates.md.
   - Prefer options over free text when choices are knowable.

4. Decision gate
   - Ask the user in chat with a multiple-choice question:
     - header: "Ready"
     - question: "I have enough context to create your prompt. Ready to proceed?"
     - options:
       - "Proceed" - Create the prompt with current context
       - "Ask more questions" - I have more details to clarify
       - "Let me add context" - I want to provide additional information
   - If "Ask more questions", generate 2-4 new questions and repeat the gate.
   - If "Let me add context", accept additional context and re-evaluate.
   - If "Proceed", continue to generation.

5. Finalization
   - Confirm: "Creating a [simple/moderate/complex] [single/parallel/sequential] prompt for: [brief summary]".

## Success Criteria
- Missing or vague inputs are resolved.
- User selects "Proceed" from the decision gate.
- Complexity, structure, and execution strategy are determined.
