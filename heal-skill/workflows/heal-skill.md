# Workflow: Heal Skill Documentation

## Required Reading
1. references/scan-commands.md
2. references/proposed-changes-template.md
3. references/approval-prompt.md

## Process
1. Identify the target skill from context; if unclear, ask the user.
2. Scan the skill directory using the commands in references/scan-commands.md.
3. Analyze the issue and record what was wrong, discovery method, root cause, and scope.
4. Prepare proposed changes using references/proposed-changes-template.md.
5. Request approval using references/approval-prompt.md and wait for a response.
6. If approved, apply edits with `apply_patch` or shell edits and read back modified sections to verify.
7. If a commit was requested, run `git status`, `git add`, and `git commit` with a clear message.
8. Summarize changes, verification, and files modified.

## Success Criteria
- The correct skill is identified and scoped.
- Proposed fixes are documented with before/after text.
- Edits are applied only after explicit approval.
- Modified sections are verified by reading back.
- Optional commit is created if requested.
