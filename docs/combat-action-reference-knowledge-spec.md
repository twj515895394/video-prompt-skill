# Combat Action Reference Knowledge Spec

> 状态：Draft / Grill in Progress  
> 日期：2026-08-16  
> 来源：用户补充的《AI漫剧打斗动作提示词大全》6 张图片 + 本轮 Grill Me 确认决策  
> 目的：建立一套可被 Action Combat Runtime / Stage-2 选择与组合的“单动作级打斗参考知识库”设计真源。当前文件只记录已经确认的知识建模与字段设计，不提前实现 Runtime，不修改 RF-22 既有回归逻辑。

---

## 0. 核心定位

本知识库不是：

- 固定连招模板；
- 漫剧专属 Prompt 大全；
- 武术门派百科；
- 新的 Combat Engine；
- 新的 Camera / Physics Runtime。

本知识库回答的是：

> **在当前 Combat State / Combat Role / Response Need 下，有哪些可执行的单动作候选，它们会如何改变战斗状态，并能以什么视觉媒介与物理夸张尺度被表现。**

它应服务于现有 Action Combat 的 Exchange Spine / Stage-2 / Movement Causality / Per-Character Signature / Advantage / Re-entry 等机制，而不是取代它们。

---

# A. 已确认的知识库结构

## A1. 一级分类：按战斗功能分类

已确认：不按来源图片 1～18 的编号直接平铺，而按动作在战斗中的主要功能组织。

当前建议一级分类：

1. 突进接敌类；
2. 闪避走位类；
3. 格挡防御类；
4. 重击爆发类；
5. 腿法攻击类；
6. 空中动作类；
7. 贴身缠斗 / 近身快打类；
8. 武器瞬杀类；
9. 气劲 / 能量外放类。

说明：一级分类用于检索与知识导航，不等同于固定 Combat Role；同一动作可以在不同战斗状态下承担多个 Combat Role。

---

## A2. 最小知识颗粒度：单动作模板

已确认：

> **知识库最小颗粒度固定为“单动作模板”，不再继续拆成更细的手部动作、脚步动作、肩胯动作等独立知识节点。**

脚步、接触面、重心、轴线、支撑、发力、目标部位等属于单动作模板内部属性。

连招 / 连续片段不作为基础知识条目，而作为：

- 可衔接前置动作；
- 可衔接后续动作；
- 常见组合关系；
- Runtime 动态 Exchange 编排结果。

原则：

> **动作是积木，连招由 Runtime 根据当前 State 动态编排。**

---

# B. 单动作条目字段标准

每个动作条目至少包含以下 10 个核心字段：

1. **动作名称 / Action Name**
2. **别名 / Aliases**
3. **动作功能分类 / Functional Category**
4. **适用距离 / Applicable Range**
5. **核心动作机制 / Core Action Mechanic**
6. **关键身体 / 接触关系 / Body & Contact Relation**
7. **立即可见结果 / Immediate Visible Result**
8. **风格表现层 / Style Realization**
9. **可衔接前置动作 / 后续动作 / Transition Compatibility**
10. **使用风险 / 避免事项 / Risks & Failure Modes**

图片中的“核心关键词”不作为一级核心字段，降级为检索辅助 Metadata，可由条目内容自动归纳。

随着 Grill 深入，Combat Role、Response Compatibility、State Transition、Tempo Profile、Risk / Commitment Profile 等属于运行期高价值结构化属性；最终字段表会在设计收敛后统一重排，不受当前“10 个原始核心字段”编号限制。

---

# C. 视觉媒介与动作物理解耦

## C1. 双轴模型

已确认：

> **Visual Medium（画面媒介）与 Physical Realization Level（动作物理表现等级）必须完全解耦。**

### Visual Medium

用于描述“画面是什么媒介 / 视觉表达”，例如：

- 真人写实影视；
- 国风漫剧；
- 二维动画；
- 三维动画；
- 其他风格化媒介。

Visual Medium 不决定动作是否必须遵循现实物理。

例如以下组合均合法：

```text
真人写实影视 + P1 Grounded
真人写实影视 + P2 Cinematic Exaggerated
真人写实影视 + P3 Hyper-Cinematic / Supernatural
国风漫剧 + P1 Grounded
国风漫剧 + P3 Hyper-Cinematic / Supernatural
```

即：真人影视完全可以承载高度夸张 / 超现实武打表现；不能把“真人写实画面”等价为“现实物理”。

---

## C2. Physical Realization Level

当前确认三级：

### P1｜Grounded / 写实动作物理

- 重心、惯性、距离与受力基本遵循现实人体物理；
- 可电影化，但不出现明显超现实位移 / 滞空 / 气劲外放。

### P2｜Cinematic Exaggerated / 电影夸张

- 动作仍有清晰物理起点和因果；
- 允许明显强化速度、爆发、击飞、环境反馈与视觉冲击；
- 可出现超出现实格斗但仍具有“真人动作片可接受”的重量感。

