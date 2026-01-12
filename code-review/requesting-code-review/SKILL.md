---
name: requesting-code-review
description: Use when preparing code for review or creating PR - requires pre-review checklist completion and clear review request structure
---

# Requesting Code Review

## Overview

Good review requests get better feedback faster. Poor requests waste reviewer time and miss issues.

**Core principle:** Prepare reviewable changes with clear context and self-review first.

## When to Use

**Before:**
- Creating a pull request
- Asking for code review
- Handing off work to others

## Pre-Review Checklist

**Complete ALL before requesting review:**

- [ ] All tests pass (Run full suite, not just new tests)
- [ ] Code is formatted (linter/formatter run)
- [ ] No debug code left (console.log, print statements)
- [ ] Commit messages are clear
- [ ] Self-review completed (you reviewed your own diff)
- [ ] Documentation updated if needed
- [ ] Edge cases handled

**Cannot check all boxes? Fix first, then request review.**

## Self-Review First

Before ANY external review:

1. **Read your own diff completely**
   - `git diff main...HEAD` (or appropriate comparison)
   - Read every line changed
   - Look for obvious issues

2. **Check for common problems:**
   - Unused imports/variables
   - Commented-out code
   - TODO comments that should be addressed
   - Magic numbers without explanation
   - Error handling missing
   - Tests covering the changes

3. **Fix issues found**
   - Don't send for review with known issues
   - "I know X is wrong but..." = fix it first

## Review Request Structure

```markdown
## What

[One sentence describing the change]

## Why

[Context - what problem this solves, or what feature this adds]

## How

[Brief technical approach - key design decisions]

## Testing

[How was this tested? What should reviewer verify?]

## Notes for Reviewer

[Any areas of concern, specific feedback wanted, known limitations]
```

## Example

```markdown
## What

Add retry logic to API client for transient failures.

## Why

Production seeing intermittent 503 errors from vendor API, causing job failures.

## How

- Added `retry_operation` decorator with exponential backoff
- Applied to all external API calls
- Max 3 retries with 1s/2s/4s delays

## Testing

- Unit tests for retry logic (see test_retry.py)
- Tested manually against staging API with artificial failures
- Verified in staging environment for 24 hours

## Notes for Reviewer

- Considered circuit breaker pattern but felt YAGNI for now
- Would appreciate review of error classification logic in lines 45-60
```

## Small, Focused Changes

**Keep PRs small:**
- One logical change per PR
- Easier to review = better feedback
- Faster merge

**If change is large:**
- Consider splitting into multiple PRs
- Stack PRs if dependencies exist
- Label as "[Part 1 of 3]" etc.

| PR Size | Review Time | Quality |
|---------|-------------|---------|
| < 200 lines | Fast | High |
| 200-500 lines | Moderate | Medium |
| > 500 lines | Slow | Lower |

## Red Flags - STOP

- Requesting review before self-review
- Tests not passing
- "I know this is messy but..."
- 1000+ line PR without splitting
- No testing information
- Vague "please review" requests

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "Reviewer will catch issues" | Self-review first |
| "It's obvious what it does" | Write the context anyway |
| "Can't split the PR" | Usually you can |
| "Tests take too long" | Run them anyway |

## Related Skills

- **receiving-code-review** - How to respond to feedback
- **verification-before-completion** - Verify before claiming ready
- **test-driven-development** - Ensure tests exist for changes
