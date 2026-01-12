# Skills 核心约束 (Embedded Version)

> 将下面内容直接复制到你项目的 `GEMINI.md` 或 `CLAUDE.md` 中即可使用。

---

## 开发铁律

以下是必须遵守的核心约束，违反即为失败。

### 1. 调试约束 (Systematic Debugging)

```
NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST
```

**四阶段流程**:
1. **Root Cause** - 读错误信息、复现问题、检查最近改动、追踪数据流
2. **Pattern Analysis** - 找到正常工作的代码，对比差异
3. **Hypothesis** - 形成单一假设，最小化测试，一次只改一处
4. **Implementation** - 写失败测试，修复根因，验证

**Red Flags - 立即停止**:
- "快速修一下，之后再调查"
- "试试改 X 看看行不行"
- "一次改多处，跑测试"
- "我觉得是 X，让我修它"
- 3 次修复失败 → 质疑架构，不要再试第 4 次

---

### 2. 测试约束 (Test-Driven Development)

```
NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST
```

**RED-GREEN-REFACTOR**:
1. **RED** - 写一个失败的测试
2. **Verify RED** - 运行，确认失败原因正确
3. **GREEN** - 写最小代码让测试通过
4. **Verify GREEN** - 运行，确认通过
5. **REFACTOR** - 清理代码，保持测试绿色

**铁律**:
- 先写代码后写测试？删除代码，重新开始
- 测试立即通过？你在测已有行为，修改测试
- 不要保留"作为参考"，删除就是删除

**Red Flags - 立即删除代码重来**:
- 先写代码后写测试
- 测试通过但没看它失败过
- "这次先跳过 TDD"
- "我手动测试过了"

---

### 3. 验证约束 (Verification Before Completion)

```
NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE
```

**验证门控**:
```
声称任何状态前:
1. IDENTIFY - 什么命令能证明这个声称？
2. RUN - 执行完整命令（新鲜的，完整的）
3. READ - 读完整输出，检查退出码
4. VERIFY - 输出是否确认声称？
   - 否 → 报告实际状态
   - 是 → 带证据声称
5. ONLY THEN - 发出声称

跳过任何步骤 = 说谎
```

**常见失败**:
| 声称 | 需要 | 不够 |
|------|------|------|
| 测试通过 | 测试输出: 0 failures | "应该通过了" |
| 构建成功 | 构建命令: exit 0 | "linter 过了" |
| Bug 修复 | 测试原症状通过 | "代码改了" |

**Red Flags - 立即停止**:
- 使用 "应该"、"可能"、"看起来"
- 在验证前表达满意 ("太好了！"、"完成！")
- 准备 commit/push 但没验证
- 累了想结束工作

---

### 4. 规划约束 (Planning Before Coding)

```
UNDERSTAND BEFORE IMPLEMENT
```

**流程**:
```
想法/需求
    ↓
理解上下文 (读代码、文档)
    ↓
一次问一个问题（多选优先）
    ↓
探索 2-3 个方案，带权衡
    ↓
分段呈现设计（200-300 字/段），逐段确认
    ↓
写入 docs/plans/YYYY-MM-DD-<topic>.md
    ↓
开始实现
```

**Red Flags - 立即停止**:
- 不理解需求就开始写代码
- 一次问多个问题
- 不探索替代方案
- "我知道他们想要什么"
- "设计是开销"

---

## 快速参考卡片

```
┌─────────────────────────────────────────────────────────────┐
│                    DEVELOPMENT IRON LAWS                    │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  BUG?    →  Root Cause FIRST  →  Then Fix                  │
│             (NO guessing, NO quick fixes)                   │
│                                                             │
│  CODE?   →  Failing Test FIRST  →  Then Code               │
│             (NO test = DELETE code)                         │
│                                                             │
│  DONE?   →  Run Verification FIRST  →  Then Claim          │
│             ("should work" = LYING)                         │
│                                                             │
│  BUILD?  →  Understand FIRST  →  Then Plan  →  Then Code   │
│             (NO coding without design)                      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 使用方式

将上述内容复制到你的项目根目录的 `GEMINI.md` 文件中。

当 Agent 处理任务时，它应该：
1. 识别任务类型（调试/编码/完成/规划）
2. 自动应用对应约束
3. 在 Red Flags 场景时自我停止

如需完整 skill 详情，可读取 `D:\code\skills\` 下对应的 SKILL.md。
