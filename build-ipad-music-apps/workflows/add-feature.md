# Workflow: Add Feature to iPad Music App

## Required Reading
1. references/audio-architecture.md
2. references/avaudioengine-graph.md
3. references/swiftui-patterns.md
4. references/metal-rendering.md

## Process
1. Clarify feature scope, expected UX, and audio/visual behavior.
2. Identify impacted modules: UI, audio graph, DSP, Metal renderer.
3. Implement smallest viable version.
4. Add tests for DSP or state logic changes.
5. Build and run; validate sound and visuals.

## Success Criteria
- Feature works as described
- DSP or state changes are tested
- App launches and audio engine is stable
