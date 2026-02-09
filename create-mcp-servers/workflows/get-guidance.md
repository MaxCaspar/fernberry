# Get Guidance For MCP Server Design

## Objective
Help the user decide the right MCP server type, operations, architecture, and language before building.

## Step 1: Clarify The Goal
Ask what Codex should be able to do. Identify whether this is:
- API integration
- File operations
- Database access
- Custom tools or calculations

## Step 2: Determine Operations
Extract a concrete list of operations the server must support. Count them.

## Step 3: Choose Architecture
- 1-2 operations -> Traditional pattern (flat tools)
- 3+ operations -> On-demand discovery pattern (meta-tools + operations.json)

References:
- [references/traditional-pattern.md](../references/traditional-pattern.md)
- [references/large-api-pattern.md](../references/large-api-pattern.md)

## Step 4: Choose Language
- Default: Python
- Use TypeScript if user prefers Node.js / npm / TS ecosystem

## Step 5: Route To Build
Summarize the decisions and route to:
- [workflows/create-new-server.md](./create-new-server.md)

References:
- [references/best-practices.md](../references/best-practices.md)

