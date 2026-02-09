---
name: build-ipad-music-apps
description: Build professional native iPad music apps in Swift with SwiftUI, Metal, and AVAudioEngine. Full lifecycle - build, debug, test, optimize, ship. CLI-only, no Xcode.
---

## Objective
Build professional native iPad music apps in Swift with SwiftUI, Metal, and AVAudioEngine. Full lifecycle - build, debug, test, optimize, ship. CLI-only, no Xcode.

## Essential Principles
## How We Work

**The user is the product owner. Codex is the developer.**

The user does not write code. The user does not read code. The user describes what they want and judges whether the result is acceptable. Codex implements, verifies, and reports outcomes.

### 1. Prove, Don't Promise

Never say "this should work." Prove it:
```bash
xcodebuild build 2>&1 | xcsift  # Build passes
xcodebuild test                  # Tests pass
xcrun simctl launch booted ...    # App launches (sim)
```
If you didn't run it, you don't know it works.

### 2. Tests for Correctness, Ears for Audio, Eyes for Visuals

| Question | How to Answer |
|----------|---------------|
| Does DSP logic work? | Write test, see it pass |
| Does it sound right? | Play test tone, user listens |
| Does it look right? | Launch app, user looks at it |
| Does it feel right? | User uses it |
| Does it crash? | Test + launch |
| Is it fast enough? | Profiler |

Tests verify *correctness*. The user verifies *desirability*.

### 3. Report Outcomes, Not Code

**Bad:** "I refactored the audio graph to use a mixer node"
**Good:** "Audio engine now starts without underruns. 10 minutes playback, 0 glitches."

### 4. Small Steps, Always Verified

```
Change -> Verify -> Report -> Next change
```

### 5. Ask Before, Not After

Unclear requirement? Ask now.
Multiple valid approaches? Ask which.
Scope creep? Ask if wanted.
Big refactor needed? Ask permission.

### 6. Always Leave It Working

Every stopping point = working state. Tests pass, app launches, changes committed. The user can walk away anytime and come back to something that works.

## Intake
**Ask the user:**

What would you like to do?
1. Build a new app
2. Debug an existing app
3. Add a feature
4. Write/run tests
5. Optimize performance
6. Ship/release to App Store
7. Build an AUv3
8. Background audio / headless DSP
9. Something else

**Then read the matching workflow from `workflows/` and follow it.**

## Routing
| Response | Workflow |
|----------|----------|
| 1, "new", "create", "build", "start" | `workflows/build-new-app.md` |
| 2, "broken", "fix", "debug", "crash", "bug" | `workflows/debug-app.md` |
| 3, "add", "feature", "implement", "change" | `workflows/add-feature.md` |
| 4, "test", "tests", "TDD", "coverage" | `workflows/write-tests.md` |
| 5, "slow", "optimize", "performance", "glitch", "underrun" | `workflows/optimize-performance.md` |
| 6, "ship", "release", "App Store" | `workflows/ship-app.md` |
| 7, "auv3", "audio unit", "plugin" | `workflows/build-auv3.md` |
| 8, "background", "headless", "dsp engine" | `workflows/background-dsp.md` |
| 9, other | Clarify, then select workflow or references |

## Verification Loop
## After Every Change

```bash
# 1. Does it build?
xcodebuild -scheme AppName -destination 'platform=iOS Simulator,name=iPad Pro (12.9-inch) (6th generation)' build 2>&1 | xcsift

# 2. Do tests pass?
xcodebuild -scheme AppName -destination 'platform=iOS Simulator,name=iPad Pro (12.9-inch) (6th generation)' test

# 3. Does it launch? (if UI or audio changed)
xcrun simctl launch booted com.example.AppName
```

Report to the user:
- "Build: OK"
- "Tests: 12 pass, 0 fail"
- "App launches, ready for you to check audio/visual behavior"

## When To Test
## Testing Decision

**Write a test when:**
- DSP math and filters
- Audio graph state changes (start/stop, route changes)
- Edge cases (silence, clipping, buffer size boundaries)
- Bug fix (test reproduces bug, then proves it's fixed)
- Refactoring (tests prove behavior unchanged)

**Skip tests when:**
- Pure UI exploration
- Rapid prototyping
- Subjective sound design
- One-off verification

## Reference Index
## Domain Knowledge

All in `references/`:

**Audio & DSP:** audio-architecture, avaudioengine-graph, audio-units-aux, dsp-testing
**Rendering:** metal-rendering, gpu-audio-sync
**UI:** swiftui-patterns, ipad-interaction
**System:** app-extensions, background-audio, audio-session-routing
**Development:** project-scaffolding, cli-workflow, testing-tdd, testing-debugging
**Polish:** design-system, appstore-release

## Workflows Index
## Workflows

All in `workflows/`:

| File | Purpose |
|------|---------|
| build-new-app.md | Create new app from scratch |
| debug-app.md | Find and fix bugs |
| add-feature.md | Add to existing app |
| write-tests.md | Write and run tests |
| optimize-performance.md | Profile and speed up |
| ship-app.md | Sign, archive, submit |
| build-auv3.md | Create an AUv3 extension |
| background-dsp.md | Background audio + headless DSP |

## Templates Index
## Templates

All in `templates/`:

| File | Purpose |
|------|---------|
| audio-graph-plan.md | Capture audio graph requirements |
| dsp-module-skeleton.md | DSP module API + constraints |
| appstore-release-checklist.md | Release checklist |
