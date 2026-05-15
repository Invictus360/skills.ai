---
name: git-workflow-branching
description: When creating, updating, and merging code in a collaborative version control environment.
version: 1.0.0
tags: [dev-tools, git, collaboration]
---

# Git Workflow & Branching

## When to use
- Starting a new feature or bugfix ticket.
- Reviewing PRs and merging code into the mainline.
- Hotfixing production environments.

## What it does
Standardizes branch naming, commit history formatting, and merging strategies to ensure a clean, readable, and revertible git history.

## Workflow
1. **Sync Main**: Fetch and pull the latest changes from the `main` branch.
2. **Branch Off**: Create a new branch using the convention `type/ticket-id-short-description` (e.g., `feat/PROJ-123-add-login`).
3. **Commit Atomically**: Commit code in small, logical chunks. Use Conventional Commits (`feat: ...`, `fix: ...`).
4. **Rebase**: Before opening a PR, rebase your branch against `main` to resolve conflicts locally and maintain a linear history.
5. **Squash & Merge**: Merge the PR into `main` using a squash-merge strategy to keep the mainline history consisting only of complete features.

## Rules
- Never push directly to `main`.
- Commit messages must start with a defined type (feat, fix, docs, chore, refactor, test).
- Feature branches must be deleted after merging.

## Anti-patterns
- **WIP Commits**: Pushing commit messages like "wip", "fixed typo", "trying again" to `main`.
- **Long-lived Feature Branches**: Keeping branches active for weeks without syncing with `main`.

## Output format
A series of atomic git commits culminating in a single Squash-Merged commit on the `main` branch with a descriptive, conventional message.
