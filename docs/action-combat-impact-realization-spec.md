# Action Combat Impact Realization Spec

> 状态：Design Active / Grill In Progress  
> 适用：Action Combat 的所有 meaningful force-bearing contact  
> 目标：解决“动作已经具体、连续、可执行，但命中仍缺少重量与打击感”的 Runtime 设计缺口。  
> 文档约束：本 Spec 作为长期设计真源，保持 Compact；单文件硬上限 1500 行，不演化成第二套 Combat Playbook。

---

## 1. Problem

当前 Action Combat 已具备：

- Concrete Technique Resolution；
- Action → Response → State Change → Next Action 因果；
- Movement / Support / Range / Position 连续性；
- Impact Aftermath / Damage Continuity；
- Action–Camera Handoff；
- Camera Perceptual Impact Accent。

但仍存在一个独立缺口：

> Runtime 能说明“打中了什么”与“打中以后留下什么”，却不一定能让视频模型理解“这一击为什么在接触瞬间具有重量”。

典型症状：

```text
具体攻击
→ 命中
→ 对手做出结果动作
→ 出现伤势 / 环境后果
```

动作逻辑正确，但缺少清晰的 force delivery、contact response、force transmission、follow-through / recoil 与 combat-state consequence，最终视觉可能表现为：

- 攻击像碰到目标而不是把力量送入目标；
- 受击者像主动配合后退 / 后仰；
- 攻击方命中点突然停住，缺少 follow-through / deceleration；
- 局部受击与全身重心 / 支撑变化脱节；
- Camera / Audio 即使强调，也只是装饰性“震一下 / 响一下”，没有真实物理锚点。

因此需要引入轻量的 **Impact Realization** 语义层。

---

## 2. Design Positioning

### 2.1 Core Mechanism

**Confirmed Decision 01**

Impact Realization 是 Action Combat 的**通用核心机制**，不是只有“电影化 / 强冲击 / 动漫”才启用的风格增强。

即使写实格斗没有震屏、慢动作、冲击波，也仍然需要：

- 可读的受力接触；
- 局部 recoil / deflection；
- 支撑、轴线、重心或距离变化；
- 攻击方 follow-through / recoil / deceleration；
- 下一拍可以继承的 Combat State。

Impact Realization 不等于夸张化。

---

## 3. Ownership Boundary

### 3.1 Impact Produces Semantics, Not Camera / Audio Commands

**Confirmed Decision 02**

Impact Realization 负责判断：

> **这一击应该被感知成什么样。**

它可以产出：

```text
Impact Salience
Force / Contact Semantics
Immediate Force Response
Combat State Consequence
Timing Accent Intent
Visual Accent Intent
Camera Accent Intent
Audio Accent Intent
```

但它**不直接接管 Camera 或 Audio Runtime**，也不写死：

```text
必须震镜
必须慢动作
必须 hit-stop
必须低频 BOOM
```

现有 Action–Camera Handoff 继续拥有 Camera 实现权；Audio Runtime / Adapter 继续拥有声音实现权。

原则：

> **Impact 决定是否值得被强调，以及强调的语义目标；Camera / Audio 决定是否以及怎样实现。**

不得在本 Spec 中建立第二套 Camera Runtime。

---

## 4. Trigger Scope

### 4.1 Meaningful Force-bearing Contact

**Confirmed Decision 03**

所有 **meaningful force-bearing contact** 都经过 Impact Realization Check，但展开深度自适应。

典型适用：

- Punch / Palm / Elbow / Knee / Kick；
- Block / Parry / Interception；
- Grapple / Clinch / Body Pressure；
- Throw / Takedown / Slam；
- Weapon Clash / Bind / Deflection；
- Body–Environment Collision；
- 其他真正产生 Force Exchange 的接触。

通常不需要展开 Impact Realization：

- 纯佯攻；
- 未接触闪避；
- 无明显受力交换的轻触 / 探手；
- 仅用于定位而没有形成压力、位移或结构响应的接触。

原则：

> **不为了“打击感”给不存在的 Force Exchange 硬造 recoil。**

---

## 5. Information Contract

### 5.1 Impact Minimum Contract

**Confirmed Decision 04**

所有真正有意义的 Force-bearing Contact 共用一个最小合同：

```text
Concrete Contact
+ Readable Force Response
+ Combat State Consequence
```

最低必须能回答：

1. 什么接触了什么；
2. 为什么对方看起来真的受到了力；
3. 这个力改变了什么当前 Combat State。

示意：

```text
右直拳命中左颧侧
→ 头部被冲力带偏
→ 肩线随即转开，正面防线短暂暴露
```

这已经可以 PASS，不要求每次完整展开生物力学链。

### 5.2 Expanded Force Chain

只有当前冲击真正需要更高表达深度时，才展开更多信息：

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

这是一组**可选展开维度**，不是固定八步模板。

