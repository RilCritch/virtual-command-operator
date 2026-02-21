# Agent Guide (TUI Chat)

This file is for agentic coding assistants working in this repo.
It summarizes how to build, test, and follow code style.

## Status of the codebase
- No application source code exists yet.
- No build/lint/test tooling is configured yet.
- Use this doc as a baseline and update it as tooling lands.

## Rules files
- No Cursor rules found (.cursor/rules/ or .cursorrules).
- No Copilot rules found (.github/copilot-instructions.md).

## Build, lint, and test commands
There are currently no build/lint/test commands defined.

When tooling is added, update this section with exact commands.
Include a single-test example and a single-file lint example.

Placeholders for future commands:
- Build: TBD
- Lint: TBD
- Format: TBD
- Test (all): TBD
- Test (single): TBD

## Repository orientation
- Planning and architecture docs live in project-docs/.
- Implementation plan: project-docs/plans/tui-chat-implementation-plan.md
- Task list: TASKS.md

## Intended tech stack (from project docs)
- Language: Python
- TUI framework: Textual
- Storage: SQLite + FTS5
- Search: local vector store (later phase)
- Artifacts: local filesystem + Python HTTP server (later phase)

## Coding conventions (baseline)
These are baseline guidelines until code style tooling is defined.

### Python version
- Use a modern Python version (3.11+ preferred).
- Avoid version-specific features unless documented.

### Imports
- Order: standard library, third-party, local.
- Use one import per line when importing many names.
- Avoid unused imports; keep imports minimal and explicit.

### Formatting
- Keep lines readable; prefer 88-100 char max length.
- Use consistent indentation (4 spaces).
- Use trailing commas where it improves diffs.
- If a formatter is added (Black/Ruff), follow it exactly.

### Naming
- Modules: snake_case
- Classes: PascalCase
- Functions and variables: snake_case
- Constants: UPPER_CASE
- Avoid single-letter names except trivial loops.

### Types
- Use type hints for public functions and class methods.
- Prefer builtin generics (list[str], dict[str, int]).
- Keep typing simple; avoid overly complex typing constructs.

### Error handling
- Fail fast with clear error messages.
- Wrap external I/O with explicit error handling.
- Prefer returning errors to the UI layer with context.
- Do not swallow exceptions silently.

### Logging
- Keep logs structured and minimal.
- Avoid logging secrets or API keys.
- When in doubt, log at debug level.

### Async and concurrency
- Keep the UI responsive; run blocking work off the UI thread.
- Use async tasks for network calls and streaming.
- Batch UI updates to avoid excessive redraws.

### Textual guidelines
- Keep view composition modular.
- Separate state management from rendering where possible.
- Prefer reactive state for UI updates.
- Avoid heavy work in render methods.

### Persistence and search
- Use SQLite as the source of truth for messages and metadata.
- Keep schema changes explicit and documented.
- Use FTS5 for keyword search; keep indices updated.

### Artifacts (later phase)
- Treat artifact outputs as live workspaces on disk.
- Keep generated files isolated per artifact.
- Serve artifacts with a local Python HTTP server.

## Updating this file
When new tooling is added, update the following:
- Exact build/lint/test commands
- Single test invocation examples
- Formatter and linter rules
- Python version constraints

## When in doubt
- Follow the implementation plan in project-docs/plans/.
- Keep tasks lightweight in TASKS.md.
- Document significant decisions as ADRs.
