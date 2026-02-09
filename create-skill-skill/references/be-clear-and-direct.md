# Be Clear And Direct

## Say What To Do

Write imperative instructions. Avoid vague language like "consider" or "maybe" when you need a specific behavior.

## Provide Context Up Front

If the task depends on constraints (data sources, formats, policies), state them explicitly.

## Make Decisions Explicit

If Codex must choose between options, provide the decision criteria.

## Use Small, Ordered Steps

List steps in the order they should happen. Short steps reduce omissions.

## Define Success

Include a short, measurable Success Criteria section so the agent can self-check.

## Example

```markdown
## Objective
Refactor the data loader to reduce memory usage.

## Steps
1. Identify the largest in-memory structures.
2. Stream data instead of buffering all rows.
3. Add a benchmark for the new path.

## Success Criteria
- Peak memory reduced by at least 30% on the benchmark dataset
- No behavior changes in output
```
