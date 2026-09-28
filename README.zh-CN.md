<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# 给真正工程师的技能库（Skills For Real Engineers）

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

> [![English](https://img.shields.io/badge/docs-English-blue)](./README.md) | 简体中文

我每天用来做**真实工程**（而不是"凭感觉写代码"）的 AI 智能体技能。

开发真实的应用是很难的。GSD、BMAD、Spec-Kit 这类方法试图通过**接管整个流程**来帮你，但代价是夺走你的控制权，流程里出了 bug 也很难排查。

这些技能的设计目标是：**小、易改造、可组合**。它们适配任何模型，基于数十年的工程经验。随便改、改成你自己的、用得开心。

如果你想跟进这些技能的更新和我新做的技能，可以加入我 6 万多开发者的订阅通讯：

[订阅 Newsletter](https://www.aihero.dev/s/skills-newsletter)

## 安装（30 秒搞定）

两条路，两种哲学。**[Claude Code 插件](https://code.claude.com/docs/en/plugins)**把整套技能装成一个托管的只读包，随我发布自动更新——你是"订阅"而不是"复制"。**[skills.sh](https://skills.sh/mattpocock/skills)**则把可编辑的技能文件复制进你的项目，随便改、变成你自己的。**二选一**：两个都装会让你每个技能出现两份。

### 1. 拿到技能

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude plugins install mattpocock-skills
```

或者在会话里输入：

```
/plugin install mattpocock-skills
```

它就在 Claude Code 官方插件市场里，不需要先配置任何东西，更新自动到达。

</details>

<details>
<summary><strong>Codex 及其它智能体</strong></summary>

```bash
npx skills@latest add mattpocock/skills
```

选择你想要的技能，以及要装到哪些编码智能体上。**安装器允许你挑技能，务必把 `setup-matt-pocock-skills` 选上。**

原生 Codex 插件已在计划中（见 [`.agents/adr/0002-ship-as-a-claude-code-plugin.md`](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)）。

</details>

<details>
<summary><strong>给爱折腾的人</strong></summary>

用同一个安装器，装到任何智能体上，包括 Claude Code：

```bash
npx skills@latest add mattpocock/skills
```

它会把技能写成你仓库里的普通文件，归你所有、可以编辑。不会有任何东西在你背后偷偷更新；想要我的最新改动时，运行 `npx skills update` 拉取即可。

</details>

### 2. 运行 `/setup-matt-pocock-skills`

在你的智能体里，每个仓库运行一次。它会：

- 问你想用哪个工单系统（GitHub、Linear 或本地文件）
- 问你在分诊工单时打什么标签（`/triage` 依赖标签）
- 问你想把生成的文档存放在哪里

### 3. 完成，可以开工了。

## 这些技能为什么存在

我做这些技能，是为了修复我在 Claude Code、Codex 等编码智能体上看到的一些常见失败模式。

### #1：智能体没做我想要的

> "没有人能确切知道自己想要什么"
>
> David Thomas & Andrew Hunt，《程序员修炼之道》（The Pragmatic Programmer）

**问题**。软件开发中最常见的失败模式是"理解错位"。你以为开发者明白你要什么，然后看到他做出来的东西——才发现他完全没理解你。

AI 时代一模一样。你和智能体之间存在沟通鸿沟。解法是**"拷问"环节（grilling session）**——让智能体就你要做的东西，向你提出一大堆细节问题。

**解药**是使用：

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md) —— 非代码场景用
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md) —— 同 [`/grill-me`](./skills/productivity/grill-me/SKILL.md)，但附带更多好东西（见下文）

这是我最受欢迎的两个技能。它们帮你在动手之前与智能体对齐，并深入思考你要做的改动。**每次**想改东西都用它。

### #2：智能体太啰嗦

> 有了统一语言，开发者之间的对话和代码的表达都源自同一个领域模型。
>
> Eric Evans，《领域驱动设计》（Domain-Driven Design）

**问题**：项目初期，开发者和服务对象（领域专家）说的往往是两套语言。

我和我的智能体之间也有同样的隔阂。智能体通常被直接扔进一个项目，靠边干边猜术语。结果就是：能用 1 个词说清的事，它要用 20 个词。

**解药**是**共享语言**——一份帮智能体解码项目术语的文档。

<details>
<summary>
示例
</summary>

这是我 `course-video-manager` 仓库里的 [`CONTEXT.md`](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md) 示例。哪种更好读？

- **改前**："课程某小节里的课程（lesson）被'实体化'（即在文件系统里获得位置）时出了问题"
- **改后**："materialization 级联出了问题"

这种简洁会在之后的每一次会话里持续回报你。

</details>

它内建于 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md)：一次拷问环节，同时帮你和 AI 建立共享语言，并把难以解释的决策沉淀进 ADR（架构决策记录）。

这种能力有多强很难用语言说清。它可能是这个仓库里最酷的单项技术。试试看。

> [!TIP]
> 共享语言除了减少啰嗦，还有很多别的好处：
>
> - **变量、函数和文件的命名保持一致**——都用共享语言
> - 因此**代码库对智能体来说更容易导航**
> - 智能体**思考消耗的 token 也更少**，因为它掌握着一套更精炼的语言

### #3：代码跑不起来

> "永远采取小的、深思熟虑的步子。反馈的速度就是你的速度上限。永远不要接手过大的任务。"
>
> David Thomas & Andrew Hunt，《程序员修炼之道》（The Pragmatic Programmer）

**问题**：假设你和智能体已经对齐了要做什么。可智能体**还是**产出了垃圾代码，怎么办？

这时候该检查你的反馈回路了。如果智能体得不到"它写的代码实际运行得如何"的反馈，它就是在盲飞。

**解药**：你需要常规那套反馈回路——静态类型、浏览器访问、自动化测试。

自动化测试方面，红-绿-重构循环至关重要：智能体先写一个失败的测试，再修到通过。这给智能体提供了稳定水平的反馈，代码质量会好得多。

我做了一个可以装进任何项目的 **[`/tdd`](./skills/engineering/tdd/SKILL.md) 技能**。它强调红-绿-重构，并就"什么是好测试、什么是坏测试"给智能体大量指导。

调试方面，我还做了 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)** 技能，把最佳调试实践包装成一个有纪律的循环，逐阶段把守。

### #4：我们造了一个泥球（Ball of Mud）

> "**每天**都投资于系统的设计。"
>
> Kent Beck，《解析极限编程》（Extreme Programming Explained）

> "最好的模块是深的。它们让你通过一个简单的接口访问大量的功能。"
>
> John Ousterhout，《软件设计哲学》（A Philosophy of Software Design）

**问题**：用智能体造出来的大多数应用又复杂又难改。智能体能大幅加速写代码，也同样在加速软件的熵增。代码库以前所未有的速度变得复杂。

**解药**是一种全新的 AI 开发思路：**真正在乎代码的设计**。

这内建在这些技能的每一层里：

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md) 在生成规格之前，先盘问你这次要动到哪些模块

更关键的是 [`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md)，它会扫描整个代码库寻找"深化"机会并把候选清单交给你。我建议每隔几天在你的代码库上跑一次。它是**普查，不是救援**：在一个真正老旧的代码库上它能找到真实的候选点，但它不会替你把泥球解开。

### 小结

软件工程的基本功比以往任何时候都重要。这些技能是我把这些基本功浓缩成可重复实践的最佳努力，帮你交付职业生涯中最好的应用。祝用得开心。

## 参考（Reference）

这些技能按一个维度划分：**谁能调用它们**。**用户调用（user-invoked）**技能只有你亲手输入时才会触发（如 `/grill-me`），它们的职责是编排。**模型调用（model-invoked）**技能既可以由你调用，也会被智能体在任务匹配时自动取用，它们承载可复用的纪律。用户调用技能可以调用模型调用技能，但永远不会调用另一个用户调用技能。

### Engineering（工程类）

我每天写代码时用的技能。

**用户调用**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)**：问我哪个技能或流程适合你当前的情况。本仓库用户调用技能的路由器。
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)**：拷问环节，同时构建你项目的领域模型，就地打磨术语并更新 `CONTEXT.md` 与 ADR。
- **[triage](./skills/engineering/triage/SKILL.md)**：让 issue 按分诊角色的状态机流转。
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)**：扫描代码库寻找"深化"机会，以可视化 HTML 报告呈现，然后对你选中的那一条展开拷问。
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)**：为本仓库配置工程类技能（工单系统、分诊标签、领域文档布局）。使用其它工程技能前，每个仓库先运行一次。
- **[to-spec](./skills/engineering/to-spec/SKILL.md)**：把当前对话变成规格并发布到工单系统。不做访谈，只综合你们已经讨论过的内容。
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)**：把任何计划、规格或对话拆解成一组"曳光弹"工单，每张声明自己的阻塞关系，可以写成本地文件文本，也可以写成真实工单系统上的原生阻塞链接。
- **[implement](./skills/engineering/implement/SKILL.md)**：实现规格或工单描述的工作，在预先约定的接缝处驱动 `/tdd`，提交前以 `/code-review` 收尾。
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)**：规划超出单个智能体会话容量的一大块工作——在工单系统上建成一张共享的"决策工单地图"，逐个解决，直到通往终点的路完全清晰。

