# Action Combat Impact Realization Spec

> 状态：Design Active / Grill In Progress  
> 适用：Action Combat 的所有 meaningful force-bearing contact  
> 目标：解决“动作已经具体、连续、可执行，但命中仍缺少重量与打击感”的 Runtime 设计缺口。  
> 文档约束：长期 Compact Spec；单文件硬上限 1500 行，不演化成第二套 Combat Playbook。

---

## 1. Problem

当前 Action Combat 已具备 Concrete Technique、Action → Response → State Change → Next Action、Movement / Support / Range / Position 连续性、Impact Aftermath、Action–Camera Handoff 等能力。

仍存在独立缺口：

> Runtime 能说明“打中了什么”与“打中后留下什么”，但不一定能让视频模型理解“这一击为什么在接触瞬间有重量”。

典型失败：

- 攻击像碰到目标，而不是把力量送入目标；
- 受击者像主动配合后退 / 后仰；
- 攻击方命中点突然停住，缺少 follow-through / deceleration；
- 局部受击与全身轴线、重心、支撑变化脱节；
- Camera / Audio 只有装饰性“震一下 / 响一下”，没有真实 Contact 锚点。

因此引入轻量 **Impact Realization** 语义层。

---

## 2. Confirmed Architecture Decisions

### Decision 01 — Core Mechanism

Impact Realization 是 Action Combat 的通用核心机制，不是电影化 / 动漫 / 强冲击风格才启用的可选增强。

写实格斗同样需要可读受力、局部 recoil / deflection、支撑 / 轴线 / 重心变化、follow-through 与下一拍可继承的 Combat State。

> Impact Realization ≠ 夸张化。

### Decision 02 — Semantic Ownership Only

Impact Realization 负责判断：

> **这一击应该被感知成什么样。**

它产出 Impact Salience、Force / Contact Semantics、Immediate Force Response、Combat State Consequence，以及必要的 Perceptual Accent Intent；但不直接控制 Camera / Audio，也不写死 camera shake、slow motion、hit-stop、BOOM 等实现。

现有 Action–Camera Handoff / Audio Runtime 保留最终执行权。

### Decision 03 — Trigger Scope

所有 meaningful force-bearing contact 都经过 Impact Realization Check，但展开深度自适应。

典型适用：Punch / Palm / Elbow / Knee / Kick、Block / Parry / Interception、Grapple / Clinch / Body Pressure、Throw / Takedown / Slam、Weapon Clash / Bind / Deflection、Body–Environment Collision。

通常不展开：纯佯攻、未接触闪避、无明显 Force Exchange 的轻触 / 探手。

### Decision 04 — Minimum Contract + Selective Expansion

所有有效 Force-bearing Contact 共用最小合同：

```text
Concrete Contact
+ Readable Force Response
+ Combat State Consequence
```

最低回答：

1. 什么接触了什么；
2. 为什么对方看起来真的受到了力；
3. 这个力改变了什么当前 Combat State。

只有关键 Impact 才按需展开：

```text
Force Delivery / Commitment
→ Pre-contact Acceleration
→ Contact
→ Local Reaction
→ Whole-body Force Transmission
→ Attacker Follow-through / Recoil / Deceleration
→ Displacement / Recovery Burden
→ New Combat State
```

以上是可选维度，不是固定八步模板。

### Decision 05 — Three-level Dynamic Salience

```text
I1 — Minimal
I2 — Standard
I3 — Emphasized
```

**I1**：真实受力，但主要是局部 deflection / pressure、小 State Change、连接性 Contact。  
**I2**：普通有效 Contact，观众需要明确读懂其成立，并产生明显 Axis / Support / Balance / Range / Pressure / Opening 等状态后果。  
**I3**：I2 基础上具有更高 Force / Tactical / Narrative Salience，例如高动量、明显 whole-body displacement / support loss、强 Recovery Burden、Initiative Reversal、Signature / Finisher、Environment Collision 或 major payoff。

Salience 不按动作名称硬编码。

### Decision 06 — One Core + Modality Branches

统一：

```text
Impact Core
+ lightweight Modality-specific Realization
```

不建立 Strike / Grapple / Weapon 等多套独立 Impact Engine。

### Decision 07 — Responsibility Boundary

```text
Impact Realization
→ Immediate Dynamics

Core Combat State / Condition
→ Medium-term Functional State

Impact Aftermath / Damage Continuity
→ Persistent / Progressive Visible State
```

Impact 负责即时 Local Reaction、Force Transmission、Recoil / Deflection、Forced Step / Rotation、Support Loss、Immediate Recovery Burden 与下一拍 State Consequence。

