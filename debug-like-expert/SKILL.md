---
name: debug-like-expert
description: Deep analysis debugging mode for complex issues that activates methodical investigation, hypothesis testing, and rigorous verification when standard troubleshooting fails.
---

## Objective
Enter a rigorous, evidence-driven debugging mode. Favor scientific method over quick fixes, and treat your own code with more skepticism than unfamiliar code to avoid bias. Only propose solutions that are verified.

## Steps
1. Run the context scan to identify project domain and available expertise.
2. If a domain is detected, load the matching domain expertise before investigating.
3. Gather evidence: capture exact errors, reproduction steps, and expected vs actual behavior.
4. Map the system: trace the execution path, read relevant files completely, and identify dependencies.
5. Form falsifiable hypotheses and test them one at a time.
6. Confirm the root cause with evidence before changing code.
7. Implement the minimal change that addresses the root cause.
8. Verify the fix using the original reproduction steps and regression checks.
9. Present results in the required output format.

## Context Scan (PowerShell)
Run this at the start of every invocation and present findings before investigation.

```powershell
Write-Host "FILE_TYPES:"
Get-ChildItem -Recurse -File -ErrorAction SilentlyContinue |
  Where-Object { $_.Extension -match '^(\.py|\.js|\.jsx|\.ts|\.tsx|\.rs|\.swift|\.c|\.cpp|\.go|\.java)$' } |
  Select-Object -First 10 -ExpandProperty FullName

if (Test-Path "package.json") { Write-Host "DETECTED: JavaScript/Node project" }
if (Test-Path "Cargo.toml") { Write-Host "DETECTED: Rust project" }
if ((Test-Path "setup.py") -or (Test-Path "pyproject.toml")) { Write-Host "DETECTED: Python project" }
if ((Get-ChildItem -Filter "*.xcodeproj" -ErrorAction SilentlyContinue) -or (Test-Path "Package.swift")) { Write-Host "DETECTED: Swift/macOS project" }
if (Test-Path "go.mod") { Write-Host "DETECTED: Go project" }

Write-Host "EXPERTISE_SKILLS:"
Get-ChildItem "$env:USERPROFILE\.codex\skills\expertise" -ErrorAction SilentlyContinue |
  Select-Object -First 5 -ExpandProperty Name
```

## Domain Expertise
Domain-specific expertise lives in `$env:USERPROFILE\.codex\skills\expertise`.

### Scan Domains
```powershell
Get-ChildItem "$env:USERPROFILE\.codex\skills\expertise" -ErrorAction SilentlyContinue |
  Select-Object -ExpandProperty Name
```

### Inference Rules
If the user description or codebase indicates a domain, infer the skill:

- "Python", "game", "pygame", `.py` + game loop -> `expertise/python-games`
- "React", "Next.js", `.jsx` or `.tsx` -> `expertise/nextjs-ecommerce`
- "Rust", "cargo", `.rs` files -> `expertise/rust-systems`
- "Swift", "macOS", `.swift` + AppKit/SwiftUI -> `expertise/macos-apps`
- "iOS", "iPhone", `.swift` + UIKit -> `expertise/iphone-apps`
- "Unity", `.cs` + Unity imports -> `expertise/unity-games`
- "SuperCollider", `.sc`, `.scd` -> `expertise/supercollider`
- "Agent SDK", "agents-sdk" -> `expertise/with-agent-sdk`

If inferred, confirm with the user:
```
Detected: [domain] issue -> expertise/[skill-name]
Load this debugging expertise? (Y / see other options / none)
```

### If No Domain Is Obvious
Offer options:
```
What type of project are you debugging?

Available domain expertise:
1. macos-apps - macOS Swift (SwiftUI, AppKit, debugging, testing)
2. iphone-apps - iOS Swift (UIKit, debugging, performance)
3. python-games - Python games (Pygame, physics, performance)
4. unity-games - Unity (C#, debugging, optimization)
[... any others found in expertise/]

N. None - proceed with general debugging methodology
C. Create domain expertise for this domain
```

### Load Domain Expertise
When a domain is selected, read all references from that skill before investigation:

```powershell
Get-ChildItem "$env:USERPROFILE\.codex\skills\expertise\[domain]\references" -Filter "*.md" -ErrorAction SilentlyContinue |
  ForEach-Object { Get-Content -Raw $_.FullName }
```

Announce: "Loaded [domain] expertise. Investigating with domain-specific context."

If the domain skill is missing, inform the user and offer to proceed with general methodology or create the expertise.

## Investigation Workflow
### Evidence Gathering
- Document exact errors and behaviors.
- Capture exact reproduction steps.
- Record actual output vs expected output.
- Note when the issue started, if known.

### Map the System
- Trace execution path from entry point to failure.
- Identify components and dependencies.
- Read relevant files completely.

### Hypothesis Testing
- List candidate causes with supporting evidence.
- Define what would prove or disprove each.
- Test one hypothesis at a time.

### Solution Development
- Make the minimal change that addresses the confirmed root cause.
- Consider side effects and regressions.
- Verify with the original reproduction steps and related tests.

## Critical Rules
1. No drive-by fixes. Explain why the change works.
2. Verify everything. Test assumptions with evidence.
3. Use all tools available (MCP, web search, code reading) when needed.
4. Think out loud. Document reasoning and results.
5. One variable at a time. Change, verify, then proceed.
6. Read files completely. Do not skim.
7. Chase dependencies and configuration.
8. Re-examine earlier fixes. They may be wrong.

## Output Format
```markdown
## Issue: [Problem Description]

### Evidence
[What you observed - exact errors, behaviors, outputs]

### Investigation
[What you checked, what you found, what you ruled out]

### Root Cause
[The actual underlying problem with evidence]

### Solution
[What you changed and WHY it addresses the root cause]

### Verification
[How you confirmed this works and doesn't break anything else]
```

## References
- `references/debugging-mindset.md`
- `references/investigation-techniques.md`
- `references/hypothesis-testing.md`
- `references/verification-patterns.md`
- `references/when-to-research.md`

## Success Criteria
- Context scan executed and findings presented.
- Domain expertise loaded when available and relevant.
- Root cause confirmed with evidence.
- Fix verified using reproduction steps.
- Side effects checked.
- Solution is explainable and review-ready.
