# Mistral Vibe Tool Mapping

Skills use Claude Code tool names. When you encounter these in a skill, use your platform equivalent:

| Skill references | Mistral Vibe equivalent |
|-----------------|------------------------|
| `Read` (file reading) | `read_file` |
| `Write` (file creation) | `write_file` |
| `Edit` (file editing) | `search_replace` |
| `Bash` (run commands) | `bash` |
| `Grep` (search file content) | `grep` |
| `Glob` (search files by name) | Use `bash` with `find` or `grep` for file discovery |
| `TodoWrite` (task tracking) | `todo` (use action="write" with todo items) |
| `Skill` tool (invoke a skill) | `skill` |
| `WebSearch` | `websearch` |
| `WebFetch` | `webfetch` |
| `Task` tool (dispatch subagent) | `task` (default agent: `explore`) |
| `EnterPlanMode` | Switch to `plan` agent via `--agent plan` or agent switching |
| `ExitPlanMode` | `exit_plan_mode` |

## Subagent support

Mistral Vibe supports subagent dispatch via the `task` tool. Subagent configurations are defined in `mistral-vibe/agents/` as TOML files with `agent_type = "subagent"`. Only SUBAGENT types can be dispatched via `task`; built-in AGENT types (`default`, `accept-edits`, `auto-approve`, `plan`, `chat`, `lean`) cannot.

### Superpowers Subagents (Dispatchable via `task`)

| Skill reference | Mistral Vibe agent | Purpose | Enabled tools |
|-----------------|--------------------|---------|---------------|
| `superpowers:explore` | `explore` (built-in) | Read-only codebase exploration | `grep`, `read_file` |
| `superpowers:implementer` | `implementer` | Implements tasks with isolated context | `grep`, `read_file`, `write_file` |
| `superpowers:spec-reviewer` | `spec-reviewer` | Spec compliance review | `grep`, `read_file` |
| `superpowers:code-quality-reviewer` | `code-quality-reviewer` | Code quality review | `grep`, `read_file` |
| `superpowers:code-reviewer` | `code-reviewer` | Final code review against requirements | `grep`, `read_file` |
| `superpowers:spec-document-reviewer` | `spec-document-reviewer` | Specification document review | `read_file` |

When a skill dispatches a named subagent, use the `task` tool with the corresponding agent name and include the prompt content from the skill's prompt template (e.g., `subagent-driven-development/implementer-prompt.md`).

## Additional Mistral Vibe tools

These tools are available in Mistral Vibe but have no Claude Code equivalent:

| Tool | Purpose |
|------|---------|
| `ask_user_question` | Request structured input from the user with choices |

## Context files

Mistral Vibe automatically discovers and injects `AGENTS.md` files from `.vibe/` directories. Use these for project-specific instructions.