禁止为了通过 Impact Gate，把每次普通接触都写成微观生物力学说明书。

---

## 6. Impact Salience

### 6.1 Three-level Dynamic Salience

**Confirmed Decision 05**

Impact 使用三档动态 Salience：

```text
I1 — Minimal
I2 — Standard
I3 — Emphasized
```

### I1 — Minimal

适合：

- 有真实受力，但不是当前节奏重点；
- 轻度有效 Block / Parry；
- 小幅身体压力 / 路线改向；
- 连接性 Contact。

通常只需要：

```text
Contact
+ 局部 / 结构响应
+ 必要 State Change
```

### I2 — Standard

适合：

- 普通有效命中；
- 明确的支撑 / 平衡改变；
- 有意义的 Clinch / Grapple pressure；
- 普通 Throw / Takedown impact；
- 需要观众清楚感知“这一下真的成立”的动作。

通常可包含：

```text
Contact
+ Local Reaction
+ Axis / Support / Balance / Range Response
+ Follow-through / Pressure Continuation
+ New Combat State
```

### I3 — Emphasized

适合：

- 关键重击；
- Reversal / Initiative Theft；
- Signature Moment；
- 高动量碰撞；
- Finisher / major payoff；
- 当前叙事明确需要观众感受重量的 Contact。

允许更完整 Force Chain，并可向 Camera / Audio / Timing 提交更强 Accent Intent。

### 6.2 Salience Is State-derived

Impact Salience 不按动作名称硬编码。

禁止：

```text
拳 = I2
肘 = I3
踢 = I3
摔 = I3
```

Salience 应综合当前：

```text
Contact Effectiveness
+ Incoming Momentum / Acceleration
+ Body Commitment
+ Target / Contact Geometry
+ Range / Support / Balance State
+ Physical Presentation Domain
+ Narrative Importance
```

因此同一种肘击、拳击、摔法在不同 State 下可以得到不同 Salience。

三档只是 Impact Realization 的轻量表达深度，不建立第二套 Physical Scale。

---

## 7. Contact Modality Architecture

### 7.1 One Core + Lightweight Modality-specific Realization

**Confirmed Decision 06**

不为不同 Contact 建立多套独立 Impact Engine。

统一结构：

```text
Impact Core
+ Modality-specific Realization Branch
```

所有分支共用：

```text
Force-bearing Contact
→ Force enters the contact
→ Readable response
→ Combat State consequence
```

但不同 Modality 的可见受力语言不同。

### Strike Impact

重点可包括：

```text
Local Hit
→ Recoil / Axis Displacement
→ Support / Balance Change
→ Follow-through / Recovery
```

### Block / Parry / Interception

重点可包括：

```text
Force meets defensive structure
→ pressure / deflection / interception
→ attack line changes
→ defender structure / support responds
→ opening / pressure state changes
```

### Grapple / Clinch / Body Pressure

重点可包括：

```text
Pressure established through body relationship
→ support / center-of-mass transfer
→ forced step / rotation / range compression
→ continuing contact state
```

### Throw / Takedown

重点可包括：

```text
Balance / support broken
→ support loss
→ body acceleration / redirection
→ surface contact
→ recovery burden / new ground state
```

### Weapon Clash

重点可包括：

```text
Weapon contact point
→ vibration / deflection / bind / rebound
→ hand–arm–body structure response
→ weapon line / opening changes
```

### Body–Environment Collision

重点可包括：

```text
Body meets material / object
→ body deceleration / rebound / compression
→ material response
→ position / recovery consequence
```

这些只是分支关注点，不是固定句式、固定动作模板或独立 Gate。

---

## 8. Responsibility Boundary With Aftermath / Condition

### 8.1 Immediate Dynamics vs Medium-term Condition vs Persistent State

**Confirmed Decision 07**

三层职责固定为：

```text
Impact Realization
→ Immediate Dynamics

Core Combat State / Condition
→ Medium-term Functional State

Impact Aftermath / Damage Continuity
→ Persistent / Progressive Visible State
```

### Impact Realization owns

- Contact 当下；
- Local Reaction；
- Force Transmission；
- Recoil / Deflection；
- Forced Step / Rotation；
- Support Loss；
- Immediate Recovery Burden；
- 直接进入下一拍的 Combat State Consequence。

### Core Combat State / Condition owns

例如：

- 短期呼吸负担；
- 暂时眩晕 / orientation burden；
- 手臂麻木 / 功能下降；
- 持续多个 Exchange 的 Recovery Burden；
- 其他不是永久外观变化、但会影响后续动作能力的状态。

这些状态可以由 Impact 产生，但由 Combat State / Condition 维护其后续影响。

### Impact Aftermath owns

- 血迹 / 红肿 / 擦伤 / 淤青；
- 衣物拉扯、歪斜、开线、破损；
- 环境裂痕、擦痕、掉灰；
- 物体位移 / 翻倒 / 散落；
- Persistent / Progressive Damage；
- Damage Onset / Baseline / Lifetime / Continuity。

