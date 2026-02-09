# Workflows And Validation

## Complex Workflows

For multi-step tasks, write a clear process section with ordered steps. Include checkpoints if the task is long.

## Validation Loops

If outputs can be validated, include a Verification section with commands or checks.

## Decision Points

When branching is required, make the decision criteria explicit so Codex does not guess.

## Example

```markdown
## Process
1. Unpack the archive
2. Modify the config
3. Rebuild the artifact

## Verification
Run `scripts/validate.py output/` and fix any errors
```
