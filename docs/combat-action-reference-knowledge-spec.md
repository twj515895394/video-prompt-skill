# Combat Action Reference Knowledge Spec

> 状态：Draft / Grill in Progress  
> 日期：2026-08-16  
> 来源：用户补充的《AI漫剧打斗动作提示词大全》6 张图片 + 本轮 Grill Me 确认决策  
> 目的：建立一套可被 Action Combat Runtime / Stage-2 选择与组合的“单动作级打斗参考知识库”设计真源。当前文件只记录已经确认的知识建模与字段设计，不提前实现 Runtime，不修改 RF-22 既有回归逻辑。

---

## 0. 核心定位

本知识库不是固定连招模板、漫剧专属 Prompt 大全、武术门派百科，也不是新的 Combat Engine / Camera / Physics Runtime。

它回答：

> **在当前 Combat State / Combat Role / Response Need 下，有哪些可执行的单动作候选，它们会如何改变战斗状态，并能以什么视觉媒介与物理夸张尺度被表现。**

它服务现有 Exchange Spine / Stage-2 / Movement Causality / Per-Character Signature / Advantage / Re-entry，而不是取代这些机制。

---

# A. 知识库结构

## A1. 一级分类：按战斗功能分类

当前一级分类：

1. 突进接敌类；
2. 闪避走位类；
3. 格挡防御类；
4. 重击爆发类；
5. 腿法攻击类；
6. 空中动作类；
7. 贴身缠斗 / 近身快打类；
8. 武器瞬杀类；
9. 气劲 / 能量外放类。

一级分类用于检索和导航，不等同于固定 Combat Role；同一动作可以承担多个 Combat Role。

## A2. 最小颗粒度：单动作模板

> **知识库最小颗粒度固定为“单动作模板”，不再继续拆成手部、脚步、肩胯等更细独立节点。**

脚步、接触面、重心、轴线、支撑、发力、目标部位等只作为单动作内部属性。

连招不作为基础知识条目，而由：

- 可衔接前置动作；
- 可衔接后续动作；
- 常见组合关系；
- Runtime 动态 Exchange 编排；

共同形成。

原则：

> **动作是积木，连招由 Runtime 根据当前 State 动态编排。**

---

# B. 单动作条目基础字段

基础字段至少包含：

1. Action Name / 动作名称
2. Aliases / 别名
3. Functional Category / 动作功能分类
4. Applicable Range / 适用距离
5. Core Action Mechanic / 核心动作机制
6. Body & Contact Relation / 关键身体与接触关系
7. Immediate Visible Result / 立即可见结果
8. Style Realization / 风格表现
9. Transition Compatibility / 可衔接前置与后续动作
10. Risks & Failure Modes / 使用风险与避免事项

“核心关键词”降级为检索 Metadata，可由条目内容自动归纳。

随着 Grill 深入，下列属于高价值结构化属性，最终字段表会统一重排，不受最初 10 字段编号限制：

- Physical Level Range
- Combat Role
- Response Compatibility
- State Transition
- Tempo Profile
- Risk / Commitment Profile
- Initiative Effect
- Prerequisites

---

# C. 视觉媒介与动作物理解耦

## C1. 双轴模型

> **Visual Medium 与 Physical Realization Level 完全解耦。**

Visual Medium 只描述画面媒介，例如：

- 真人写实影视；
- 国风漫剧；
- 二维动画；
- 三维动画；
- 其他风格化媒介。

因此以下组合均合法：

```text
真人写实影视 + P1 Grounded
真人写实影视 + P2 Cinematic Exaggerated
真人写实影视 + P3 Hyper-Cinematic / Supernatural
国风漫剧 + P1 Grounded
国风漫剧 + P3 Hyper-Cinematic / Supernatural
```

真人写实画面不等于只能使用现实物理。

## C2. Physical Realization Level

### P1｜Grounded

