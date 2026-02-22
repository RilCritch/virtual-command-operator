# Project Idea Review: VCO (Virtual Command Operator)

## Overview
Build a terminal-native TUI with Shell Mode as the default for command passthrough and interactive terminal workflows. Chat Mode, backed by the OpenCode server, is a secondary mode for AI conversations. The app runs in the terminal with strong aesthetics, efficient keyboard navigation, and shared UI scaffolding across modes. It supports native terminal output rendering, chat history, projects, personal memory, search, custom agents, and a future artifact/canvas system that runs in the default browser.

## Core Goals
- Shell Mode as the default workflow for command passthrough
- Native terminal output rendering with PTY-backed emulation
- Interactive TUI support inside the output pane (fzf, vim, htop, less)
- File explorer sidebar with vim-inspired navigation
- Mode switching between Shell and Chat
- Terminal-first experience with rich TUI styling
- Chat history with sessions and projects
- Personal and project memory
- Search across messages and artifacts
- Custom agents (GPT-like profiles)
- Artifacts/canvas system that can render in the browser
- OpenCode server as the AI backend

## Chosen Technology
- TUI: Textual (Python)
- Terminal emulation: PTY-backed subprocess + ANSI rendering in output pane
- Storage: SQLite + FTS5
- Semantic search: local vector store (plugin for remote later)
- Artifacts: local filesystem + metadata
- Artifact serving: Python HTTP server

## Architectural Summary
- UI Layer: Textual app with terminal emulator output pane, chat views, history, memory, search, projects, artifacts, and agent builder views
- Mode Manager: routes input/output and sidebar content per mode (Shell, Chat)
- Input Layer: slash commands, file references, keybindings, Vim-style modes, and mode routing
- Shell Backend: PTY subprocess runner + terminal emulator rendering
- Chat Backend: OpenCode server client (OpenAPI + SSE)
- Storage Layer: SQLite tables + FTS5 index + vector index
- Artifact Runtime: static artifact serving with optional future dev server support

## Staged Development Plan

### Stage 1 - Core TUI + Shell Mode
- Textual UI scaffold (header, sidebar, output pane, input bar)
- Shell command runner using PTY
- Terminal emulator output pane (ANSI parsing + screen buffer)
- Stage milestone: PTY output rendering first, then interactive input routing
- Interactive TUI support inside output pane (fzf, vim, htop, less)
- Directory tree sidebar with vim-inspired navigation
- Mode switching stub to Chat Mode

### Stage 2 - Chat Mode + OpenCode Integration
- OpenCode server start/stop
- OpenCode message flow + streaming
- Chat history list in sidebar
- Shared input pipeline across modes

### Stage 3 - Structure + Persistence
- Projects/sessions view
- SQLite persistence
- Search (FTS5)

### Stage 4 - Memory + Agents
- Personal + project memory store
- Agent creation/registry
- Semantic search with vector store

### Stage 5 - Artifacts (Later)
- HTML/Markdown previews
- JSX compilation to static output
- Python HTTP server for artifacts
- Future dev server support

## Key UX Requirements
- Shell Mode is the default experience
- Interactive TUI support inside the output pane
- Native ANSI color rendering via PTY
- Command history and editable input
- CWD indicator and directory tree navigation
- Vim-inspired modal navigation (not full editor)
- Note: VCO stands for Virtual Command Operator; in keybinding contexts it can also be read as Vim Command Operator.
- Customizable keybindings per user
- Fast, snappy performance (async streaming, batched renders)
- File references (OpenCode-style)
- Slash commands (with custom command support)

## Performance Considerations
- Async networking and SSE streaming
- PTY stream handling without blocking the UI
- Terminal emulator redraw throttling
- Scrollback buffer limits for output pane
- Batch UI updates to reduce redraws
- Lazy rendering for long histories
- Background search indexing

## Artifact Strategy
- Start with static artifact output
- Support JSX compilation (Node toolchain) and HTML/MD previews
- Serve artifacts locally in browser
- Treat artifacts as live workspaces on disk

## Risks and Mitigations
- Scope creep: enforce staged rollout
- Terminal emulator complexity: start with MVP support and expand
- Interactive TUI edge cases: provide fallbacks or limits as needed
- Performance: benchmark early, optimize UI rendering
- Artifact complexity: defer to later stage

## Reference Projects and Documentation

### OpenCode
- Server API and OpenAPI spec: https://opencode.ai/docs/server/
- TUI behaviors and commands: https://opencode.ai/docs/tui/

### OpenCode Integration Reference
- opencode-manager server lifecycle: https://deepwiki.com/chriswritescode-dev/opencode-manager/6.3-opencode-server-integration

### Textual
- Custom keymaps (supports Vim-style overrides): https://darren.codes/posts/textual-keymaps/
- Actions: https://textual.textualize.io/guide/actions
- Input handling: https://textual.textualize.io/guide/input/
- Command palette: https://textual.textualize.io/guide/command_palette/

### Artifact Build Tooling
- Vite React overview: https://software.land/vite-react/
- Vite SWC plugin: https://www.npmjs.com/package/@vitejs/plugin-react-swc

## Open Questions
- Final Vim-style mode set and default mappings
- Exact keybinding override strategy (per-mode vs per-view)
- Persistent shell PTY vs per-command PTY session model
- Terminal emulator approach (Textual widget vs custom)
- Scrollback, selection, and clipboard behavior in terminal pane
- Resize behavior for interactive sessions
- JSX build pipeline orchestration (Vite vs esbuild)
