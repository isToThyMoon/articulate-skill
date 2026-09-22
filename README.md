# Articulate

把模糊想法，说成可执行的要求。

两个可以独立使用的 Agent skills：

| Skill | 何时使用 | 帮你获得什么 |
|---|---|---|
| [orient](skills/orient/SKILL.md) | 进入陌生领域，不知道该问什么 | 领域地图、核心概念与关系、工作流和评价标准，以及按理解依赖组织的学习路径 |
| [clarify](skills/clarify/SKILL.md) | 已有感觉或诉求，但说不清楚 | 通过关键追问澄清意图，形成领域化问题描述和可执行、可验收的要求 |

## 安装

```sh
npx skills add isToThyMoon/articulate-skill
```

## 使用

在支持 `$skill` 调用的 Agent 中，例如：

```text
$orient 带我进入 UI 设计领域。我没有项目，先让我理解全景。

$clarify 这个页面感觉很乱，帮我讨论清楚，再整理成专业要求。
```

也可以直接要求 Agent 使用对应 skill；具体调用界面取决于客户端。

`orient` 先交付领域总览、八类地图、贯穿案例和导航，再邀请你选择是否整理核心概念与学习顺序。`clarify` 不要求先学地图，每轮围绕关键歧义讨论；如果你说“直接整理，别追问”，就交付条件化描述并保留未知项。

专业术语是准确表达的工具，不是质量保证。两个 skill 都区分已知事实、候选解释和假设，不记录学习进度或掌握等级，也不因生成任务说明而自动执行修改。

## 维护与验证

本仓库是 `orient` 与 `clarify` 的维护源，已从 `isToThyMoon/skills` 迁出。新增 skill 可放在 `skills/<name>/SKILL.md`，与现有技能并列。

`orient` 的[设计说明](skills/orient/DESIGN.md)与[测试报告](skills/orient/evals/SOURCES-RETEST.md)保留了原始输出和已知局限。历史测试中的旧名 `domain-fluency` 指更名前的 `orient`；它们是历史记录，不代表当前路径。`clarify` 目前完成格式检查，尚未进行独立行为实测。测试材料不等同于真实用户成效证明。
