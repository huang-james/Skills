# Skills

Some public skills of AI tools for personal use.

## Available Skills

### [simplicity-first](./simplicity-first/README.md) · [SKILL](./simplicity-first/SKILL.md)

Simplicity gate for ALL code written, fixed, or reviewed. Invoke BEFORE writing any code change and when reviewing any diff. Treats over-complex or oversized code as a correctness bug, not a style issue.

### [code-simplification](./code-simplification/README.md) · [SKILL](./code-simplification/SKILL.md)

Simplifies code for clarity without changing behavior. Use when code works but is harder to read, maintain, or extend than it should be, or when reviewing code that has accumulated unnecessary complexity.

## Installation

Copy a skill folder into your agent's skills directory:

| Tool | Location |
|---|---|
| ZCode | `~/.zcode/skills/<skill-name>/SKILL.md` |
| Claude Code | `~/.claude/skills/<skill-name>/SKILL.md` |
| Codex | `$CODEX_HOME/skills/<skill-name>/SKILL.md` |