- 重心、惯性、距离、受力基本遵循现实人体物理；
- 可电影化，但不出现明显超现实位移、滞空、气劲外放。

### P2｜Cinematic Exaggerated

- 仍有清晰物理起点和动作因果；
- 允许显著强化速度、爆发、击飞、环境反馈和视觉冲击；
- 仍保持真人动作片可感知的重量与接触感。

### P3｜Hyper-Cinematic / Supernatural

- 允许残影、超高速瞬移感、长距离击飞、滞空、气劲、冲击波、剑气、地面崩裂等非现实表现；
- 仍必须保持方向、目标、动作前后因果和战斗状态可读。

## C3. 每个动作的合法物理区间

每个动作记录：

- **Min Physical Level**
- **Default Physical Level**
- **Max Physical Level**

定义：

```text
Min
= 保持 Core Action Mechanic 不变时，最低还能成立的表现等级

Default
= 无额外要求时最自然、最典型的等级

Max
= 不改变动作身份时允许强化到的最高等级
```

Runtime 只能在合法区间内选级：

```text
Min ≤ Selected Physical Level ≤ Max
```

示意：

```text
侧身闪避走位
Min P1 / Default P1 / Max P2

极速瞬身突袭
Min P1 或 P2（逐条知识化时确定） / Default P2 / Max P3

落地震地重击
Min P2 / Default P2 / Max P3

抬手震气击退
若 Core Mechanic 是“不接触目标、靠掌劲 / 气浪直接震退”
Min P3 / Default P3 / Max P3
```

核心边界：

> **降低 Physical Level 可以削弱速度、破坏、击飞和特效，但不能改变 Core Action Mechanic。若为了降级必须把气劲震退改成普通推掌，就已经是另一个动作。**

---

# D. Combat Role / 战斗功能角色

每个动作增加多值 `Combat Role`，用于描述它在当前 Exchange 中承担的战术作用。

当前候选包括但不限于：

```text
Entry
Defense
Counter
Pressure
Re-entry
Range Change
Route Change
Base Disruption
Reversal
Signature
Finisher
Recovery
```

规则：

- 一个动作可以有多个 Role；
- Role 是知识属性，不是固定 Battle Beat 模板；
- Runtime 根据 Current State 选择 Role，不为凑流程机械轮换。

目标：

> 从“随机挑一个好看的动作”升级为“当前战斗需要什么功能，再选动作”。

---

# E. Response Compatibility / 攻防响应关系

它回答：

> **这个动作最适合回应什么类型的攻击、接触关系或战斗状态？**

示意：

```text
侧身闪避走位
Role: Defense / Route Change
优先响应：直线突进、重拳、正面抓抱入口
不优先：已经建立的贴身抱控、大范围封锁型横扫

双臂交叉防御
Role: Defense
优先响应：正面重击、下劈、爆发冲击
代价：通常仍保留正面对线，容易继续承受 Pressure

横扫腿击
Role: Counter / Base Disruption
优先条件：对方重心前压、承重脚明确、突进刚落脚
```

目标链：

```text
Incoming Attack / Current State
→ Response Need
→ Compatible Action Candidate
```

而不是：

```text
A 发起任意攻击
→ B 随机抽一个 Defense
```

---

# F. State Transition / 战斗状态变化

一个动作执行后，只记录它真正改变的状态维度，例如：

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
```

无需每个动作全部填写。

核心链：

```text
Attack / Current State
→ Response Action
→ State Transition
→ New Combat State
→ Next Action Selection
```

示意：

```text
侧身闪避走位
→ Route changed
→ Axis changed
→ Outside angle created
→ Counter window opened

双臂交叉防御
→ Contact absorbed / blocked
→ Range mostly unchanged
→ Axis mostly unchanged
→ Defender may still be under pressure

