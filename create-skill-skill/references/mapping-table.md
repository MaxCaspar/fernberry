# External To Codex Mapping Table

| External Concept | Codex Equivalent | Notes |
| --- | --- | --- |
| System prompt / instructions | SKILL.md Objective + Essential Principles | Keep concise; move depth to references/ |
| Tool definitions | Workflow steps or references | Include constraints and verification |
| Agent role/goal | Objective and Success Criteria | Preserve intent |
| Policies / safety rules | References + workflow checks | Make explicit |
| Commands / aliases | Codex command file | Use frontmatter + body |
| Examples | References or Examples section | Avoid long blocks in SKILL.md |

## Field Mapping Hints
- `name` ? skill directory + frontmatter `name`
- `description` ? frontmatter `description`
- `instructions` ? Objective/Essential Principles
- `tools` ? workflow steps and verification
