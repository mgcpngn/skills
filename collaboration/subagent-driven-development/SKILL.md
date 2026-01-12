---
name: subagent-driven-development
description: Use when executing a plan in the same session with fresh subagent per task and two-stage review (spec compliance then code quality)
---

# Subagent-Driven Development

## Overview

Execute plan by dispatching fresh subagent per task, with two-stage review after each: spec compliance review first, then code quality review.

**Core principle:** Fresh subagent per task + two-stage review = high quality, fast iteration

## When to Use

```
Have implementation plan?
         │
         ▼
   Tasks mostly independent?
    ┌────┴────┐
    │         │
   No        Yes
    │         │
    ▼         ▼
 Manual   Stay in this
 execution session?
           ┌────┴────┐
           │         │
          No        Yes
           │         │
           ▼         ▼
     executing-   subagent-driven-
     plans        development
```

**vs. Executing Plans:**
- Same session (no context switch)
- Fresh subagent per task (no context pollution)
- Two-stage review after each task
- Faster iteration (no human-in-loop between tasks)

## The Process

```
┌─────────────────────────────────────────────────┐
│              PER TASK CYCLE                     │
├─────────────────────────────────────────────────┤
│                                                 │
│  1. Dispatch implementer subagent               │
│            │                                    │
│            ▼                                    │
│  2. Subagent asks questions? ──yes──┐           │
│            │                        │           │
│            no                       ▼           │
│            │                Answer questions    │
│            │                        │           │
│            ◀────────────────────────┘           │
│            │                                    │
│            ▼                                    │
│  3. Subagent implements, tests, commits         │
│            │                                    │
│            ▼                                    │
│  4. Dispatch spec reviewer                      │
│            │                                    │
│            ▼                                    │
│  5. Spec compliant? ──no───┐                    │
│            │               │                    │
│           yes         Fix gaps                  │
│            │               │                    │
│            │◀──────────────┘                    │
│            ▼                                    │
│  6. Dispatch code quality reviewer              │
│            │                                    │
│            ▼                                    │
│  7. Quality approved? ──no──┐                   │
│            │                │                   │
│           yes          Fix issues               │
│            │                │                   │
│            │◀───────────────┘                   │
│            ▼                                    │
│  8. Mark task complete                          │
│                                                 │
└─────────────────────────────────────────────────┘
         │
         ▼
   More tasks? ──yes──▶ [Repeat cycle]
         │
         no
         │
         ▼
   Final review + complete
```

### Setup

1. Read plan file once
2. Extract all tasks with full text and context
3. Create task tracking list

### Per Task

1. **Dispatch implementer subagent**
   - Provide full task text + context
   - Don't make subagent read plan file

2. **Answer questions if any**
   - Subagent may ask clarifying questions
   - Answer before proceeding

3. **Subagent implements**
   - Follows TDD
   - Tests, commits
   - Self-reviews

4. **Spec compliance review**
   - Dispatch spec reviewer subagent
   - Confirms code matches spec
   - Nothing extra, nothing missing

5. **Code quality review**
   - Only AFTER spec compliance passes
   - Reviews implementation quality
   - Clean code, good practices

6. **Fix and re-review**
   - If issues found, implementer fixes
   - Reviewer reviews again
   - Repeat until approved

7. **Mark complete**
   - Move to next task

### Completion

After all tasks:
- Dispatch final code reviewer for entire implementation
- Verify all requirements met
- Complete development

## Review Templates

### Spec Reviewer Focus

- Does code match requirements?
- Is anything missing?
- Is anything extra (YAGNI violation)?

### Code Quality Reviewer Focus

- Clean code principles?
- Proper error handling?
- Good naming?
- No code smells?

## Advantages

**vs. Manual execution:**
- Subagents follow TDD naturally
- Fresh context per task (no confusion)
- Parallel-safe (subagents don't interfere)
- Subagent can ask questions

**vs. Executing Plans:**
- Same session (no handoff)
- Continuous progress (no waiting)
- Review checkpoints automatic

**Quality gates:**
- Self-review catches issues before handoff
- Two-stage review: spec compliance, then code quality
- Review loops ensure fixes actually work

## Red Flags - STOP

**Never:**
- Skip reviews (spec OR quality)
- Proceed with unfixed issues
- Dispatch multiple implementation subagents in parallel
- Make subagent read plan file (provide full text instead)
- Skip scene-setting context
- Ignore subagent questions
- Accept "close enough" on spec compliance
- Skip review loops
- **Start code quality review before spec compliance is ✅**
- Move to next task while review has open issues

**If reviewer finds issues:**
- Implementer fixes them
- Reviewer reviews again
- Repeat until approved
- Don't skip the re-review

## Related Skills

- **writing-plans** - Creates the plan this skill executes
- **test-driven-development** - Subagents follow TDD for each task
- **executing-plans** - Alternative for parallel session execution