横扫腿击
→ Support disrupted
→ Balance reduced
→ Forced step / fall risk
→ Initiative window opened
```

该字段直接服务 Movement Causality / Exchange Spine / Advantage Runtime。

---

# G. Tempo Profile / 节奏特征

Tempo 不绑定固定秒数，只描述相对节奏作用。

当前候选包括：

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

示意：

```text
侧身闪避走位
Quick Reactive

极速瞬身突袭
Burst

蓄力重拳冲击
Build-up → Impact

贴身缠斗快打
Sustained Rapid

落地震地重击
Acceleration → Impact → Recovery
```

Runtime 可据此形成：

```text
Burst
→ Quick Reactive
→ Sustained Rapid
→ Heavy Pause
→ Reversal Burst
```

而不是简单轮流出招。

---

# H. Risk / Commitment Profile / 风险与动作承诺度

该字段回答：

> **角色一旦开始执行这个动作，需要投入多少路线、重心和恢复成本；如果被闪避、格挡或打断，会暴露多大的反击窗口；命中后的回报又有多大。**

至少包含：

```text
Commitment: Low / Medium / High / Very High
Miss / Block Risk
Recovery Exposure
Payoff
```

示意：

```text
侧身闪避走位
Commitment: Low
Recovery Exposure: Low
Payoff: Route Change / Counter Window

极速瞬身突袭
Commitment: Medium
Miss Risk: Medium
Recovery Exposure: 前冲落空后可能短暂暴露
Payoff: 快速压缩距离 / 抢 Entry / Pressure

蓄力重拳冲击
Commitment: High
Miss / Block Risk: High
Recovery Exposure: 蓄势与空挥后恢复较慢
Payoff: High Impact / 强制位移 / Advantage Shift

腾空旋转斩击
Commitment: Very High
Miss Risk: High
Recovery Exposure: 空中路线难改，落地存在恢复窗口
Payoff: Signature / Finisher / 高视觉收益
```

联动：

```text
High Commitment Attack
→ Miss / Block / Evade
→ Recovery Exposure Opened
→ Counter / Initiative Theft 候选权重上升
```

主动权翻转应尽量来自动作本身的承诺度和失手代价，而不是人为硬安排。

---

# I. Initiative Effect / 主动权影响

已确认增加，但必须保持**轻量**，不建立复杂结果状态机。

基础枚举：

```text
Retain
Gain
Steal
Lose
Open Counter Window
Neutral
```

用途：让 Runtime 快速判断动作通常怎样影响主动权，而不必每次从完整 State Transition 重新推导。

示意：

```text
双臂交叉防御
Initiative Effect: Opponent Retains Pressure / Neutral

横扫腿击
Initiative Effect: Steal

后仰规避反击
Initiative Effect: Steal / Gain
```

仅当动作确实存在非常明显的条件差异时，允许补一条简短自然语言条件，例如：

```text
蓄力重拳冲击
通常命中：Retain / Gain
明显落空：Open Counter Window / Lose
```

但**不要求每个动作机械拆成 On Hit / On Block / On Miss / On Evade 四套分支**。

原则：

> **Initiative Effect 是选动作的轻量辅助，不是第二套 Combat State Machine。**

---

# J. Prerequisites / 使用条件

已确认增加一个统一的 `Prerequisites` 字段，不再拆成体型、柔韧、武器、环境等多套子字段。

它只回答：

> **这个动作成立之前，必须满足什么最小条件？**

示意：

```text
侧身拔刀斩
→ 当前持有 / 佩戴可拔出的刀剑

腾空旋转斩击
→ 有足够起跳、旋转与落地空间；需要对应武器

贴身缠斗快打
→ 已进入近身距离

横扫腿击
→ 目标腿部 / 支撑区域可达

落地震地重击
→ 当前存在落地阶段；环境材质允许当前 Physical Level 对应反馈

