---
name: build-n8n-automations
description: Build n8n workflows with Codex assistance, from design to deployment.
---

# Build n8n Workflows

## Objective
Build reliable n8n workflows with Codex assistance across the full lifecycle: design, build, debug, test, optimize, and deploy.

## Essential Principles
- Design Before Building: Sketch the workflow flow (trigger -> nodes -> outputs) before touching the n8n canvas. Validate logic before wiring nodes.
- Use Native Nodes First: Search for existing nodes before using HTTP Request or Code nodes. Less custom code is more maintainable.
- Pin Data for Tests: Always pin data at trigger nodes during development. Never test with live/production data or credentials.
- Atomic Workflows: Each workflow should do one thing well. Chain workflows via triggers rather than building monoliths.
- Expression Safety: Use n8n expression syntax (`{{ }}`) correctly. Validate expressions before execution.

## Canonical Terminology
- workflow (avoid: automation, flow, pipeline)
- node (avoid: block, step, action)
- trigger (avoid: starter, initiator)
- execution (avoid: run, instance)
- expression (avoid: formula, template)
- credentials (avoid: secrets, keys, auth tokens)
- pin data (avoid: mock data, test data, sample data)

## Steps
1. Identify the user goal and classify the request: build, debug, add node, test, optimize, or deploy.
2. Load the required references for that workflow (see References section).
3. Follow the matching workflow file under `workflows/`.
4. Verify using the commands in Verification Commands.

## References
Batch 1 (Core Architecture):
- `references/architecture.md`
- `references/nodes-catalog.md`
- `references/expressions.md`

Batch 2 (Domain-Specific):
- `references/ai-nodes.md`
- `references/http-api.md`
- `references/code-nodes.md`

Batch 3 (Supporting):
- `references/testing-debugging.md`
- `references/performance.md`
- `references/deployment.md`

## Workflows
Batch 4 (Core Workflows):
- `workflows/build-workflow.md`
- `workflows/debug-workflow.md`
- `workflows/add-node.md`

Batch 5 (Supporting Workflows):
- `workflows/write-tests.md`
- `workflows/optimize-workflow.md`
- `workflows/deploy-workflow.md`

## Verification Commands
- Execute workflow with pin data in the n8n editor.
- Review execution history for errors.
- Compare output against expected results.

## Success Criteria
- The requested workflow change is implemented and validated with pin data.
- The execution history shows no errors.
- Output matches expected results.
