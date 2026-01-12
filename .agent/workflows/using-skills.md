---
description: How to use skills in any project - automatically triggered by task type
---

# Using Skills in Your Project

## 架构概览

Skills 分为两类：

| 类别 | 定位 | 示例 |
|------|------|------|
| **Process Skills** | HOW - 工程流程方法论 | brainstorming, TDD, debugging |
| **Tool Skills** | WHAT - 具体技术工具 | mcp-builder, webapp-testing, docx |

## Quick Setup

1. 复制或链接 skills 目录到项目：
   ```bash
   # 复制
   cp -r d:/code/skills /path/to/your/project/.agent/skills
   
   # 或符号链接
   ln -s d:/code/skills /path/to/your/project/.agent/skills
   ```

2. 在项目 agent 配置中引用 skills。

## 自动匹配规则

Skills 通过 `description` 字段自动匹配，格式为 "Use when..."

### Process Skills 触发

| 任务类型 | 自动触发 Skill |
|----------|----------------|
| 新功能开发 | `brainstorming` → `writing-plans` → `executing-plans` |
| Bug 修复 | `systematic-debugging` → `test-driven-development` |
| 代码审查 | `requesting-code-review` / `receiving-code-review` |
| 声称完成 | `verification-before-completion` |
| 多个独立问题 | `dispatching-parallel-agents` |
| 开始开发 | `using-git-worktrees` → `brainstorming` |
| 完成开发 | `finishing-dev-branch` |

### Tool Skills 触发

| 任务类型 | 自动触发 Skill |
|----------|----------------|
| MCP 服务器 | `mcp-builder` |
| Web UI 测试 | `webapp-testing` |
| 前端设计 | `frontend-design` |
| React 应用 | `web-artifacts-builder` |
| Word 文档 | `docx-creation` |
| PPT 演示 | `pptx-creation` |
| Excel 表格 | `xlsx-creation` |
| PDF 文档 | `pdf-creation` |

## Skill 优先级

当多个 skills 可能适用时：

1. **Process Skills 优先** - 确定 HOW to approach
   - `brainstorming` - 创意工作前
   - `systematic-debugging` - 修复 bug 前
   
2. **Tool Skills 其次** - 确定 WHAT to use
   - `frontend-design` - UI 设计指导
   - `mcp-builder` - MCP 开发指导

## 组合使用示例

### 示例 1: 开发 Web 应用

```
1. brainstorming (Process)
   └── 理解需求，探索方案

2. frontend-design (Tool)
   └── 设计美学指导

3. writing-plans (Process)
   └── 制定实现计划

4. web-artifacts-builder (Tool)
   └── React + Tailwind 技术栈

5. executing-plans (Process)
   └── 分步执行计划

6. webapp-testing (Tool)
   └── Playwright 测试

7. verification-before-completion (Process)
   └── 验证完成
```

### 示例 2: 构建 MCP 服务器

```
1. brainstorming (Process)
   └── 理解 API 需求

2. mcp-builder (Tool)
   └── MCP 开发指南

3. writing-plans (Process)
   └── 制定 tool 实现计划

4. test-driven-development (Process)
   └── TDD 开发

5. verification-before-completion (Process)
   └── 验证完成
```

## Skill 调用模式

调用 skill 时：

1. **宣告**: "I'm using [skill-name] to [purpose]"
2. **加载**: 读取 SKILL.md 文件
3. **执行**: 按文档精确执行
4. **验证**: 对照 skill 标准检查

## 添加项目特定 Skills

按 `SKILL_TEMPLATE.md` 创建：

```
skills/
└── your-category/
    └── your-skill/
        └── SKILL.md
```

关键要素：
- `description` 明确 "Use when..." 触发条件
- 步骤可执行、可验证
- 有 "Red Flags" 防止绕过
- 有 "Common Rationalizations" 堵住借口

// turbo-all
