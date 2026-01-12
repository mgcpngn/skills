---
name: writing-skills
description: Use when creating new skills - requires TDD approach to documentation with pressure scenarios as tests
---

# Writing Skills

## Overview

**Writing skills IS Test-Driven Development applied to process documentation.**

You write test cases (pressure scenarios), watch them fail (baseline behavior), write the skill (documentation), watch tests pass (agents comply), and refactor (close loopholes).

**Core principle:** If you didn't watch an agent fail without the skill, you don't know if the skill teaches the right thing.

## When to Create a Skill

**Create when:**
- Technique wasn't intuitively obvious
- You'd reference this again across projects
- Pattern applies broadly (not project-specific)
- Others would benefit

**Don't create for:**
- One-off solutions
- Standard practices well-documented elsewhere
- Project-specific conventions (put in project docs)
- Mechanical constraints (if enforceable with automation, automate it)

## Skill Types

| Type | Description | Example |
|------|-------------|---------|
| **Technique** | Concrete method with steps | condition-based-waiting |
| **Pattern** | Way of thinking about problems | test-invariants |
| **Reference** | API docs, syntax guides | tool documentation |

## Directory Structure

```
skills/
└── category/
    └── skill-name/
        ├── SKILL.md              # Main reference (required)
        └── supporting-file.*     # Only if needed (100+ lines)
```

**Flat namespace within category** - all skills searchable

**Separate files for:**
1. **Heavy reference** (100+ lines) - API docs, comprehensive syntax
2. **Reusable tools** - Scripts, utilities, templates

**Keep inline:**
- Principles and concepts
- Code patterns (< 50 lines)
- Everything else

## SKILL.md Structure

### Frontmatter (YAML)

```yaml
---
name: skill-name-with-hyphens
description: Use when [specific triggering conditions and symptoms]
---
```

**Rules:**
- `name`: Letters, numbers, hyphens only
- `description`: Third-person, describes ONLY when to use (NOT what it does)
- Start with "Use when..." to focus on triggering conditions
- Max 1024 characters total

### Body Structure

```markdown
# Skill Name

## Overview
What is this? Core principle in 1-2 sentences.

## When to Use
Bullet list with SYMPTOMS and use cases
When NOT to use

## The Iron Law (for discipline skills)
```
[Unbreakable rule]
```

## The Process / Core Pattern
Steps or pattern description

## Quick Reference
Table for scanning common operations

## Common Mistakes
What goes wrong + fixes

## Red Flags - STOP
If you catch yourself thinking...

## Common Rationalizations
| Excuse | Reality |

## Related Skills
Links to related skills

## Real-World Impact (optional)
Concrete results
```

## TDD for Skills

### RED: Baseline Test

1. Create pressure scenario where agent would fail
2. Run agent without skill
3. Document exact violations/rationalizations

### GREEN: Write Skill

1. Write skill addressing those specific violations
2. Run agent with skill
3. Verify agent now complies

### REFACTOR: Close Loopholes

1. Find new rationalizations agent uses
2. Add to "Common Rationalizations" and "Red Flags"
3. Re-test until loopholes closed

## Skill Quality Checklist

Before marking skill complete:

- [ ] Has clear triggering conditions (description)
- [ ] Core principle in one sentence
- [ ] Steps are executable and verifiable
- [ ] Has "Red Flags" section
- [ ] Has "Common Rationalizations" table
- [ ] Related skills are referenced
- [ ] Tested with pressure scenario (RED phase done)
- [ ] Agent complies with skill (GREEN phase done)
- [ ] Loopholes identified and closed (REFACTOR done)

## Anti-Patterns

| Anti-Pattern | Problem |
|--------------|---------|
| **Narrative example** | "I once fixed X by..." - not reusable |
| **Multi-language dilution** | Examples in 5 languages - pick one, stay focused |
| **Code in flowcharts** | Logic belongs in code blocks, not diagrams |
| **Generic labels** | "Do the thing" - be specific |
| **Description explains what** | Should explain WHEN to use, not what it does |

## Related Skills

- **test-driven-development** - TDD concept adapted for skills
- **using-skills** - How skills are discovered and used

## The Bottom Line

If you didn't watch an agent fail without the skill, you don't know if the skill teaches the right thing.

Write the test (scenario) first. Watch it fail. Then write the skill.
