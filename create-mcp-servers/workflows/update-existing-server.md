# Update Existing MCP Server

## Required Reading`n
- [references/validation-checkpoints.md](../references/validation-checkpoints.md) - For verifying changes




## Step: 1_identify

**Title**: Identify Server`n

List installed servers:
```bash
codex mcp list
```

Ask user which server to modify and what changes are needed.


## Step: 2_locate

**Title**: Locate Server Files`n

Standard location: `~/Developer/mcp/{server-name}/`

Read current implementation:
- `src/server.py` or `src/index.ts`
- `pyproject.toml` or `package.json`
- Any `operations.json` if using on-demand discovery pattern


## Step: 3_understand

**Title**: Understand Current Architecture`n

Determine current pattern:
- Traditional (flat tools): Look for `@app.list_tools()` returning Tool list
- On-demand discovery: Look for 4 meta-tools (discover, get_schema, execute, continue)

Note current:
- Operation count
- Authentication method
- Response optimization (if any)


## Step: 4_plan_changes

**Title**: Plan Changes`n

Based on user's request, determine:
- Adding new operations? May require architecture change if crossing 2->3 threshold
- Changing auth? May need OAuth pattern from [references/oauth-implementation.md](../references/oauth-implementation.md)
- Adding list/search? May need response optimization from [references/response-optimization.md](../references/response-optimization.md)

Present plan to user for confirmation.


## Step: 5_implement

**Title**: Implement Changes`n

Make changes following the same patterns used in create workflow:
- Load relevant references for new functionality
- Apply patterns consistently with existing code
- Update operations.json if using on-demand discovery


## Step: 6_verify

**Title**: Verify Changes`n

Run relevant validation checkpoints:
- [references/validation-checkpoints.md#code-syntax](../references/validation-checkpoints.md#code-syntax)
- [references/validation-checkpoints.md#Codex-code-install](../references/validation-checkpoints.md#Codex-code-install)

Test:
```bash
codex mcp list
# Should show OK Connected

# Check logs for errors
tail -20 ~/Library/Logs/Codex/mcp-server-{name}.log
```




## Success Criteria`n
Update is complete when:
- Changes implemented
- Server still shows OK Connected in `codex mcp list`
- No new errors in logs
- User confirms functionality works as expected




