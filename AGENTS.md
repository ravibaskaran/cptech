# Project Instructions

## Repository Identity

Use this canonical project path for local context and memory routing:

`D:\onedrive\Onedrive - Justo\OneDrive - JUSTO REALFINTECH PRIVATE LIMITED\dev\cptech`

## Persistence Requirement

At the end of every Codex/OpenCode run for this project:

1. Check `git status --short`.
2. Commit all project-relevant changes, including `.planning/` context files and generated BRD/planning documents.
3. Push the current branch to `origin` so work can continue from another machine.
4. If push fails, report the exact failure and leave the commit local.

This should be treated as an automatic project operating rule; the user should not need to ask for it each run.

## Local Git Hook

This repo includes `.githooks/post-commit`, which attempts to push the current branch to `origin` after each successful commit. If this repo is cloned on another machine, run:

```powershell
git config core.hooksPath .githooks
```

The hook is best-effort and exits successfully even if the push fails, so it does not corrupt local commits when offline or unauthenticated.
