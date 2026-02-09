# Create New MCP Server

## Required Reading`n
Before starting, ensure you understand:
- [references/creation-workflow.md](../references/creation-workflow.md) - Complete step-by-step commands
- Architecture pattern based on operation count (determined in Step 0)




## Step: 0_intake_gate

**Title**: Mandatory Intake Gate`n

**Critical First Action**: 
Intake must complete before any other action.
Do not analyze directories, search files, make assumptions, write code, or create files until intake complete.



**No Context Handler**: 
IF no context provided (user just invoked the skill without describing what to build):

Ask the user in chat with:
- header: "Mode"
- question: "What would you like to do?"
- options:
  - "Create a new MCP server" - Build a server from scratch based on an idea
  - "Update an existing MCP server" - Modify or improve a server I already have
  - "Get guidance on MCP design" - Help me figure out what kind of server I need

Routing after selection:
- "Create new" -> Ask: "Describe what you want Codex to be able to do" (plain text input)
- "Update existing" -> Route to workflows/update-existing-server.md
- "Guidance" -> Route to workflows/get-guidance.md

IF context was provided: Skip to adaptive_analysis.



**Adaptive Analysis**: 
Analyze the user's description to extract and infer:

**Extraction targets:**
- Server name: Explicit OR derive from service (e.g., "Spotify" -> "spotify-mcp")
- Language: Default Python unless TypeScript/Node.js ecosystem mentioned
- Purpose category: API integration, file operations, database access, custom tools
- Operation list: Explicit operations mentioned
- Operation count: Count to determine architecture

**Inference rules:**
- "search and get details" = 2 operations -> traditional architecture
- "full CRUD" = 4+ operations -> on-demand discovery
- Service name mentioned = API Integration purpose
- "Node.js", "npm", "TypeScript" mentioned = TypeScript language
- No language mentioned = Python (default)



**Contextual Questioning**: 
Generate 2-4 questions in chat based ONLY on genuine gaps.

**When service known:** Ask about specific endpoints, auth method, response optimization needs. Do NOT ask "what API?"

**When service vague:** First question: Which specific service?

**When operations unclear:** Ask about specific use cases to derive operations.

**Always infer:** If operations listed, count them. If name obvious, suggest it. If purpose clear, don't ask.

Question templates: [references/adaptive-questioning-guide.md](../references/adaptive-questioning-guide.md)



**Decision Gate**: 
After receiving answers, ask the user in chat:
- header: "Ready to proceed"
- question: "I've gathered requirements. Ready to proceed to API research?"
- options:
  - "Proceed to API research" - Start building
  - "Ask more questions" - I have gaps
  - "Let me add details" - Additional context

If "Ask more questions": Generate 2-4 NEW questions, present gate again.



**Finalization**: 
After "Proceed" selected:

1. Determine architecture from operation count:
   - 1-2 operations -> Traditional (flat tools)
   - 3+ operations -> On-demand discovery (meta-tools)

2. State confirmation:
   "I'll create a {language} MCP server called '{name}' with {count} operations using {architecture} architecture."

3. Proceed to Step 1





## Step: 1_api_research

**Title**: API Research & Documentation`n

**Delegate To Subagent**: 
This step is delegated to mcp-api-researcher subagent for token efficiency.

Skip only for non-API servers (file operations, custom calculations).

Launch using Task tool:
- subagent_type: "mcp-api-researcher"
- description: "Research {API-SERVICE-NAME} API for MCP server development"
- prompt: "Research the {API-SERVICE-NAME} API for MCP server '{SERVER-NAME}'. Required operations: {OPERATION-LIST}. Output directory: ~/Developer/mcp/{SERVER-NAME}/. Create API_RESEARCH.md with verified endpoints for each operation and run validations."

After subagent completes:
1. Review findings report
2. Read API_RESEARCH.md
3. If unverified endpoints: discuss with user
4. If failure: ask if user wants to proceed without research or cancel



**Fallback Protocol**: 
If subagent not available:

1. Try Context7 MCP server first:
   - Resolve library: mcp__context7__resolve-library-id
   - Fetch docs with resolved ID

2. Fall back to WebSearch:
   - Search: "{service-name} API documentation 2024"
   - Only use results dated 2024-2025

