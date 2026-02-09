# Reference: Glob And Numbering

## Purpose
Ensure prompt files are saved with correct sequential numbering.

## Rules
- Use Glob `./prompts/*.md` to check for existing prompts.
- If no files exist, start at `001`.
- Determine the highest existing number (prefix before first hyphen) and increment by 1.
- Use three-digit numbering: `001`, `002`, `003`, etc.
- Filenames: lowercase, hyphen-separated, max 5 words describing the task.
- Examples:
  - `./prompts/001-implement-user-authentication.md`
  - `./prompts/012-fix-payment-timeouts.md`
