# Bearletter for AI agents

The Bearletter MCP server and a skill for using it, packaged for the agents that take plugins. The server is `https://api.bearletter.com/mcp`; you approve it in the browser the first time, with no key. Docs: https://docs.bearletter.com/mcp/skills

The same files are served from docs, for agents that cannot reach GitHub: https://docs.bearletter.com/skills/bearletter/SKILL.md, https://docs.bearletter.com/skills/bearletter.zip and https://docs.bearletter.com/agents.zip.

| Agent | Install |
| --- | --- |
| Claude Code | `/plugin marketplace add devxiyang/bearletter-agents`, then `/plugin install bearletter@bearletter` |
| Codex | Install this folder as a plugin (`plugin.json`, `mcp.json`, `skills/`) |
| Gemini CLI | `gemini extensions install https://github.com/devxiyang/bearletter-agents` |
| Others | Copy `skills/bearletter` into `.agents/skills/` (or your agent's skills folder) and add the MCP server above |

Everything here is plain files: `skills/bearletter/SKILL.md` is the skill, the rest tells each agent where the server is.
