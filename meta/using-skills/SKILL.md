---
name: using-skills
description: Use at the START of any conversation or task - establishes how to find and use skills, requiring skill invocation BEFORE any response including clarifying questions
---

# Using Skills

## The Rule

**Invoke relevant skills BEFORE any response or action.**

Even a 1% chance a skill might apply means you should check it. If an invoked skill turns out to be wrong for the situation, you don't need to use it.

```
User message received
         │
         ▼
   Might any skill apply?
    ┌────┴────┐
    │         │
   No        Yes (even 1%)
    │         │
    ▼         ▼
 Respond   Load skill
           Announce: "Using [skill] to [purpose]"
           Follow skill exactly
           Then respond
```

## How to Access Skills

Skills are located in the `skills/` directory, organized by category:
- `testing/` - Test-related skills
- `debugging/` - Debugging skills  
- `planning/` - Planning and design skills
- `collaboration/` - Multi-agent skills
- `verification/` - Verification skills

Read the `SKILL.md` file in the relevant skill directory.

## Skill Priority

When multiple skills could apply, use this order:

1. **Process skills first** (brainstorming, debugging) - these determine HOW to approach the task
2. **Implementation skills second** (TDD, specific patterns) - these guide execution

Examples:
- "Let's build X" → brainstorming first, then implementation skills
- "Fix this bug" → systematic-debugging first, then domain-specific skills

## Skill Types

**Rigid** (TDD, debugging): Follow exactly. Don't adapt away discipline.

**Flexible** (patterns): Adapt principles to context.

The skill itself tells you which type it is.

## Red Flags - STOP

These thoughts mean you're rationalizing:

| Thought | Reality |
|---------|---------|
| "This is just a simple question" | Questions are tasks. Check for skills. |
| "I need more context first" | Skill check comes BEFORE clarifying questions. |
| "Let me explore the codebase first" | Skills tell you HOW to explore. Check first. |
| "This doesn't need a formal skill" | If a skill exists, use it. |
| "I remember this skill" | Skills evolve. Read current version. |
| "This doesn't count as a task" | Action = task. Check for skills. |
| "The skill is overkill" | Simple things become complex. Use it. |
| "I'll just do this one thing first" | Check BEFORE doing anything. |
| "I know what that means" | Knowing the concept ≠ using the skill. Read it. |

## User Instructions

Instructions say WHAT, not HOW. 

"Add X" or "Fix Y" doesn't mean skip workflows:
- "Add feature" → brainstorming → writing-plans → executing
- "Fix bug" → systematic-debugging → test-driven-development

## Quick Reference

| Task Type | Primary Skill |
|-----------|---------------|
| New feature | brainstorming |
| Bug fix | systematic-debugging |
| Multi-step implementation | writing-plans → executing-plans |
| Claiming done | verification-before-completion |
| Writing tests | test-driven-development |
| Multiple independent issues | dispatching-parallel-agents |

## The Bottom Line

**If a skill applies to your task, you MUST use it.**

This is not optional. This is not negotiable.

Check skills FIRST. Always.
