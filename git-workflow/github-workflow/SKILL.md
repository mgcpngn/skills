---
name: github-workflow
description: Use when interacting with GitHub - creating repositories, pushing code, managing PRs, issues, and releases. Complete end-to-end GitHub workflow using gh CLI.
---

# GitHub Workflow

## Overview

Complete end-to-end GitHub interaction using GitHub CLI (`gh`).

**Core principle:** Use `gh` CLI for all GitHub operations - faster than web UI, scriptable, and consistent.

## Prerequisites

### Install GitHub CLI

```bash
# Windows (winget)
winget install --id GitHub.cli

# Windows (scoop)
scoop install gh

# macOS
brew install gh

# Linux (Debian/Ubuntu)
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update && sudo apt install gh
```

### Authenticate

```bash
# Interactive login (opens browser)
gh auth login

# With token from stdin
echo $TOKEN | gh auth login --with-token

# Check status
gh auth status
```

## Complete Workflow: New Project to GitHub

### Step 1: Initialize Local Repository

```bash
cd /path/to/your/project

# Initialize git if not already
git init

# Add all files
git add -A

# Initial commit
git commit -m "feat: initial commit"
```

### Step 2: Create GitHub Repository and Push

```bash
# Create public repo from current directory and push
gh repo create my-project --public --source=. --push

# Or: Create private repo
gh repo create my-project --private --source=. --push

# Or: Create in organization
gh repo create my-org/my-project --public --source=. --push
```

**Options:**
| Flag | Description |
|------|-------------|
| `--public` | Public repository |
| `--private` | Private repository |
| `--source=.` | Use current directory |
| `--push` | Push commits after creating |
| `--description "..."` | Add description |
| `--license mit` | Add license |
| `--add-readme` | Add README |

### Step 3: Verify

```bash
# View repo in browser
gh repo view --web

# Check remote
git remote -v
```

## Common Operations

### Repository Management

```bash
# Create empty repo
gh repo create my-project --public

# Create from current directory
gh repo create --source=. --public --push

# Clone existing repo
gh repo clone owner/repo

# Fork a repo
gh repo fork owner/repo --clone

# View repo info
gh repo view owner/repo

# List your repos
gh repo list

# Delete repo (careful!)
gh repo delete owner/repo --yes
```

### Branches

```bash
# Create branch
git checkout -b feature/my-feature

# Push new branch
git push -u origin feature/my-feature

# List remote branches
git branch -r
```

### Pull Requests

```bash
# Create PR (interactive)
gh pr create

# Create PR with title and body
gh pr create --title "feat: add feature" --body "Description"

# Create PR and fill from commit messages
gh pr create --fill

# List PRs
gh pr list

# View PR
gh pr view 123

# Checkout PR locally
gh pr checkout 123

# Merge PR
gh pr merge 123 --merge
gh pr merge 123 --squash
gh pr merge 123 --rebase

# Close PR
gh pr close 123
```

### Issues

```bash
# Create issue
gh issue create --title "Bug: something broken" --body "Details"

# List issues
gh issue list

# View issue
gh issue view 123

# Close issue
gh issue close 123

# Reopen issue
gh issue reopen 123

# Add labels
gh issue edit 123 --add-label "bug,priority:high"
```

### Releases

```bash
# Create release
gh release create v1.0.0 --title "Version 1.0.0" --notes "Release notes"

# Create release with auto-generated notes
gh release create v1.0.0 --generate-notes

# Upload assets to release
gh release upload v1.0.0 ./dist/app.zip

# List releases
gh release list

# Download release assets
gh release download v1.0.0
```

### Workflow / Actions

```bash
# List workflow runs
gh run list

# View run details
gh run view 123456

# Watch run in progress
gh run watch 123456

# Re-run failed jobs
gh run rerun 123456 --failed

# Trigger workflow
gh workflow run workflow.yml
```

## Quick Reference

### One-liner: New Project to GitHub

```bash
git init && git add -A && git commit -m "feat: initial commit" && gh repo create my-project --public --source=. --push
```

### One-liner: Feature Branch to PR

```bash
git checkout -b feature/my-feature && git add -A && git commit -m "feat: add feature" && git push -u origin feature/my-feature && gh pr create --fill
```

### Command Cheat Sheet

| Task | Command |
|------|---------|
| Login | `gh auth login` |
| Create repo | `gh repo create name --public --source=. --push` |
| Create PR | `gh pr create --fill` |
| Merge PR | `gh pr merge 123 --squash` |
| Create issue | `gh issue create --title "..." --body "..."` |
| Create release | `gh release create v1.0.0 --generate-notes` |
| View in browser | `gh repo view --web` |
| Clone repo | `gh repo clone owner/repo` |

## Troubleshooting

| Issue | Solution |
|-------|----------|
| `gh: command not found` | Install GitHub CLI |
| `not logged in` | Run `gh auth login` |
| `permission denied` | Check repo access, re-login |
| `remote already exists` | Use `git remote set-url origin <url>` |
| `push rejected` | Pull first or force push (careful) |

## Best Practices

1. **Always verify before push**: `git status`, `git diff`
2. **Use meaningful commit messages**: Follow conventional commits
3. **Create PR for review**: Don't push directly to main
4. **Tag releases**: Use semantic versioning
5. **Use `--source=.`**: When creating from existing local repo

## Related Skills

- **git-workflow** - Git operations and worktrees
- **finishing-dev-branch** - Complete development workflow
- **requesting-code-review** - PR best practices
