# Human Checkpoints in Plans

Plans execute autonomously. Checkpoints formalize the interaction points where human verification or decisions are needed.

**Core principle:** Codex automates everything with CLI/API. Checkpoints are for verification and decisions, not manual work.

## Checkpoint Types

### 1. `checkpoint:human-verify` (Most Common)

**When:** Codex completed automated work, human confirms it works correctly.

**Use for:**
- Visual UI checks (layout, styling, responsiveness)
- Interactive flows (click through wizard, test user flows)
- Functional verification (feature works as expected)
- Audio/video playback quality
- Animation smoothness
- Accessibility testing

**Structure:**
```xml
### Task (type="checkpoint:human-verify" gate="blocking")
  ## What Built[What Codex automated and deployed/built]
  ## How To Verify
    [Exact steps to test - URLs, commands, expected behavior]
  
  ## Resume Signal[How to continue - "approved", "yes", or describe issues]

```

**Key elements:**
- `## What Built`: What Codex automated (deployed, built, configured)
- `## How To Verify`: Exact steps to confirm it works (numbered, specific)
- `## Resume Signal`: Clear indication of how to continue

**Example: Vercel Deployment**
```xml
### Task (type="auto")
  ## NameDeploy to Vercel
  ## Files.vercel/, vercel.json
  ## ActionRun `vercel --yes` to create project and deploy. Capture deployment URL from output.
  ## Verifyvercel ls shows deployment, curl {url} returns 200
  ## DoneApp deployed, URL captured


### Task (type="checkpoint:human-verify" gate="blocking")
  ## What BuiltDeployed to Vercel at https://myapp-abc123.vercel.app
  ## How To Verify
    Visit https://myapp-abc123.vercel.app and confirm:
    - Homepage loads without errors
    - Login form is visible
    - No console errors in browser DevTools
  
  ## Resume SignalType "approved" to continue, or describe issues to fix

```

**Example: UI Component**
```xml
### Task (type="auto")
  ## NameBuild responsive dashboard layout
  ## Filessrc/components/Dashboard.tsx, src/app/dashboard/page.tsx
  ## ActionCreate dashboard with sidebar, header, and content area. Use Tailwind responsive classes for mobile.
  ## Verifynpm run build succeeds, no TypeScript errors
  ## DoneDashboard component builds without errors


### Task (type="checkpoint:human-verify" gate="blocking")
  ## What BuiltResponsive dashboard layout at /dashboard
  ## How To Verify
    1. Run: npm run dev
    2. Visit: http://localhost:3000/dashboard
    3. Desktop (>1024px): Verify sidebar left, content right, header top
    4. Tablet (768px): Verify sidebar collapses to hamburger
    5. Mobile (375px): Verify single column, bottom nav
    6. Check: No layout shift, no horizontal scroll
  
  ## Resume SignalType "approved" or describe layout issues

```

**Example: Xcode Build**
```xml
### Task (type="auto")
  ## NameBuild macOS app with Xcode
  ## FilesApp.xcodeproj, Sources/
  ## ActionRun `xcodebuild -project App.xcodeproj -scheme App build`. Check for compilation errors in output.
  ## VerifyBuild output contains "BUILD SUCCEEDED", no errors
  ## DoneApp builds successfully


### Task (type="checkpoint:human-verify" gate="blocking")
  ## What BuiltBuilt macOS app at DerivedData/Build/Products/Debug/App.app
  ## How To Verify
    Open App.app and test:
    - App launches without crashes
    - Menu bar icon appears
    - Preferences window opens correctly
    - No visual glitches or layout issues
  
  ## Resume SignalType "approved" or describe issues

```

### 2. `checkpoint:decision`

**When:** Human must make choice that affects implementation direction.

**Use for:**
- Technology selection (which auth provider, which database)
- Architecture decisions (monorepo vs separate repos)
- Design choices (color scheme, layout approach)
- Feature prioritization (which variant to build)
- Data model decisions (schema structure)

**Structure:**
```xml
### Task (type="checkpoint:decision" gate="blocking")
  ## Decision[What's being decided]
  ## Context[Why this decision matters]
  ## Options
    ## Option
      ## Name[Option name]
      ## Pros[Benefits]
      ## Cons[Tradeoffs]
    
    ## Option
      ## Name[Option name]
      ## Pros[Benefits]
      ## Cons[Tradeoffs]
    
  
  ## Resume Signal[How to indicate choice]

```

**Key elements:**
- `## Decision`: What's being decided
- `## Context`: Why this matters
- `## Options`: Each option with balanced pros/cons (not prescriptive)
- `## Resume Signal`: How to indicate choice