原则：

> **凡是直接参与下一拍 Combat Causality 的瞬时受力反应，优先属于 Impact Realization。**
>
> **凡是接触结束后仍需要被 Continuity 记住的可见状态，属于 Aftermath。**

避免 Impact 与 Aftermath 重复描述同一瞬态反应。

---

## 9. Spec Scope / Length Contract

### 9.1 Long-term Independent Spec

**Confirmed Decision 08**

本文件是独立长期设计 Spec：

`docs/action-combat-impact-realization-spec.md`

不是当前 G01 Regression 的临时章节。

原因：Impact / Force Realization 属于 Combat Engine 的长期能力。

### 9.2 Compact Spec

本 Spec 只保存：

1. Problem；
2. Confirmed Decisions；
3. Semantic Contracts；
4. Runtime Integration Map；
5. 尚未 resolved 的关键设计项。

不复制：

- 完整 Strike / Grapple / Weapon 教程；
- Camera 正文规则；
- Audio 正文规则；
- Damage Continuity 正文；
- 大量 Prompt 示例；
- 已有 Playbook / Runtime 的重复知识。

写作原则：

```text
Confirmed Decision > 详细讨论过程
Contract > 教程
引用现有真源 > 复制正文
少量代表性示例 > 大量案例堆积
```

项目文档硬约束：

> **每个 Spec / Playbook / Runtime 单文件不超过 1500 行。**

1500 行是硬上限，不是目标长度；本 Spec 应尽可能保持远低于该上限。

---

## 10. Impact Force Model

### 10.1 Local Derived Evaluation, Not Persistent Force State

**Confirmed Decision 09**

Impact Force Model 采用**局部派生模型**，复用现有 Combat State 与当前 Concrete Action，不新增第二套持久 Force State。

禁止为了 Impact 新增长期维护的：

```text
ImpactVelocity
ImpactMass
ForceVector
ForceLevel
BodyStiffness
```

也不引入牛顿数、精确速度或其他伪精确物理参数。

Impact 在当前 Contact 局部读取或推导：

```text
Current Momentum / Motion
Support / Balance
Body Axis
Range
Contact Relationship
Movement Direction
Concrete Technique
Physical Presentation Domain
Narrative Salience
```

并形成一次性的局部评估：

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

Impact 完成后只把真正影响后续动作的结果写回现有 Combat State，例如：

```text
Axis deviation
Forced step
Support transfer / loss
Balance change
Range / Position change
Recovery Burden
Opening / Pressure state
```

局部 Force 判断随后结束，不作为独立持久状态继续维护。

原则：

> **目标是让模型看懂力量，不是把 Combat Engine 变成物理模拟器。**

---

## 11. External Research Takeaways

本轮 GitHub 调研只作为设计启发，不成为 Runtime 真源。

可借鉴的共同结构：

- 精确 Contact Moment；
- Pre-contact acceleration / commitment；
- Impact Frame 或极短 timing emphasis；
- attacker follow-through / deceleration；
- receiver recoil / whole-body displacement；
- force transmission；
- environment / material reaction；
- Camera / Audio 与真实 Contact State 同步。

禁止直接照搬成通用规则：

- 每次命中都 slow motion；
- 每次命中都 camera shake；
- 每次命中都 shockwave；
- 每次命中都把人打飞；
- 用夸张特效代替真实 Force Response。

原则：

> **吸收“Impact 如何被组织”的结构，不照搬某一种视觉媒介的夸张尺度。**

---

## 12. Proposed Runtime Position

当前推荐的最小插入点：

```text
Concrete Technique Resolution Gate
→ Impact Realization Gate
→ Impact Aftermath / Damage Continuity Gate
```

Impact Realization 不替代现有：

- Movement Causality；
- Concrete Technique Resolution；
- Core Combat State / Continuity；
- Impact Aftermath / Damage Continuity；
- Action–Camera Handoff；
- Audio Runtime；
- Prompt Assembly / Serialization。

最终 Runtime Wiring 仍需继续 Grill 后再落地。

---

## 13. Pending Design Questions

以下仍未最终确认：

1. I1 / I2 / I3 的推导边界是否需要更明确的 runtime heuristics；
2. 各 Modality 的 Minimum Realization Contract 是否需要正式固定；
3. Impact Accent Intent 的最小输出语义；
4. Impact 与 Motion / Energy Carry-over 的具体消费关系；
5. Impact Realization 如何进入 Final Prompt，而不造成 Instruction Saturation；
6. Prompt Assembly / Adapter / Final Preflight 需要新增哪些 preservation / failure checks；
7. 哪些规则最终进入长期 Choreography Playbook，哪些只保留在 regression runtime；
8. Regression Test / Failure Signature 的最小闭环。

后续 Grill 每次只解决一个高依赖问题，并把已确认结论增量写回本 Spec。