# Superpowers for OpenCode — 个人学习笔记

> 目标读者：熟悉 OpenCode、刚接触 superpowers 的工程师自用参考

---

## WHY — 为什么需要 superpowers？

### 核心问题

OpenCode（以及所有 AI 编程助手）的默认行为是：**你说什么，它就做什么**。

这在简单任务时没问题，但在面对复杂工程任务时会产生一个根本矛盾：

- AI 倾向于**立刻动手写代码**，而不是先理解你真正要解决的问题
- 没有约束的 AI 会跳过设计、跳过测试、做出你没要求的功能（YAGNI 违反）
- 多步骤任务中，AI 容易中途偏轨，最终产出与预期偏差越来越大

**superpowers 的存在是为了解决这个问题**：它给 AI 注入了一套标准化工程流程，让 AI 的行为从「随机应变的码农」变成「有方法论的工程师」。

### 具体价值

| 没有 superpowers | 有 superpowers |
|-----------------|----------------|
| 直接开始写代码 | 先澄清需求，再设计，再写代码 |
| 任务中途容易跑偏 | 有实现计划约束，按步骤推进 |
| 测试是事后补充 | TDD 流程内嵌，测试先行 |
| 你描述 WHAT，AI 自己决定 HOW | 你参与 HOW 的设计决策 |
| 大任务一口气做，难以审查 | 分解成小任务，每步可 review |
| AI 自己决定何时完成 | 完成前有验证检查点 |

---

## WHAT — superpowers 是什么？

### 本质

superpowers 是一个 **OpenCode 插件**，通过以下机制工作：

1. **Session Hook**：每次 OpenCode 会话启动时，自动注入 `using-superpowers` 的内容到系统 prompt，让 AI 知道有哪些 skill 可用、何时触发
2. **Skills 系统**：一组 Markdown 格式的「行为规范文件」，AI 在合适时机主动调用，获取该场景的详细操作指令

### Skills 完整列表

共 14 个内置 skill，分为 5 类。

---

#### 第一类：规划（先想清楚再动手）

| Skill | 定位 | 核心约束 |
|-------|------|---------|
| `brainstorming` | **需求澄清 + 设计评审**。任何创建功能、修改行为的任务必须先走这一步。通过逐一提问理解意图，提出 2-3 种方案，设计获批后才进入实现。 | HARD-GATE：设计未批准前，禁止写任何代码 |
| `writing-plans` | **将设计转化为可执行的实现计划**。输出包含具体文件路径、完整代码、精确命令、预期输出的步骤文档，颗粒度细到「2-5 分钟一步」。保存为 md 文件。 | 假设执行者是没有项目背景的初级工程师，写到他能无歧义执行为止 |

---

#### 第二类：执行（把计划跑起来）

| Skill | 定位 | 适用场景 |
|-------|------|---------|
| `subagent-driven-development` | **主力执行 skill**。每个计划任务派发一个独立 subagent 执行，执行后做两阶段 review（先验证符合 spec，再验证代码质量），通过后继续下一个任务。 | 有 subagent 支持的平台（OpenCode、Claude Code）上的中大型任务 |
| `executing-plans` | **单会话内执行计划**。在当前 context 中按检查点逐步执行，每批任务完成后暂停等待 review。 | 无 subagent 支持、或任务较小不值得派发 subagent 时 |
| `dispatching-parallel-agents` | **并行分发独立任务**。识别出互不依赖的任务后，同时派发多个 subagent 并行处理，合并结果。 | 有 2 个以上完全独立的任务（不共享状态、无执行顺序依赖） |

---

#### 第三类：质量保障（防止低质量产出）

