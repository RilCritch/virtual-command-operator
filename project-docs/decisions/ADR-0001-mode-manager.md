# ADR 0001: Mode Manager and Shell/Chat Modes

## Status
Accepted

## Context
VCO is a terminal-native TUI with two primary workflows: a Shell Mode for command
passthrough and a Chat Mode backed by OpenCode. Shell Mode is the default
experience and must support interactive terminal workflows, while Chat Mode
reuses the same UI scaffold with different input/output behavior and sidebar
content. The application needs a clean way to route input, output rendering, and
navigation between modes without coupling features to a single view.

## Decision
Introduce a Mode Manager that owns the active mode and routes input/output and
sidebar content based on the current mode. Define a simple mode contract that
each mode implements. Shell Mode is the default mode on app start, and Chat Mode
is a secondary mode that can be switched into without losing state.

## Consequences
- Clear separation of concerns between shared UI scaffold and mode-specific
  behavior.
- Input routing and keybindings become mode-aware, enabling different behaviors
  without duplicating UI components.
- Adds an early abstraction layer that must be maintained and documented.

## Alternatives Considered
- Chat-first implementation without a mode abstraction.
- Ad-hoc view switching per screen without a shared mode contract.
- Shell Mode as a separate application rather than a first-class mode.

## Follow-ups
- ADR 0002 to decide PTY and terminal emulator architecture for Shell Mode.
- Define the mode contract in code and document expected responsibilities.
- Update architecture notes to include the Mode Manager.
