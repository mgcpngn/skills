# Skill 编写模板

> 基于 TDD 思维：先测试(压力场景) → 再实现(skill) → 验证(agent 遵守)

## Frontmatter 格式

```yaml
---
name: skill-name-with-hyphens
description: Use when [specific triggering conditions and symptoms]
---
```

**规则：**
- `name`: 仅使用字母、数字、连字符
- `description`: 第三人称，只描述**何时使用**（不描述做什么）
- 总长度不超过 1024 字符

## 标准结构

```markdown
---
name: example-skill
description: Use when [triggering conditions]
---

# Skill Name

## Overview
[核心原则，1-2 句话]

**Core principle:** [最重要的一句话]

## When to Use
**Use when:**
- [条件1]
- [条件2]

**Don't use when:**
- [排除条件]

## The Iron Law (可选)
```
[不可违反的规则]
```

## The Process / Core Pattern
### Step 1: [名称]
[具体步骤]

### Step 2: [名称]
[具体步骤]

## Quick Reference
| Phase | Key Activities | Success Criteria |
|-------|----------------|------------------|
| 1     | ...            | ...              |

## Common Mistakes
| Mistake | Fix |
|---------|-----|
| ...     | ... |

## Red Flags - STOP
如果你发现自己在想：
- "[想法1]"
- "[想法2]"

**所有这些意味着：停下来，回到第一步。**

## Common Rationalizations
| Excuse | Reality |
|--------|---------|
| "..." | ... |

## Related Skills
- **skill-name** - [关系说明]

## Real-World Impact (可选)
[实际效果数据]
```

## Skill 类型

### Technique (技术)
具体方法，有明确步骤。例如：condition-based-waiting, root-cause-tracing

### Pattern (模式)
思考问题的方式。例如：flatten-with-flags, test-invariants

### Reference (参考)
API 文档、语法指南。例如：office-docs

## 文件组织

```
skill-name/
├── SKILL.md              # 主文件 (必需)
├── supporting-file.md    # 辅助文件 (100+ 行的重型参考)
└── template.md           # 模板文件 (可复用的工具)
```

**原则：**
- 内联保持：原则概念、代码模式 (<50 行)
- 单独文件：API 文档 (100+ 行)、可复用工具/脚本

## Skill 质量检查表

- [ ] 有明确的触发条件 (description)
- [ ] 核心原则一句话说清
- [ ] 步骤可执行、可验证
- [ ] 有 Red Flags 防止绕过
- [ ] 有 Common Rationalizations 堵住借口
- [ ] 关联技能有引用
