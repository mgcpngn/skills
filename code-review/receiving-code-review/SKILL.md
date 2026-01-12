---
name: receiving-code-review
description: Use when you receive code review feedback - requires reading all feedback completely before responding and treating feedback as gift
---

# Receiving Code Review

## Overview

Code review feedback improves code quality. Defensive responses waste the feedback and damage relationships.

**Core principle:** Treat feedback as a gift. Understand before responding.

## When to Use

**When:**
- You receive PR review comments
- Someone gives code feedback
- Reviewer requests changes

## The Process

### Step 1: Read ALL Feedback First

**Before responding to ANY comment:**

1. Read every comment completely
2. Don't reply to individual comments yet
3. Understand the full picture
4. Let initial reactions settle

**Why?**
- Later comments may clarify earlier ones
- Patterns emerge across comments
- Prevents defensive knee-jerk responses

### Step 2: Understand Each Point

For each comment:
1. **Restate in your own words** - Do you understand what they're saying?
2. **Identify the concern** - What underlying issue are they pointing to?
3. **Consider validity** - Is the feedback correct?

**If unclear:**
- Ask clarifying questions
- "I want to make sure I understand - is the concern X or Y?"
- Don't guess and implement wrong fix

### Step 3: Respond Constructively

**For each comment:**

| Feedback Type | Response |
|---------------|----------|
| **Valid issue** | "Good catch, fixed" (and fix it) |
| **Disagreement** | "I see your point. I chose X because Y. Thoughts?" |
| **Clarification needed** | "Can you elaborate on what you mean by X?" |
| **Already addressed** | "This is handled in [specific location]" |

**Never:**
- "That's just how I like it"
- "It works fine"
- Ignore without response
- Defensive justification

### Step 4: Implement Changes

1. Address all requested changes
2. Resolve conversations as you fix
3. Request re-review when done

## Handling Disagreement

**When you disagree with feedback:**

1. **Acknowledge the point first**
   - "I see why X approach would work..."
   
2. **Explain your reasoning**
   - "I went with Y because of [specific reason]..."
   
3. **Invite discussion**
   - "What do you think? I'm open to changing if you see issues with Y."

4. **Defer to senior reviewers on judgment calls**
   - If still disagreeing, they usually have context you lack

**Don't:**
- Dig in defensively
- Appeal to authority ("Google does it this way")
- Dismiss without consideration

## Feedback Categories

| Category | Action |
|----------|--------|
| **Bug/Error** | Fix immediately, thanks for catching |
| **Style/Convention** | Follow team conventions, not personal preference |
| **Design concern** | Discuss, understand, adjust if valid |
| **Nit** | Fix if easy, or note "will fix in follow-up" |
| **Question** | Answer clearly |

## Red Flags - STOP

If you catch yourself:
- Responding before reading everything
- Getting defensive
- Explaining why they're wrong
- Ignoring comments
- Taking it personally
- Rushing to mark resolved

**STOP. Re-read. Breathe. Respond carefully.**

## Common Rationalizations

| Excuse | Reality |
|--------|---------|
| "They don't understand" | Explain clearly, they might be right |
| "This is just style" | Style affects readability |
| "It works" | Working != good |
| "No time to change" | Make time or don't ask for review |
| "They're being picky" | Details matter |

## The Bottom Line

**Feedback makes code better.** The reviewer spent time to help you.

Thank them. Consider carefully. Respond thoughtfully.

Even when you disagree.

## Related Skills

- **requesting-code-review** - How to request review effectively