**模型调用**

- **[prototype](./skills/engineering/prototype/SKILL.md)**：造一个用完即弃的原型来回答设计问题——状态/逻辑问题用单个可分享的 HTML 文件，UI 问题则给出几个截然不同的变体、从一个路由里切换。
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)**：针对疑难 bug 和性能回归的纪律化诊断循环：建立"这个 bug 能变红"的反馈回路 → 最小化 → 假设 → 插桩 → 修复 → 回归测试。
- **[research](./skills/engineering/research/SKILL.md)**：以高可信度的一手来源调查某个问题，把发现连同引用写成仓库里的 Markdown 文件，以后台智能体方式运行。
- **[tdd](./skills/engineering/tdd/SKILL.md)**：红-绿-重构循环的测试驱动开发。一次一条垂直切片地构建功能或修复 bug。
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)**：主动构建并打磨项目的领域模型：用术语表挑战用词、用边界场景做压力测试，就地更新 `CONTEXT.md` 与 ADR。
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)**：设计"深模块"的共享纪律与词汇：大量行为藏在小小的接口后面、落在干净的接缝上、可以通过该接口测试。
- **[code-review](./skills/engineering/code-review/SKILL.md)**：对某个基准点以来的 diff 做双轴评审：**规范轴**（是否遵守仓库编码标准 + Fowler 坏味道基线？）与**规格轴**（是否忠实实现了源头 issue/规格？），由并行子智能体执行，互不污染。
- **[resolving-merge-conflicts](./skills/engineering/resolving-merge-conflicts/SKILL.md)**：逐块（hunk）处理进行中的 git merge/rebase 冲突，每一块都追溯到双方的原始出处、按意图解决，然后完成整个操作（**绝不** `--abort`）。
- **[wizard](./skills/engineering/wizard/SKILL.md)**：生成一个交互式 bash 向导，引导人类完成只有人能做的步骤：开通基础设施、配置凭据或 CI 密钥、走通陌生的第三方控制台、执行一次性的迁移或切换。