Condition 维护持续多个 Exchange 的呼吸负担、orientation burden、肢体功能下降等中期状态。

Aftermath 维护血迹 / 红肿 / 擦伤 / 淤青、衣损、环境损伤、物体位移，以及 Baseline / Onset / Lifetime / Continuity。

### Decision 08 — Independent Compact Spec

本文件是长期设计 Spec，不是当前 G01 Regression 的临时章节。

只保存：Problem、Confirmed Decisions、Semantic Contracts、Runtime Integration Map、Pending Questions。

不复制完整 Camera / Audio / Damage / Strike / Grapple 教程或大量 Prompt 示例。

项目硬约束：

> **每个 Spec / Playbook / Runtime 单文件不超过 1500 行。**

1500 行是硬上限，不是目标长度。

### Decision 09 — Local Derived Force Model

Impact Force Model 复用现有 Combat State 与当前 Concrete Action，只做一次性局部派生，不新增持久 Force State。

禁止引入长期维护的 ImpactVelocity、ImpactMass、ForceVector、ForceLevel、BodyStiffness，也不引入牛顿数、精确速度等伪精确参数。

局部可读取 / 推导：

```text
Current Momentum / Motion
Support / Balance
Body Axis
Range / Contact Relationship
Movement Direction
Concrete Technique
Physical Presentation Domain
Narrative Salience
```

形成：

```text
Contact Effectiveness
+ Incoming Momentum / Acceleration
+ Body Commitment
+ Contact Geometry
+ Receiver Support State
+ Narrative Salience
→ I1 / I2 / I3
→ Immediate Force Response
```

随后只把 Axis deviation、Forced Step、Support Transfer / Loss、Balance、Range / Position、Recovery Burden、Opening / Pressure 等真实结果写回既有 Combat State。

> 目标是让模型看懂力量，不是把 Combat Engine 变成物理模拟器。

### Decision 10 — Qualitative Salience Heuristics

I1 / I2 / I3 使用定性、结果导向 Heuristic Gate，不做数值评分模型。

推荐判断顺序：

```text
Effective Contact?
↓
Meaningful Force / Combat State Consequence?
↓
Major Force / Tactical / Narrative Salience?
↓
I1 / I2 / I3
```

I3 不等于“伤害更大”。例如借对方高速来势完成破重心并直接反转 Initiative，即使没有重拳，也可以是 I3。

### Decision 11 — Modality Minimum Realization Contracts

六类 Modality 各自固定一个**极薄的最小语义验收合同**。这些是 Runtime PASS 条件，不是固定 Prompt 字段、固定句式或动作模板。

#### Strike

```text
Concrete Contact Point / Body Relationship
+ Local Reaction
+ 至少一种 Axis / Support / Balance / Range / Opening 后果
```

#### Block / Parry / Interception

```text
Force meets defensive structure
+ attack force 被截停 / 改向 / 吸收中的真实一种
+ 至少一方结构 / attack line / support / opening 发生变化
```

#### Grapple / Clinch / Body Pressure

```text
Pressure / body relationship established
+ force 持续进入对方结构的可读方式
+ forced step / rotation / range compression / support change 中至少一种
```

#### Throw / Takedown

```text
Balance / Support 为什么失效
+ body 怎样被 redirection / acceleration
+ landing / ground-state / recovery 的即时后果
```

#### Weapon Clash

```text
Concrete Weapon Contact
+ deflection / bind / rebound / vibration 中真实成立的响应
+ weapon line / opening / hand–arm–body structure 后果
```

#### Body–Environment Collision

```text
Body 与具体 material / object 的方向性碰撞
+ body deceleration / rebound / compression 中真实成立的响应
+ position / recovery consequence
```

统一验收问题：

> 删除“猛烈 / 强力 / 震撼 / 沉重”等形容词后，是否仍能读出该 Modality 特有的受力机制？

如果不同 Contact 最终都退化成“受到强烈冲击 → 身体后仰 → 退一步”，判 Realization 不足。

### Decision 12 — Channel-agnostic Impact Accent Intent

Impact Accent Intent 收敛成一个 **channel-agnostic Perceptual Intent**，而不是分别维护 Camera / Audio / Timing / Visual 四套输出槽位。

最小语义：

```text
Impact Accent Intent
= Concrete Impact Anchor
+ Perceptual Goal
+ optional Channel Eligibility
```

