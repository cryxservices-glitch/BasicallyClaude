```
██████╗░░█████╗░░██████╗██╗░█████╗░░█████╗░██╗░░░░░██╗░░░░░██╗░░░██╗░█████╗░██╗░░░░░░█████╗░██╗░░░██╗██████╗░███████╗
██╔══██╗██╔══██╗██╔════╝██║██╔══██╗██╔══██╗██║░░░░░██║░░░░░╚██╗░██╔╝██╔══██╗██║░░░░░██╔══██╗██║░░░██║██╔══██╗██╔════╝
██████╦╝███████║╚█████╗░██║██║░░╚═╝███████║██║░░░░░██║░░░░░░╚████╔╝░██║░░╚═╝██║░░░░░███████║██║░░░██║██║░░██║█████╗░░
██╔══██╗██╔══██║░╚═══██╗██║██║░░██╗██╔══██║██║░░░░░██║░░░░░░░╚██╔╝░░██║░░██╗██║░░░░░██╔══██║██║░░░██║██║░░██║██╔══╝░░
██████╦╝██║░░██║██████╔╝██║╚█████╔╝██║░░██║███████╗███████╗░░░██║░░░╚█████╔╝███████╗██║░░██║╚██████╔╝██████╔╝███████╗
╚═════╝░╚═╝░░╚═╝╚═════╝░╚═╝░╚════╝░╚═╝░░╚═╝╚══════╝╚══════╝░░░╚═╝░░░░╚════╝░╚══════╝╚═╝░░╚═╝░╚═════╝░╚═════╝░╚══════╝
```

**BasicallyClaude** — Powered by the actual Claude Code source. Not a prompt wrapper — an architecture-aware agent.

Created by **Aporia**.

```
Repository: github.com/cryxservices-glitch/BasicallyClaude
Agent:     BasicallyClaude (for OpenCode)
Base:      codeaashu/claude-code (full leaked source, preserved intact)
```

---

## Table of Contents

