# GPU/Audio Sync

## Goals
- Avoid stutter when audio and visuals are coupled.
- Use shared timing source if needed.

## Practices
- Measure render time and audio callback timing.
- Decouple render from audio where possible.
