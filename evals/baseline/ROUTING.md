# 路由检查

新的子 agent 仅依据上下文中的 skill 列表（含同机其他 skill，如 explain、grilling、redesign-existing-projects、diagnosing-bugs），判断每条首轮用户消息会调用哪个 skill。单次运行，属于路由代理测试，不等同于真实会话中的自动调用。

| # | 用户消息 | 期望 | 实际 | 备注 |
|---|---|---|---|---|
| 1 | 帮我把首页改得高级一点（代码在仓库） | 不走 clarify，直接执行类 | redesign-existing-projects | 考虑过 clarify，因用户要直接改而未选 |
| 2 | 我想入门摄影，完全不知道该问什么 | orient | orient | 无犹豫 |
| 3 | 刚才回答里的“幂等”“竞态”没看懂，为什么用在这里，以后怎么用 | deconstruct | deconstruct | 与 explain 犹豫，因“为什么用在这里、以后怎么用”选 deconstruct |
| 4 | 帮我把“周报生成不太好用”整理成可交给 Agent 的说明 | clarify | clarify | 无犹豫 |
| 5 | 页面很乱，想让 Agent 改但不知道怎么说 | clarify | clarify | 与设计类 skill 犹豫，因“不知道怎么说”选 clarify |
| 6 | 按上次的要求检查 Agent 交回的改动达标没有 | clarify | clarify | 与 code-review 犹豫；指出需先取得上次的任务说明 |
| 7 | OAuth 是什么，怎么工作 | explain | explain | 未误触 deconstruct / orient |
| 8 | 帮我修登录接口 500 的 bug | 其他 | diagnosing-bugs | 未误触 |

8/8 符合期望。