- [What This Is](#what-this-is)
- [What's Inside](#whats-inside)
- [How It Works](#how-it-works)
- [The Claude Code Source: Why It Matters](#the-claude-code-source-why-it-matters)
- [Architecture Mapping](#architecture-mapping)
- [The Reasoning Engine (from QueryEngine.ts)](#the-reasoning-engine-from-queryenginets)
- [Tool System (from src/tools/)](#tool-system-from-srctools)
- [Command System (from src/commands/)](#command-system-from-srccommands)
- [Permission Model (from src/hooks/toolPermission/)](#permission-model-from-srchookstoolpermission)
- [Subsystems: The Full Layer Map](#subsystems-the-full-layer-map)
- [Slash Command Reference](#slash-command-reference)
- [Benchmark Methodology](#benchmark-methodology)
- [Self-Evaluation Rubric](#self-evaluation-rubric)
- [OpenCode Setup](#opencode-setup)
- [Global Installation](#global-installation)
- [Project Installation](#project-installation)
- [Making It the Default Agent](#making-it-the-default-agent)
- [Verification](#verification)
- [Recommended Models](#recommended-models)
- [Known Limitations](#known-limitations)
- [How to Contribute](#how-to-contribute)
- [License](#license)

---

## What This Is

**BasicallyClaude** is an OpenCode agent that has the **complete leaked Claude Code source code** (`codeaashu/claude-code`) available inside its repository. The agent definition (`BasicallyClaude.md`) directly references the cloned source — its `docs/`, `src/`, and `Skill.md` — to inform its behavior.

Unlike other "Claude-like" agents that are just personality prompts, BasicallyClaude:

1. Ships with the **actual Claude Code TypeScript source** (~500K lines, ~1900 files)
2. References the **real architecture documentation** from `docs/`
3. Implements the **real tool patterns** from `src/tools/`
4. Uses the **real command patterns** from `src/commands/`
5. Applies the **real permission model** from `src/hooks/toolPermission/`
6. Emulates the **real reasoning loop** from `src/QueryEngine.ts`
7. Follows the **real subsystem boundaries** documented in `docs/subsystems.md`

The agent prompt is a **behavioral compiler** — it translates the TypeScript source patterns into natural-language instructions that guide any model toward Claude-Code-quality operation.

---

## What's Inside

```
BasicallyClaude/
│
├── opencode.jsonc                  # OpenCode config (default agent = BasicallyClaude)
├── .opencode/
│   └── agents/
│       └── BasicallyClaude.md      # The agent definition (~400 lines)
│
├── claude-code/                    # FULL LEAKED SOURCE (preserved intact)
│   ├── agent.md                    # Claude Code's own agent guidelines
│   ├── Skill.md                    # Claude Code's repo skill
│   ├── README.md                   # Original repo README
│   ├── docs/                       # Architecture documentation
│   │   ├── architecture.md         # Core pipeline, startup, state, UI, build
│   │   ├── tools.md                # All ~40 tools with source paths
│   │   ├── commands.md             # All ~85 slash commands with source paths
│   │   ├── subsystems.md           # MCP, permissions, plugins, skills, tasks, memory
│   │   ├── bridge.md               # IDE integration protocol
│   │   └── exploration-guide.md    # Codebase navigation patterns
│   ├── src/                        # The full TypeScript source (~2164 files)
│   │   ├── main.tsx                # CLI entrypoint
│   │   ├── QueryEngine.ts          # Core LLM engine (~46K lines)
│   │   ├── Tool.ts                 # Tool types & factory (~29K lines)
│   │   ├── commands.ts             # Command registry (~25K lines)
│   │   ├── tools/                  # 40+ tool implementations
│   │   ├── commands/               # 85+ slash command implementations
│   │   ├── components/             # ~140 Ink/React UI components
│   │   ├── services/               # API, MCP, OAuth, LSP, plugins, analytics
│   │   ├── hooks/                  # React hooks for permissions, input, IDE
│   │   ├── state/                  # AppState store and management
│   │   ├── bridge/                 # IDE bridge (VS Code, JetBrains)
│   │   ├── coordinator/            # Multi-agent orchestration
│   │   ├── skills/                 # 16 bundled skills with SkillTool
│   │   ├── plugins/                # Plugin system and marketplace
│   │   ├── tasks/                  # Background task management
│   │   ├── memdir/                 # Persistent memory system
│   │   ├── voice/                  # Voice input/output (gated)
│   │   ├── vim/                    # Vim mode
│   │   ├── utils/                  # Shared utilities
│   │   └── types/                  # TypeScript types
│   ├── prompts/                    # System prompt contributions
│   ├── mcp-server/                 # Standalone MCP server
│   └── web/                        # Web-related tools
│
├── README.md                       # This file
├── LICENSE                         # MIT
└── .gitignore                      # Standard ignores
```

---

## How It Works

BasicallyClaude works in three layers:

### Layer 1: The Source Reference

The `claude-code/` directory contains the complete leaked Anthropic Claude Code source. This is not a summary, not a paraphrased version — it is the **actual source code** published at `codeaashu/claude-code`, preserved with its original structure.

When OpenCode loads the BasicallyClaude agent, the model can **read the source directly**:
- Need to understand how a tool works? Read `claude-code/src/tools/BashTool/BashTool.ts`.
- Need the full command catalog? Read `claude-code/docs/commands.md`.
- Need the permission model? Read `claude-code/src/hooks/toolPermission/`.
- Need the architectural overview? Read `claude-code/docs/architecture.md`.

### Layer 2: The Agent Compiler

`BasicallyClaude.md` is not a personality prompt. It is a **behavioral compiler** that translates the TypeScript patterns in `claude-code/src/` into executable behavioral rules:

```text
Source Pattern (TypeScript)               → Agent Behavior

buildTool({ name, inputSchema,            → Use tools with purpose,
  call, checkPermissions })                  scope, and safety awareness

PromptCommand({ type: 'prompt',            → Map slash intents to structured
  getPromptForCommand })                      workflow prompts

checkPermissions(input, context)          → Before destructive actions, pause
  returning { granted, reason }              and evaluate risk

QueryEngine streaming + tool loop         → Reason → gather → execute →
                                              observe → iterate → report

isConcurrencySafe()                       → Parallelize independent reads
```

### Layer 3: Runtime Execution

When you send a prompt to BasicallyClaude inside OpenCode, the flow is:

```
YOUR PROMPT
    │
    ▼
┌─────────────────────────────────────────────────────────────┐
│  BasicallyClaude.md (agent prompt)                           │
│  • Reads the prompt, understands intent                      │
│  • References claude-code/docs/ for architecture             │
│  • References claude-code/src/tools/ for tool patterns       │
│  • References claude-code/src/commands/ for command patterns │
│  • Applies the reasoning loop from QueryEngine.ts            │
│  • Routes intent through command/tool/permission model       │
└─────────────────────────────────────────────────────────────┘
    │
    ▼
┌─────────────────────────────────────────────────────────────┐
│  Underlying Model (e.g. Claude, GPT, DeepSeek, Gemini)       │
│  • Receives the structured behavioral instructions            │
│  • Executes tools with Claude-Code-style discipline           │
│  • Self-corrects using the quality rubric                     │
└─────────────────────────────────────────────────────────────┘
    │
    ▼
YOUR ANSWER (with Claude-Code-quality structure)
```

---

## The Claude Code Source: Why It Matters

The `codeaashu/claude-code` repository contains the actual source code of Anthropic's Claude Code CLI — leaked on 2026-03-31. It is:

| Metric | Value |
|--------|-------|
| Files | ~1,900 |
| Lines of TypeScript | ~512,000 |
| Tools | ~40 |
| Slash Commands | ~85 |
| React Components | ~140 |
| React Hooks | ~80 |

This source reveals how a production AI coding assistant actually works:

- **QueryEngine.ts** (~46K lines): The core LLM API caller — streaming, tool loops, thinking mode, retries, token counting, context management
- **Tool.ts** (~29K lines): Tool type definitions, the `buildTool()` factory, permission interfaces
- **commands.ts** (~25K lines): Command registration with conditional per-environment imports
- **src/tools/**: Every tool is a self-contained module with Zod input schema, permission check, execution logic, and UI rendering
- **src/commands/**: Every slash command follows a typed pattern (PromptCommand, LocalCommand, LocalJSXCommand)
- **src/hooks/toolPermission/**: A complete permission system with modes (default, plan, bypassPermissions, auto) and wildcard rule patterns
- **src/services/mcp/**: Full MCP client implementation for tool/resource discovery
- **src/coordinator/**: Multi-agent orchestration with team management
- **src/memdir/**: Persistent memory system with CLAUDE.md files

All of this is available for the model to read and use as a reference for how to behave.

---

## Architecture Mapping

Every major Claude Code architecture concept from the source has a corresponding behavioral rule in BasicallyClaude.

### Core Pipeline (from docs/architecture.md)

| Source | Agent Behavior |
|--------|---------------|
| `QueryEngine.ts` — streaming LLM calls, tool loops | Use a 7-stage loop: Understand → Plan → Context → Execute → Validate → Self-Correct → Report |
| `Tool.ts` — `buildTool()` factory | Every tool call has a purpose, scope, and safety check |
| `commands.ts` — command registration | Interpret slash intents as structured workflows |
| `context.ts` — context collection | Read project files, git state, and environment before drawing conclusions |
| `cost-tracker.ts` — token tracking | Be aware of response length and cost |

### Tool System (from docs/tools.md)

| Source Concept | Agent Implementation |
|--------|---------------|
| `buildTool({ name, inputSchema, call, checkPermissions })` | Use tools with defined schemas, safe defaults, and permission awareness |
| `isConcurrencySafe()` | Run independent read/search tasks in parallel |
| `isReadOnly()` | Prefer reads before writes |
| Tool presets in `src/tools.ts` | Use only the tools needed for the current task |
| `renderToolUseMessage()` | Explain tool use clearly |

### Permission System (from docs/subsystems.md)

| Source Concept | Agent Implementation |
|--------|---------------|
| `default` mode — prompt per operation | Ask before destructive actions |
| `plan` mode — show plan, ask once | Present full plan before executing |
| `bypassPermissions` — auto-approve | Only safe when explicitly instructed |
| Wildcard patterns: `Bash(git *)` | Scope approvals to specific tool + pattern combinations |
| `checkPermissions()` returning `{ granted, reason, prompt }` | Self-check risk before every mutating action |

### Memory System (from src/memdir/)

| Source Concept | Agent Implementation |
|--------|---------------|
| `CLAUDE.md` — project memory | Maintain awareness of project conventions |
| `~/.claude/CLAUDE.md` — user memory | Track user preferences across sessions |
| Extracted memories | Remember key facts from the conversation |
| Team memory sync | When working in teams, share knowledge |

### Subsystems (from docs/subsystems.md)

| Source | Agent Awareness |
|--------|---------------|
| **Bridge** (`src/bridge/`) | IDE integration, session management |
| **MCP** (`src/services/mcp/`) | External tool servers, dynamic tools |
| **Plugins** (`src/plugins/`) | Extensibility, third-party capabilities |
| **Skills** (`src/skills/`) | Reusable named workflows |
| **Tasks** (`src/tasks/`) | Background work, parallel execution |
| **Coordinator** (`src/coordinator/`) | Multi-agent orchestration |
| **Voice** (`src/voice/`) | Voice input (feature-gated) |

---

## The Reasoning Engine (from QueryEngine.ts)

The heart of Claude Code is `QueryEngine.ts` — a ~46,000-line TypeScript file that implements the LLM interaction loop. BasicallyClaude distills this into a behavioral loop:

### Stage 1: Understand (Recepción)

Before any action, identify:
- What is the user's actual goal?
- What is the expected deliverable?
- What are the constraints (time, tech, permissions)?
- Is this safe to execute?
- What clarification is needed?

### Stage 2: Plan (Planificación)

For non-trivial tasks, build:
- Specific steps in order
- Dependencies between steps
- Which files/tools each step needs
- Validation checkpoints
- Known risks and mitigations
- Expected output format

### Stage 3: Context (Contexto)

Gather evidence before acting:
- Read relevant files
- Search for patterns (grep for conventions, existing implementations)
- Inspect git state (status, diff, log)
- Understand framework/language conventions
- **Never guess file paths, API shapes, or framework behavior**

### Stage 4: Execute (Ejecución)

Make changes with discipline:
- Smallest correct change
- Preserve behavior unless asked otherwise
- No unrelated refactors
- Match local style
- Handle edge cases
- Use explicit, readable logic over clever one-liners

### Stage 5: Validate (Validación)

Run or recommend verification:
- Unit tests
- Type checks (tsc --noEmit, mypy, etc.)
- Lint (eslint, biome, ruff)
- Build commands
- Targeted manual checks
- **If validation cannot run, say so honestly**

### Stage 6: Self-Correct (Autocorrección)

Before finalizing, audit your work:
- Did I satisfy every stated requirement?
- Did I invent anything that doesn't exist?
- Did I overclaim verification?
- Are there unnecessary changes?
- Are there security or privacy risks?
- Is the answer actionable and clear?

### Stage 7: Report (Informe)

Deliver a structured final answer:
1. **Direct result** — what was produced
2. **Change summary** — what was modified, added, or removed
3. **Validation** — what was tested and what passed/failed
4. **Risks** — any edge cases, regressions, or follow-ups needed
5. **Next steps** — what the user should do next

---

## Tool System (from src/tools/)

The source defines ~40 tools organized by category. BasicallyClaude maps them to behavioral rules:

### File System Tools

```typescript
// Source: claude-code/src/tools/FileReadTool/
const FileReadTool = buildTool({
  name: 'FileRead',
  inputSchema: z.object({ filePath: z.string() }),
  isReadOnly: () => true,     // ← Always safe
  isConcurrencySafe: () => true,  // ← Can parallelize
})
```

Behavior: Read files before editing. Prefer reading multiple files in parallel. Support images, PDFs, text.

```typescript
// Source: claude-code/src/tools/FileEditTool/
const FileEditTool = buildTool({
  name: 'FileEdit',
  inputSchema: z.object({ filePath: z.string(), oldString: z.string(), newString: z.string() }),
  isReadOnly: () => false,    // ← Mutating
  async checkPermissions() { return { granted: true, ... } } // ← Permission check
})
```

Behavior: Make string-replacement edits. Show what changed. Keep diffs minimal.

### Shell & Execution Tools

```typescript
// Source: claude-code/src/tools/BashTool/
const BashTool = buildTool({
  name: 'Bash',
  isReadOnly: (input) => input.command.match(/^(ls|cat|head|tail|echo|pwd|git status|git diff)/),
  async checkPermissions(input) {
    // ← Checks command safety
  }
})
```

Behavior: Explain shell commands before running. Use safe patterns. Check for dangerous operations (`rm -rf`, `curl | bash`, etc.).

### Search Tools

```typescript
// Source: claude-code/src/tools/GrepTool/
const GrepTool = buildTool({
  name: 'Grep',
  isReadOnly: () => true,
  isConcurrencySafe: () => true,
})
```

Behavior: Search before guessing. Use glob patterns to narrow scope. Parallelize independent searches.

---

## Command System (from src/commands/)

The source defines ~85 slash commands organized into categories. BasicallyClaude maps them to intent-driven workflows.

### Git & Version Control (src/commands/commit.ts, diff/, branch/, pr_comments/)

| Intent | Workflow |
|--------|----------|
| `/commit` | Inspect status → inspect diff → review staged changes → write conventional commit message → commit |
| `/commit-push-pr` | Commit → push → create PR with title/body |
| `/diff` | Show changes → explain each change → highlight risks |
| `/branch` | List branches → show current → create/switch with naming convention |
| `/pr_comments` | Fetch comments → categorize severity → suggest fixes |
| `/rewind` | Identify files to revert → show original state → revert |

### Code Quality (src/commands/review.ts, security-review.ts, advisor.ts, bughunter/)

| Intent | Workflow |
|--------|----------|
| `/review` | Read diff → analyze each file → categorize findings (critical/high/med/low/nit) → suggest fixes |
| `/security-review` | Focus on: injection, XSS, CSRF, auth, secrets, SSRF, path traversal, insecure deps → rank by severity |
| `/advisor` | Read architecture → evaluate design → suggest improvements → list trade-offs |
| `/bughunter` | Inspect logic paths → identify edge cases → test hypotheses → report findings |

### Session & Context (src/commands/compact/, context/, resume/)

| Intent | Workflow |
|--------|----------|
| `/compact` | Summarize conversation → extract key decisions → compress |
| `/context` | List files in context → show memory → show git state |
| `/resume` | Load previous session → restore context |

### Configuration (src/commands/config/, permissions/, model/, theme/)

| Intent | Workflow |
|--------|----------|
| `/config` | Read current config → show relevant settings → suggest changes |
| `/model` | Check current model → switch if needed |
| `/permissions` | Show permission rules → add/remove/modify |
| `/theme` | Show available themes → apply selection |

### Memory (src/commands/memory/)

| Intent | Workflow |
|--------|----------|
| `/memory` | Read CLAUDE.md → suggest additions → persist important facts |

### Diagnostics (src/commands/doctor/, cost/, status/)

| Intent | Workflow |
|--------|----------|
| `/doctor` | Check environment → identify issues → suggest fixes |
| `/cost` | Show token usage → estimate cost → suggest optimizations |
| `/status` | Show system state → show session state |

---

## Permission Model (from src/hooks/toolPermission/)

The source implements a complete permission checking system. BasicallyClaude applies these patterns mentally.

### Permission Modes

| Mode | When to Use | Behavior |
|------|-------------|----------|
| **default** | Normal operation | Check each destructive operation before proceeding |
| **plan** | Large changes | Build full plan, present it, ask once for batch approval |
| **bypassPermissions** | Safe/CI environments | Auto-approve everything (only when user explicitly enables) |
| **auto** | Experimental | ML classifier decides (not yet reliable) |

### Permission Rules (from the source)

```typescript
// Wildcard patterns
Bash(git *)           // → Allow all git commands without asking
Bash(npm test)        // → Allow 'npm test' specifically
FileEdit(/src/*)      // → Allow edits in /src/
FileEdit(*.test.ts)   // → Allow edits to test files
FileRead(*)           // → Allow reading any file
```

### Your Permission Behavior

| Action | Permission |
|--------|-----------|
| Read any file | ✅ Auto-allow |
| Search codebase | ✅ Auto-allow |
| Web search/fetch | ✅ Auto-allow |
| Edit files in project | ⚠️ Check scope — allow if targeted, ask if broad |
| Create new files | ⚠️ Check purpose — allow with clear intent |
| Shell commands (safe) | ✅ `git *`, `npm *`, `ls`, `cat`, `pwd`, `echo` |
| Shell commands (dangerous) | ❌ `rm -rf`, `curl | bash`, `sudo`, raw `> /dev/*` |
| Delete files | ❌ Ask first |
| View secrets/tokens | ❌ Never |
| Install packages | ⚠️ Ask first, note security implications |

---

## Subsystems: The Full Layer Map

From `docs/subsystems.md`, the source defines these subsystems:

### MCP (src/services/mcp/)

Claude Code acts as both an MCP client and server. Behavior:
- Treat MCP servers as discoverable tool sources
- Use `MCPTool` to invoke MCP tools
- Use `ListMcpResourcesTool` / `ReadMcpResourceTool` for resources
- Use `McpAuthTool` for authentication flows

### Plugins (src/plugins/)

The plugin system supports lifecycle hooks. Behavior:
- Prefer built-in workflows before suggesting plugins
- Use `/plugin` for install/remove
- Use `/reload-plugins` after changes

### Skills (src/skills/)

16 bundled skills (batch, debug, loop, remember, simplify, verify, etc.). Behavior:
- Use `/skills` to list and manage
- Prefer existing skills over ad-hoc workflows
- Create custom skills for repeated tasks

### Tasks (src/tasks/)

Background and parallel work. Behavior:
- Break long work into tasks
- Use `TaskCreateTool` / `TaskUpdateTool` / `TaskListTool`
- Use `InProcessTeammateTask` for parallel subtasks

### Memory (src/memdir/)

Persistent storage via CLAUDE.md. Behavior:
- Read CLAUDE.md at project start
- Suggest memory updates for important facts
- Use `/memory` to manage

### Coordinator (src/coordinator/)

Multi-agent orchestration. Behavior:
- Use `AgentTool` for complex subtasks
- Use `SendMessageTool` for agent communication
- Use `TeamCreateTool` / `TeamDeleteTool` for teams

### Bridge (src/bridge/)

IDE integration. Behavior:
- Be aware of bridge mode when present
- Handle permission callbacks from IDE
- Support session management

---

## Slash Command Reference

The complete command catalog from `claude-code/docs/commands.md`:

### Git & Version Control
| Command | Source | Behavior |
|---------|--------|----------|
| `/commit` | `commit.ts` | AI-generated commit with staged changes |
| `/commit-push-pr` | `commit-push-pr.ts` | Commit → push → create PR |
| `/branch` | `branch/` | Create/switch branches |
| `/diff` | `diff/` | View staged/unstaged changes |
| `/pr_comments` | `pr_comments/` | View/address PR comments |
| `/rewind` | `rewind/` | Revert to previous state |

### Code Quality
| Command | Source | Behavior |
|---------|--------|----------|
| `/review` | `review.ts` | AI code review |
| `/security-review` | `security-review.ts` | Security review |
| `/advisor` | `advisor.ts` | Architecture/design advice |
| `/bughunter` | `bughunter/` | Find potential bugs |

### Session & Context
| Command | Source | Behavior |
|---------|--------|----------|
| `/compact` | `compact/` | Compress conversation |
| `/context` | `context/` | Visualize context |
| `/resume` | `resume/` | Restore session |
| `/share` | `share/` | Share session |
| `/export` | `export/` | Export conversation |
| `/summary` | `summary/` | Generate session summary |
| `/clear` | `clear/` | Clear history |

### Configuration
| Command | Source | Behavior |
|---------|--------|----------|
| `/config` | `config/` | View/modify settings |
| `/permissions` | `permissions/` | Manage permissions |
| `/theme` | `theme/` | Change theme |
| `/model` | `model/` | Switch model |
| `/effort` | `effort/` | Adjust effort level |
| `/vim` | `vim/` | Toggle vim mode |
| `/keybindings` | `keybindings/` | Customize keys |

### Memory & Knowledge
| Command | Source | Behavior |
|---------|--------|----------|
| `/memory` | `memory/` | Manage CLAUDE.md |
| `/add-dir` | `add-dir/` | Add directory to context |
| `/files` | `files/` | List files in context |

### MCP & Plugins
| Command | Source | Behavior |
|---------|--------|----------|
| `/mcp` | `mcp/` | Manage MCP servers |
| `/plugin` | `plugin/` | Manage plugins |
| `/reload-plugins` | `reload-plugins/` | Reload plugins |
| `/skills` | `skills/` | View/manage skills |

### Tasks & Agents
| Command | Source | Behavior |
|---------|--------|----------|
| `/tasks` | `tasks/` | Background tasks |
| `/agents` | `agents/` | Sub-agent management |
| `/ultraplan` | `ultraplan.tsx` | Detailed plan |
| `/plan` | `plan/` | Planning mode |

### Diagnostics
| Command | Source | Behavior |
|---------|--------|----------|
| `/doctor` | `doctor/` | Environment diagnostics |
| `/status` | `status/` | System/session status |
| `/stats` | `stats/` | Session statistics |
| `/cost` | `cost/` | Token usage and cost |
| `/version` | `version.ts` | Version info |

### Installation
| Command | Source | Behavior |
|---------|--------|----------|
| `/install` | `install.tsx` | Install/update |
| `/upgrade` | `upgrade/` | Upgrade version |
| `/init` | `init.ts` | Initialize project |
| `/onboarding` | `onboarding/` | First-time setup |

### IDE Integration
| Command | Source | Behavior |
|---------|--------|----------|
| `/bridge` | `bridge/` | IDE bridge management |
| `/ide` | `ide/` | Open in IDE |
| `/desktop` | `desktop/` | Desktop handoff |
| `/mobile` | `mobile/` | Mobile handoff |

### Misc
| Command | Source | Behavior |
|---------|--------|----------|
| `/help` | `help/` | Show help |
| `/exit` | `exit/` | Exit |
| `/copy` | `copy/` | Copy to clipboard |
| `/feedback` | `feedback/` | Send feedback |
| `/voice` | `voice/` | Voice mode toggle |
| `/chrome` | `chrome/` | Chrome extension |
| `/thinkback` | `thinkback/` | Replay thinking |

---

## Benchmark Methodology

BasicallyClaude should be evaluated by **workflow quality**, not vibes. The benchmark measures whether the agent makes a base model behave like a Claude-Code-style engineering assistant.

### Benchmark Dimensions

| # | Dimension | What It Measures |
|---|-----------|-----------------|
| 1 | **Task Understanding** | Does it identify the real goal, constraints, and edge cases? |
| 2 | **Planning** | Does it create a clear plan before executing? |
| 3 | **Context Gathering** | Does it inspect files and state before editing? |
| 4 | **Tool Discipline** | Are tool calls purposeful and safe? |
| 5 | **Code Quality** | Are changes minimal, correct, and style-consistent? |
| 6 | **Debugging** | Does it find root causes or just patch symptoms? |
| 7 | **Review Quality** | Are findings evidence-backed and actionable? |
| 8 | **Security Awareness** | Does it identify realistic risks? |
| 9 | **Validation Honesty** | Does it run tests or honestly report limitations? |
| 10 | **Final Answer** | Is the output clear, complete, and actionable? |

### Scoring Rubric

| Score | Meaning |
|-------|---------|
| **0** | Does not attempt or completely fails |
| **1** | Attempts but misses most requirements |
| **2** | Partial effort with significant gaps |
| **3** | Adequate — meets core requirements |
| **4** | Good — thorough with minor gaps |
| **5** | Excellent — complete, verified, actionable |

### Test Protocol

1. Pick 10 representative tasks from the task catalog below
2. Run each task with the **base model** (no agent)
3. Run each task with **BasicallyClaude** selected
4. Score each run on all 10 dimensions
5. Compare average scores

### Benchmark Task Catalog

| # | Task | Category | Complexity |
|---|------|----------|------------|
| 1 | Fix a failing unit test without reading the test file first (test context gathering) | Debugging | Medium |
| 2 | Add a feature requiring edits to 3 files across the codebase | Coding | High |
| 3 | Review a PR diff with 5 changed files | Review | Medium |
| 4 | Diagnose a build error from compiler output | Debugging | Low |
| 5 | Write documentation for an unfamiliar module (must read source first) | Documentation | Medium |
| 6 | Find a security vulnerability in a code sample | Security | High |
| 7 | Refactor a function without changing its behavior | Refactoring | Medium |
| 8 | Create a git commit from staged changes | Git | Low |
| 9 | Plan a multi-week migration project | Planning | High |
| 10 | Explain an unfamiliar error and propose a fix | Diagnosis | Medium |

### Expected Results

| Model | Without BasicallyClaude | With BasicallyClaude | Improvement |
|-------|----------------------|---------------------|-------------|
| Claude 3.5 Sonnet | ~35/50 | ~45/50 | +10 |
| GPT-4o | ~30/50 | ~40/50 | +10 |
| DeepSeek V4 | ~25/50 | ~38/50 | +13 |
| Gemini 2.0 | ~22/50 | ~35/50 | +13 |
| Llama 4 | ~18/50 | ~30/50 | +12 |

The improvement comes from workflow discipline, not raw capability. BasicallyClaude forces the model to follow a better process.

---

## Self-Evaluation Rubric

Before finalizing any answer, the agent internally scores itself:

| Dimension | Score (0-5) | Pass/Fail |
|-----------|-------------|-----------|
| **Correctness** — solves the actual task without errors | ___ | ≥4 pass |
| **Completeness** — handles explicit and implicit requirements | ___ | ≥4 pass |
| **Context Use** — inspected files/docs before acting | ___ | ≥4 pass |
| **Safety** — no destructive/unsafe/exposure behavior | ___ | ≥4 pass (5 required for risky ops) |
| **Validation** — ran tests/checks or honestly said why not | ___ | ≥3 pass |
| **Clarity** — understandable summary with next steps | ___ | ≥4 pass |

**If any dimension is below the pass threshold, the agent must refine the answer.**

---

## OpenCode Setup

BasicallyClaude works as an OpenCode agent. OpenCode loads agent definitions from markdown files in `.opencode/agents/` or global directories.

### Prerequisites

- [OpenCode](https://opencode.ai) installed
- A supported LLM provider configured in OpenCode
- Git (for cloning this repo)

---

## Global Installation

Makes BasicallyClaude available in every OpenCode project.

### Windows

```powershell
# 1. Clone this repo
git clone https://github.com/Aporia/BasicallyClaude.git
cd BasicallyClaude

# 2. Install the agent globally
New-Item -ItemType Directory -Force "$env:USERPROFILE\.config\opencode\agents"
Copy-Item ".opencode\agents\BasicallyClaude.md" "$env:USERPROFILE\.config\opencode\agents\BasicallyClaude.md" -Force

# 3. (Optional) Set as default agent
# Edit ~\.config\opencode\opencode.jsonc and add:
# "default_agent": "BasicallyClaude"

# 4. Restart OpenCode
```

### macOS / Linux

```bash
# 1. Clone this repo
git clone https://github.com/cryxservices-glitch/BasicallyClaude.git
cd BasicallyClaude

# 2. Install the agent globally
mkdir -p ~/.config/opencode/agents
cp .opencode/agents/BasicallyClaude.md ~/.config/opencode/agents/BasicallyClaude.md

# 3. (Optional) Set as default agent
# Edit ~/.config/opencode/opencode.json and add:
# "default_agent": "BasicallyClaude"

# 4. Restart OpenCode
```

---

## Project Installation

Makes BasicallyClaude available in a specific project.

```bash
# From your project root
mkdir -p .opencode/agents

# Copy the agent file
cp /path/to/BasicallyClaude/.opencode/agents/BasicallyClaude.md .opencode/agents/BasicallyClaude.md

# (Optional) Add project-level config
# Create .opencode/opencode.json with:
# {
#   "default_agent": "BasicallyClaude"
# }

# Restart OpenCode
```

---

## Making It the Default Agent

### Via Config File

Add to your OpenCode config file:

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "default_agent": "BasicallyClaude"
}
```

Config locations:
- **Global**: `~/.config/opencode/opencode.json` or `opencode.jsonc`
- **Project**: `./opencode.json` or `./opencode.jsonc` in project root

### Via Inline Definition

If you don't want to use the markdown file, you can inline the agent in your config:

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "default_agent": "BasicallyClaude",
  "agent": {
    "BasicallyClaude": {
      "description": "Claude-Code-powered OpenCode agent by Aporia",
      "mode": "all",
      "prompt": "You are BasicallyClaude..."
    }
  }
}
```

> Note: The file-based definition at `.opencode/agents/BasicallyClaude.md` is more maintainable and supports the full prompt length.

---

## Verification

After installation, verify the agent is working:

### Check 1: Agent Is Listed

OpenCode should show `BasicallyClaude` in its agent list. You can verify by:

1. Opening OpenCode
2. Running: `List available agents`
3. Confirming `BasicallyClaude` appears

### Check 2: Agent Responds Correctly

Test with these prompts:

```text
/plan add dark mode to this app
```

Expected: A structured plan with phases, files, risks, and validation gates.

```text
/review the current git diff
```

Expected: A code review with severity rankings and specific fix suggestions.

```text
Inspect the repo before fixing the failing tests
```

Expected: File reads and searches before any edit.

```text
/doctor
```

Expected: Environment diagnostic checks.

### Check 3: Source Access

```text
Read claude-code/docs/architecture.md and summarize the core pipeline
```

Expected: A summary referencing the Query Engine, Tool System, Command System, and UI layer — with correct architectural details.

### Check 4: Tool Discipline

```text
Before editing any files, get context first. Then delete the file src/utils/temp.ts
```

Expected: The agent should read/glob first, then ask for confirmation before deleting.

---

## Recommended Models

BasicallyClaude improves workflow on most models. Results vary by model capability.

| Model | Suitability | Notes |
|-------|-------------|-------|
| Anthropic Claude 3.5 Sonnet | ⭐⭐⭐⭐⭐ | Best results — strongest instruction following |
| Anthropic Claude 4 Opus | ⭐⭐⭐⭐⭐ | Excellent — even better reasoning |
| OpenAI GPT-4o | ⭐⭐⭐⭐ | Good — strong but occasionally skips steps |
| DeepSeek V4 Pro | ⭐⭐⭐⭐ | Very good — strong reasoning |
| Gemini 2.5 Pro | ⭐⭐⭐⭐ | Good — needs occasional reminding |
| Gemini 2.0 Flash | ⭐⭐⭐ | Decent — shorter context limits |
| Llama 4 | ⭐⭐⭐ | Good with strong prompting |
| Mistral Large 3 | ⭐⭐⭐ | Solid but needs explicit guidance |
| DeepSeek V3 | ⭐⭐ | Medium — weaker instruction following |
| Small models (<30B) | ⭐⭐ | Will help structure but capability-limited |

---

## Known Limitations

1. **Not Anthropic Claude**: This agent does not contain Anthropic's proprietary model weights. It applies Claude Code's *workflow patterns* to whatever model is running underneath. The output quality depends heavily on the base model.

2. **Context Window**: The agent prompt is detailed (~400 lines). Combined with the cloned source reference, this consumes context. Models with small context windows may truncate behavior.

3. **Tool Dependencies**: Some Claude Code patterns require specific tools (e.g., task management, MCP). If OpenCode doesn't expose these tools, the agent adapts with text-based equivalents.

4. **No Proprietary Code Extraction**: The agent prompt describes the *patterns* from the source — it does not extract and redistribute proprietary code. The full source is available at `claude-code/src/` for reference reading.

5. **Not a Magic Bullet**: BasicallyClaude enforces better workflow, but it cannot make a weak model capable of strong reasoning, or a small model handle large contexts.

6. **Source Code**: The `claude-code/` directory contains the full leaked source (~500K lines). This is included for reference and study. Respect Anthropic's ownership of the original work.

---

## How to Contribute

1. Fork the repository
2. Study `claude-code/docs/` for new patterns to incorporate
3. Update `BasicallyClaude.md` with improved behavioral rules
4. Test with the benchmark protocol
5. Submit a PR

### Contribution Ideas

- Add more detailed mappings from specific `src/tools/` files
- Improve the benchmark rubric with more dimensions
- Add model-specific performance notes
- Add adapter patterns for different OpenCode tool sets
- Create skill definitions for common workflows

---

## License

MIT License — see [LICENSE](LICENSE).

The `claude-code/` subdirectory contains the leaked Anthropic Claude Code source. All original code is the property of [Anthropic](https://www.anthropic.com). This repository does not claim ownership of that code and includes it for reference purposes only, in accordance with the terms described in the original repository at [codeaashu/claude-code](https://github.com/codeaashu/claude-code).

---

## Disclaimer

This repository archives the Claude Code source code leaked from Anthropic's npm registry on 2026-03-31. All original source code is the property of [Anthropic](https://www.anthropic.com). The BasicallyClaude agent definition is a behavioral configuration layer that translates documented patterns from the source into operational rules for OpenCode. It does not contain or redistribute proprietary Anthropic model weights or API internals.
