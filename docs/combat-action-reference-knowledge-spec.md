# Combat Action Reference Knowledge Spec

> 状态：Draft / Grill in Progress  
> 日期：2026-08-16  
> 来源：用户补充的《AI漫剧打斗动作提示词大全》6 张图片 + 本轮 Grill Me 确认决策  
> 目的：建立一套可被 Action Combat Runtime / Stage-2 选择与组合的“单动作级打斗参考知识库”设计真源。当前文件只记录已经确认的知识建模与字段设计，不提前实现 Runtime，不修改 RF-22 既有回归逻辑。

---

## 0. 核心定位

本知识库不是固定连招模板、漫剧专属 Prompt 大全、武术门派百科、新 Combat Engine、新 Camera / Physics Runtime。

它回答：

> **在当前 Combat State / Combat Role / Response Need 下，有哪些可执行的单动作候选，它们需要什么前提，会如何改变战斗状态与主动权，并能以什么视觉媒介、物理夸张尺度和环境反馈被表现。**

它服务现有 Exchange Spine / Stage-2 / Movement Causality / Per-Character Signature / Advantage / Re-entry 等机制，不取代这些机制。

设计约束：

> **只保留能直接改善动作选择、动作因果、攻防节奏和最终画面执行的字段；不为了理论完整继续拆状态机。**

---

# A. 知识颗粒度与一级分类

## A1. 一级分类：按战斗功能分类

当前分类：

1. 突进接敌类；
2. 闪避走位类；
3. 格挡防御类；
4. 重击爆发类；
5. 腿法攻击类；
6. 空中动作类；
7. 贴身缠斗 / 近身快打类；
8. 武器瞬杀类；
9. 气劲 / 能量外放类。

一级分类用于知识导航与初筛，不等于 Combat Role；同一动作可以承担多个战斗角色。

## A2. 最小颗粒度：单动作模板

> **单动作模板是最小知识颗粒度，不继续拆成独立的手、脚、肩胯、重心等更细节点。**

脚步、接触面、轴线、重心、支撑、目标部位等都是单动作模板内部属性。

连招不作为基础条目，只记录前后衔接关系，由 Runtime 根据当前 State 动态组合。

原则：

> **动作是积木，连招由 Runtime 编排。**

---

# B. 单动作条目的核心信息

原始基础字段：

1. Action Name / 动作名称
2. Aliases / 别名
3. Functional Category / 动作功能分类
4. Applicable Range / 适用距离
5. Core Action Mechanic / 核心动作机制
6. Body & Contact Relation / 关键身体与接触关系
7. Immediate Visible Result / 立即可见结果
8. Style Realization / 风格表现
9. Transition Compatibility / 可衔接前后动作
10. Risks & Failure Modes / 使用风险与避免事项

图片中的“核心关键词”降级为辅助 Metadata，不作为一级知识结构。

随着 Grill 深入，以下运行期高价值字段已确认加入：

- Physical Level Range
- Combat Role
- Response Compatibility
- State Transition
- Tempo Profile
- Risk / Commitment Profile
- Initiative Effect
- Prerequisites
- Environment Impact

最终字段表在设计收敛后统一重排，不受原始“10 字段”编号限制。

---

# C. Visual Medium 与 Physical Realization Level 双轴解耦

## C1. Visual Medium

画面媒介与动作物理夸张程度完全解耦。

Visual Medium 可包括：

- 真人写实影视；
- 国风漫剧；
- 二维动画；
- 三维动画；
- 其他风格化媒介。

合法组合包括：

```text
真人写实影视 + P1 Grounded
真人写实影视 + P2 Cinematic Exaggerated
真人写实影视 + P3 Hyper-Cinematic / Supernatural
国风漫剧 + P1 Grounded
国风漫剧 + P3 Hyper-Cinematic / Supernatural
```

即：真人写实画面可以承载高度夸张甚至超现实武打；“真人”不等于“现实物理”。

## C2. Physical Realization Level

### P1｜Grounded

- 基本遵循现实人体重心、惯性、距离与受力；
- 允许电影化强化；
- 不依赖明显气劲、长时间滞空、超自然位移。

### P2｜Cinematic Exaggerated

- 仍有明确物理起点和动作因果；
- 允许明显强化速度、爆发、击飞和环境反馈；
- 可用于真人动作影视中的夸张武打。

