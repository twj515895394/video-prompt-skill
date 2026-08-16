# Combat Action Reference Knowledge Spec

> 状态：**Implementation Ready / Knowledge Implemented / Runtime Wiring Frozen**  
> 日期：2026-08-16  
> 来源：用户补充的 18 个国风漫剧打斗动作素材 + 本轮 Grill Me 已确认决策  
> 目的：建立可被 Action Combat Stage-2 后续消费的“单动作级打斗参考知识库”设计真源。

---

# 0. 当前实施边界

本 Spec 已完成设计收敛，并已进入**知识本体实施**。

当前允许：

- 建立 Concrete Action Reference Catalog；
- 固化单动作 Schema；
- 完成 18 个动作逐条知识化；
- 建立本地目录索引；
- 做静态知识验证与去重检查。

RF-22 关闭前明确禁止：

- 修改 `SKILL.md` Runtime Direct READ；
- 修改 Action Combat Task Router；
- 修改 `regression-fix-runtime-policy.md`；
- 修改当前 `minimum-validation-set.md`；
- 把新 Catalog 加进 Stage-2 Mandatory Read；
- 增加默认 Library 加载预算；
- 修改 Quick Mode / Camera Runtime。

核心实施原则：

> **Knowledge First, Wiring Later.**

---

# 1. 核心定位

本知识库回答：

> **在当前 Combat State / Combat Role / Response Need 下，有哪些具体单动作候选；它们需要什么前提，会如何改变战斗状态与主动权，并能以什么物理夸张尺度和环境反馈被表现。**

它不是：

- 固定 Combo；
- 新 Battle Beat Engine；
- 新 Combat State Machine；
- Martial / Fighting Profile 的替代品；
- Camera Runtime；
- Visual Style Library；
- Prompt 大全。

它服务现有：

- Exchange Spine；
- Stage-2 Pattern Selection；
- Movement Causality；
- Per-Character Signature；
- Advantage / Re-entry；
- Concrete Action Phrase Resolution。

设计约束：

> **只保留能直接改善动作选择、动作因果、攻防节奏和最终画面执行的字段；不为了理论完整继续拆状态机。**

---

# 2. 知识颗粒度与分类

## 2.1 最小颗粒度

固定为：

> **Single Action Template / 单动作模板**

手、脚、肩胯、重心、支撑、接触点、轴线等属于动作内部属性，不再拆成独立知识节点。

连招不作为基础条目，只记录前后衔接关系，由 Runtime 按 Current State 动态组合。

原则：

> **动作是积木，连招由 Runtime 编排。**

## 2.2 一级分类

按动作主要战斗功能导航：

1. 突进接敌类；
2. 闪避走位类；
3. 格挡防御类；
4. 重击爆发类；
5. 腿法攻击类；
6. 空中动作类；
7. 贴身缠斗 / 近身快打类；
8. 武器瞬杀类；
9. 气劲 / 能量外放类。

一级分类用于知识导航，不等于 Combat Role。

---

# 3. Visual Medium 与 Physical Level 双轴解耦

## 3.1 Visual Medium

画面媒介与动作物理夸张程度完全独立。

可包括：

- 真人写实影视；
- 国风漫剧；
- 2D 动画；
- 3D 动画；
- 其他风格化媒介。

以下组合均合法：

```text
真人写实 + P1
真人写实 + P2
真人写实 + P3
国风漫剧 + P1
国风漫剧 + P3
```

即：

> **真人写实画面不等于现实物理。**

## 3.2 Physical Realization Level

### P1｜Grounded

- 现实人体重心、惯性、距离与受力为主；
- 允许有限电影强化；
- 不依赖明显气劲、长时间滞空或超自然位移。

### P2｜Cinematic Exaggerated

- 保留明确物理起点和动作因果；
- 允许强化速度、爆发、击飞与环境反馈；
- 可用于真人动作影视中的夸张武打。

### P3｜Hyper-Cinematic / Supernatural

- 允许残影、超高速位移感、明显滞空、长距离击飞、气劲、剑气、冲击波、地裂等；
- 仍要求动作方向、目标、状态变化和因果可读。

