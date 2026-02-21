# VCO (Virtual Chat Operator) Implementation Plan

## Overview
This document defines the overarching phased plan for implementing the terminal AI TUI. It is a guide for sequencing work and preventing scope creep. Each phase will later receive its own detailed, granular plan.

## Phase 0 - Project Foundation + Direction
Goals: lock scope, targets, and architecture boundaries.

Deliverables:
- Project charter (vision, scope limits, success criteria)
- Reference list maintained (OpenCode, Textual, opencode-manager, artifact tooling)
- High-level architecture diagram: UI -> core service -> OpenCode backend
- OS target decision: Linux first, macOS next, Windows via WSL

Exit criteria:
- Agreement on data ownership (local DB primary, OpenCode for execution)
- Single-process initial architecture with clean service boundaries documented

## Phase 1 - Core TUI + Backend Connectivity (Single Process)
Goals: prove end-to-end chat UX with OpenCode.

Deliverables:
- Textual shell with chat pane and history list
- OpenCode server lifecycle management (start/stop/health)
- SSE streaming + message flow + rendering

Exit criteria:
- Chat is stable and responsive with streaming
- OpenCode server control works from within the app

## Phase 2 - Input System + Navigation Model
Goals: unlock power-user workflow and input pipeline.

Deliverables:
- Slash command parsing layer (custom command support)
- File reference parsing (OpenCode-style)
- Keyboard system with user-configurable keymaps
- Vim-inspired modal navigation (Normal/Insert/Command) baseline
- Note: VCO stands for Virtual Chat Operator; in keybinding contexts it can also be read as Vim Chat Operator.

Exit criteria:
- Keyboard-first navigation is complete for core views
- Keymaps are user-editable and apply cleanly

## Phase 3 - Persistence + Search Foundation
Goals: local durability and fast search.

Deliverables:
- SQLite schema for conversations, messages, projects, metadata
- FTS5 indexing + search UI
- Project/session list views
- OpenCode session ID stored for cross-linking

Exit criteria:
- Full persistence across runs
- Keyword search is fast and reliable

## Phase 4 - Memory + Agents
Goals: personalization and multi-agent capability.

Deliverables:
- Personal + project memory system
- Agent creation and selection UI
- Local vector store for semantic search

Exit criteria:
- Memory can be created, edited, and retrieved
- Agents influence prompts and tool usage

## Phase 4.5 - Core Service Extraction (Daemonization)
Goals: split UI and core while preserving behavior.

Deliverables:
- Core service extracted into lightweight local daemon
- Internal HTTP + JSON API over localhost
- TUI becomes a pure client of the core service

Exit criteria:
- Feature parity with single-process mode
- Clear service boundaries documented and stable

## Phase 5 - Artifacts + Browser Runtime
Goals: visual outputs and JSX execution.

Deliverables:
- Artifact workspace model (live on disk)
- HTML/Markdown previews
- JSX compilation to static output (Node toolchain)
- Python HTTP server for local previews

Exit criteria:
- Artifacts can be created, previewed, and reopened
- JSX builds render correctly in browser

## Phase 6 - Hardening + Polish
Goals: stability, performance, and packaging.

Deliverables:
- Performance profiling and tuning (batch renders, stream buffering)
- Error handling and recovery paths
- UX polish and theme refinement
- Packaging guidance for Linux/macOS + WSL notes

Exit criteria:
- Stable daily usage and responsive UI
- Ready for external testing or early release

## Cross-Phase Practices
- Performance checks at every phase
- Documentation updated per milestone
- Small acceptance criteria per phase to prevent scope creep
