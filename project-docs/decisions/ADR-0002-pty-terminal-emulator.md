# ADR 0002: PTY and Terminal Emulator for Shell Mode

## Status
Accepted

## Context
Shell Mode is the default experience and must render terminal output with native
fidelity, including colors, cursor movement, screen clears, and interactive TUI
applications (fzf, vim, htop, less) inside the output pane. Pipe-based output
does not reliably trigger terminal behavior in many tools, and suspending to the
real terminal would prevent output from appearing inside VCO.

## Decision
Use PTY-backed subprocesses for Shell Mode output. Render output in an embedded
terminal surface within the output pane (ANSI parsing + screen buffer). Route
interactive key events to the PTY while a process is active. Treat embedded
interactive TUI support as a core requirement, with a staged milestone of
"PTY output first" followed by "interactive input routing."

## Consequences
- Higher implementation complexity early, including terminal emulation and
  input routing behavior.
- Best-possible fidelity for terminal output and interactive applications.
- Requires resize handling and explicit control for signals (e.g., Ctrl+C).

## Alternatives Considered
- Pipe-based subprocess I/O with raw output rendering.
- Forcing color output via environment flags and tool-specific options.
- Suspending VCO to run interactive tools in the real terminal.

## Open Decisions
- Persistent shell PTY vs per-command PTY session model.
- Scrollback, selection, and clipboard behavior in the terminal pane.
- Resize behavior and buffer limits for interactive sessions.

## Follow-ups
- Define Shell Mode input routing for interactive sessions.
- Plan terminal emulation implementation (kept tool-agnostic for now).