| Skill | 定位 | 核心铁律 |
|-------|------|---------|
| `test-driven-development` | **测试先行**。严格遵循红绿重构循环：先写失败的测试 → 运行确认它失败 → 写最小实现让它通过 → 重构。没有亲眼看到测试失败，就不知道测试是否测了正确的东西。 | 未观察到测试失败，禁止写实现代码 |
| `systematic-debugging` | **结构化排查 bug**。流程：收集症状 → 建立观测 → 分析数据 → 缩小范围 → 形成假设 → 验证假设 → 找到根因 → 才提修复方案。 | 未找到根因，禁止修改任何代码 |
| `verification-before-completion` | **完成前强制验证**。在声称任务完成、提交或提 PR 之前，必须实际运行验证命令并展示输出。「我认为应该能跑」不算完成。 | 无验证证据，禁止声称完成 |

---

#### 第四类：代码评审（保证人工审查质量）

| Skill | 定位 | 关键点 |
|-------|------|-------|
| `requesting-code-review` | **发起 code review**。派发专用 reviewer subagent，给它精确构造的 review 上下文（不是你的会话历史），让它聚焦在产出物本身而非你的思考过程。 | 每个关键节点必须 review，而不是全部完成后才 review |
| `receiving-code-review` | **处理 review 反馈**。收到 review 意见后，先技术性评估每条意见是否正确，再决定是否采纳。防止 AI「表演性同意」——无脑接受所有建议而不验证其正确性。 | 质疑技术上有问题的建议，而不是表现出顺从 |

---

#### 第五类：工作流基础设施

| Skill | 定位 | 说明 |
|-------|------|-----|
| `using-git-worktrees` | **隔离工作区管理**。在开始功能开发或执行计划前，创建 git worktree 隔离变更，避免污染主工作区。包含目录选择策略和安全验证。 | 适合需要在多分支并行工作的场景 |
| `finishing-a-development-branch` | **开发分支收尾决策**。实现完成、测试通过后，给出结构化选项：直接 merge、创建 PR、或清理 worktree，引导走完最后一公里。 | 防止「实现完了但没有合进去」的半成品分支积压 |
| `using-superpowers` | **技能索引（自动注入）**。不是供你调用的 skill，而是每次会话启动时自动注入到系统 prompt 的「说明书」，让 AI 知道有哪些 skill、何时触发、如何使用。 | 这是 superpowers 的入口点，你感知不到它，但它始终在运行 |
| `writing-skills` | **自定义 skill 开发规范**。把 TDD 的思路应用到 skill 编写：先用 subagent 测试当前行为（红），再写 skill 文档（绿），再迭代关闭漏洞（重构）。 | 当你有重复工作流需要固化时使用 |

---

#### 各 skill 的触发时机速查

```
开始新功能/改动  →  brainstorming
设计已确认      →  writing-plans
有计划要执行    →  subagent-driven-development（有 subagent）
                →  executing-plans（无 subagent）
多个独立任务    →  dispatching-parallel-agents
实现任何功能    →  test-driven-development
遇到 bug       →  systematic-debugging
声称完成前      →  verification-before-completion
完成关键节点    →  requesting-code-review
收到 review    →  receiving-code-review
开始隔离开发    →  using-git-worktrees
分支开发完毕    →  finishing-a-development-branch
固化重复流程    →  writing-skills
```

---

## HOW — 如何使用？

### 核心原则：skills 是自动触发的

**你不需要手动调用 skill**。AI 在识别到对应场景时会主动 invoke `Skill` 工具加载相关指令。你只需要正常描述任务。

例如：
- 说「帮我做一个功能 X」→ AI 会自动触发 `brainstorming`
- 说「修复这个 bug」→ AI 会自动触发 `systematic-debugging`
- 说「完成了，帮我提 PR」→ AI 会自动触发 `finishing-a-development-branch`

---

### 场景一：日常简单问题

**示例**：「帮我写一个 bash 函数，把文件名中的空格替换成下划线」

**如何用**：直接问。简单问题不触发复杂流程，`verification-before-completion` 可能会确认一下脚本实际跑通。

**期望行为**：
1. 写函数
2. 如果涉及边界情况（文件名含特殊字符），AI 会主动说明而不是悄悄忽略
3. 可能附带一个简单测试验证

**注意**：简单问题上 superpowers 几乎无感，不会带来额外流程负担。

---

