---
name: finishing-dev-branch
description: Use when development work is complete and ready for merge - requires verification, test passing, and decision on merge vs PR
---

# Finishing a Development Branch

## Overview

Completing a development branch requires verification that work is done, all tests pass, and a decision on how to integrate.

**Core principle:** Verify completely before integrating. Choose integration method based on context.

## When to Use

**After:**
- All tasks in plan completed
- All reviews passed
- Ready to integrate to main

## The Process

### Step 1: Final Verification

```bash
# Run full test suite
pytest  # or npm test, cargo test, etc.

# Verify linter clean
ruff check .  # or eslint, clippy, etc.

# Verify build passes
python -m build  # or npm run build, cargo build, etc.
```

**All must pass. No exceptions.**

### Step 2: Review Changes

```bash
# See what changed
git log main..HEAD --oneline

# Review diff
git diff main...HEAD

# Check for:
# - Debug code left behind
# - TODO comments unaddressed
# - Commented-out code
# - Large binary files accidentally added
```

### Step 3: Clean Up Commits (Optional)

If commits are messy:

```bash
# Interactive rebase to clean up
git rebase -i main

# Squash trivial commits
# Reword unclear messages
# Reorder if needed
```

**Don't rewrite if already pushed and others have pulled.**

### Step 4: Choose Integration Method

| Method | When to Use |
|--------|-------------|
| **Direct merge** | Solo work, small changes, no review needed |
| **Pull Request** | Team review needed, CI required, documentation |
| **Squash merge** | Many small commits to combine |

### Step 5A: Direct Merge

```bash
# Switch to main
git checkout main
git pull origin main

# Merge feature branch
git merge feature/my-feature

# Push
git push origin main
```

### Step 5B: Create Pull Request

```bash
# Push branch
git push -u origin feature/my-feature

# Create PR (using gh CLI)
gh pr create --title "feat: description" --body "Details..."

# Or via web interface
```

**Use requesting-code-review skill for PR description.**

### Step 6: Clean Up

After merge:

```bash
# Delete local branch
git branch -d feature/my-feature

# Delete remote branch
git push origin --delete feature/my-feature

# If using worktree
git worktree remove ../project-feature-name
```

## Integration Decision Flowchart

```
Is review required?
       │
       ▼
   ┌───┴───┐
   │       │
  Yes      No
   │       │
   ▼       ▼
  PR    Direct merge
```

## Verification Checklist

Before ANY integration:

- [ ] All tests pass
- [ ] Linter clean
- [ ] Build passes
- [ ] No debug code
- [ ] Self-reviewed diff
- [ ] Commits are clean/meaningful
- [ ] Documentation updated if needed

## Red Flags - STOP

- Merging with failing tests
- "Tests pass locally" (run them again)
- Skipping verification "just this time"
- Large diff not reviewed
- Unclear commit messages
- Leftover debug code

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "Tests passed earlier" | Run again before merge |
| "It's a small change" | Small changes break things too |
| "I'll clean up later" | Clean up now |
| "CI will catch it" | Don't rely on CI as only gate |

## Related Skills

- **verification-before-completion** - Final verification before claiming done
- **requesting-code-review** - How to create good PR
- **using-git-worktrees** - Clean up worktree after finish