### P3｜Hyper-Cinematic / Supernatural

- 允许残影、超高速位移感、长距离击飞、明显滞空、气劲、冲击波、剑气、地裂等；
- 仍要求方向、目标、动作因果和战斗状态可读。

## C3. Min / Default / Max Physical Level

每个动作记录：

- **Min Physical Level**：不改变动作核时，动作最低还能成立的等级；
- **Default Physical Level**：无额外要求时最自然的等级；
- **Max Physical Level**：不改变动作身份时允许强化到的最高等级。

Runtime 只能在合法区间内调整。

示意：

```text
侧身闪避走位
Min: P1
Default: P1
Max: P2

落地震地重击
Min: P2
Default: P2
Max: P3

抬手震气击退
若 Core Mechanic = 不接触目标、靠掌劲 / 气浪直接震退
Min: P3
Default: P3
Max: P3
```

核心边界：

> **降低 Physical Level 可以削弱速度、击飞、破坏和特效，但不能偷偷改变 Core Action Mechanic。需要改变动作核才能降级时，应视为另一个动作。**

---

# D. Combat Role / 战斗功能角色

每个动作允许多值 Combat Role，例如：

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

它用于回答“当前战斗需要什么功能”，不是规定固定 Battle Beat 流程。

原则：

> **先确定为什么现在需要这个动作，再选具体动作。**

---

# E. Response Compatibility / 攻防响应关系

该字段回答：

> **这个动作最适合回应什么攻击类型、接触关系或战斗状态？**

示意：

```text
侧身闪避走位
Role: Defense / Route Change
优先响应：直线突进、重拳、正面抓抱入口
不优先响应：已经建立的贴身抱控

双臂交叉防御
Role: Defense
优先响应：正面重击、下劈、爆发冲击
代价：通常仍处正面对线，可能继续承受 Pressure

横扫腿击
Role: Counter / Base Disruption
优先条件：对方重心前压、承重脚暴露、突进刚落脚
```

目标从：

```text
A 攻击 → B 随机抽 Defense
```

变成：

```text
Incoming State → Response Need → Compatible Action Candidate
```

---

# F. State Transition / 战斗状态变化

动作执行后，只记录它真正改变的状态，不要求每个字段都填。

可涉及：

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

核心链：

```text
Current State
→ Action
→ State Transition
→ New Combat State
→ Next Action Selection
```

该字段直接服务 Movement Causality / Exchange Spine / Advantage。

---

# G. Tempo Profile / 节奏特征

使用相对节奏，不绑定固定秒数。

当前可用类型包括：

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
侧身闪避走位 → Quick Reactive
极速瞬身突袭 → Burst
蓄力重拳冲击 → Build-up → Impact
贴身缠斗快打 → Sustained Rapid
落地震地重击 → Acceleration → Impact → Recovery
```

目标是允许：

```text
Burst → Quick Reactive → Sustained Rapid → Heavy Pause → Reversal Burst
```

而不是机械轮流出招。

---

# H. Risk / Commitment Profile

记录动作投入程度与失手代价，不记录固定成功率。

至少包含：

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

> **越重、路线越难改、恢复越慢的动作，失败后越应该产生真实反击窗口。**

---

# I. Initiative Effect / 主动权影响

保留为轻量字段，不建立结果状态机。

基础值：

```text
Retain
Gain
Steal
Lose
Open Counter Window
Neutral
```

只有动作确实存在明显条件差异时，才允许补一句简短说明，例如：

```text
蓄力重拳：命中通常 Retain / Gain；明显落空时 Open Counter Window。
```

不要求所有动作拆成 On Hit / On Block / On Miss / On Evade 四套分支。

原则：

> **字段用于帮助选动作，不用于建立第二套战斗状态机。**

---

# J. Prerequisites / 使用条件

只使用一个统一字段，不拆成角色体型、柔韧、武器、环境等多个子系统。

它回答：

> **这个动作成立之前必须满足什么条件？**

示意：

```text
侧身拔刀斩
→ 当前持有 / 佩戴可拔出的刀剑

腾空旋转斩击
→ 有足够起跳与旋转空间；对应武器可用

贴身缠斗快打
→ 已进入近身距离

横扫腿击
→ 目标腿部 / 支撑区域可达

