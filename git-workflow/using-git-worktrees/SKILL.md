---
name: using-git-worktrees
description: Use when starting new feature development or need parallel development branches - creates isolated workspace for each feature
---

# Using Git Worktrees

## Overview

Git worktrees let you have multiple branches checked out simultaneously in different directories. Each feature gets its own isolated workspace.

**Core principle:** Isolated workspaces prevent context pollution and enable parallel work.

## When to Use

**Use when:**
- Starting new feature development
- Need to work on multiple features simultaneously
- Want clean separation between work items
- Following brainstorming/writing-plans workflow

**Don't use when:**
- Quick one-file fix
- No need for parallel branches
- Simple linear development

## The Pattern

### Create Worktree for New Feature

```bash
# From main repo directory
git worktree add ../project-feature-name feature/feature-name

# Or create new branch at same time
git worktree add -b feature/feature-name ../project-feature-name
```

**Structure:**
```
/projects/
├── my-project/              # Main repo (main branch)
└── my-project-feature-name/ # Worktree (feature branch)
```

### Work in Worktree

```bash
cd ../project-feature-name

# Normal git operations work
git add .
git commit -m "feat: add feature"
git push -u origin feature/feature-name
```

### List Worktrees

```bash
git worktree list
# /projects/my-project              abc123 [main]
# /projects/my-project-feature-name def456 [feature/feature-name]
```

### Remove Worktree When Done

```bash
# After merge
git worktree remove ../project-feature-name

# Force remove if needed
git worktree remove --force ../project-feature-name

# Prune stale worktree references
git worktree prune
```

## Naming Convention

```
<project-name>-<feature-short-name>
```

Examples:
- `myapp-auth-refactor`
- `myapp-api-v2`
- `myapp-bug-123`

## Workflow Integration

### With Brainstorming

1. Brainstorming produces design
2. Create worktree for implementation
3. Writing-plans creates plan in worktree
4. Execute plan in worktree
5. Merge and remove worktree

### Multiple Features

```
/projects/
├── webapp/                    # main
├── webapp-feature-a/          # feature/feature-a (in progress)
├── webapp-feature-b/          # feature/feature-b (in progress)
└── webapp-hotfix/             # hotfix/urgent-fix
```

Switch between features by changing directories. No stashing needed.

## Common Issues

| Issue | Solution |
|-------|----------|
| Can't checkout same branch twice | Worktrees must have unique branches |
| Changes in wrong directory | Always verify which worktree you're in |
| Forgot to push | Push from worktree before removing |
| Branch conflicts | Resolve in worktree, then remove |

## Red Flags - STOP

- Creating worktree without clear feature scope
- Multiple worktrees for same feature
- Not removing worktrees after merge
- Working in main repo instead of worktree

## Quick Reference

| Command | Purpose |
|---------|---------|
| `git worktree add <path> <branch>` | Create worktree for existing branch |
| `git worktree add -b <branch> <path>` | Create worktree with new branch |
| `git worktree list` | List all worktrees |
| `git worktree remove <path>` | Remove worktree |
| `git worktree prune` | Clean up stale references |

## Related Skills

- **brainstorming** - Creates design, then creates worktree
- **writing-plans** - Creates plan in worktree
- **finishing-dev-branch** - Completes work in worktree
