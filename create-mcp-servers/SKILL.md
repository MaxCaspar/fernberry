---
name: create-mcp-servers
description: Create Model Context Protocol (MCP) servers that expose tools, resources, and prompts to Codex. Use when building custom integrations, APIs, data sources, or any server that Codex should interact with via the MCP protocol. Supports both TypeScript and Python implementations.
---

## Objective

MCP servers extend Codex's capabilities by exposing tools, resources, and prompts. This skill guides creation of production-ready MCP servers with API integrations, OAuth authentication, response optimization, and proper installation in Codex clients.


## Essential Principles


### The 5 Rules

Every MCP server must follow these:

1. **Never Hardcode Secrets** - Use `${VAR}` expansion in configs, environment variables in code
2. **Use `cwd` Property** - Isolates dependencies (not `--cwd` in args)
3. **Always Absolute Paths** - `which uv` to find paths, never relative
4. **One Server Per Directory** - `~/Developer/mcp/{server-name}/`
5. **Use `uv` for Python** - Better than pip, handles venvs automatically


### Security Checklist

- Never ask user to paste secrets into chat
- Always use environment variables for credentials
- Use ${VAR} expansion in configs
- Provide exact commands for user to run in terminal
- Verify environment variable existence without showing values
- Never hardcode API keys in code or configs


### Architecture Decision

Operation count determines architecture:

- **1-2 operations** -> Traditional pattern (flat tools)
- **3+ operations** -> On-demand discovery pattern (meta-tools)

Traditional: Each operation is a separate tool
On-demand: 4 meta-tools (discover, get_schema, execute, continue) + operations.json


### Context

MCP servers expose:
- **Tools**: Functions Codex can call (API requests, file operations, calculations)
- **Resources**: Data Codex can read (files, database records, API responses)
- **Prompts**: Reusable prompt templates with arguments

Standard location: `~/Developer/mcp/{server-name}/`




## Routing

- Guidance route: `workflows/get-guidance.md`

Based on user intent, route to appropriate workflow:

**No context provided** (skill invoked without description):
Ask the user in chat (multiple-choice when possible):
- header: "Mode"
- question: "What would you like to do?"
- options:
  - "Create a new MCP server" -> workflows/create-new-server.md
  - "Update an existing MCP server" -> workflows/update-existing-server.md
  - "Troubleshoot a server" -> workflows/troubleshoot-server.md
  - "Get guidance on MCP design" -> workflows/get-guidance.md

**Context provided** (user described what they want):
Route directly to workflows/create-new-server.md


## Workflows

| Workflow | Purpose |
|----------|---------|
| create-new-server.md | Full 8-step workflow from intake to verification |
| update-existing-server.md | Modify or extend an existing server |
| troubleshoot-server.md | Diagnose and fix connection/runtime issues |
| get-guidance.md | Help decide server type, operations, and architecture |


## Templates

| Template | Purpose |
|----------|---------|
| python-server.py | Traditional pattern starter for Python |
| typescript-server.ts | Traditional pattern starter for TypeScript |
| operations.json | On-demand discovery operations definition |


## Scripts

| Script | Purpose |
|--------|---------|
| setup-python-project.sh | Initialize Python MCP project with uv |
| setup-typescript-project.sh | Initialize TypeScript MCP project with npm |


## References

**Core workflow:**
- creation-workflow.md - Complete step-by-step with exact commands

**Architecture patterns:**
- traditional-pattern.md - For 1-2 operations (flat tools)
- large-api-pattern.md - For 3+ operations (on-demand discovery)

**Language-specific:**
- python-implementation.md - Async patterns, type hints
- typescript-implementation.md - Type safety, SDK features

**Advanced topics:**
- oauth-implementation.md - OAuth with stdio isolation
- response-optimization.md - Field truncation, pagination
- tools-and-resources.md - Resources API, prompts, streaming
- testing-and-deployment.md - Unit tests, packaging, publishing
- validation-checkpoints.md - All validation checks
- adaptive-questioning-guide.md - Question templates for intake
- api-research-template.md - API research document format


## Quick Reference

```bash
# List servers
codex mcp list

# Add server (Python)
codex mcp add --transport stdio <name> \
  --env API_KEY='${API_KEY}' \
  -- uv --directory ~/Developer/mcp/<name> run python -m src.server

# Add server (TypeScript)
codex mcp add --transport stdio <name> \
  --env API_KEY='${API_KEY}' \
  -- node ~/Developer/mcp/<name>/build/index.js

# Remove server
codex mcp remove <name>

# Check logs
tail -f <mcp-client-log-path>/mcp-server-<name>.log

# Find paths
which uv && which node && which python
```


## Troubleshooting Quick

**Server not appearing:** Check `codex mcp list`, verify config in your MCP client's settings

**"command not found":** Use absolute paths from `which uv` / `which node`

**Environment variable not found:**
```bash
echo $MY_API_KEY  # Check if set
echo 'export MY_API_KEY="value"' >> ~/.zshrc && source ~/.zshrc
```

**Secrets visible in conversation:** STOP. Delete conversation. Rotate credentials. Never paste secrets in chat.

Full troubleshooting: workflows/troubleshoot-server.md


## Success Criteria

A production-ready MCP server has:
- Valid configuration in Codex (`codex mcp list` shows OK Connected)
- Valid configuration in your MCP client's config
- Environment variables set securely in ~/.zshrc
- Architecture matches operation count
- OAuth stdio isolation if applicable
- Response optimization for list/search operations
- All validation checkpoints passed
- No errors in logs