凌空飞踢
→ 有起跳空间与可落地区域
```

它用于避免：

```text
隔着很远 → 突然贴身缠斗
没有刀 → 突然拔刀
狭小空间 → 无条件巨大腾空旋转
人物仍在地面 → 下一拍直接“落地震击”
```

原则：

> **Prerequisites 只保存动作成立的必要条件，不演变成角色能力数值系统。**

---

# K. 当前图片来源动作清单（待逐条知识化）

当前 6 张图片共提供 18 个原始动作：

1. 极速瞬身突袭
2. 凌空飞踢
3. 反手格挡防御
4. 蓄力重拳冲击
5. 侧身闪避走位
6. 腾空旋转斩击
7. 低空滑步突袭
8. 双臂交叉防御
9. 后仰规避反击
10. 横扫腿击
11. 空中滞空连击
12. 蓄力霸体冲击
13. 侧身拔刀斩
14. 后撤蓄力重击
15. 抬手震气击退
16. 灵活跳跃突袭
17. 贴身缠斗快打
18. 落地震地重击

后续知识化要求：

- 原图名可以保留为 Alias；
- 可建立更中性的 Canonical Action Name；
- 气流、灵气、剑气、地裂、残影等不能无脑写进 Core Mechanic；
- 必须区分动作核、视觉表现、Physical Level、Combat Role、Response Compatibility、State Transition、Tempo、Risk / Commitment、Initiative Effect、Prerequisites。

---

# L. 已确认设计决策清单

截至当前 Grill：

1. 按战斗功能分类，不按 1～18 原编号平铺；
2. 单动作模板是最小知识颗粒度；
3. 连招由 Transition Compatibility + Runtime 动态组合；
4. 关键词降级为 Metadata；
5. Visual Medium 与 Physical Realization Level 双轴解耦；
6. P1/P2/P3 只描述动作物理与夸张尺度，不代表真人或动画；
7. 真人写实媒介允许 P3 超现实武打；
8. 每个动作记录 Min + Default + Max Physical Level；
9. 降低 Physical Level 不允许改变 Core Action Mechanic；
10. 增加多值 Combat Role；
11. 增加 Response Compatibility；
12. 增加 State Transition；
13. 增加 Tempo Profile，不绑定固定秒数；
14. Combat Role + Response Compatibility + State Transition 用于提高攻防匹配与节奏；
15. 增加 Risk / Commitment Profile；
16. High Commitment 动作失败后应自然提高 Counter / Initiative Theft 候选权重；
17. 增加轻量 Initiative Effect；
18. Initiative Effect 不拆成强制 On Hit / On Block / On Miss / On Evade 状态机；
19. 增加统一 Prerequisites 字段，不拆多套能力 / 环境子系统；
20. 本知识库服务现有 Combat Runtime，不新建第二套战斗 Engine。

---

# M. 尚未确认 / 后续 Grill

后续只讨论对实际动作生成有直接价值的分支，避免过度设计：

- Combat Role 的正式枚举是否需要继续收敛；
- Response Compatibility 是否保持自然语言即可；
- State Transition 是否保持轻量描述即可；
- P2 / P3 的环境破坏如何表达；
- 18 个动作逐条知识化后的去重、Canonical Name 与 Alias；
- 最终 `references/libraries/` 目录结构与加载预算；
- 与现有 `combat-choreography-patterns` / fighting / martial libraries 的职责边界；
- Regression / Minimum Validation Set。

---

## 当前原则

> **先确定动作在战斗中“为什么现在用”，再决定“用哪个动作”。**
>
> **先确定动作核，再决定视觉媒介和合法的 Min → Default → Max 物理表现区间。**
>
> **一攻一守不是轮流出招，而是 Incoming State → Compatible Response → State Transition → New Initiative。**
>
> **节奏不是固定秒数，而是 Burst / React / Pressure / Heavy / Recovery 的相对关系。**
>
> **高承诺动作的风险应真实创造或关闭反击窗口。**
>
> **字段只保留能直接改善动作选择、动作因果和最终画面执行的内容；不为理论完整建立第二套复杂 Combat Engine。**