**Example: Auth Provider Selection**
```xml
### Task (type="checkpoint:decision" gate="blocking")
  ## DecisionSelect authentication provider
  ## Context
    Need user authentication for the app. Three solid options with different tradeoffs.
  
  ## Options
    ## Option
      ## NameSupabase Auth
      ## ProsBuilt-in with Supabase DB we're using, generous free tier, row-level security integration
      ## ConsLess customizable UI, tied to Supabase ecosystem
    
    ## Option
      ## NameClerk
      ## ProsBeautiful pre-built UI, best developer experience, excellent docs
      ## ConsPaid after 10k MAU, vendor lock-in
    
    ## Option
      ## NameNextAuth.js
      ## ProsFree, self-hosted, maximum control, widely adopted
      ## ConsMore setup work, you manage security updates, UI is DIY
    
  
  ## Resume SignalSelect: supabase, clerk, or nextauth

```

### 3. `checkpoint:human-action` (Rare)

**When:** Action has NO CLI/API and requires human-only interaction, OR Codex hit an authentication gate during automation.

**Use ONLY for:**
- **Authentication gates** - Codex tried to use CLI/API but needs credentials to continue (this is NOT a failure)
- Email verification links (account creation requires clicking email)
- SMS 2FA codes (phone verification)
- Manual account approvals (platform requires human review before API access)
- Credit card 3D Secure flows (web-based payment authorization)
- OAuth app approvals (some platforms require web-based approval)

**Do NOT use for pre-planned manual work:**
- Manually deploying to Vercel (use `vercel` CLI - auth gate if needed)
- Manually creating Stripe webhooks (use Stripe API - auth gate if needed)
- Manually creating databases (use provider CLI - auth gate if needed)
- Running builds/tests manually (use Bash tool)
- Creating files manually (use Write tool)

**Structure:**
```xml
### Task (type="checkpoint:human-action" gate="blocking")
  ## Action[What human must do - Codex already did everything automatable]
  ## Instructions
    [What Codex already automated]
    [The ONE thing requiring human action]
  
  ## Verification[What Codex can check afterward]
  ## Resume Signal[How to continue]

```

**Key principle:** Codex automates EVERYTHING possible first, only asks human for the truly unavoidable manual step.

**Example: Email Verification**
```xml
### Task (type="auto")
  ## NameCreate SendGrid account via API
  ## ActionUse SendGrid API to create subuser account with provided email. Request verification email.
  ## VerifyAPI returns 201, account created
  ## DoneAccount created, verification email sent


### Task (type="checkpoint:human-action" gate="blocking")
  ## ActionComplete email verification for SendGrid account
  ## Instructions
    I created the account and requested verification email.
    Check your inbox for SendGrid verification link and click it.
  
  ## VerificationSendGrid API key works: curl test succeeds
  ## Resume SignalType "done" when email verified

```

**Example: Credit Card 3D Secure**
```xml
### Task (type="auto")
  ## NameCreate Stripe payment intent
  ## ActionUse Stripe API to create payment intent for $99. Generate checkout URL.
  ## VerifyStripe API returns payment intent ID and URL
  ## DonePayment intent created


### Task (type="checkpoint:human-action" gate="blocking")
  ## ActionComplete 3D Secure authentication
  ## Instructions
    I created the payment intent: https://checkout.stripe.com/pay/cs_test_abc123
    Visit that URL and complete the 3D Secure verification flow with your test card.
  
  ## VerificationStripe webhook receives payment_intent.succeeded event
  ## Resume SignalType "done" when payment completes

```

**Example: Authentication Gate (Dynamic Checkpoint)**
```xml
### Task (type="auto")
  ## NameDeploy to Vercel
  ## Files.vercel/, vercel.json
  ## ActionRun `vercel --yes` to deploy
  ## Verifyvercel ls shows deployment, curl returns 200


<!-- If vercel returns "Error: Not authenticated", Codex creates checkpoint on the fly -->

### Task (type="checkpoint:human-action" gate="blocking")
  ## ActionAuthenticate Vercel CLI so I can continue deployment
  ## Instructions
    I tried to deploy but got authentication error.
    Run: vercel login
    This will open your browser - complete the authentication flow.
  
  ## Verificationvercel whoami returns your account email
  ## Resume SignalType "done" when authenticated


<!-- After authentication, Codex retries the deployment -->

### Task (type="auto")
  ## NameRetry Vercel deployment
  ## ActionRun `vercel --yes` (now authenticated)
  ## Verifyvercel ls shows deployment, curl returns 200

```