### Productivity（效率类）

通用工作流工具，不局限于代码。

**用户调用**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)**：就一个计划或设计接受无情拷问，直到设计树的每个分支都被解决。
- **[handoff](./skills/productivity/handoff/SKILL.md)**：把当前对话压缩成交接文档，让另一个智能体继续这项工作。
- **[teach](./skills/productivity/teach/SKILL.md)**：跨多个会话教用户一项新技能或概念，把当前目录用作有状态的教学工作区。
- **[to-questionnaire](./skills/productivity/to-questionnaire/SKILL.md)**：把你一个人答不了的决策变成 Markdown 问卷，交给唯一能回答的人异步填写，或在会议里一起过。它拷问的是"怎么发"（发给谁、要什么反馈），而不是问题本身。
- **[wait-what](./skills/productivity/wait-what/SKILL.md)**：一条消息没被听懂时立刻触发。智能体用你缺失的上下文、用 `CONTEXT.md` 的词汇、用大白话重新讲一遍。

**模型调用**

- **[grilling](./skills/productivity/grilling/SKILL.md)**：就一个计划、决策或想法无情拷问用户，直到设计树的每个分支都被解决。`grill-me`、`grill-with-docs`、`triage`、`wayfinder` 和 `improve-codebase-architecture` 背后可复用的访谈原语。
- **[writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md)**：为智能体写文档：技能、AGENTS.md/CLAUDE.md，以及任何智能体通过指针读取的文档。
