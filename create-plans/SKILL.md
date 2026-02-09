---
name: create-plans
description: Create hierarchical project plans optimized for solo agentic development with Codex. Use when planning new projects, building roadmaps, planning phases, researching unknowns, handling handoffs, or managing milestone completion. Produces executable PLAN prompts and verified SUMMARY outcomes.
---

# Create Plans

## Essential Principles

- Plan for one human owner and one implementer (`Codex`).
- Keep plans atomic: target 2-3 tasks per plan file.
- `PLAN.md` is executable prompt content, not PM documentation.
- Automate everything possible with CLI/API before asking for human intervention.
- Use checkpoints for decisions and verification, not routine execution.
- Treat deviations explicitly: auto-fix critical issues, ask only for architectural decisions.
- Keep planning artifacts versioned in git.

## Context Scan

Run this at invocation to determine state:

```bash
if (git rev-parse --git-dir 2>$null) { } else { "NO_GIT_REPO" }
Get-ChildItem -Force .planning -ErrorAction SilentlyContinue
Get-ChildItem -Force .planning/phases -ErrorAction SilentlyContinue
Get-ChildItem -Recurse -File -Filter ".continue-here*.md" -ErrorAction SilentlyContinue
[ -f .planning/BRIEF.md ] && echo "BRIEF: exists"
[ -f .planning/ROADMAP.md ] && echo "ROADMAP: exists"
```

If no repo exists, ask whether to initialize git before planning.

## Domain Expertise

- Preferred location: `~/.codex/skills/expertise/`
- Load domain expertise before roadmap and phase planning.
- Read the domain `SKILL.md` first, then load only references relevant to the phase type.
- If no domain skill exists, continue without it.

## Intake

Choose based on discovered state:

If handoff file exists:

1. Resume from handoff
2. Discard handoff and continue fresh
3. Different action

If `.planning` exists:

1. Plan next phase
2. Execute current phase
3. Create handoff
4. View/update roadmap
5. Other

If `.planning` missing:

1. Start new project (brief)
2. Create roadmap from brief
3. Jump to phase planning
4. Get guidance

## Routing

| Intent | Workflow |
| --- | --- |
| brief/new/start | `workflows/create-brief.md` |
| roadmap/phases | `workflows/create-roadmap.md` |
| plan phase/next phase | `workflows/plan-phase.md` |
| plan chunk/what's next | `workflows/plan-chunk.md` |
| execute/run/build | `workflows/execute-phase.md` |
| research/investigate | `workflows/research-phase.md` |
| handoff/stop | `workflows/handoff.md` |
| resume/continue | `workflows/resume.md` |
| transition/complete | `workflows/transition.md` |
| milestone/release | `workflows/complete-milestone.md` |
| guidance/help | `workflows/get-guidance.md` |

## Hierarchy

```text
BRIEF.md
  -> ROADMAP.md
  -> RESEARCH.md (optional)
  -> FINDINGS.md (optional)
  -> PLAN.md
  -> SUMMARY.md
```

Rules:

- Roadmap depends on brief.
- Phase plan depends on roadmap.
- `SUMMARY.md` marks a plan complete.

## Output Structure

Use `.planning/` with chronological naming:

```text
.planning/
  BRIEF.md
  ROADMAP.md
  phases/
    01-foundation/
      01-01-PLAN.md
      01-01-SUMMARY.md
      .continue-here-01-01.md
```

## References

- `references/plan-format.md`
- `references/scope-estimation.md`
- `references/checkpoints.md`
- `references/context-management.md`
- `references/user-gates.md`
- `references/git-integration.md`
- `references/milestone-management.md`
- `references/research-pitfalls.md`
- `references/domain-expertise.md`

## Templates

- `templates/brief.md`
- `templates/roadmap.md`
- `templates/phase-prompt.md`
- `templates/research-prompt.md`
- `templates/summary.md`
- `templates/milestone.md`
- `templates/issues.md`
- `templates/continue-here.md`

## Success Criteria

- Context scan completed before intake.
- Correct workflow selected for current planning state.
- Plans are atomic and executable.
- Handoffs preserve context for clean resume.
- Decisions and deviations are documented in summaries.
- Planning artifacts are consistent with hierarchy and naming rules.
