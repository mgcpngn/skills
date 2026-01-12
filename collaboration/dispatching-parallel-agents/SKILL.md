---
name: dispatching-parallel-agents
description: Use when you have 3+ independent failures or tasks across different subsystems that can be investigated or executed concurrently without shared state
---

# Dispatching Parallel Agents

## Overview

When you have multiple unrelated failures (different test files, different subsystems, different bugs), investigating them sequentially wastes time. Each investigation is independent and can happen in parallel.

**Core principle:** Dispatch one agent per independent problem domain. Let them work concurrently.

## When to Use

```
Multiple failures/tasks?
         │
         ▼
   Are they independent?
    ┌────┴────┐
    │         │
   No        Yes
    │         │
    ▼         ▼
 Single    Can they work
 agent     in parallel?
           ┌────┴────┐
           │         │
          No        Yes
           │         │
           ▼         ▼
       Sequential  Parallel
       agents      dispatch
```

**Use when:**
- 3+ test files failing with different root causes
- Multiple subsystems broken independently
- Each problem can be understood without context from others
- No shared state between investigations

**Don't use when:**
- Failures are related (fix one might fix others)
- Need to understand full system state
- Agents would interfere with each other (same files, shared resources)

## The Pattern

### 1. Identify Independent Domains

Group failures by what's broken:
- File A tests: Authentication flow
- File B tests: Data processing
- File C tests: API integration

Each domain is independent - fixing authentication doesn't affect API tests.

### 2. Create Focused Agent Tasks

Each agent gets:
- **Specific scope:** One test file or subsystem
- **Clear goal:** Make these tests pass
- **Constraints:** Don't change other code
- **Expected output:** Summary of what you found and fixed

### 3. Dispatch in Parallel

```
Agent 1 → Fix authentication tests
Agent 2 → Fix data processing tests  
Agent 3 → Fix API integration tests
// All three run concurrently
```

### 4. Review and Integrate

When agents return:
- Read each summary
- Verify fixes don't conflict
- Run full test suite
- Integrate all changes

## Agent Prompt Structure

Good agent prompts are:
1. **Focused** - One clear problem domain
2. **Self-contained** - All context needed to understand the problem
3. **Specific about output** - What should the agent return?

**Example:**

```markdown
Fix the 3 failing tests in src/auth/login.test.py:

1. "test_login_success" - expects token in response
2. "test_login_invalid_password" - wrong error message
3. "test_login_expired_session" - session not invalidated

Your task:

1. Read the test file and understand what each test verifies
2. Identify root cause - timing issues or actual bugs?
3. Fix by:
   - Correcting logic if bugs found
   - Adjusting test expectations if testing changed behavior

Do NOT change other test files.

Return: Summary of what you found and what you fixed.
```

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| **Too broad:** "Fix all tests" | **Specific:** "Fix login.test.py" |
| **No context:** "Fix the race condition" | **Context:** Paste error messages |
| **No constraints:** Agent might refactor everything | **Constraints:** "Only fix tests" |
| **Vague output:** "Fix it" | **Specific:** "Return summary of changes" |

## When NOT to Use

- **Related failures:** Fixing one might fix others - investigate together first
- **Need full context:** Understanding requires seeing entire system
- **Exploratory debugging:** You don't know what's broken yet
- **Shared state:** Agents would interfere (editing same files)

## Verification

After agents return:
1. **Review each summary** - Understand what changed
2. **Check for conflicts** - Did agents edit same code?
3. **Run full suite** - Verify all fixes work together
4. **Spot check** - Agents can make systematic errors

## Red Flags - STOP

- Dispatching agents for related failures
- No clear scope per agent
- Agents editing same files
- Not reviewing agent outputs
- Not running full test suite after

## Related Skills

- **systematic-debugging** - For single complex problems
- **subagent-driven-development** - For sequential task execution

## Real-World Impact

From debugging sessions:
- 6 failures across 3 files
- 3 agents dispatched in parallel
- All investigations completed concurrently
- All fixes integrated successfully
- Zero conflicts between agent changes

**Time saved:** 3 problems solved in time of 1
