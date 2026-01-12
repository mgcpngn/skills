---
name: writing-plans
description: Use when you have a spec or requirements for a multi-step task, BEFORE touching any code. Creates bite-sized implementation plans for execution.
---

# Writing Plans

## Overview

Write comprehensive implementation plans assuming the engineer has zero context for the codebase and questionable taste.

**Core principle:** Document everything they need to know - which files to touch, exact code, how to test. Give the whole plan as bite-sized tasks.

**Announce at start:** "I'm using the writing-plans skill to create the implementation plan."

## When to Use

**After:**
- Brainstorming has produced a design
- Requirements are clear
- Scope is defined

**Before:**
- Writing any implementation code
- Starting multi-step tasks

## Plan Document Header

**Every plan MUST start with:**

```markdown
# [Feature Name] Implementation Plan

> **For execution:** Use executing-plans skill to implement this plan task-by-task.

**Goal:** [One sentence describing what this builds]

**Architecture:** [2-3 sentences about approach]

**Tech Stack:** [Key technologies/libraries]

---
```

## Bite-Sized Task Granularity

**Each step is one action (2-5 minutes):**

```
- "Write the failing test" - step
- "Run it to make sure it fails" - step
- "Implement the minimal code to make the test pass" - step
- "Run the tests and make sure they pass" - step
- "Commit" - step
```

NOT: "Implement the feature" - too big

## Task Structure Template

```markdown
### Task N: [Component Name]

**Files:**
- Create: `exact/path/to/file.py`
- Modify: `exact/path/to/existing.py:123-145`
- Test: `tests/exact/path/to/test.py`

**Step 1: Write the failing test**

```python
def test_specific_behavior():
    result = function(input)
    assert result == expected
```

**Step 2: Run test to verify it fails**

Run: `pytest tests/path/test.py::test_name -v`
Expected: FAIL with "function not defined"

**Step 3: Write minimal implementation**

```python
def function(input):
    return expected
```

**Step 4: Run test to verify it passes**

Run: `pytest tests/path/test.py::test_name -v`
Expected: PASS

**Step 5: Commit**

```bash
git add tests/path/test.py src/path/file.py
git commit -m "feat: add specific feature"
```
```

## Plan Quality Checklist

- [ ] Exact file paths always
- [ ] Complete code in plan (not "add validation")
- [ ] Exact commands with expected output
- [ ] DRY, YAGNI, TDD enforced
- [ ] Frequent commits specified
- [ ] Each task is 2-5 minutes

## Save Location

```
docs/plans/YYYY-MM-DD-<feature-name>.md
```

## Execution Handoff

After saving the plan, offer execution choice:

**"Plan complete and saved. Two execution options:**

**1. Subagent-Driven (this session)** 
- Fresh subagent per task
- Review between tasks
- Fast iteration

**2. Sequential Execution**
- Execute tasks one by one
- Checkpoint after batches
- Use executing-plans skill

**Which approach?"**

## Red Flags - STOP

- Tasks that take more than 5 minutes
- "Add the necessary validation" (vague)
- Missing file paths
- Missing test commands
- No expected output specified

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "They'll figure out the path" | Specify exact paths |
| "The code is obvious" | Write complete code |
| "Too much detail" | Detail prevents errors |
| "They know how to test" | Specify exact commands |

## Related Skills

- **brainstorming** - Creates the design this skill plans
- **executing-plans** - Executes the plan this skill creates
- **test-driven-development** - Plans should enforce TDD

## Remember

- Exact file paths always
- Complete code in plan
- Exact commands with expected output
- DRY, YAGNI, TDD
- Frequent commits
