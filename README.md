# Articulate

把模糊想法，说成可执行的要求。

四个可以独立使用、共享同一知识方法的 Agent skills：

知识 → 领域语言 → 任务建模 → Agent 执行 → 专业评价。orient 和 explain 建立领域语言，clarify 做任务建模与评价，deconstruct 从专业输出反推领域语言。

| Skill | 何时使用 | 帮你获得什么 |
|---|---|---|
| [orient](skills/orient/SKILL.md) | 领域入门：进入陌生领域，不知道该问什么 | 八类领域地图、按五层与理解依赖排列的核心概念、向 Agent 提问的要素 |
| [clarify](skills/clarify/SKILL.md) | 任务建模：有具体任务，但只能用普通话描述 | 追问你的表达，按八类拆出专业人士会关注的要素、用五层讲清概念，写成专业说法和可执行、可验收的任务说明；可按同一说明验收产出 |
| [explain](skills/explain/SKILL.md) | 名词解释：遇到一个不懂的名词、概念、协议或技术 | 用五层讲清它：定义与机制、反事实与时间线、何时想到它、怎样判断用对；需要时给出向 Agent 表达它的方式。只问“是什么”时走短路径 |
| [deconstruct](skills/deconstruct/SKILL.md) | 专业拆解：看到专业输出，想读懂并学会这样说 | 用八类、五层拆出术语、结论与依据，识别误用与缺口，形成可迁移表达 |

## 安装

```sh
npx skills add isToThyMoon/articulate-skill
```

## 使用

在支持 `$skill` 调用的 Agent 中，例如：

```text
$orient 带我进入摄影领域。我没有项目，先让我理解全景。

$explain 幂等是什么？我给 Agent 写需求时怎么用它？

$clarify 这个页面感觉很乱，帮我讨论清楚，再整理成专业要求。

$deconstruct 拆解刚才的代码评审，告诉我这些概念为什么用在这里，以及以后怎样使用。

$clarify 按刚才那份要求验收这个改版，逐项给证据和结论。
```

也可以直接要求 Agent 使用对应 skill；具体调用界面取决于客户端。

`orient` 先交付领域总览、八类地图、贯穿案例和导航，再邀请你选择是否整理核心概念与学习顺序。`clarify` 不要求先学地图，每轮围绕关键歧义讨论；如果你说“直接整理，别追问”，就交付条件化描述并保留未知项。带来产物时，它按任务说明中的评价与失败模式逐项验收，给证据落点、结论和修改要求。

`deconstruct` 从现成材料出发，既解释原文的专业知识，也检查其使用条件和证据；不会把专业腔自动当作正确结论。

共同底层是八类知识覆盖、五层理解和来源交叉检查，而非几套互不相干的方法。专业术语是准确表达的工具，不是质量保证。四个 skill 都区分已知事实、候选解释和假设；交付的要求是可移交的，写目标状态与依据，而非罗列禁令。它们不记录学习进度或掌握等级，也不因生成任务说明而自动执行修改。

## 维护与验证

### 可选领域知识库

各入口可以把选定知识沉淀到同一个库：八类组织索引，五层组织条目，并保留来源、适用条件和可复用要求。它记录知识，不记录学习进度；只有用户要求时才保存，位置不明确时先确认。检索不自动修改知识库。

```text
$orient 把刚才的核心概念整理到 ./knowledge/ui，保留适用条件、关系和验收依据。
$clarify 用 ./knowledge/ui，把“页面专业一点”变成有依据的检查要求，别假定页面已经有什么问题。
$deconstruct 把这段评审中值得复用的知识加入 ./knowledge/ui；先检查已有条目，冲突先保留。
```

目标是“原始诉求 → 对象与证据 → 概念及关系 → 条件化选择 → 可执行要求与验收”，而非将形容词换成术语。

保存、调用、位置确认与增量更新的实际样本见 [知识库测试报告](evals/lexicon/REPORT.md)。

本仓库是四个 skill 的维护源；`orient`、`clarify` 与 `explain` 已从 `isToThyMoon/skills` 迁出。新增 skill 可放在 `skills/<name>/SKILL.md`，与现有技能并列。

共同方法编辑 [shared/foundation.md](shared/foundation.md)，知识库流程编辑 [shared/lexicon.md](shared/lexicon.md)，随后运行 `node scripts/sync-foundation.mjs` 生成各 skill 内的副本；用 `node scripts/sync-foundation.mjs --check` 检查一致性。副本随 skill 分发，单独安装不依赖仓库外路径或其他 skill。增加参与共享方法的 skill 时也需更新脚本中的名单。

`orient` 的[设计说明](docs/orient-design.md)与[测试报告](evals/orient/SOURCES-RETEST.md)保留了原始输出和已知局限。历史测试中的旧名 `domain-fluency` 指更名前的 `orient`；它们是历史记录，不代表当前路径。最新的[正向引导改写与行为测试](evals/guidance/REPORT.md)覆盖三个入口，区分首次输出与修订后复测。测试材料不等同于真实用户成效证明。

[有 skill / 无 skill 的盲评对照](evals/baseline/REPORT.md)覆盖三个入口及 UI、写作、园艺三个领域，每格单次运行，是小样本观察。

`deconstruct` 的[有界行为测试](evals/unpack-smoke.md)检查了离线拆解、概念误用与过度断言，包含原始输出和残余问题；不是完整可靠性验证。

后续[证据边界优化复测](evals/unpack-refinement.md)保留 UI 与写作两组首次失败及反馈后输出，用于检查改写是否凭空增加事实。

`deconstruct` 原名 `unpack`；历史测试文件和原始输出保留旧名称，不代表当前调用入口。