**Key distinction:** Authentication gates are created dynamically when Codex encounters auth errors during automation. They're NOT pre-planned - Codex tries to automate first, only asks for credentials when blocked.

See references/cli-automation.md "Authentication Gates" section for more examples and full protocol.

## Execution Protocol

When Codex encounters `type="checkpoint:*"`:

1. **Stop immediately** - do not proceed to next task
2. **Display checkpoint clearly:**

```
════════════════════════════════════════
CHECKPOINT: [Type]
════════════════════════════════════════

Task [X] of [Y]: [Name]

[Display checkpoint-specific content]

[Resume signal instruction]
════════════════════════════════════════
```

3. **Wait for user response** - do not hallucinate completion
4. **Verify if possible** - check files, run tests, whatever is specified
5. **Resume execution** - continue to next task only after confirmation

**For checkpoint:human-verify:**
```
════════════════════════════════════════
CHECKPOINT: Verification Required
════════════════════════════════════════

Task 5 of 8: Responsive dashboard layout

I built: Responsive dashboard at /dashboard

How to verify:
1. Run: npm run dev
2. Visit: http://localhost:3000/dashboard
3. Test: Resize browser window to mobile/tablet/desktop
4. Confirm: No layout shift, proper responsive behavior

Type "approved" to continue, or describe issues.
════════════════════════════════════════
```

**For checkpoint:decision:**
```
════════════════════════════════════════
CHECKPOINT: Decision Required
════════════════════════════════════════

Task 2 of 6: Select authentication provider

Decision: Which auth provider should we use?

Context: Need user authentication. Three options with different tradeoffs.

Options:
1. supabase - Built-in with our DB, free tier
2. clerk - Best DX, paid after 10k users
3. nextauth - Self-hosted, maximum control

Select: supabase, clerk, or nextauth
════════════════════════════════════════
```

## Writing Good Checkpoints

**DO:**
- Automate everything with CLI/API before checkpoint
- Be specific: "Visit https://myapp.vercel.app" not "check deployment"
- Number verification steps: easier to follow
- State expected outcomes: "You should see X"
- Provide context: why this checkpoint exists
- Make verification executable: clear, testable steps

