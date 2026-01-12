# Skills Library

> **通用能力库**：整合 [obra/superpowers](https://github.com/obra/superpowers) 的工程流程方法论与 [anthropics/skills](https://github.com/anthropics/skills) 的具体工具技能，构建可按需自动调用的 AI Agent 能力框架。

## 架构设计

本库将 Skills 分为两大类：

| 类别 | 来源 | 定位 | 说明 |
|------|------|------|------|
| **Process Skills** | superpowers | 算法集 | 工程流程、方法论、决策框架 |
| **Tool Skills** | anthropics | 工具集 | 具体技术、API 用法、文件格式 |

```
┌──────────────────────────────────────────────────────────────────┐
│                        SKILLS LIBRARY                            │
├─────────────────────────────┬────────────────────────────────────┤
│    PROCESS SKILLS           │         TOOL SKILLS                │
│    (HOW to work)            │         (WHAT to use)              │
├─────────────────────────────┼────────────────────────────────────┤
│ • brainstorming             │ • mcp-builder                      │
│ • writing-plans             │ • webapp-testing                   │
│ • executing-plans           │ • frontend-design                  │
│ • systematic-debugging      │ • web-artifacts-builder            │
│ • test-driven-development   │ • docx/pptx/xlsx/pdf-creation      │
│ • code-review               │ • ...                              │
│ • git-workflow              │                                    │
└─────────────────────────────┴────────────────────────────────────┘
```

## 设计理念

| 原则 | 说明 |
|------|------|
| **Process > Guessing** | 系统化流程优于临时猜测 |
| **Evidence > Claims** | 证据先于断言，验证后才能声称完成 |
| **TDD for Everything** | 测试驱动，包括文档本身也用 TDD 方式编写 |
| **Composable Skills** | 可组合的能力单元，按需触发 |
| **Concise is Key** | 简洁至上，只添加 Claude 不知道的信息 |

## 目录结构

```
skills/
├── README.md                        # 本文件
├── SKILL_TEMPLATE.md                # Skill 编写模板
│
├── .agent/workflows/                # 工作流集成
│   └── using-skills.md
│
│   ╔═══════════════════════════════════════════════════════╗
│   ║            PROCESS SKILLS (流程方法论)                ║
│   ╚═══════════════════════════════════════════════════════╝
│
├── planning/                        # 规划相关
│   ├── brainstorming/               # 想法→设计
│   ├── writing-plans/               # 设计→计划
│   └── executing-plans/             # 计划→执行
│
├── testing/                         # 测试相关
│   └── test-driven-development/     # TDD 核心流程
│
├── debugging/                       # 调试相关
│   └── systematic-debugging/        # 四阶段根因分析
│
├── verification/                    # 验证相关
│   └── verification-before-completion/
│
├── collaboration/                   # 协作相关
│   ├── dispatching-parallel-agents/ # 并行 Agent 调度
│   └── subagent-driven-development/ # 子 Agent 驱动开发
│
├── code-review/                     # 代码审查
│   ├── requesting-code-review/
│   └── receiving-code-review/
│
├── git-workflow/                    # Git 工作流
│   ├── github-workflow/             # GitHub 完整交互 (gh CLI)
│   ├── using-git-worktrees/
│   └── finishing-dev-branch/
│
├── meta/                            # 元能力
│   ├── writing-skills/              # 如何编写 Skill
│   └── using-skills/                # 如何使用 Skill
│
│   ╔═══════════════════════════════════════════════════════╗
│   ║            TOOL SKILLS (具体工具技能)                 ║
│   ╚═══════════════════════════════════════════════════════╝
│
├── tooling/                         # 开发工具
│   ├── mcp-builder/                 # MCP 服务器构建
│   ├── webapp-testing/              # Web 应用测试 (Playwright)
│   ├── frontend-design/             # 前端设计美学
│   └── web-artifacts-builder/       # Web Artifacts 构建
│
└── documents/                       # 文档生成
    ├── docx-creation/               # Word 文档
    ├── pptx-creation/               # PowerPoint 演示
    ├── xlsx-creation/               # Excel 表格
    └── pdf-creation/                # PDF 文档
```

## 使用方式

### 自动触发

Skills 通过 `description` 字段实现自动匹配：

```yaml
description: Use when [specific triggering conditions]
```

### 显式调用

在对话中使用：
```
请使用 systematic-debugging skill 来分析这个问题
```

### 组合使用

Process Skills 指导 HOW，Tool Skills 提供 WHAT：

```
任务：创建一个 Web 应用

流程：
1. brainstorming (Process) → 理解需求
2. frontend-design (Tool) → 设计美学
3. writing-plans (Process) → 制定计划
4. web-artifacts-builder (Tool) → 技术栈
5. executing-plans (Process) → 执行实现
6. webapp-testing (Tool) → 测试验证
7. verification-before-completion (Process) → 完成确认
```

## 快速参考

### Process Skills

| Skill | 使用场景 |
|-------|----------|
| `brainstorming` | 创建功能、构建组件前 |
| `writing-plans` | 有规格后，写代码前 |
| `executing-plans` | 有计划，需要分批执行 |
| `test-driven-development` | 写新功能、修 bug、重构 |
| `systematic-debugging` | 任何技术问题调试 |
| `verification-before-completion` | 声称完成前必须验证 |
| `github-workflow` | GitHub 仓库创建、PR、发布 |

### Tool Skills

| Skill | 使用场景 |
|-------|----------|
| `mcp-builder` | 构建 MCP 服务器 |
| `webapp-testing` | Playwright UI 测试 |
| `frontend-design` | 高质量 UI 设计 |
| `web-artifacts-builder` | React/Tailwind 应用 |
| `docx-creation` | 生成 Word 文档 |
| `pptx-creation` | 生成 PowerPoint |
| `xlsx-creation` | 生成 Excel 表格 |
| `pdf-creation` | 生成 PDF 文档 |

## 核心流程链

```
┌─────────────────────────────────────────────────────────────────┐
│                    DEVELOPMENT WORKFLOW                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  brainstorming ──→ writing-plans ──→ executing-plans            │
│       │                 │                  │                    │
│       │                 ↓                  ↓                    │
│       │         [frontend-design]   [Tool Skills]               │
│       │         [mcp-builder]       [as needed]                 │
│       │                                    │                    │
│       ↓                                    ↓                    │
│  systematic-debugging ←── test-driven-development               │
│                                    │                            │
│                                    ↓                            │
│                     verification-before-completion              │
│                                    │                            │
│                                    ↓                            │
│                         finishing-dev-branch                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## 扩展 Skills

使用 `SKILL_TEMPLATE.md` 创建新 Skill：

```
skills/
└── your-category/
    └── your-skill/
        └── SKILL.md
```

关键要素：
- `description` 明确触发条件 ("Use when...")
- 步骤可执行、可验证
- 有 "Red Flags" 防止绕过
- 有 "Common Rationalizations" 堵住借口

## License

MIT License
