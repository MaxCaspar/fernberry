# Template: DSP Module Skeleton

## Module Name

## Public API
- init(sampleRate:bufferSize:channels:)
- process(input:output:frames:)
- setParameter(id:value:)

## Constraints
- No allocations in process()
- Lock-free parameter reads

## Tests
- Deterministic unit tests
- Boundary cases (silence, clipping)