**DON'T:**
- Ask human to do work Codex can automate (deploy, create resources, run builds)
- Assume knowledge: "Configure the usual settings" ❌
- Skip steps: "Set up database" ❌ (too vague)
- Mix multiple verifications in one checkpoint (split them)
- Make verification impossible (Codex can't check visual appearance without user confirmation)

## When to Use Checkpoints

**Use checkpoint:human-verify for:**
- Visual verification (UI, layouts, animations)
- Interactive testing (click flows, user journeys)
- Quality checks (audio/video playback, animation smoothness)
- Confirming deployed apps are accessible

**Use checkpoint:decision for:**
- Technology selection (auth providers, databases, frameworks)
- Architecture choices (monorepo, deployment strategy)
- Design decisions (color schemes, layout approaches)
- Feature prioritization

**Use checkpoint:human-action for:**
- Email verification links (no API)
- SMS 2FA codes (no API)
- Manual approvals with no automation
- 3D Secure payment flows

**Don't use checkpoints for:**
- Things Codex can verify programmatically (tests pass, build succeeds)
- File operations (Codex can read files to verify)
- Code correctness (use tests and static analysis)
- Anything automatable via CLI/API

## Checkpoint Placement

Place checkpoints:
- **After automation completes** - not before Codex does the work
- **After UI buildout** - before declaring phase complete
- **Before dependent work** - decisions before implementation
- **At integration points** - after configuring external services

Bad placement:
- Before Codex automates (asking human to do automatable work) ❌
- Too frequent (every other task is a checkpoint) ❌
- Too late (checkpoint is last task, but earlier tasks needed its result) ❌

## Complete Examples

### Example 1: Deployment Flow (Correct)

```xml
<!-- Codex automates everything -->
### Task (type="auto")
  ## NameDeploy to Vercel
  ## Files.vercel/, vercel.json, package.json
  ## Action
    1. Run `vercel --yes` to create project and deploy
    2. Capture deployment URL from output
    3. Set environment variables with `vercel env add`
    4. Trigger production deployment with `vercel --prod`
  
  ## Verify
    - vercel ls shows deployment
    - curl {url} returns 200
    - Environment variables set correctly
  
  ## DoneApp deployed to production, URL captured


<!-- Human verifies visual/functional correctness -->
### Task (type="checkpoint:human-verify" gate="blocking")
  ## What BuiltDeployed to https://myapp.vercel.app
  ## How To Verify
    Visit https://myapp.vercel.app and confirm:
    - Homepage loads correctly
    - All images/assets load
    - Navigation works
    - No console errors
  
  ## Resume SignalType "approved" or describe issues

```

### Example 2: Database Setup (Correct)

```xml
<!-- Codex automates everything -->
### Task (type="auto")
  ## NameCreate Upstash Redis database
  ## Files.env
  ## Action
    1. Run `upstash redis create myapp-cache --region us-east-1`
    2. Capture connection URL from output
    3. Write to .env: UPSTASH_REDIS_URL={url}
    4. Verify connection with test command
  
  ## Verify
    - upstash redis list shows database
    - .env contains UPSTASH_REDIS_URL
    - Test connection succeeds
  
  ## DoneRedis database created and configured


<!-- NO CHECKPOINT NEEDED - Codex automated everything and verified programmatically -->
```

### Example 3: Stripe Webhooks (Correct)

```xml
<!-- Codex automates everything -->
### Task (type="auto")
  ## NameConfigure Stripe webhooks
  ## Files.env, src/app/api/webhooks/route.ts
  ## Action
    1. Use Stripe API to create webhook endpoint pointing to /api/webhooks
    2. Subscribe to events: payment_intent.succeeded, customer.subscription.updated
    3. Save webhook signing secret to .env
    4. Implement webhook handler in route.ts
  
  ## Verify
    - Stripe API returns webhook endpoint ID
    - .env contains STRIPE_WEBHOOK_SECRET
    - curl webhook endpoint returns 200
  
  ## DoneStripe webhooks configured and handler implemented


<!-- Human verifies in Stripe dashboard -->
### Task (type="checkpoint:human-verify" gate="blocking")
  ## What BuiltStripe webhook configured via API
  ## How To Verify
    Visit Stripe Dashboard > Developers > Webhooks
    Confirm: Endpoint shows https://myapp.com/api/webhooks with correct events
  
  ## Resume SignalType "yes" if correct

```

## Anti-Patterns

### ❌ BAD: Asking human to automate

```xml
### Task (type="checkpoint:human-action" gate="blocking")
  ## ActionDeploy to Vercel
  ## Instructions
    1. Visit vercel.com/new
    2. Import Git repository
    3. Click Deploy
    4. Copy deployment URL
  
  ## VerificationDeployment exists
  ## Resume SignalPaste URL

```

**Why bad:** Vercel has a CLI. Codex should run `vercel --yes`.

### ✅ GOOD: Codex automates, human verifies

```xml
### Task (type="auto")
  ## NameDeploy to Vercel
  ## ActionRun `vercel --yes`. Capture URL.
  ## Verifyvercel ls shows deployment, curl returns 200


### Task (type="checkpoint:human-verify")
  ## What BuiltDeployed to {url}
  ## How To VerifyVisit {url}, check homepage loads
  ## Resume SignalType "approved"

```

### ❌ BAD: Too many checkpoints

```xml
### Task (type="auto")Create schema
### Task (type="checkpoint:human-verify")Check schema
### Task (type="auto")Create API route
### Task (type="checkpoint:human-verify")Check API
### Task (type="auto")Create UI form
### Task (type="checkpoint:human-verify")Check form
```

**Why bad:** Verification fatigue. Combine into one checkpoint at end.

### ✅ GOOD: Single verification checkpoint

```xml
### Task (type="auto")Create schema
### Task (type="auto")Create API route
### Task (type="auto")Create UI form

### Task (type="checkpoint:human-verify")
  ## What BuiltComplete auth flow (schema + API + UI)
  ## How To VerifyTest full flow: register, login, access protected page
  ## Resume SignalType "approved"

```

### ❌ BAD: Asking for automatable file operations

```xml
### Task (type="checkpoint:human-action")
  ## ActionCreate .env file
  ## Instructions
    1. Create .env in project root
    2. Add: DATABASE_URL=...
    3. Add: STRIPE_KEY=...
  

```

**Why bad:** Codex has Write tool. This should be `type="auto"`.

## Summary

Checkpoints formalize human-in-the-loop points. Use them when Codex cannot complete a task autonomously OR when human verification is required for correctness.

**The golden rule:** If Codex CAN automate it, Codex MUST automate it.

**Checkpoint priority:**
1. **checkpoint:human-verify** (90% of checkpoints) - Codex automated everything, human confirms visual/functional correctness
2. **checkpoint:decision** (9% of checkpoints) - Human makes architectural/technology choices
3. **checkpoint:human-action** (1% of checkpoints) - Truly unavoidable manual steps with no API/CLI

**See also:** references/cli-automation.md for exhaustive list of what Codex can automate.

