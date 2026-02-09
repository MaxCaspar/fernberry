## Overview
Codex-executable plans have a specific format that enables Codex to implement without interpretation. This reference defines what makes a plan executable vs. vague.

**Key insight:** PLAN.md IS the executable prompt. It contains everything Codex needs to execute the phase, including objective, context references, tasks, verification, success criteria, and output specification.


## Core Principle
A plan is Codex-executable when Codex can read the PLAN.md and immediately start implementing without asking clarifying questions.

If Codex has to guess, interpret, or make assumptions - the task is too vague.


## Prompt Structure
Every PLAN.md follows this XML structure:

```markdown
---
phase: XX-name
type: execute
domain: [optional]
---

## Objective
[What and why]
Purpose: [...]
Output: [...]


## Context
@.planning/BRIEF.md
@.planning/ROADMAP.md
@relevant/source/files.ts


## Tasks
### Task (type="auto")
  ## NameTask N: [Name]
  ## Files[paths]
  ## Action[what to do, what to avoid and WHY]
  ## Verify[command/check]
  ## Done[criteria]


### Task (type="checkpoint:human-verify" gate="blocking")
  ## What Built[what Codex automated]
  ## How To Verify[numbered verification steps]
  ## Resume Signal[how to continue - "approved" or describe issues]


### Task (type="checkpoint:decision" gate="blocking")
  ## Decision[what needs deciding]
  ## Context[why this matters]
  ## Options
    ## Option## Name[Name]## Pros[pros]## Cons[cons]
    ## Option## Name[Name]## Pros[pros]## Cons[cons]
  
  ## Resume Signal[how to indicate choice]



## Verification
[Overall phase checks]


## Success Criteria
[Measurable completion]


## Output
[SUMMARY.md specification]

```


## Task Anatomy
Every task has four required fields:

## Field
**What it is**: Exact file paths that will be created or modified.

**Good**: `src/app/api/auth/login/route.ts`, `prisma/schema.prisma`
**Bad**: "the auth files", "relevant components"

Be specific. If you don't know the file path, figure it out first.


## Field
**What it is**: Specific implementation instructions, including what to avoid and WHY.

**Good**: "Create POST endpoint that accepts {email, password}, validates using bcrypt against User table, returns JWT in httpOnly cookie with 15-min expiry. Use jose library (not jsonwebtoken - CommonJS issues with Next.js Edge runtime)."

**Bad**: "Add authentication", "Make login work"

Include: technology choices, data structures, behavior details, pitfalls to avoid.


## Field
**What it is**: How to prove the task is complete.

**Good**:
- `npm test` passes
- `curl -X POST /api/auth/login` returns 200 with Set-Cookie header
- Build completes without errors

**Bad**: "It works", "Looks good", "User can log in"

Must be executable - a command, a test, an observable behavior.


## Field
**What it is**: Acceptance criteria - the measurable state of completion.

**Good**: "Valid credentials return 200 + JWT cookie, invalid credentials return 401"

**Bad**: "Authentication is complete"

Should be testable without subjective judgment.



## Task Types
Tasks have a `type` attribute that determines how they execute:

## Type
**Default task type** - Codex executes autonomously.

**Structure:**
```xml
### Task (type="auto")
  ## NameTask 3: Create login endpoint with JWT
  ## Filessrc/app/api/auth/login/route.ts
  ## ActionPOST endpoint accepting {email, password}. Query User by email, compare password with bcrypt. On match, create JWT with jose library, set as httpOnly cookie (15-min expiry). Return 200. On mismatch, return 401.
  ## Verifycurl -X POST localhost:3000/api/auth/login returns 200 with Set-Cookie header
  ## DoneValid credentials → 200 + cookie. Invalid → 401.

```

Use for: Everything Codex can do independently (code, tests, builds, file operations).


## Type
**RARELY USED** - Only for actions with NO CLI/API. Codex automates everything possible first.

**Structure:**
```xml
### Task (type="checkpoint:human-action" gate="blocking")
  ## Action[Unavoidable manual step - email link, 2FA code]
  ## Instructions
    [What Codex already automated]
    [The ONE thing requiring human action]
  
  ## Verification[What Codex can check afterward]
  ## Resume Signal[How to continue]

```

Use ONLY for: Email verification links, SMS 2FA codes, manual approvals with no API, 3D Secure payment flows.

Do NOT use for: Anything with a CLI (Vercel, Stripe, Upstash, Railway, GitHub), builds, tests, file creation, deployments.

See: references/cli-automation.md for what Codex can automate.

**Execution:** Codex automates everything with CLI/API, stops only for truly unavoidable manual steps.


## Type
**Human must verify Codex's work** - Visual checks, UX testing.

**Structure:**
```xml
### Task (type="checkpoint:human-verify" gate="blocking")
  ## What BuiltResponsive dashboard layout
  ## How To Verify
    1. Run: npm run dev
    2. Visit: http://localhost:3000/dashboard
    3. Desktop (>1024px): Verify sidebar left, content right
    4. Tablet (768px): Verify sidebar collapses to hamburger
    5. Mobile (375px): Verify single column, bottom nav
    6. Check: No layout shift, no horizontal scroll
  
  ## Resume SignalType "approved" or describe issues

```

Use for: UI/UX verification, visual design checks, animation smoothness, accessibility testing.

