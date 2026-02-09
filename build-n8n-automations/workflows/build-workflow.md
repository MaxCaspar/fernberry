# Workflow: Build Workflow

## Required Reading
1. `references/architecture.md`
2. `references/nodes-catalog.md`
3. `references/expressions.md`

## Process
1. Clarify the goal, inputs, outputs, and trigger type.
2. Sketch the workflow flow (trigger ? nodes ? outputs) and validate logic.
3. Choose native nodes first; use HTTP Request or Code nodes only when needed.
4. Wire nodes in the n8n canvas with clear naming.
5. Pin data at the trigger node and execute the workflow.
6. Validate outputs and adjust expressions as needed.

## Success Criteria
- Workflow executes successfully with pin data.
- Output matches the expected results.
