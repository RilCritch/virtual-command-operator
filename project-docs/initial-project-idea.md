# Project Idea Review: Terminal AI TUI

## Overview
Build a terminal-native AI chat interface inspired by ChatGPT/Claude and OpenCode TUI. The app runs in the terminal with strong aesthetics, efficient keyboard navigation, and deep integration with the OpenCode server. It supports chat history, projects, personal memory, search, custom agents, and a future artifact/canvas system that runs in the default browser.

## Core Goals
- Terminal-first experience with rich TUI styling
- Chat history with sessions and projects
- Personal and project memory
- Search across messages and artifacts
- Custom agents (GPT-like profiles)
- Artifacts/canvas system that can render in the browser
- OpenCode server as the AI backend

## Chosen Technology
- TUI: Textual (Python)
- Storage: SQLite + FTS5
- Semantic search: local vector store (plugin for remote later)
- Artifacts: local filesystem + metadata
- Artifact serving: Python HTTP server

## Architectural Summary
- UI Layer: Textual app with chat, history, memory, search, projects, artifacts, and agent builder views
- Input Layer: slash commands, file references, keybindings, Vim-style modes
- Backend Client: OpenCode server client (OpenAPI + SSE)
- Storage Layer: SQLite tables + FTS5 index + vector index
- Artifact Runtime: static artifact serving with optional future dev server support

## Staged Development Plan

### Stage 1 - Core TUI + Backend Connectivity
- Textual UI (chat + history)
- OpenCode server start/stop
- OpenCode message flow + streaming

### Stage 2 - Input System + Navigation
- Slash commands
- File references
- Basic keyboard shortcuts and customizable keymaps

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
- Vim-inspired modal navigation (not full editor)
- Customizable keybindings per user
- Fast, snappy performance (async streaming, batched renders)
- File references (OpenCode-style)
- Slash commands (with custom command support)

## Performance Considerations
- Async networking and SSE streaming
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
- JSX build pipeline orchestration (Vite vs esbuild)
