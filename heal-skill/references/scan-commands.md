# Reference: Scan Commands

## Purpose
Commands to inspect a skill directory and related folders before proposing fixes.

## Details
Bash-style:
- `ls -la $SKILL_DIR/`
- `ls -la $SKILL_DIR/references/ 2>/dev/null`
- `ls -la $SKILL_DIR/workflows/ 2>/dev/null`
- `ls -la $SKILL_DIR/templates/ 2>/dev/null`
- `ls -la $SKILL_DIR/scripts/ 2>/dev/null`

PowerShell-style:
- `Get-ChildItem -Force $SKILL_DIR`
- `Get-ChildItem -Force $SKILL_DIR\references -ErrorAction SilentlyContinue`
- `Get-ChildItem -Force $SKILL_DIR\workflows -ErrorAction SilentlyContinue`
- `Get-ChildItem -Force $SKILL_DIR\templates -ErrorAction SilentlyContinue`
- `Get-ChildItem -Force $SKILL_DIR\scripts -ErrorAction SilentlyContinue`
