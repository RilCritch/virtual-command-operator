# VCO (Virtual Command Operator) Implementation Plan

## Overview
This document defines the overarching phased plan for implementing the terminal TUI with Shell and Chat modes. It is a guide for sequencing work and preventing scope creep. Each phase will later receive its own detailed, granular plan.

## Phase 0 - Project Foundation + Direction
Goals: lock scope, targets, and architecture boundaries.

Deliverables:
- Project charter (vision, scope limits, success criteria)
- Reference list maintained (OpenCode, Textual, opencode-manager, artifact tooling)
- High-level architecture diagram: UI -> mode manager -> backend handlers (Shell, Chat)
- Mode contract definition and switching strategy
- ADR-0001 and ADR-0002 recorded
- OS target decision: Linux first, macOS next, Windows via WSL

Exit criteria:
- Agreement on data ownership (local DB primary, OpenCode for execution)
- Single-process initial architecture with clean service boundaries documented
- Mode contract defined and accepted (Shell + Chat)
## Phase 1a - Core TUI + Shell Output Baseline (Single Process)
Goals: prove the shared UI scaffold with non-interactive shell output.

Deliverables:
- Textual app scaffold with header, sidebar, output pane, input bar
- Mode manager with Shell Mode wired in
- Shell command runner (PTY-backed subprocess) with streaming output
- Terminal emulator output pane (ANSI parsing + screen buffer)
- CWD tracking and display
- Sidebar file explorer (DirectoryTree) with vim-inspired navigation
- Minimal shell history (up/down)
- Mode switch stub to Chat Mode

Exit criteria:
- Commands execute and stream without blocking the UI
- ANSI colors and cursor movement render correctly
- Sidebar navigation works and reflects CWD
- Mode switching is stable (Chat Mode can be a stub)

## Phase 1b - Interactive PTY + Input Routing
Goals: enable full-screen and interactive terminal apps.

Deliverables:
- Interactive TUI support inside output pane
- Input routing to PTY during interactive sessions
- Resize handling and signal forwarding (Ctrl+C, Ctrl+Z)

Exit criteria:
- Interactive TUIs render and accept input in the output pane
- Resizes and signals are handled correctly

## Phase 2 - Chat Mode + OpenCode + Minimal Persistence
Goals: integrate OpenCode using the shared UI scaffold with durable chat history. Chat Mode is the AI chat interface alongside the default Shell Mode.

Deliverables:
- Chat Mode implementation using the mode contract
- OpenCode server lifecycle management (start/stop/health)
- SSE streaming + message flow + rendering
- Minimal persistence for sessions and messages (SQLite)
- History list view in sidebar for Chat Mode

Exit criteria:
- Chat is stable and responsive with streaming
- OpenCode server control works from within the app
- Chat history persists across runs
- Switching between Shell and Chat modes preserves per-mode state

## Phase 3 - Vim-Modal Keymaps + Input System
Goals: establish keyboard-first navigation and input pipeline.

Deliverables:
- Keyboard system with user-configurable keymaps
- Vim-inspired modal navigation (Normal/Insert/Command) baseline
- Mode-specific keybinding overlays
- Slash command parsing layer (custom command support)
- File reference parsing (OpenCode-style)
- Note: VCO stands for Virtual Command Operator; in keybinding contexts it can also be read as Vim Command Operator.

Exit criteria:
- Keyboard-first navigation is complete for core views
- Keymaps are user-editable and apply cleanly in both modes

## Phase 4 - Search Foundation
Goals: fast keyword search on persisted data.

Deliverables:
- FTS5 indexing + search UI
- Project/session list views
- OpenCode session ID stored for cross-linking

Exit criteria:
- Keyword search is fast and reliable

## Phase 5 - Memory + Agents
Goals: personalization and multi-agent capability.

Deliverables:
- Personal + project memory system
- Agent creation and selection UI
- Local vector store for semantic search

Exit criteria:
- Memory can be created, edited, and retrieved
- Agents influence prompts and tool usage

## Phase 5.5 - Core Service Extraction (Daemonization)
Goals: split UI and core while preserving behavior.

Deliverables:
- Core service extracted into lightweight local daemon
- Internal HTTP + JSON API over localhost
- TUI becomes a pure client of the core service

Exit criteria:
- Feature parity with single-process mode
- Clear service boundaries documented and stable

## Phase 6 - Artifacts + Static Previews
Goals: visual outputs and durable artifact workspaces.

Deliverables:
- Artifact workspace model (live on disk)
- HTML/Markdown previews
- Python HTTP server for local previews

Exit criteria:
- Artifacts can be created, previewed, and reopened

## Phase 7 - Hardening + Polish
Goals: stability, performance, and packaging.

Deliverables:
- Performance profiling and tuning (batch renders, stream buffering)
- Error handling and recovery paths
- UX polish and theme refinement
- Packaging guidance for Linux/macOS + WSL notes

Exit criteria:
- Stable daily usage and responsive UI
- Ready for external testing or early release

## Phase 8 - JSX Runtime (Feature Upgrade)
Goals: JSX execution after stable daily usage.

Deliverables:
- JSX compilation to static output (Node toolchain)
- Runtime preview support in browser

Exit criteria:
- JSX builds render correctly in browser

## Cross-Phase Practices
- Performance checks at every phase
- Documentation updated per milestone
- Small acceptance criteria per phase to prevent scope creep