## 3.3 每个动作的 Physical Level Range

固定记录：

```text
Min Physical Level
Default Physical Level
Max Physical Level
```

定义：

- `Min`：不改变 Core Action Mechanic 时最低还能成立的等级；
- `Default`：无额外要求时最自然的等级；
- `Max`：不改变动作身份时允许强化到的最高等级。

Runtime 只能在合法范围内调整。

核心边界：

> **降低表现等级可以削弱速度、击飞、破坏和特效，但不能偷偷改变 Core Action Mechanic。**

例如：

```text
非接触震劲击退
Min = P3
```

不能为了 P2 把它自动改写成普通接触推掌；如果需要普通推掌，应是另一个动作。

---

# 4. Combat Role

正式收敛为 8 个核心枚举：

```text
Entry
Pressure
Defense
Counter
Re-entry
Reversal
Signature
Finisher
```

它只回答：

> **这一拍为什么现在需要这个动作？**

不再把以下内容继续塞进 Role：

- Range Change；
- Route Change；
- Base Disruption；
- Recovery。

这些已经由 State Transition / Tempo / Risk 表达。

Combat Role 是动作选择标签，不是固定流程模板。

---

# 5. Response Compatibility

采用轻量半结构化：

```text
Best Against
Poor Against
Best State
```

目的：提高“一攻一守”的真实匹配，而不是：

```text
A 发起攻击
→ B 随机抽一个 Defense
```

目标：

```text
Incoming State
→ Response Need
→ Compatible Action Candidate
```

不继续拆攻击方向、轨迹、速度、接触类型等复杂子状态机。

---

# 6. State Transition

采用：

> **Sparse Before → After / 稀疏状态变化**

只记录动作真正改变的维度，例如：

```text
Route: Frontal → Outside Angle
Balance: Stable → Disrupted
Range: Mid → Close
Initiative: Opponent → Steal
```

没有变化的字段不写。

可使用但不要求全部填写的维度：

```text
Range
Route
Axis
Position
Support
Balance
Contact
Advantage
Initiative
Environment
Height / Level
Weapon State
```

核心链：

```text
Current State
→ Action
→ State Transition
→ New Combat State
→ Next Action Selection
```

---

# 7. Initiative Effect

保留为轻量独立字段，正式值：

```text
Retain
Gain
Steal
Lose
Open Counter Window
Neutral
```

只有动作确实存在明显条件差异时才加一句自然语言，例如：

```text
蓄势重拳：命中通常 Gain / Retain；明显落空时 Open Counter Window。
```

不要求每个动作建立 On Hit / On Block / On Miss / On Evade 四套状态。

原则：

> **字段用于帮助选动作，不用于建立第二套战斗状态机。**

---

# 8. Tempo Profile

使用相对节奏，不绑定固定秒数。

当前可用表达包括：

```text
Instant
Quick Reactive
Burst
Sustained Rapid
Heavy
Build-up → Impact
Pause-and-Explode
Acceleration → Impact → Recovery
Recovery
```

目标是允许 Runtime 形成：

```text
Burst
→ Quick Reactive
→ Sustained Rapid
→ Heavy Pause
→ Reversal Burst
```

而不是机械的轮流出招。

---

# 9. Risk / Commitment Profile

记录动作投入程度与失手代价。

至少包括：

```text
Commitment: Low / Medium / High / Very High
Miss / Block Risk
Recovery Exposure
Payoff
```

核心联动：

```text
High Commitment Attack
→ Miss / Block / Evade
→ Recovery Exposure
→ Counter / Initiative Theft 候选权重提高
```

原则：

> **动作越重、路线越难改、恢复越慢，失败后越应该形成真实反击窗口。**

---

# 10. Prerequisites

只保留一个统一字段，不拆体型、柔韧、武器、环境等多个子系统。

它回答：

> **这个动作成立之前必须满足什么条件？**

例如：

- 拔刀斩：当前必须有可拔出的刀剑；
- 腾空旋转斩：必须有起跳、旋转和落地空间；
- 贴身快打：必须已经进入 Close Range；
- 落地震地重击：必须存在前序腾空 / 下落状态。