### P3｜Hyper-Cinematic / Supernatural / 超现实武打

- 允许残影、超高速瞬移感、长距离击飞、明显滞空、气劲、冲击波、剑气、地面崩裂等非现实表现；
- 仍要求动作前后因果、方向、目标与战斗状态可读，避免纯随机特效。

---

## C3. 每个动作的等级属性

已确认：每个动作不是固定只属于一个等级，而增加：

- **Default Physical Level**
- **Max Physical Level**

这样同一个动作可以根据用户题材和表现需求被压低或拉高。

示意：

```text
侧身闪避走位
Default: P1
Max: P2

极速瞬身突袭
Default: P2
Max: P3

落地震地重击
Default: P2
Max: P3
```

对于本身依赖超现实机制才能成立的动作，可以声明更高的最低可用等级；这一字段是否正式加入，尚未 Grill 确认。

---

# D. Combat Role / 战斗功能角色

## D1. Combat Role 字段

已确认：每个动作增加多值 `Combat Role`，用于描述该动作在一段 Exchange 中承担什么战术 / 节奏作用。

当前候选角色包括但不限于：

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

注意：

- 这是知识属性，不是固定 Battle Beat 模板；
- 一个动作可以同时承担多个 Role；
- Runtime 应依据 Current State 选择 Role，而不是为了“凑流程”机械轮换 Role。

核心意义：

> 从“随机挑一个好看的动作”升级为“当前战斗需要什么功能，再选动作”。

---

# E. Response Compatibility / 攻防响应关系

已确认增加 `Response Compatibility`。

它回答：

> **这个动作最适合回应什么类型的攻击、接触关系或战斗状态？**

例如：

```text
侧身闪避走位
Role: Defense / Route Change
优先响应：直线突进、重拳、正面抓抱入口
不优先响应：已建立的贴身抱控、大范围封锁型横扫

双臂交叉防御
Role: Defense
优先响应：正面重击、下劈、爆发冲击
代价：通常保留正面对线，容易继续承受 Pressure

横扫腿击
Role: Counter / Base Disruption
优先条件：对方重心前压、承重脚明确、突进刚落脚
```

该字段用于提高“一攻一守”的动作匹配准确度，避免：

```text
A 发起任意攻击
→ B 随机抽一个 Defense
```

目标变成：

```text
Incoming Attack / Current State
→ Response Need
→ Compatible Action Candidate
```

---

# F. State Transition / 战斗状态变化

已确认增加 `State Transition`。

一个动作执行后，应记录它真正改变了哪些战斗状态，而不是只描述“动作看起来怎么样”。

可记录维度包括：

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

无需每个动作全部填写，只记录实际发生变化的维度。

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
Incoming: 正面直线突进
Action: 侧移离开攻击线
State Transition:
- Route changed
- Axis changed
- Outside angle created
- Counter window opened

双臂交叉防御
Incoming: 正面重击
State Transition:
- Contact absorbed / blocked
- Range mostly unchanged
- Axis mostly unchanged
- Defender may still be under pressure

横扫腿击
Incoming: 前压 + 承重脚暴露
State Transition:
- Support disrupted
- Balance reduced
- Forced step / fall risk
- Initiative window opened
```

该字段直接服务现有 Movement Causality / Exchange Spine / Advantage Runtime。

---

# G. Tempo Profile / 节奏特征

已确认增加 `Tempo Profile`。

目的：让动作不仅按攻防功能匹配，还能参与整段战斗的速度 / 重拍 / 停顿 / 再爆发设计。

不绑定固定秒数，不规定“一个动作必须 0.8s / 1.2s”。使用相对节奏类型。

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
Tempo: Quick Reactive
→ 短、快，不明显打断高速交锋

极速瞬身突袭
Tempo: Burst
→ 突然提速并快速压缩距离

蓄力重拳冲击
Tempo: Build-up → Impact
→ 短暂蓄势后形成明显重拍

贴身缠斗快打
Tempo: Sustained Rapid
→ 连续高频攻防，不完全 Reset

落地震地重击
Tempo: Acceleration → Impact → Recovery
→ 明显峰值和落地后的余韵
```

目标是允许 Runtime 形成动态节奏，例如：

```text
Burst
→ Quick Reactive
→ Sustained Rapid
→ Heavy Pause
→ Reversal Burst
```

而不是机械的：

```text
A 打一下
→ B 打一下
→ A 再打一招
```

---

# H. Risk / Commitment Profile / 风险与动作承诺度

已确认增加 `Risk / Commitment Profile`。

它回答：

> **角色一旦开始执行这个动作，需要把多少身体状态、路线、重心或时间投入进去；如果被闪避、格挡或打断，会暴露多大的恢复窗口；命中后的回报又有多大。**

该字段不记录固定成功率，也不把动作硬编码成“高风险一定失败”；它用于 Runtime 在当前 State 下理解动作的战术成本与反击机会。

