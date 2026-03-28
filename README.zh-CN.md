# Research Skills

一组面向 Codex / Claude Code 的按研究目的拆分的 research skills。

这个仓库最初只有一个 `researcher` skill，现在已经升级成一个小型 research
skill system：

- 一个共享 core 和总入口 skill
- 多个按搜索目的拆分的 skill
- 一组共享 references，用来定义证据类型、查询策略和反证路径

[English](README.md) | 中文

## 这套仓库是干什么的

它适合处理这类研究任务：

- 问题开放，不是一条链接就能回答
- 来源很多，而且经常互相矛盾
- 最终需要判断，不只是摘录资料
- 很容易被 hype、单边叙事、浅层总结带偏

整套方法保留了原来“先广后深”的核心思想，但把它升级成了“证据驱动的调查流程”：

```text
FRAME -> MAP -> FRONTIER -> DEEPEN -> CHALLENGE -> SYNTHESIZE
```

这意味着：

- 第一轮不是堆网页，而是建证据地图
- 后续搜索不是改关键词，而是沿线索推进
- 重要结论必须经过支持路径、反证路径和外显日志

## 包含哪些 Skills

| Skill | 适用场景 |
|---|---|
| `researcher` | 当问题比较模糊，需要先路由研究模式并运行共享 research OS |
| `field-mapping-research` | 先摸清一个领域、赛道、问题空间的地图 |
| `claim-validation-research` | 验证某个 claim、报告、数据、说法是否站得住 |
| `decision-support-research` | 为真实决策做研究，比较选项并给建议 |
| `opportunity-research` | 找机会、找增长点、找值得下注的方向 |
| `due-diligence-research` | 做公司/产品/叙事的压力测试和尽调 |
| `operator-reality-research` | 看一线从业者真实体验、隐藏摩擦和社区现实 |

## 设计核心

### 1. 先按搜索目的分，不按主题分

顶层 skill 不是按“搜论文 / 搜工作 / 搜公司”来切，而是按“为什么要搜”来切。

因为一个真实问题经常同时跨很多来源。

比如：

`“AI agent engineer 到底是不是一个真实的 entry-level 路径？”`

这不是单纯的招聘问题，它可能同时需要：

- 精确标题岗位
- 相邻标题岗位
- 公司 career page
- LinkedIn 职业轨迹
- Reddit / forum 真实体验
- 反方或怀疑路径

### 2. 不再只用单一 source hierarchy

共享 references 把互联网看成一个混合证据环境，而不是简单的“权威来源列表”。

核心 source classes 包括：

- official
- behavioral
- operator
- lived experience
- adversarial
- market proxy
- artifact

这样就不会：

- 把官方来源直接当成事实本身
- 把 Reddit / X / LinkedIn / 做空报告直接排除掉

### 3. 强制外显推理

每个 skill 都要求在执行中维护 `research-{topic}.md`，把研究路径写出来。

目标很明确：避免“搜了很多，但看不到推理过程”。

## 仓库结构

```text
researcher-skill/
├── README.md
├── README.zh-CN.md
├── researcher/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
│       ├── core-method.md
│       ├── frontier-management.md
│       ├── query-shaping.md
│       ├── saturation-and-counterevidence.md
│       ├── scientific-literature.md
│       ├── source-hierarchy.md
│       ├── source-packs-company-intel.md
│       ├── source-packs-field-signals.md
│       └── source-packs-jobs.md
├── field-mapping-research/
├── claim-validation-research/
├── decision-support-research/
├── opportunity-research/
├── due-diligence-research/
└── operator-reality-research/
```

## 它们怎么协作

`researcher/` 是共享 core：

- 总入口 skill
- 核心工作流
- source hierarchy
- query shaping
- challenge path 逻辑
- 各类 source packs

其他 purpose-specific skills 刻意写得更薄：

- trigger 更清晰
- workflow 更聚焦
- 通过 `../researcher/references/...` 复用共享方法

这样做的好处是：

- 共享方法统一维护
- 各 skill 可以按研究目的单独调优
- 不会把一个 skill 写成巨大的万能 prompt

## 安装方式

### 本地安装

先克隆仓库：

```bash
git clone https://github.com/recomby-ai/researcher-skill.git
```

然后把所有 skill 目录一起复制到你的 Codex / Claude skill 目录：

```bash
cp -R researcher-skill/researcher ~/.codex/skills/
cp -R researcher-skill/field-mapping-research ~/.codex/skills/
cp -R researcher-skill/claim-validation-research ~/.codex/skills/
cp -R researcher-skill/decision-support-research ~/.codex/skills/
cp -R researcher-skill/opportunity-research ~/.codex/skills/
cp -R researcher-skill/due-diligence-research ~/.codex/skills/
cp -R researcher-skill/operator-reality-research ~/.codex/skills/
```

如果你用的是 Claude Code，就复制到 `~/.claude/skills/`。

注意：

- `researcher/` 必须和其他 purpose skills 一起安装
- 因为共享 references 都在 `researcher/` 里面

### 网页版上传

如果你要上传到网页版，请把多个 skill 目录一起打包成 zip。

至少要包含：

- `researcher/`
- `field-mapping-research/`
- `claim-validation-research/`
- `decision-support-research/`
- `opportunity-research/`
- `due-diligence-research/`
- `operator-reality-research/`

不要只上传某一个 purpose-specific skill 而不带 `researcher/`，否则共享
references 会缺失。

## 使用示例

```text
Use $field-mapping-research to map the AI agent engineering job market.
Use $claim-validation-research to verify whether this industry claim holds up.
Use $decision-support-research to compare quant, AI infrastructure, and applied ML for a math undergraduate.
Use $opportunity-research to identify the most promising wedges in vertical AI for SMBs.
Use $due-diligence-research to stress-test this startup narrative.
Use $operator-reality-research to find what practitioners actually complain about in production agent systems.
Use $researcher to investigate what is really happening here and choose the right research mode.
```

## 当前这版重点修了什么

这次重构主要是为了修掉几个常见问题：

- 只会泛搜，不会沿线索深追
- 只找支持证据，不主动找反证
- 招聘/市场研究被岗位标题表面带偏
- 搜了很多，但推理过程不可见

所以现在这些 skill 会明确推动：

- breadth-first 的证据建图
- 可见研究日志
- exact-title 和 adjacent-title 并查
- 把社区信号、对抗性材料和 operator 视角正式纳入研究

## 局限

- 仍然受限于当前搜索和抓取工具能访问到的公开网页
- 某些来源会被登录、平台限制或付费墙挡住
- 社区/社交来源很有价值，但仍然需要交叉验证
- 这些 skill 是研究方法增强，不是领域知识的替代品

## License

MIT
