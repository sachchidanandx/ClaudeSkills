# Codebase Explorer Agent

A Socratic codebase exploration mentor that guides interactive learning of unfamiliar codebases through questioning and incremental discovery.

## What It Does

Instead of dumping documentation or explanations, this agent teaches you to navigate and understand codebases yourself through:

1. **Environment Sensing** — Scans dependencies and structure, gives you a concise overview, and offers exploration paths
2. **Socratic Learning** — Asks what YOU think before explaining, validates your mental model, corrects incrementally
3. **Language-Specific Guidance** — Adapts mentoring to Go, Python, or JavaScript/TypeScript idioms and patterns

## Features

- Multi-language support (Go, Python, JavaScript/TypeScript)
- Persistent memory — remembers your expertise level and what you've explored across sessions
- First-run setup — asks whether to store memory at user level or project level
- No info dumps — keeps responses short, uses questions liberally
- Grounded in actual code — every statement is verifiable against the codebase

## Requirements

- Claude Code with agent support
- Opus model access (configured via `model: opus` in frontmatter)

## Installation

### Via Marketplace (Recommended)

```bash
# Add the ClaudeSkills marketplace
/plugin marketplace add sachchidanandx/ClaudeSkills

# Install the plugin
/plugin install codebase-explorer@sachchidanandx-skills
```

### Manual

```bash
cp agents/codebase-explorer.md ~/.claude/agents/
```

On first use, the agent will ask where to store its memory (user-level or project-level).

## Usage

Invoke the agent through Claude Code's agent selection. Example prompts:

- "I just joined a new team and need to understand this Go microservice codebase"
- "How does the authentication flow work in this project?"
- "I want to understand the architecture and design patterns used here"
- "Help me learn how this service handles dependency injection"

## How It Works

The agent follows three phases:

**Phase 1 — Environment Sensing:** Reads dependency files (`go.mod`, `package.json`, etc.), provides a brief overview, and suggests 3-4 exploration paths.

**Phase 2 — Socratic Loop:** For each concept, it probes your understanding first, validates against the code, and corrects incrementally. One concept at a time, always conversational.

**Phase 3 — Language Lenses:** Applies language-specific patterns (Go interfaces, Python decorators, TS generics) to deepen understanding.

## Customization

Edit the agent file to:
- Add or modify language-specific lenses (e.g., Rust, Java)
- Adjust guardrails (e.g., allow documentation generation)
- Change the model (e.g., `model: sonnet` for faster responses)
- Modify the memory types or what gets recorded