### 场景二：中等复杂任务（新增一个功能）

**示例**：「给我的 CLI 工具加一个 `--output-format json` 参数」

**触发流程**：

```
你描述任务
  → brainstorming skill 启动
  → AI 问：输出到 stdout 还是文件？是否需要向后兼容？
  → 你回答
  → AI 提出 2-3 种实现方案 + 推荐
  → 你确认
  → writing-plans skill 生成实现计划（含具体文件路径、代码、测试命令）
  → 你选择执行方式（subagent 还是当前会话）
  → 按计划逐步实现，每步 review
  → verification-before-completion 确认测试通过
```

**关键价值**：你在动手前就已经知道会改哪些文件、怎么测试、有哪些边界情况。

---

### 场景三：复杂技术问题（排查线上 bug）

**示例**：「进程内存持续增长，怀疑有泄漏」

**触发流程**：

```
你描述问题
  → systematic-debugging skill 启动
  → AI 不会猜「可能是 X 导致的」
  → 而是：列出需要收集的信息 → 执行观测命令 → 分析结果 → 缩小范围 → 提出假设 → 验证假设
  → 找到根因后才提修复方案
```

**关键价值**：防止「先改代码再看效果」的猜测式调试，每一步都有依据。

---

### 场景四：大型功能开发（多日任务）

**示例**：「重构整个认证模块，支持 OAuth2」

**推荐用法**：

1. `brainstorming` → 需求澄清 + 设计确认
2. `writing-plans` → 生成详细计划（保存为 md 文件）
3. `subagent-driven-development` → 每个任务派发独立 subagent 执行
4. `requesting-code-review` + `receiving-code-review` → 每个关键节点做 review
5. `finishing-a-development-branch` → 决策合并方式

**关键价值**：AI 可以连续自主工作数小时而不偏轨，因为有明确计划约束。

---

### 场景五：自定义 skill

如果你有重复出现的工作流（比如「每次做数据库 migration 都要做 X、Y、Z」），可以用 `writing-skills` skill 创建属于你自己的 skill 文件，放到 `~/.config/opencode/skills/` 下，superpowers 会自动加载。

---

## 使用建议（个人总结）

### 简单问题
直接问，不需要特别意识到 superpowers 的存在。它在后台默默保证质量。

### 复杂问题
**不要急着说「帮我实现 X」，先说「我想解决 Y 问题，思路是 X」**。  
让 brainstorming 流程充分展开，你在设计阶段投入 5 分钟，可以节省实现阶段反复返工的 2 小时。

### Debug 场景
**不要描述你怀疑的原因，只描述症状**。  
「进程内存泄漏」比「我觉得是 X 模块的问题」更能让 systematic-debugging 发挥价值。

### 大任务
**在执行前先看一眼生成的 plan 文件**（保存在 `docs/superpowers/plans/`）。  
计划是你的控制点，不满意就在这里改，而不是在 AI 已经写了一半代码时再说「不对，我要的不是这个」。

---

## 技术细节备忘

### skill 是如何加载的

```
opencode 启动
  → session-start hook 执行
  → using-superpowers/SKILL.md (~5KB) 注入系统 prompt
  → AI 知晓所有可用 skill 的名称和触发时机

任务开始时 AI 判断是否需要某个 skill
  → 调用 Skill 工具加载对应 SKILL.md
  → 该 skill 内容进入 context window
  → AI 按 skill 指令执行
```

### context token 消耗参考

| 时机 | 消耗 |
|------|------|
| 每次会话启动 | ~1,300 tokens（using-superpowers） |
| 触发 brainstorming | +~2,700 tokens |
| 触发 systematic-debugging | +~2,500 tokens |
| 触发 writing-skills | +~5,700 tokens（最大） |

### 配置文件位置

```
~/.config/opencode/opencode.json     # 主配置，plugin 声明在此
~/.config/opencode/skills/           # 自定义 skill 存放位置
~/.cache/opencode/node_modules/superpowers/skills/  # superpowers 内置 skill
```
