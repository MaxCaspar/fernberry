# Workflow: Add Node

## Required Reading
1. `references/nodes-catalog.md`
2. `references/architecture.md`

## Process
1. Identify the new functionality and the best insertion point in the workflow.
2. Select the appropriate node (native first) and configure credentials if required.
3. Wire the node and update downstream expressions if data shape changes.
4. Pin data at the trigger node and execute the workflow.
5. Validate outputs and ensure no regressions.

## Success Criteria
- New node is integrated and workflow executes successfully.
- Outputs match expected results.
