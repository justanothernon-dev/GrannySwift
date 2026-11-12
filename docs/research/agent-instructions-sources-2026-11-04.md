# Agent instruction references

**Purpose:** The sources behind this repository's coding-agent instructions. Nothing loads this note.  
**Primary sources reviewed:** November 4, 2026 (America/New_York).

## Reference register

| Source | Type | GrannySwift use |
| --- | --- | --- |
| [OpenAI: AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md) | Official | Concise project instructions; scoped overrides only for real differences |
| [Claude Code: best practices](https://code.claude.com/docs/en/best-practices) | Official | Small always-loaded instructions, focused skills, enforceable CI/hooks for deterministic rules |
| [Claude Code: memory and AGENTS.md](https://code.claude.com/docs/en/memory) | Official | Project instructions differ from automatic memory; current versions can read AGENTS.md. The existing CLAUDE.md symlink is valid single-source sharing |
| [Matt Pocock: writing-for-agents](https://github.com/mattpocock/skills/blob/main/skills/productivity/writing-for-agents/SKILL.md) | Upstream skill | Progressive disclosure, strong context pointers, one authoritative home per rule |
| [Matt Pocock: grill-with-docs](https://github.com/mattpocock/skills/blob/main/skills/engineering/grill-with-docs/SKILL.md), [grilling](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md), [domain-modeling](https://github.com/mattpocock/skills/blob/main/skills/engineering/domain-modeling/SKILL.md) | Upstream skills | Ask only unresolved owner decisions, record actual answers, add glossary/ADRs when warranted |
| [Matt Pocock: handoff](https://github.com/mattpocock/skills/blob/main/skills/productivity/handoff/SKILL.md) | Upstream skill | Point agents to canonical records, not copies of an entire conversation |
| [Community AGENTS.md examples](https://gist.github.com/0xfauzi/7c8f65572930a21efa62623557d83f6e) | Community | Evaluate relevant patterns selectively; do not copy unrelated Python/AWS instructions or version claims |

The register is a map of sources and adopted practices, not a copy of those instruction sets. Prefer current official documentation to community claims or older summaries.