3. Create API_RESEARCH.md using [references/api-research-template.md](../references/api-research-template.md)

Validation: [references/validation-checkpoints.md#api-research](../references/validation-checkpoints.md#api-research)





## Step: 2_requirements

**Title**: Gather Additional Requirements`n

After API research validation passes:
- Required environment variables (from API_RESEARCH.md authentication section)
- Special dependencies (prioritize official SDK if exists)

Confirm plan with user before Step 3.


## Step: 3_project_structure

**Title**: Create Project Structure`n

Read: [references/creation-workflow.md](../references/creation-workflow.md) -> Step 2

Or use setup script:
- Python: `bash scripts/setup-python-project.sh {server-name}`
- TypeScript: `bash scripts/setup-typescript-project.sh {server-name}`

Validation: [references/validation-checkpoints.md#project-structure](../references/validation-checkpoints.md#project-structure)


## Step: 4_generate_code

**Title**: Generate Server Code`n

### Substep: 4a

**Title**: Load Architecture Pattern`n

IF 1-2 operations: Read [references/traditional-pattern.md](../references/traditional-pattern.md)
IF 3+ operations: Read [references/large-api-pattern.md](../references/large-api-pattern.md)


### Substep: 4b

**Title**: Load OAuth Pattern (if applicable)`n

IF OAuth detected: Read [references/oauth-implementation.md](../references/oauth-implementation.md)

Apply:
- stdout/stderr isolation with redirect context managers
- Pre-authorization script (authorize.py)
- Token caching
- Isolation around EVERY API call


### Substep: 4c

**Title**: Load Response Optimization`n

IF server returns lists/search results: Read [references/response-optimization.md](../references/response-optimization.md)

Apply:
- Field truncation (FIELD_CONFIGS per resource type)
- Token estimation
- Truncation in execute handler BEFORE pagination
- Adaptive pagination for responses > 20k tokens


### Substep: 4d

**Title**: Write Code`n

Verify loaded:
- Architecture pattern (4a)
- OAuth pattern (4b) if applicable
- Response optimization (4c) if applicable

Use templates as starting point:
- Python: [templates/python-server.py](../templates/python-server.py)
- TypeScript: [templates/typescript-server.ts](../templates/typescript-server.ts)
- Operations: [templates/operations.json](../templates/operations.json)

Write to: `src/server.py` or `src/index.ts`

Validation: [references/validation-checkpoints.md#code-syntax](../references/validation-checkpoints.md#code-syntax)




## Step: 5_env_vars

**Title**: Configure Environment Variables`n

**Security Critical**: 
NEVER ask user to paste secrets into chat.



1. List required variables and where to get them
2. Provide exact commands for user to run in terminal
3. Wait for confirmation via a direct user question in chat
4. Verify existence without showing values

Read: [references/creation-workflow.md](../references/creation-workflow.md) -> Step 4

Validation: [references/validation-checkpoints.md#env-vars](../references/validation-checkpoints.md#env-vars)


## Step: 6_Codex_code_install

**Title**: Install in Codex`n

Read: [references/creation-workflow.md](../references/creation-workflow.md) -> Step 5

Use absolute paths (`which uv`, `which node`) and `${VAR}` expansion.

Validation: [references/validation-checkpoints.md#Codex-code-install](../references/validation-checkpoints.md#Codex-code-install)


## Step: 7_Codex_desktop_install

**Title**: Install in Codex Desktop`n

Read: [references/creation-workflow.md](../references/creation-workflow.md) -> Step 6

Update `~/Library/Application Support/Codex/codex_desktop_config.json`

Validation: [references/validation-checkpoints.md#Codex-desktop-config](../references/validation-checkpoints.md#Codex-desktop-config)


## Step: 8_test_verify

**Title**: Test and Verify`n

Read: [references/creation-workflow.md](../references/creation-workflow.md) -> Step 7

**Final Checklist**: 
- Server appears in `codex mcp list` with OK Connected
- Environment variables exist in ~/.zshrc
- No secrets visible in conversation
- Server added to Codex Desktop config
- Standalone test passes
- No errors in logs: `~/Library/Logs/Codex/mcp-server-{name}.log`







## Success Criteria`n
Server is complete when:
- All 8 steps executed
- All validation checkpoints passed
- `codex mcp list` shows OK Connected
- No errors in logs




