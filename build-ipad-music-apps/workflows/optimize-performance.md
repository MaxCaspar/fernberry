# Workflow: Optimize Performance

## Required Reading
1. references/dsp-testing.md
2. references/gpu-audio-sync.md
3. references/audio-architecture.md

## Process
1. Measure baseline: CPU, audio underruns, GPU frame time.
2. Identify top offenders in DSP or rendering.
3. Optimize one hotspot at a time and re-measure.
4. Validate no audio artifacts or visual regressions.

## Success Criteria
- Audio underruns reduced or eliminated
- Frame time within target
- No regressions in sound quality
