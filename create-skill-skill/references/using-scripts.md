# Using Scripts

Scripts are executable code that Codex runs as-is rather than regenerating each time.

## When To Use

- Repeated operations
- Fragile sequences that must be exact
- Tasks requiring deterministic output

## How To Use

- Place scripts in `scripts/`.
- Document inputs and outputs clearly.
- Run scripts directly instead of rewriting code.

## Example

```
python scripts/validate.py path/to/output
```