目的：阻止错误距离、无武器、无空间或无前序状态时硬塞动作。

---

# 11. Environment Impact

保留轻量字段，只回答：

> **当前动作在不同 Physical Level 下，典型可以造成什么可见环境反馈。**

不建立独立 Environment Destruction Engine，不建材质模拟器或破坏树。

例如：

```text
重拳 P2
→ 对手撞翻椅子 / 撞墙 / 局部裂纹

震地 P3
→ 地面龟裂 / 碎石 / 冲击波
```

核心原则：

> **环境反馈是动作结果的视觉延伸，不是独立表演。**

持久后果必须遵守现有 Aftermath / Continuity，不能下一拍无因 Reset。

---

# 12. 最终单动作 Schema

正式 Schema：

```text
id
canonical_name
aliases
functional_category
applicable_range
core_action_mechanic
body_contact_relation
immediate_visible_result
physical_level_range: Min / Default / Max
combat_role
response_compatibility: Best Against / Poor Against / Best State
state_transition
initiative_effect
tempo_profile
risk_commitment: Commitment / Miss-Block Risk / Recovery Exposure / Payoff
prerequisites
transition_compatibility: Good Before / Good After
environment_impact
risks_failure_modes
metadata
```

要求：

- 无意义字段允许省略；
- 不机械填满；
- Metadata 只负责辅助检索；
- Final Prompt 不直接输出内部 Schema 名。

---

# 13. 当前 18 个来源动作

已纳入 Catalog：

1. 极速瞬身突袭；
2. 凌空飞踢；
3. 反手格挡防御；
4. 蓄力重拳冲击；
5. 侧身闪避走位；
6. 腾空旋转斩击；
7. 低空滑步突袭；
8. 双臂交叉防御；
9. 后仰规避反击；
10. 横扫腿击；
11. 空中滞空连击；
12. 蓄力霸体冲击；
13. 侧身拔刀斩；
14. 后撤蓄力重击；
15. 抬手震气击退；
16. 灵活跳跃突袭；
17. 贴身缠斗快打；
18. 落地震地重击。

正式知识化正文见：

`references/libraries/combat-choreography-patterns/action-reference-catalog.md`

---

# 14. 与现有知识的职责边界

## Combat Fighting / Martial / Weapon Profiles

负责：

> 某 Combat System / Technique Backbone 通常怎样打。

## `minimum-validation-set.md`

负责：

> 当前 Stage-2 Gap 可以用哪类 Movement / Technique / Transition Pattern 解决。

## Action Reference Catalog

负责：

> 一个具体单动作怎样成立、适合何时用、会造成什么状态变化。

## Combat Environment Patterns

负责：

> 环境 Affordance 怎样改变路线 / Position / Range / Advantage。

## Styles

负责：

> 画面长什么样。

## Action Combat Task

负责：

> Battle State / Exchange Spine / Advantage / Coverage / Runtime 流程。

原则：

> **同一知识只保留一个正文真源。**

---

# 15. 当前实施结果

已创建：

- `references/libraries/combat-choreography-patterns/index.md`
- `references/libraries/combat-choreography-patterns/action-reference-catalog.md`
- `references/libraries/combat-choreography-patterns/action-reference-validation.md`

当前故意未修改：

- `SKILL.md`
- `references/libraries/index.md` 的正式运行路由
- `references/tasks/action-combat-video/index.md`
- `references/tasks/action-combat-video/regression-fix-runtime-policy.md`
- `references/libraries/combat-choreography-patterns/minimum-validation-set.md`

因此当前 Catalog：

> **Implemented, indexed locally, statically validated, but NOT runtime-wired.**

---

# 16. Runtime Wiring 前置条件

只有 RF-22 固定 G01 连续两次 `PASS-NATIVE` 后，才进入下一实施分支：

1. Pattern → Concrete Action Selection Policy；
2. Catalog Loading / Routing；
3. Library Detail Budget；
4. 与 Persistent Combat Signature 的权重关系；
5. Runtime Regression Cases；
6. Final Prompt Concrete Action Resolution 验证。

RF-22 未关闭前不提前实施这些内容。
