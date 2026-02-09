# Workflow: Build New iPad Music App

## Required Reading
1. references/project-scaffolding.md
2. references/audio-architecture.md
3. references/avaudioengine-graph.md
4. references/metal-rendering.md
5. references/swiftui-patterns.md

## Process
1. Confirm app goals: audio engine type, target latency, rendering scope, and AUv3 needs.
2. Scaffold iOS app (Swift + SwiftUI) with audio engine module and Metal renderer module.
3. Implement audio session configuration and background audio entitlement.
4. Build initial AVAudioEngine graph with test tone and metering taps.
5. Create Metal view pipeline and connect to SwiftUI host view.
6. Wire UI controls to audio graph parameters with safe threading.
7. Add a minimal integration test: engine start/stop and buffer sanity.
8. Build + run on simulator; if audio is required, run on device and validate.

## Success Criteria
- Builds in CLI
- App launches on iPad simulator
- Audio engine starts without errors
- Metal view renders without frame drops
