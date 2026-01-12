---
description: How to integrate skills library into other projects
---

# Skills 集成指南

## 本质理解

Skills 本质上是**结构化的 Prompt 片段**：
- 不是可执行代码，而是约束条件和流程指导
- 通过 `description` 字段实现自动触发
- 被 Agent 读取后遵循其中的规则

## 集成方式

### 方式 1: 符号链接（推荐）

**优点**: 单一源头，更新即时生效，不占用项目空间

```powershell
# Windows (PowerShell 管理员权限)
cd D:\path\to\your-project
New-Item -ItemType SymbolicLink -Path ".agent\skills" -Target "D:\code\skills"
```

```bash
# Linux/Mac
cd /path/to/your-project
ln -s /path/to/skills .agent/skills
```

### 方式 2: Git Submodule

**优点**: 版本控制，可锁定特定版本

```bash
# 添加为 submodule
git submodule add https://github.com/your-repo/skills.git .agent/skills

# 克隆项目时
git clone --recursive <your-project>

# 更新 skills
git submodule update --remote
```

### 方式 3: 直接复制

**优点**: 完全独立，可定制

```powershell
# Windows
xcopy /E /I D:\code\skills D:\path\to\your-project\.agent\skills

# 或者只复制需要的 skills
xcopy /E /I D:\code\skills\planning D:\path\to\your-project\.agent\skills\planning
```

### 方式 4: 在项目中引用（不复制）

在项目的 `GEMINI.md` 或 `CLAUDE.md` 中直接引用：

```markdown
## Skills 引用

当需要使用 skills 时，请读取 `D:\code\skills\` 目录下对应的 SKILL.md 文件：

- 新功能开发: 读取 `D:\code\skills\planning\brainstorming\SKILL.md`
- Bug 修复: 读取 `D:\code\skills\debugging\systematic-debugging\SKILL.md`
- 测试: 读取 `D:\code\skills\testing\test-driven-development\SKILL.md`
```

## 推荐目录结构

```
your-project/
├── .agent/
│   ├── skills/           # skills 库 (链接或复制)
│   │   ├── planning/
│   │   ├── debugging/
│   │   └── ...
│   └── workflows/        # 项目特定工作流
│       └── your-workflow.md
│
├── GEMINI.md             # Agent 配置 (引用 skills)
├── CLAUDE.md             # 或其他 agent 配置
└── src/
```

## Agent 配置示例

### GEMINI.md / CLAUDE.md 配置

```markdown
# Project: Your Project Name

## Skills 集成

本项目使用 Skills 能力库提升开发质量。

### 自动触发规则

| 场景 | 触发 Skill | 路径 |
|------|------------|------|
| 新功能 | brainstorming | `.agent/skills/planning/brainstorming/SKILL.md` |
| Bug 修复 | systematic-debugging | `.agent/skills/debugging/systematic-debugging/SKILL.md` |
| 写代码 | test-driven-development | `.agent/skills/testing/test-driven-development/SKILL.md` |
| 声称完成 | verification-before-completion | `.agent/skills/verification/verification-before-completion/SKILL.md` |

### 使用方式

1. 识别当前任务类型
2. 读取对应 SKILL.md 文件
3. 宣告: "I'm using [skill-name] skill"
4. 严格遵循 skill 中的流程和约束
```

## 最小化配置（只用核心 Skills）

如果不想复制整个库，可以只使用最核心的几个：

```
.agent/skills/
├── planning/
│   └── brainstorming/SKILL.md      # 必备：需求理解
├── debugging/
│   └── systematic-debugging/SKILL.md # 必备：问题排查
├── testing/
│   └── test-driven-development/SKILL.md # 必备：TDD
└── verification/
    └── verification-before-completion/SKILL.md # 必备：完成验证
```

## 在 System Prompt 中直接内嵌

对于简单场景，可以直接将核心约束内嵌到 system prompt：

```markdown
## 开发约束

### 调试约束 (from systematic-debugging)
- NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST
- 四阶段: Root Cause → Pattern Analysis → Hypothesis → Implementation
- 3+ fixes failed = question architecture, not fix again

### 测试约束 (from TDD)
- NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST
- RED → GREEN → REFACTOR
- Write code before test? Delete it. Start over.

### 验证约束 (from verification-before-completion)
- NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE
- Run command → Read output → THEN claim result
```

## 验证集成

集成后，测试是否生效：

1. 开始一个 bug 修复任务
2. 观察 Agent 是否：
   - 宣告使用 systematic-debugging skill
   - 遵循四阶段流程
   - 不直接跳到修复

如果没有触发，检查：
- Skills 路径是否正确
- Agent 配置是否引用了 skills
- description 字段是否匹配任务类型
