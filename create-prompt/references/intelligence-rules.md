# Reference: Intelligence Rules

## Purpose
Set guardrails for prompt quality, depth, and clarity.

## Rules
1. Clarity first: if anything is unclear, ask before proceeding.
2. Context is critical: include WHY it matters, WHO it is for, and WHAT it will be used for.
3. Be explicit: use unambiguous instructions and specific outputs.
4. Scope assessment: simple tasks get concise prompts; complex tasks get comprehensive structure and extended thinking triggers.
5. Context loading: only request file reading when needed; keep file references specific.
6. Precision over brevity: longer, clear prompts are better than short, ambiguous ones.
7. Tool integration: include MCP servers only when explicitly mentioned or obviously beneficial.
8. Output clarity: always specify where outputs are saved using relative paths.
9. Verification always: include success criteria and explicit verification steps.