至少包含以下维度：

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
Miss / Block Risk: Low
Recovery Exposure: Low
Payoff: Route Change / Counter Window

极速瞬身突袭
Commitment: Medium
Miss Risk: Medium
Recovery Exposure: 前冲路线落空后可能短暂暴露
Payoff: 快速压缩距离 / 抢 Entry / 形成 Pressure

蓄力重拳冲击
Commitment: High
Miss / Block Risk: High
Recovery Exposure: 蓄势与空挥后恢复较慢
Payoff: High Impact / 强制位移 / Advantage Shift

腾空旋转斩击
Commitment: Very High
Miss Risk: High
Recovery Exposure: 空中路线难临时改变，落地存在 Recovery Window
Payoff: Signature / Finisher / 高视觉收益
```

该属性与 Response Compatibility、State Transition、Tempo Profile 联动，可形成更自然的反击逻辑：

```text
High Commitment Attack
→ Miss / Block / Evade
→ Recovery Exposure Opened
→ Counter / Initiative Theft 候选权重上升
```

因此，主动权翻转不再只依赖人为安排，而可以由动作本身的承诺度与失手代价产生。

原则：

> **动作越重、路线越难改、恢复越慢，越需要明确其失败后的反击窗口；动作越轻、越短、越可撤回，越不应自动制造夸张的大暴露。**

---

# I. 当前图片来源动作清单（待逐条知识化）

当前 6 张来源图片共提供 18 个动作条目。原始名称如下：

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

注意：

- 上述名称来自用户提供图片，只作为当前原始素材名；
- 后续知识化时允许保留原名作为 Alias，并建立更中性的 Canonical Action Name；
- 图片中的“气流、灵气、剑气、地裂、残影”等既可能是动作视觉实现，也可能是 P2/P3 风格表现，不应无脑写入 Core Action Mechanic；
- 后续需要逐条区分：动作核、视觉表现、物理尺度、Combat Role、Response Compatibility、State Transition、Tempo Profile、Risk / Commitment Profile。

---

# J. 已确认设计决策清单

截至当前 Grill，已确认：

1. 知识库按战斗功能分类，不按 1～18 原编号平铺；
2. 单动作模板是最小知识颗粒度，不再拆更细独立节点；
3. 连招不作为基础条目，由前后衔接关系 + Runtime 动态组合形成；
4. 单动作采用 10 个基础核心字段，关键词降级为 Metadata；
5. Visual Medium 与 Physical Realization Level 双轴解耦；
6. P1 / P2 / P3 只描述动作物理 / 破坏 / 超现实尺度，不代表真人或动画；
7. 真人写实媒介允许 P3 超现实武打；
8. 每个动作记录 Default Physical Level + Max Physical Level；
9. 增加多值 Combat Role；
10. 增加 Response Compatibility；
11. 增加 State Transition；
12. 增加 Tempo Profile，使用相对节奏，不绑定固定秒数；
13. Combat Role + Response Compatibility + State Transition 用于提高攻防匹配、反击、主动权转换和整体节奏感；
14. 增加 Risk / Commitment Profile，记录动作承诺度、失手 / 被挡风险、恢复暴露与命中回报；
15. High Commitment 动作在 Miss / Block / Evade 后应自然提高 Counter / Initiative Theft 候选权重；
16. 本知识库服务现有 Combat Runtime，不新建第二套战斗 Engine。

---

# K. 尚未确认 / 后续 Grill

以下内容仍未确认，后续逐项 Grill：

- 动作是否需要 `Min Physical Level`，还是 Default + Max 足够；
- Combat Role 的正式枚举边界；
- Response Compatibility 的结构化维度；
- State Transition 是描述式还是结构化 Before → After；
- Tempo Profile 与 Risk / Commitment 的职责边界；
- 动作是否需要 `Initiative Effect` 独立字段，还是由 State Transition + Risk / Commitment 推导；
- 动作是否需要角色体型 / 柔韧 / 武器 / 环境条件；
- P2 / P3 的 Environment Destruction 如何建模；
- 18 个动作逐条知识化后的去重、Canonical Name 与 Alias；
- 该知识库最终放入 `references/libraries/` 的目录结构与 Runtime 加载预算；
- 与现有 `combat-choreography-patterns` / fighting / martial libraries 的职责边界和去重策略；
- Regression / Minimum Validation Set。

---

## 当前原则

> **先确定动作在战斗中“为什么现在用”，再决定“用哪个动作”。**
>
> **先确定动作核，再决定真人 / 动画等视觉媒介，以及 P1 / P2 / P3 物理表现。**
>
> **一攻一守不是轮流出招，而是 Incoming State → Compatible Response → State Transition → New Initiative。**
>
> **节奏不是固定秒数，而是动作之间 Burst / React / Pressure / Heavy / Recovery 的相对关系。**
>
> **高承诺动作的风险不是装饰字段，而应真实创造或关闭反击窗口。**