- **Concrete Impact Anchor**：必须绑定已成立的具体 Contact / Force Response，而不是抽象“重击”；
- **Perceptual Goal**：描述观众这一刻需要感受到什么；
- **Channel Eligibility**：仅在必要时指出 Camera / Audio / Timing 等哪些下游渠道可以参与，不指定实现方式。

Impact Realization 回答 **What should be felt?**；Action–Camera Handoff / Audio / Timing 等既有下游机制回答 **How should it be perceived?**。

Accent Intent 禁止直接写死 camera shake、push-in、slow motion、hit-stop、具体音效等实现，也不与 I1 / I2 / I3 做机械映射。是否生成，应综合 Impact Salience、Viewer Readability 与 Narrative / Rhythm Need。

### Decision 13 — Impact as Motion Carry-over Conversion Node

Impact Realization 是现有 Motion / Energy Carry-over 的**转换节点**，不是动作结束点。

```text
Incoming Motion
→ Contact / Force Exchange
→ Motion 被保留 / 传递 / 改向 / 截停 / 吸收 / 反弹中的真实一种
→ Post-impact Motion Carry-over
→ Immediate Continuation Entry
```

Impact 必须回答：

> **接触之后，双方原来的运动趋势去了哪里？**

但不建立 Energy Meter、Momentum Meter 或新的持久 Motion State。`Post-impact Motion Carry-over` 只是当前 Force Event 结束后仍然存活的局部运动趋势语义，例如 continue、redirect、deflect、rebound、absorb / decelerate、transfer、collapse / support loss；这些不是固定枚举字段。

下一拍 Choreography 应消费：

```text
Post-impact Body / Range / Support State
+ Post-impact Motion Carry-over
→ Immediate Continuation Entry
```

默认禁止 Contact 后自动回到 Neutral Reset。只有动作、风格、战术或真实 recovery 明确要求停顿 / 重置时，才允许运动趋势真正结束。

> **Contact 应当改变运动，而不是默认终止运动。**

### Decision 14 — Fuse Impact Into Existing Action Phrase

Impact Realization 保持内部 Gate；Final Prompt 默认把必要 Force Causality **融合进现有 Concrete Action Phrase**，不新增固定 `Impact / Force` 独立段落。

Runtime 内部可以完整执行：

```text
Concrete Technique
→ Impact Realization
→ Motion Carry-over
→ Aftermath
```

但序列化时应尽量形成一条连续动作因果链：

```text
Concrete Technique
+ Contact
+ Readable Force Response
+ State Consequence
+ 必要 Follow-through / Motion Carry-over
+ Immediate Continuation Entry
```

Salience 只控制 Final Prompt 的保留密度：

```text
I1 → Contact + 最必要 Force Response / State Change
I2 → 融合清晰 Force Response + Continuation
I3 → 可额外保留 1–2 个最高价值 Force Transmission / Recovery / Perceptual Anchor
```

Impact Gate 决定“哪些语义不能丢”，不决定“必须新增一个段落”。禁止动作段、Impact 段、State 段重复描述同一次 Contact。

原则：

> **Impact Semantics Internalized, Force Causality Serialized.**

这与既有 `State Machine Internalized, Choreography Externalized` 保持同一方向。

---

## 3. External Research Takeaways

GitHub 调研只作为设计启发，不成为 Runtime 真源。

可借鉴：精确 Contact Moment、pre-contact acceleration / commitment、极短 timing emphasis、attacker follow-through / deceleration、receiver recoil / whole-body displacement、force transmission、environment / material reaction，以及 Camera / Audio 与真实 Contact State 同步。

禁止直接照搬成通用规则：每次 slow motion、每次 camera shake、每次 shockwave、每次把人打飞、用夸张特效替代真实 Force Response。

> 吸收“Impact 如何被组织”的结构，不照搬某一种视觉媒介的夸张尺度。

---

## 4. Proposed Runtime Position

当前推荐最小插入点：

```text
Concrete Technique Resolution Gate
→ Impact Realization Gate
→ Impact Aftermath / Damage Continuity Gate
```

Impact Realization 不替代 Movement Causality、Concrete Technique Resolution、Core Combat State / Continuity、Impact Aftermath、Action–Camera Handoff、Audio Runtime、Prompt Assembly / Serialization。

最终 Runtime Wiring 继续 Grill 后再落地。

---

## 5. Pending Design Questions

1. Prompt Assembly / Adapter / Final Preflight 需要新增哪些 preservation / failure checks；
2. 哪些规则进入长期 Choreography Playbook，哪些只保留在 regression runtime；
3. Regression Test / Failure Signature 的最小闭环。

后续 Grill 每次只解决一个高依赖问题，并把已确认结论增量写回本 Spec。
