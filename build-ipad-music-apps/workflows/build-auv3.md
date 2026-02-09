# Workflow: Build AUv3 Extension

## Required Reading
1. references/audio-units-aux.md
2. references/audio-architecture.md
3. references/project-scaffolding.md

## Process
1. Confirm whether AUv3 is the core product or a companion to the app.
2. Create AUv3 target and shared DSP core module.
3. Implement parameter tree and preset handling.
4. Build a minimal AUv3 UI and host integration test.
5. Validate in a host app on device.

## Success Criteria
- AUv3 builds and validates
- Parameters are exposed and stable
- Host can instantiate without crashes