凌空飞踢
→ 有起跳空间与可落地区域

落地震地重击
→ 必须存在前序腾空 / 下落 / 重落地阶段
```

目的：避免错误距离、无武器、无起跳空间、无前序状态时硬塞动作。

---

# K. Environment Impact / 环境影响

已确认增加轻量 `Environment Impact`。

它只描述：

> **当前动作在不同 Physical Level 下，典型可以带来什么可见环境反馈。**

它不是独立 Environment Destruction Engine，不建立复杂材质模拟器、破坏树或损伤状态机。

推荐写法是按当前动作真正有意义的等级给出简短典型反馈；不要求所有动作机械填满 P1 / P2 / P3。

示意：

```text
横扫腿击
P1：脚步摩擦、轻微扬尘；命中后对手补步或碰到近处物体
P2：对手被扫偏后撞翻椅子 / 撞墙，物体保持新位置
P3：可强化冲击气流、碎屑或夸张位移，但仍服务该次腿击结果

落地震地重击
P2：重落地、灰尘震起、附近小型家具震动
P3：地面龟裂、碎石飞溅、冲击波扩散

蓄力重拳冲击
P2：对手被轰退撞墙 / 家具，出现局部裂纹或明显位移
P3：墙体大面积崩裂、碎屑扩散、冲击波强化

抬手震气击退
P3：气浪推动衣物、纸张、灰尘或小型物件，并沿明确方向扩散
```

核心原则：

> **环境反馈是动作结果的视觉延伸，不是独立表演。**

> **Physical Level 越高，可以强化破坏与视觉反馈，但环境后果仍必须对应当前动作方向、目标和力度。**

同时继续服从现有 Aftermath / Continuity 原则：已经形成的持久环境位移或破坏，后续不得无因 Reset。

---

# L. 当前图片来源动作清单

当前 6 张来源图片共 18 个原始动作：

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

原始名称可保留为 Alias，后续逐条知识化时建立更稳定的 Canonical Action Name，并区分动作核、视觉表现和物理等级。

---

# M. 已确认设计决策

1. 按战斗功能分类，不按图片 1～18 原编号平铺；
2. 单动作模板是最小知识颗粒度；
3. 连招由衔接关系 + Runtime 动态组合产生；
4. 关键词降级为 Metadata；
5. Visual Medium 与 Physical Realization Level 双轴解耦；
6. 真人写实媒介允许 P3 超现实武打；
7. 每个动作记录 Min / Default / Max Physical Level；
8. 降低 Physical Level 不得改变 Core Action Mechanic；
9. 增加 Combat Role；
10. 增加 Response Compatibility；
11. 增加 State Transition；
12. 增加 Tempo Profile，不绑定固定秒数；
13. 增加 Risk / Commitment Profile；
14. High Commitment 失败后应自然提高 Counter / Initiative Theft 候选权重；
15. 增加轻量 Initiative Effect，不建立条件状态机；
16. 增加统一 Prerequisites，不拆多个前提子系统；
17. 增加轻量 Environment Impact，不建立独立破坏 Engine；
18. 本知识库服务现有 Combat Runtime，不新建第二套战斗 Engine；
19. 设计优先“够用和可执行”，不追求理论字段完备。

---

# N. 尚未确认 / 后续 Grill

- Combat Role 是否需要进一步收敛正式枚举；
- Response Compatibility 是否保留自然语言，还是做轻量结构化；
- State Transition 是否保持描述式，还是做轻量 Before → After；
- 18 个动作逐条知识化后的去重、Canonical Name 与 Alias；
- 知识库最终放入 `references/libraries/` 的目录结构与加载预算；
- 与现有 `combat-choreography-patterns` / fighting / martial libraries 的职责边界和去重策略；
- Regression / Minimum Validation Set。

---

## 当前原则

> **先确定动作在战斗中为什么现在用，再决定用哪个动作。**

> **一攻一守不是轮流出招，而是 Incoming State → Compatible Response → State Transition → New Initiative。**

> **节奏来自 Burst / React / Pressure / Heavy / Recovery 的关系，不来自固定动作数和固定秒数。**

> **夸张程度属于 Physical Level；真人 / 漫剧属于 Visual Medium，两者互不绑死。**

> **环境破坏必须服务动作因果，而不是为了华丽独立堆特效。**
