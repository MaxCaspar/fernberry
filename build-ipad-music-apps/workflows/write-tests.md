# Workflow: Write and Run Tests

## Required Reading
1. references/testing-tdd.md
2. references/dsp-testing.md

## Process
1. Identify the logic or DSP unit to test.
2. Write unit tests for deterministic DSP math and edge cases.
3. Add integration tests for audio graph start/stop and routing changes.
4. Run tests on simulator; run device tests for audio timing if needed.

## Success Criteria
- Tests execute in CLI
- DSP math and edge cases are covered
- Tests are deterministic and fast
