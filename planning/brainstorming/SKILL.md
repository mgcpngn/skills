---
name: brainstorming
description: Use BEFORE any creative work - creating features, building components, adding functionality, or modifying behavior. Explores user intent, requirements and design through dialogue before implementation.
---

# Brainstorming Ideas Into Designs

## Overview

Help turn ideas into fully formed designs and specs through natural collaborative dialogue.

**Core principle:** Understand before implementing. Explore before committing.

Start by understanding the current project context, then ask questions one at a time to refine the idea. Once you understand what you're building, present the design in small sections, checking after each section whether it looks right.

## When to Use

**Always before:**
- Creating new features
- Building new components
- Adding functionality
- Modifying existing behavior
- Starting any implementation work

**Don't skip when:**
- "I already know what to build" - validate assumptions
- "It's simple" - simple can become complex
- "Let me just start coding" - design first

## The Process

### Phase 1: Understanding the Idea

1. **Check project context first**
   - Read relevant files, docs, recent commits
   - Understand current state

2. **Ask questions one at a time**
   - Prefer multiple choice when possible
   - Open-ended is fine for exploration
   - Only ONE question per message
   - If topic needs more exploration, break into multiple questions

3. **Focus on understanding:**
   - Purpose: What problem are we solving?
   - Constraints: What limitations exist?
   - Success criteria: How do we know it's done?

### Phase 2: Exploring Approaches

1. **Propose 2-3 different approaches**
   - Each with clear trade-offs
   - Lead with your recommendation
   - Explain reasoning for recommendation

2. **Present conversationally**
   - Not a formal document yet
   - Discussion, not dictation

### Phase 3: Presenting the Design

1. **Break into sections of 200-300 words**
   - Don't overwhelm with wall of text

2. **Ask after each section**
   - "Does this look right so far?"
   - Ready to clarify or go back

3. **Cover essentials:**
   - Architecture
   - Components
   - Data flow
   - Error handling
   - Testing approach

### Phase 4: Documentation

After validation:
1. Write design to `docs/plans/YYYY-MM-DD-<topic>-design.md`
2. Commit the design document

### Phase 5: Implementation Handoff

Ask: "Ready to set up for implementation?"

If yes:
- Use **writing-plans** skill to create detailed implementation plan
- Or proceed directly if scope is small

## Key Principles

| Principle | Why |
|-----------|-----|
| **One question at a time** | Don't overwhelm |
| **Multiple choice preferred** | Easier to answer |
| **YAGNI ruthlessly** | Remove unnecessary features |
| **Explore alternatives** | Always 2-3 approaches |
| **Incremental validation** | Validate each section |
| **Be flexible** | Go back when needed |

## Red Flags - STOP

If you catch yourself:
- Jumping to code without design
- Asking multiple questions at once
- Presenting everything at once
- Not exploring alternatives
- Assuming you know what's needed

**STOP. Return to Phase 1.**

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "I know what they want" | Validate assumptions |
| "It's obvious" | Make it explicit |
| "Design is overhead" | Design prevents rework |
| "Let me prototype first" | Fine, but throw away prototype |

## Related Skills

- **writing-plans** - Create implementation plan after design
- **executing-plans** - Execute the plan after creation

## Output

Design document at: `docs/plans/YYYY-MM-DD-<topic>-design.md`