**Execution:** Codex builds the feature, stops, provides testing instructions, waits for approval/feedback.


## Type
**Human must make implementation choice** - Direction-setting decisions.

**Structure:**
```xml
### Task (type="checkpoint:decision" gate="blocking")
  ## DecisionSelect authentication provider
  ## ContextWe need user authentication. Three approaches with different tradeoffs:
  ## Options
    ## Option
      ## NameSupabase Auth
      ## ProsBuilt-in with Supabase, generous free tier
      ## ConsLess customizable UI, tied to ecosystem
    
    ## Option
      ## NameClerk
      ## ProsBeautiful pre-built UI, best DX
      ## ConsPaid after 10k MAU
    
    ## Option
      ## NameNextAuth.js
      ## ProsFree, self-hosted, maximum control
      ## ConsMore setup, you manage security
    
  
  ## Resume SignalSelect: supabase, clerk, or nextauth

```

Use for: Technology selection, architecture decisions, design choices, feature prioritization.

**Execution:** Codex presents options with balanced pros/cons, waits for decision, proceeds with chosen direction.


**When to use checkpoints:**
- Visual/UX verification (after Codex builds) → `checkpoint:human-verify`
- Implementation direction choice → `checkpoint:decision`
- Truly unavoidable manual actions (email links, 2FA) → `checkpoint:human-action` (rare)

**When NOT to use checkpoints:**
- Anything with CLI/API (Codex automates it) → `type="auto"`
- Deployments (Vercel, Railway, Fly) → `type="auto"` with CLI
- Creating resources (Upstash, Stripe, GitHub) → `type="auto"` with CLI/API
- File operations, tests, builds → `type="auto"`

**Golden rule:** If Codex CAN automate it, Codex MUST automate it. See: references/cli-automation.md

See `references/checkpoints.md` for comprehensive checkpoint guidance.


## Context References
Use @file references to load context for the prompt:

```markdown
## Context
@.planning/BRIEF.md           # Project vision
@.planning/ROADMAP.md         # Phase structure
@.planning/phases/02-auth/FINDINGS.md  # Research results
@src/lib/db.ts                # Existing database setup
@src/types/user.ts            # Existing type definitions

```

Reference files that Codex needs to understand before implementing.


## Verification Section
Overall phase verification (beyond individual task verification):

```markdown
## Verification
Before declaring phase complete:
- [ ] `npm run build` succeeds without errors
- [ ] `npm test` passes all tests
- [ ] No TypeScript errors
- [ ] Feature works end-to-end manually

```


## Success Criteria Section
Measurable criteria for phase completion:

```markdown
## Success Criteria
- All tasks completed
- All verification checks pass
- No errors or warnings introduced
- JWT auth flow works end-to-end
- Protected routes redirect unauthenticated users

```


## Output Section
Specify the SUMMARY.md structure:

```markdown
## Output
After completion, create `.planning/phases/XX-name/SUMMARY.md`:

# Phase X: Name Summary

**[Substantive one-liner]**

## Accomplishments
## Files Created/Modified
## Decisions Made
## Issues Encountered
## Next Phase Readiness

```


## Specificity Levels
## Too Vague
```xml
### Task (type="auto")
  ## NameTask 1: Add authentication
  ## Files???
  ## ActionImplement auth
  ## Verify???
  ## DoneUsers can authenticate

```

Codex: "How? What type? What library? Where?"


## Just Right
```xml
### Task (type="auto")
  ## NameTask 1: Create login endpoint with JWT
  ## Filessrc/app/api/auth/login/route.ts
  ## ActionPOST endpoint accepting {email, password}. Query User by email, compare password with bcrypt. On match, create JWT with jose library, set as httpOnly cookie (15-min expiry). Return 200. On mismatch, return 401. Use jose instead of jsonwebtoken (CommonJS issues with Edge).
  ## Verifycurl -X POST localhost:3000/api/auth/login -H "Content-Type: application/json" -d '{"email":"test@test.com","password":"test123"}' returns 200 with Set-Cookie header containing JWT
  ## DoneValid credentials → 200 + cookie. Invalid → 401. Missing fields → 400.

```

Codex can implement this immediately.


## Too Detailed
Writing the actual code in the plan. Trust Codex to implement from clear instructions.



## Anti Patterns
## Vague Actions
- "Set up the infrastructure"
- "Handle edge cases"
- "Make it production-ready"
- "Add proper error handling"

These require Codex to decide WHAT to do. Specify it.


## Unverifiable Completion
- "It works correctly"
- "User experience is good"
- "Code is clean"
- "Tests pass" (which tests? do they exist?)

These require subjective judgment. Make it objective.


## Missing Context
- "Use the standard approach"
- "Follow best practices"
- "Like the other endpoints"

Codex doesn't know your standards. Be explicit.



## Sizing Tasks
Good task size: 15-60 minutes of Codex work.

**Too small**: "Add import statement for bcrypt" (combine with related task)
**Just right**: "Create login endpoint with JWT validation" (focused, specific)
**Too big**: "Implement full authentication system" (split into multiple plans)

If a task takes multiple sessions, break it down.
If a task is trivial, combine with related tasks.

**Note on scope:** If a phase has >7 tasks or spans multiple subsystems, split into multiple plans using the naming convention `{phase}-{plan}-PLAN.md`. See `references/scope-estimation.md` for guidance.


