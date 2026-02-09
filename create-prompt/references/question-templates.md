# Reference: Question Templates

## Purpose
Provide structured question templates and rules for clarifying user intent without unnecessary back-and-forth.

## Templates
**For ambiguous scope** (e.g., "build a dashboard"):
- header: "Dashboard type"
- question: "What kind of dashboard is this?"
- options:
  - "Admin dashboard" - Internal tools, user management, system metrics
  - "Analytics dashboard" - Data visualization, reports, business metrics
  - "User-facing dashboard" - End-user features, personal data, settings

**For unclear target** (e.g., "fix the bug"):
- header: "Bug location"
- question: "Where does this bug occur?"
- options:
  - "Frontend/UI" - Visual issues, user interactions, rendering
  - "Backend/API" - Server errors, data processing, endpoints
  - "Database" - Queries, migrations, data integrity

**For auth/security tasks**:
- header: "Auth method"
- question: "What authentication approach?"
- options:
  - "JWT tokens" - Stateless, API-friendly
  - "Session-based" - Server-side sessions, traditional web
  - "OAuth/SSO" - Third-party providers, enterprise

**For performance tasks**:
- header: "Performance focus"
- question: "What's the main performance concern?"
- options:
  - "Load time" - Initial render, bundle size, assets
  - "Runtime" - Memory usage, CPU, rendering performance
  - "Database" - Query optimization, indexing, caching

**For output/deliverable clarity**:
- header: "Output purpose"
- question: "What will this be used for?"
- options:
  - "Production code" - Ship to users, needs polish
  - "Prototype/POC" - Quick validation, can be rough
  - "Internal tooling" - Team use, moderate polish

## Rules
- Ask only about genuine gaps; do not ask what is already stated.
- Each option needs a short description explaining implications.
- Prefer options over free-text when choices are knowable.
- Limit to 2-4 questions per round.
- The user can always choose "Other" for custom input.
