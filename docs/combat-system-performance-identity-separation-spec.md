# Combat System × Performance Identity Separation Spec

> 状态：设计中（Grill-Me 逐分支确认）
> 日期：2026-08-15
> 背景：G01 最新真实 Interactive 回归暴露出 `职业杀手` 与 `Fighting Direction / Combat System` 混层问题。

## 1. 已确认问题

当前 Interactive 候选曾把：

- `现代职业杀手近身格斗`
- `综合格斗 / MMA`
- `中国武术电影化近身格斗`

放在同一 Fighting Direction 层级。

这会把人物身份 / 题材语义错误地当成技法体系。真实运行中因此出现：用户输入“两名职业杀手”后，系统推荐“现代职业杀手短打”，从而让固定 G01 的 MMA 基线发生漂移。

## 2. 已确认原则：身份与技法体系分离

正式拆分为两个正交维度：

```text
Character / Performance Identity
职业杀手、特工、警察、街头人物、竞技选手、武术宗师……
        ↓ 不直接决定
Combat System / Technique Backbone
MMA、太极、咏春、八极、泰拳、拳击、柔术、散打……
        ↓
Performance Modifier
效率感、杀意、克制、凶狠、试探感、竞技感、表演性……
        ↓
Final Choreography
```

核心约束：

> Character / Performance Identity ≠ Combat System / Technique Backbone。

职业、身份、年龄、性别、外貌、体型都不能直接映射成固定技法体系。

例如以下组合全部合法：

- 职业杀手 + MMA
- 职业杀手 + 太极
- 职业杀手 + 咏春
- 职业杀手 + 八极
- 职业杀手 + 柔术

“职业杀手”可以影响动作表现气质、决策效率、杀意、冗余程度和战术意图，但不能自动变成 Tactical Close Combat / 短打 / 抱控。

## 3. 已确认 Interactive 策略：固定拆成两轮

用户明确选择：**A — 两轮交互。**

目的：相比内部静默组合，优先通过额外交互更准确地了解用户真实创作需求。

当前确认的两层结构：

```text
Round 1：Combat System / Technique Backbone
→ 这场战斗具体使用什么格斗 / 武术体系

Round 2：Performance Identity / Combat Expression
→ 这些技法以什么人物战斗气质、意图和表现方式呈现
```

这两轮属于不同 Primary Planning Node，不允许重新混成一个组合候选轴。

## 4. Interaction 原则

- 每轮仍然只问一个问题；
- Round 1 不提前替用户决定人物战斗气质；
- Round 2 不允许反向偷改已确认 Combat System；
- Performance Identity 只能修改同一技法体系的表现方式，不能把它替换成另一套武术 / 格斗体系；
- 系统应把两轮结果在 Runtime 内组合，而不是在候选层提前捆绑。

## 5. 已确认：Combat System 属于角色级属性

用户明确选择：**B — 每个角色独立定义 Combat System / Technique Backbone。**

因此 Combat System 不再被建模为“整场战斗只有一个体系”，而是绑定到具体 Combatant：

```text
Combatant A → Combat System A
Combatant B → Combat System B
...
```

允许：

- 双方使用相同体系：`太极 vs 太极`；
- 双方使用不同体系：`太极 vs MMA`；
- 多人场景中不同角色拥有不同体系；
- 用户只指定其中一方时，另一方继续保持未决，按 Interactive / Quick 规则处理。

因此 `Technique Backbone` 与后续 `Persistent Combat Signature` 应优先按角色维护，而不是整场共享一个固定 Fighting Profile。

角色的 Combat System 仍然不能由职业、性别、年龄、外貌、体型自动决定。

## 6. 已确认：Performance Identity / Combat Expression 也属于角色级属性

用户明确选择：**B — 每个角色独立定义 Performance Identity / Combat Expression。**

因此第二轮不再只给整场战斗设置一个统一“职业杀手式 / 竞技式 / 街头式”气质，而是允许每个 Combatant 拥有独立的战斗表达：

```text
Combatant A
→ Character / Narrative Identity A
→ Combat System A
→ Combat Expression A

Combatant B
→ Character / Narrative Identity B
→ Combat System B
→ Combat Expression B
```

例如双方即使都是职业杀手、也都使用太极，仍可以表现为：

```text
A：职业杀手 + 太极 + 冷静克制 / 诱导 / 借力后突然致命
B：职业杀手 + 太极 + 主动压迫 / 连续抢攻 / 更凶狠直接
```

也允许身份相同但 Combat System 和 Combat Expression 都不同，例如：

```text
A：职业杀手 + 太极 + 冷静诱导
B：职业杀手 + MMA + 强压迫抢攻
```

因此 Runtime 后续应维护角色级三元组：

```text
Character / Narrative Identity
× Combat System / Technique Backbone
× Combat Expression / Performance Identity
```

其中：

- `Character / Narrative Identity` 回答“这个人是谁 / 在剧情里是什么身份”；
- `Combat System` 回答“这个人主要用什么技法体系解决战斗”；
- `Combat Expression` 回答“这个人怎样使用这套体系，表现出怎样的意图、节奏、主动权策略与人物气质”。

三者互相影响最终 Choreography，但禁止任何一层直接吞并或替代另一层。

## 7. 待确认设计分支

当前仍需继续 Grill-Me：

1. 用户输入已经明确其中某一层时，固定两轮是否仍重复确认，还是把该轮改成确认 / 精炼；
2. Combat Branch（Modern / Wuxia）与 Combat System 的关系和路由顺序；
3. Fighting Direction 旧概念是否重命名、拆解或降级为内部组合结果；
4. G01 回归基线如何迁移到新两轴 / 角色级三元组结构。

在上述依赖分支达成共识后，再统一修改 Runtime / Interactive Contract / Choreography / Router，避免边讨论边产生半完成语义。