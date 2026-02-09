# Workflow: Background Audio / Headless DSP

## Required Reading
1. references/background-audio.md
2. references/audio-session-routing.md
3. references/audio-architecture.md

## Process
1. Confirm background use case and App Store policy risks.
2. Configure background audio mode and session category.
3. Ensure DSP runs without UI dependency and survives interruptions.
4. Add watchdog logging for engine restarts.
5. Validate with screen locked and route changes.

## Success Criteria
- Background mode enabled
- DSP continues without UI
- Interruption handling verified on device
