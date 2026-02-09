# Troubleshoot MCP Server

## Required Reading`n
- [references/validation-checkpoints.md](../references/validation-checkpoints.md) - All validation checks




## Step: 1_identify_symptom

**Title**: Identify Symptom`n

Common symptoms:
- Server not appearing in `codex mcp list`
- Server showing ERR Disconnected
- "command not found" errors
- Environment variable not found
- Tools not working as expected
- Secrets visible in conversation (CRITICAL)


## Step: 2_gather_diagnostics

**Title**: Gather Diagnostics`n

Run these commands:
```bash
# Check server status
codex mcp list

# Check logs
tail -50 ~/Library/Logs/Codex/mcp-server-{name}.log

# Check if command exists
which uv && which node && which python

# Check environment variables (existence only, not values)
env | grep -E "^[A-Z_]+=" | cut -d= -f1 | sort
```


## Step: 3_diagnose

**Title**: Diagnose Issue`n

### Issue: not_appearing

**Symptom**: Server not in `codex mcp list`

**Causes**: 
- Server never added
- Wrong server name
- Config file syntax error


**Solution**: 
Check Codex config:
```bash
cat ~/.Codex/settings.json | jq '.mcpServers'
```
Re-add if missing using `codex mcp add` command.




### Issue: disconnected

**Symptom**: Server shows ERR Disconnected

**Causes**: 
- Command path incorrect
- Missing dependencies
- Syntax error in server code
- Missing environment variables


**Solution**: 
1. Check logs for specific error
2. Verify absolute paths: `which uv`, `which node`
3. Test server standalone: `cd ~/Developer/mcp/{name} && uv run python -m src.server`
4. Check for missing env vars in error message




### Issue: command_not_found

**Symptom**: "command not found" in logs

**Causes**: 
- Relative path used instead of absolute
- Tool not installed
- Wrong path in config


**Solution**: 
1. Find absolute path: `which uv` or `which node`
2. Update config with absolute path
3. Remove and re-add server:
```bash
codex mcp remove {name}
codex mcp add --transport stdio {name} -- /absolute/path/to/uv ...
```




### Issue: env_var_missing

**Symptom**: Environment variable not found

**Causes**: 
- Variable not set in ~/.zshrc
- Shell not reloaded after setting
- Variable name mismatch


**Solution**: 
1. Check if set: `echo $VAR_NAME`
2. If missing, add to ~/.zshrc:
```bash
echo 'export VAR_NAME="value"' >> ~/.zshrc
source ~/.zshrc
```
3. Restart Codex to pick up new variables




### Issue: secrets_visible

**Symptom**: Secrets visible in conversation

**Severity**: CRITICAL

**Solution**: 
1. STOP immediately
2. Delete conversation
3. Rotate compromised credentials
4. Never paste secrets in chat
5. Use environment variables with exact commands for user to run in terminal






## Step: 4_apply_fix

**Title**: Apply Fix`n

Based on diagnosis:
1. Make required changes
2. Run relevant validation checkpoint
3. Verify server connects: `codex mcp list`
4. Check logs are clean: `tail -20 ~/Library/Logs/Codex/mcp-server-{name}.log`




## Success Criteria`n
Troubleshooting complete when:
- Root cause identified
- Fix applied
- Server shows OK Connected
- No errors in recent logs
- User confirms issue resolved




