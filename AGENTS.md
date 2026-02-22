# Agent Guide (VCO)

This file is for agentic coding assistants working in VCO (Virtual Command Operator).
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
- Lint (all): TBD
- Lint (single file): TBD (example format: <lint-tool> path/to/file.py)
- Format: TBD
- Test (all): TBD
- Test (single): TBD (example format: <test-runner> path/to/test_file.py::test_name)

Notes:
- Prefer running the narrowest command that proves the change.
- Do not introduce new tooling without updating this section.

## Repository orientation
- Planning and architecture docs live in project-docs/.
- Implementation plan: project-docs/plans/vco-implementation-plan.md
- Task list: TASKS.md
- Custom OpenCode commands live in .opencode/commands/.

## Intended tech stack (from project docs)
- Language: Python
- TUI framework: Textual
- Storage: SQLite + FTS5
- Search: local vector store (later phase)
- Artifacts: local filesystem + Python HTTP server (later phase)

## Workflow expectations
- Linux-first development; macOS follow-on; Windows via WSL.
- Single-process architecture initially; core service daemon later.
- OpenCode is the execution backend; local DB is the source of truth.

## Coding conventions (baseline)
These are baseline guidelines until code style tooling is defined.

### Python version
- Use a modern Python version (3.11+ preferred).
- Avoid version-specific features unless documented.

### Imports
- Order: standard library, third-party, local.
- Use one import per line when importing many names.
- Avoid unused imports; keep imports minimal and explicit.
- Prefer absolute imports within the project.

### Formatting
- Keep lines readable; prefer 88-100 char max length.
- Use consistent indentation (4 spaces).
- Use trailing commas where it improves diffs.
- If a formatter is added (Black/Ruff), follow it exactly.
- Keep docstrings concise and focused on behavior.

### Naming
- Modules: snake_case
- Classes: PascalCase
- Functions and variables: snake_case
- Constants: UPPER_CASE
- Avoid single-letter names except trivial loops.
- Prefer explicit names over abbreviations.

### Types
- Use type hints for public functions and class methods.
- Prefer builtin generics (list[str], dict[str, int]).
- Keep typing simple; avoid overly complex typing constructs.
- Prefer Protocols or simple interfaces over deep inheritance.

### Error handling
- Fail fast with clear error messages.
- Wrap external I/O with explicit error handling.
- Prefer returning errors to the UI layer with context.
- Do not swallow exceptions silently.
- Use custom exceptions for domain-specific failures.

### Logging
- Keep logs structured and minimal.
- Avoid logging secrets or API keys.
- When in doubt, log at debug level.
- Use consistent logger names per module.

### Async and concurrency
- Keep the UI responsive; run blocking work off the UI thread.
- Use async tasks for network calls and streaming.
- Batch UI updates to avoid excessive redraws.
- Use backpressure or throttling for high-frequency streams.

### Textual guidelines
- Keep view composition modular.
- Separate state management from rendering where possible.
- Prefer reactive state for UI updates.
- Avoid heavy work in render methods.
- Co-locate widgets with their state/controller logic.

### Persistence and search
- Use SQLite as the source of truth for messages and metadata.
- Keep schema changes explicit and documented.
- Use FTS5 for keyword search; keep indices updated.
- Avoid ad-hoc SQL strings; centralize queries where possible.

### Artifacts (later phase)
- Treat artifact outputs as live workspaces on disk.
- Keep generated files isolated per artifact.
- Serve artifacts with a local Python HTTP server.
- Favor static builds for initial React/JSX support.

## Git hygiene
- Use lightweight Conventional Commits: type: short summary.
- Types: feat, fix, docs, chore, refactor, test.
- Keep commits focused and small when possible.
- Do not commit secrets or local credentials.

## Security and secrets
- Never commit .env files or API keys.
- Review new files for credentials before committing.
- Keep tokens in local env or secure storage.

## Documentation expectations
- Keep project-docs/README.md updated when structure changes.
- Record significant decisions as ADRs in project-docs/decisions/.
- Update TASKS.md with lightweight Now/Next/Later items.
- Use VCO (Virtual Command Operator) on first mention, then VCO.

## Updating this file
When new tooling is added, update the following:
- Exact build/lint/test commands
- Single test invocation examples
- Formatter and linter rules
- Python version constraints
- Any new language/runtime requirements

## When in doubt
- Follow the implementation plan in project-docs/plans/.
- Keep tasks lightweight in TASKS.md.
- Document significant decisions as ADRs.
