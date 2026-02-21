---
description: Commit and push changes
---
Commit and push all current changes in this repo. Follow these steps exactly:

1) Show git status and staged/unstaged diff.
2) Summarize changes.
3) Refuse to commit if any secret-like files exist (e.g., .env, credentials.json, *.key, *.pem).
4) Ensure there are changes to commit; if clean, stop.
5) Stage all changes.
6) Create a commit message.
   - If "$ARGUMENTS" is provided, use it verbatim.
   - If "$ARGUMENTS" is empty, generate a lightweight Conventional Commit message.
     - Infer type from files and changes:
       - docs: README/docs changes
       - chore: config/workflow changes
       - feat/fix/refactor/test as appropriate
     - Keep summary under 72 chars.
     - Print the proposed message before committing.
   - Format: type: short summary
   - Types: feat, fix, docs, chore, refactor, test
7) Push the current branch only.
   - If upstream is missing, use: git push -u origin HEAD
8) Show final git status.

Notes:
- If HEAD is detached, stop and report.
- No tests are configured yet. When they exist, run them before commit.

Context:
- Current status: !`git status -sb`
- Diff: !`git diff`
- Staged diff: !`git diff --staged`
