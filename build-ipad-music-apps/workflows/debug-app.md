# Workflow: Debug iPad Music App

## Required Reading
1. references/cli-workflow.md
2. references/testing-debugging.md
3. references/audio-architecture.md
4. references/dsp-testing.md

## Process
1. Reproduce the issue with exact steps, device, and iOS version.
2. Capture logs and audio engine state; confirm route and session category.
3. Add or update tests to cover the failing behavior if logic-based.
4. Fix the issue with a minimal change.
5. Re-run build, tests, and device playback verification.

## Success Criteria
- Issue is reproducible then resolved
- Tests pass or manual verification documented
- No new audio glitches or crashes
