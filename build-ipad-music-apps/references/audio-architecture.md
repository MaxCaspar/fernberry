# Audio Architecture

## Principles
- Keep DSP on real-time audio thread; avoid locks and allocations.
- Separate UI state from audio graph state.
- Use a single source of truth for sample rate, buffer size, and channel count.

## Modules
- `AudioEngine`: owns AVAudioEngine and session configuration.
- `DSP`: pure functions or C++ for heavy processing.
- `Control`: parameter smoothing and mapping from UI.
