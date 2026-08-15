# Action Combat Choreography Playbook

## 1. 职责

本文件是 `action-combat-video` Task 内的 **Combat Choreography Engine / 动作编排引擎**。

它负责把 Combat Intent 转成真正可执行、连续、全身化、有空间运动、有接触实感、有角色差异的战斗动作，并在输出前执行强制质量 Gate。

它不替代：

- `core-playbook.md` 的 Range / Advantage / Condition / Position / Continuity 真源；
- Modern / Wuxia 等专项 Playbook 的具体动作语言；
- Fighting / Martial / Weapon Libraries 的专业技术知识；
- 通用 Camera / Audio / Spatial Controls。

核心分工：

> **Core 负责“打得对、接得上”。**  
> **Choreography 负责“打得够、连续、丰富、好看、有实感，而且具体到能执行”。**  
> **专项 Playbook / Library 负责“这种战斗具体怎么打”。**

实现原则：**少建运行时概念，多做高价值质量检查。** 本文件把真实成片反馈合并到少数执行合同中，不把每个 Failure Signature 都实现成独立子系统。

---

## 2. Combat Planning Graph + Planning Gate

Quick 与 Interactive 共用同一规划图：

```text
Combat Intent / 观看目标
→ Combat Branch
→ Cinematic Choreography Profile
→ Active Combat Coverage
→ Action Exchange Rhythm
→ Combat Character Identity
→ Contact Modality / Environment Affordance
→ Camera Intent
→ Model Combat Capability Input（如有）
→ Action / Camera Execution Budget
→ Signature Moment
→ Stage-2 Technique / Execution Knowledge
→ Concrete Action Phrase / Battle Beat
→ Core State / Continuity Validation
→ Final Prompt Externalization
```

### Planning Gate

进入具体 Phrase 设计前必须检查：

- 是否先解决 Profile / Coverage / Rhythm / Character Identity 等上游高影响决策；
- 高手连续对决是否遗漏“高手连续攻防型”等明显相关 Profile；
- Character Identity 是否动态推导，而不是按职业、性别、年龄、体型直接套模板；
- Interactive 是否把真正改变成片的分叉暴露给用户，而不是浪费问题在可自动推导的 Contact / Sufficiency / Camera 基础质量上；
- 目标战斗结果是否没有过早锁死整个编排路径；
- Stage-2 是否按当前 Combat Planning Context 读取真正需要的 Technique / Execution Knowledge，而不是只形成高层风格标签。

Planning Gate 失败时先内部重排规划，不默认继续追问用户。

---

## 3. Cinematic Choreography Profile

第一版稳定基础方向：

- 写实战术型；
- 凌厉电影动作型；
- 高手连续攻防型；
- 重型硬派型；
- 环境技巧型；
- 武侠流动拆招型（Wuxia 分支）。

可主次混合，但不要叠加大量冲突 Profile。

Profile 影响 Coverage、Rhythm、Exchange Depth、Kinetic Scope、Contact 表现、环境参与、Camera 倾向和 Signature Moment 方向。

具体稳定知识由 `combat-choreography-profiles` Library 提供。

---

## 4. 三个动作充分性维度

### 4.1 Active Combat Coverage

Coverage 回答“有多少时间真的在打”：

- Low：约 40–55%；
- Medium：约 60–75%；
- High：约 75–90%。

约 15 秒 High Coverage 高手 1v1 可参考：Setup 0.5–1.5s、Active Exchange 11–13s、真实 Downtime 累计尽量 ≤1–2s、纯 Ending Pose 约 0.5–1s。

受击、失衡、闪避、恢复、快速重新切入，只要仍推动下一次攻防，就属于 Active Combat。

### 4.2 Exchange Depth

Exchange Depth 回答“单次连续攻防有多深”：

```text
Defense → Counter → Re-counter → Continuation
```

衡量因果深度，不衡量动作词数量。高手高速交换通常更深；重型硬派可较浅但 Contact / Pressure 更重。

### 4.3 Combat Kinetic Scope

Kinetic Scope 回答“身体和空间到底动了多大、多丰富”。重点检查：

- Whole-body Engagement：脚步、膝髋、躯干、上肢、重心是否协同；
- Spatial Mobility：Position / Angle / Range / Route 是否有意义变化；
- Level / Axis Variation：高低位、身体轴线、方向关系是否按战斗形式合理变化；
- Contact-driven Displacement：接触是否推动身体、重心、站位或距离改变；
- Environment Flow：环境是在推动路线变化，还是把双方锁死在一点。

不设置“必须踢几次、跑几米、绕桌几圈”等固定配额。

> **Coverage 解决“打多久”；Depth 解决“攻防有多深”；Kinetic Scope 解决“身体和空间动多大”。三者互不替代。**

---

## 5. Action Phrase：连续、具体、可执行的动作主单元

层级：

```text
Action–Reaction Pair → Action Phrase → Battle Beat → Combat Sequence
```

Phrase 可参考：

```text
Entry / Setup → Attack → Defensive Answer → Counter → Re-counter / Continuation → Payoff
```

但禁止固定六步模板。

核心判断：

> **后一个动作必须从前一个动作造成的身体、接触或空间状态里自然长出来。**

Phrase 结束不等于停战。多个 Phrase 可以无缝连接在一个 Battle Beat 内；Beat 只在战术目标、Advantage、关键 Condition、主目标或阶段真正变化时切换。

### 5.1 Executable Action Granularity Contract

承担主要战斗因果的 Action Phrase，必须尽量外显当前场景真正需要的可执行信息：

```text
Current Body / Range State
→ Specific Physical / Weapon Action
→ Contact / Evasion / Interception
→ Opponent Immediate Response
→ Footwork / Body Axis / Range / Position Consequence
→ Immediate Continuation Entry
```

这是**信息要求，不是固定六步模板**。Strike、Grapple、Weapon、Wuxia、多人战可以使用完全不同的动作结构。

关键问题是：视频模型是否能从文字中理解：

1. 当前身体与距离状态是什么；
2. 具体哪个身体部位 / 武器线路做了什么；
3. 接触、躲避、截击或控制在哪里发生；
4. 对方立即被迫做了什么；
5. 这个响应改变了哪一类 Footwork / Axis / Range / Position；
6. 下一动作为什么可以立刻从这个新状态继续。

### 5.2 抽象动作词只能做摘要，不能替代关键动作

以下表达可以用于 Profile / Rhythm 摘要、次要过渡或局部压缩，但不能单独承担关键 Active Exchange：

- 连续攻击；
- 连续格挡；
- 快速反制；
- 贴身缠斗；
- 持续压迫；
- 不断换位；
- 连续拆招；
- 高频攻防；
- 双方持续互有来回。

如果删除“高速 / 连续 / 专业 / 高密度 / 反制 / 缠斗”等抽象词后，仍无法说清人物具体做了什么，这个 Phrase 颗粒度不足。

例如：

```text
过粗：
双方在移动中连续格挡、压迫、脱离和再进入。

更可执行：
男方前臂压住女方进入线时，女方不抽手归位，顺接触点旋开前臂并把前脚切到他外侧；男方尚在转髋封线，女方已利用他肩轴未回正的窗口短击迫使其缩肘，再从缩肘留下的路线继续进入。
```

示例只说明颗粒度，不构成固定招式模板。

### 5.3 细化不等于逐招机械枚举

禁止把颗粒度提升误实现成：

- 每拳每脚编号；
- 厘米级位移或关节角度；
- 为了“具体”把一个短 Phrase 塞满彼此独立动作；
- 让动作说明复杂度超过当前 Action Execution Budget。

原则：

> **关键因果动作具体，次要过渡动作可以压缩。**  
> **细节服务连续执行，不服务文字复杂度。**

---

## 6. Temporal Flow Contract：解决“一招一停”

真实成片已经证明：仅写“高速”“连续”不够。Final Action Flow 必须同时满足以下三项。

### 6.1 Temporal Action Packing

Active Exchange 时间窗不能用 3–4 秒只承载一个宏动作来假装高速。

优先组织为：

```text
当前动作产生后果
→ 对手立即响应
→ 响应改变 Contact / Position / Range / Axis
→ 下一动作从这个后果直接启动
→ 局部 Payoff
```

使用“同时、顺势、刚被偏开便、尚未站稳时、接触后立即、沿前一动作方向”等因果时间关系；不要主要靠“然后、随后、再做一个”串独立动作。

### 6.2 Combat Action Interlock / Motion Handoff

连续动作至少应继承一类当前状态：

- Contact；
- Reaction；
- Momentum；
- Footwork；
- Body Axis；
- Range / Position；
- Environment State。

High Coverage / Expert Exchange 中，Neutral Reset 应是稀缺、有意图的节奏事件；禁止默认模式：

```text
攻击 → 完整收势 → 双方站稳 → 重新起架 → 下一攻击
```

Phrase-to-Phrase 同样优先使用前一 Payoff 直接启动下一 Phrase。

### 6.3 Continuous Action Spine + Soft Time Anchors

高密度 Combat 的默认 Final Prompt 时间表达：

> **一条 Continuous Action Spine + 少量 Soft Time Anchors。**

大部分 Active Exchange 连续书写；时间主要定位：

- Setup / First Contact；
- Major Advantage Reversal；
- Signature Moment；
- Ending；
- 用户 / 模型确实要求精确同步的事件。

默认不把 15 秒拆成多个 `0–1.5 / 1.5–4.5 / 4.5–7.5` 的硬动作盒。若模型明确更依赖严格时间戳，也必须保持跨块 Motion Handoff，禁止时间边界成为 Reset 点。

> **时间码服从动作连续性，而不是动作服从时间码。**

---

## 7. Combat Character Identity

Character Identity 回答“当前这个角色怎么打”，动态来源：

```text
人物明确设定
+ 能力 / 经验 / 体型（如已知）
+ 性格 / 行为倾向（如已知）
+ Combat Intent
+ 对手与环境
+ Choreography Profile
+ 当前 State
→ Character Identity
```

至少让角色在 Movement / Attack / Defense-Counter / Rhythm 中存在可见差异，再按需选择 Fighting / Martial / Weapon Profile。

> **职业 ≠ Character Identity ≠ Fighting Profile。**

角色差异不应只写成“女方快、男方重”这类形容词，而应进入具体动作选择与主动权获取方式。例如一方偏好侧切截断，另一方偏好封线压迫；这只是动态推导结果，不建立职业模板。

---

## 8. Tactical Interaction + Visible Advantage + Initiative

Tactical Interaction 是 Phrase 内可选战术因果，可使用 Feint、Probe & Read、Bait、Anticipation、Counter-to-Counter、Pattern Break、Forced Response 等机制。

最终 Prompt 必须外显为可见动作与时机，禁止只写“她提前预判”。

### 8.1 Visible Advantage Dynamics

`Advantage` 由 Core State Engine 维护，但主要 Advantage 变化必须通过可见控制事实表现，例如：

- Attack Initiative；
- Forced Defense；
- Range / Angle / Axis Control；
- Route / Position Control；
- Environment Control；
- Recovery Burden。

Major Advantage Reversal 必须真实改变至少一类控制关系，并由后续 Phrase 继承，而不是一句“局势逆转”。

### 8.2 Initiative Handoff 必须进入动作句法

在高手 Counter / Re-counter 中，主动权应优先在动作执行过程中转移，而不是一方做完整段动作后“轮到”另一方。

可通过 Interception、Forced Response、Line / Range / Axis Control、Contact Handoff、Recovery Window 等发生转移。

设计关键 Phrase 时，优先让 Initiative Handoff 发生在：

- 对方攻击尚未收势；
- 前一个 Contact 仍未断开；
- 对方脚步尚未落稳；
- 对方肩 / 髋轴线尚未回正；
- 前一次偏转已经打开新线路；
- 失衡 / 恢复正在发生而尚未完成。

Final Prompt 应能具体表现类似语义：

```text
A 的攻击仍在形成
→ B 用 Contact / Footwork / Axis 改变它
→ A 被迫立即响应 B
→ Initiative 已在同一运动链中转到 B
```

不要只写“双方不断反制 / 主动权来回切换”。

Initiative Handoff 受 Character Identity 约束：不同角色可偏好不同的抢主动方式。它是动作设计原则，不新增独立问卷或大型状态机。

---

## 9. Combat Intensity Curve

Continuous Spine 不等于全程同速。

Combat Intensity 由 Exchange Frequency、Contact Weight / Pressure、Advantage Pressure、Kinetic Scope、Exchange Depth / Tactical Complexity、Environment Stakes、Camera / Audio Accent 等共同形成。

局部降速仍可以保持高强度，例如持续压迫、狭窄空间封锁、重型 Control。

约 15 秒电影化高手 1v1 默认至少应有一次清楚的 Intensity Turning Point，通常与 Advantage Reversal、Range / Contact 变化、Environment 压力变化或 Signature Moment 相关。

禁止把所有场景模板化为固定“低→中→高”。

---

## 10. Environment Action Affordance

环境必须先作为战术 / 空间机会参与：

```text
对象 / 空间结构 / 障碍
→ Affordance
→ Intent / Identity / State 过滤
→ Action Phrase
→ 更新 Position / Range / Advantage / Environment State
```

只有当环境真正改变攻击路线、移动路线、Range、Advantage、战术选择或 Payoff 时才使用。禁止为“丰富”随机破坏多个物件。

Environment 应尽量推动 fight-space 流动，而不是把人物永久锁在桌边 / 墙边做上半身交互。

---

## 11. Combat Contact Solidity

所有主要 Contact Event 服从通用实感链：

```text
Commitment
→ Contact
→ Force / Energy / Pressure Transfer
→ Reaction Propagation
→ State Consequence
→ Recovery / Continuation
```

按 Strike、Grapple / Control、Takedown / Throw、Blunt Weapon、Blade、Weapon Clash、Environment Impact 等模态采用不同证据。

Camera / Audio 只能强化，不能替代真实接触、受力与后果。

---

## 12. Signature Moment

约 15 秒短片默认追求 1 个主要 Signature Moment；必要时可有 1 个辅助记忆点。

来源可以是 Counter/Re-counter 高潮、环境反制、力量差异 Payoff、Weapon Distance Transition、假破绽、动量重定向、优势翻转、明显空间 / 身体轴线变化。

Signature Moment 必须由前后 Phrase 因果“挣来”，不是随机炫技，也不等于慢动作。

---

## 13. Combat Camera：Readability + Mobility + Coverage

必须区分三个问题：

```text
Camera Complexity
→ 单个 Shot / 整段方案的镜头语言有多复杂

Camera Mobility
→ 单个 Shot 内摄影机是否跟随真实 Position / Range / Axis / Route 变化

Shot Scale / Editorial Coverage
→ 整段 Combat 用哪些观察距离与 Cut 去强调动作信息
```

正式原则：

> **Stable Camera ≠ Static Camera.**  
> **Action Continuity ≠ Shot Continuity.**

高动作 / 空间复杂度时可以降低无必要 Camera Complexity，但不能把它错误执行成：

- Camera 长时间不动；
- 全程中全景 / 中景；
- 只能使用 tracking / dolly；
- 禁止 Close-up / Insert / Reaction / Impact Shot；
- Continuous Action Spine = 必须 one-take。

### 13.1 Camera Mobility

当 Kinetic Scope 出现明显 Position / Range / Axis / Route 变化时，单个 Shot 可使用简单、连续、可预测的 tracking / dolly / small arc / reframe 跟随。

目标是：动作复杂时减少无意义镜头炫技，但保留跟随真实 fight-space 所需的 Mobility。

### 13.2 Cinematic Combat Coverage

电影化 Combat 可以动态使用：

- Master / Establishing Shot；
- Medium / Medium-wide Relationship Shot；
- Close-up / Extreme Close-up；
- Insert；
- Reaction Shot；
- Impact Shot；
- Re-establish。

不设置“必须几个特写 / 几个全景”的配额。

### 13.3 Cut 可以存在，Action State 不能 Reset

跨镜 Cut 必须尽量继承：

```text
Position / Left-Right
+ Action Direction
+ Contact
+ Momentum
+ Body / Weapon Axis
+ Range
+ Initiative / Advantage Consequence
```

摄影发生 Cut，但 Action Spine 连续；禁止 Cut 后双方回到默认距离、默认站位或重新起架。

Camera 具体镜头语言继续由通用 `camera-direction` Control 提供。

---

## 14. Combat Audio Choreography

Audio 作为动作因果、Contact、身体状态和空间变化的可听证据。

> **Audio Accent Density ≠ Action Density。**

基础动作 / 环境声音维持连续存在感；关键 Contact、Phrase Payoff、Signature Moment 再获得更高 Accent。不同 Contact Modality 使用不同材质 / 身体声音证据。

Audio 不能替动作表演。

---

## 15. Action Execution Budget

不设置 Battle Beat 全局固定动作数量上限。

限制的是**同一短时间窗口中模型需要同时理解和执行的复杂信息量**。

颗粒度提升时遵循：

1. 优先具体化关键因果动作；
2. 次要过渡允许压缩；
3. 删除重复 / 装饰性 / 无状态价值动作；
4. 降低单 Phrase 次要 Tactical 分支；
5. 降低无必要 Camera Complexity；
6. 保留有信息价值的 Camera Coverage；
7. 必要时拆成多个无缝连续 Phrase；
8. 最后才缩减次要有效攻防。

**Executable Granularity 不等于动作数量无限增长。** 如果一个具体 Phrase 已超过当前模型 Execution Budget，优先减少同时独立分支，而不是重新退回“双方连续攻防”这种抽象摘要。

模型能力只能改变实现路径，不能偷偷把“高手持续对决”改成“两三次简单交换”。

---

## 16. Two-stage On-demand Loading

### Stage 1：Planning

```text
action-combat-video/index
+ core-playbook
+ choreography-playbook
+ 当前一个专项 Playbook
+ 必要轻量 indexes
+ 可选 Model Capability 摘要
→ Combat Planning Context
```

不要在正常运行加载维护文档、研究档案或未命中的叶子知识。

### Stage 2：Execution Knowledge

正常约 2 个主要 Detail Slot：

```text
Slot A：Technique / Execution
→ 最相关 Fighting / Martial / Weapon Profile

Slot B：Choreography Enhancement
→ 最相关 Signature Pattern / 其他必要增强知识
```

优先级：用户指定专业知识 → 正确执行所需知识 → Character Identity 差异化 → Signature / 创意增强。

Stage-2 的首要责任不是“提供更多术语”，而是帮助构造**具体、可组合、符合当前 Range / Contact / Character Identity 的 Action Phrase**。

如果 Stage-2 已正确读取、Choreography 已执行 Granularity Contract、Assembly 也保留具体动作，但相同 Golden Scenario 仍持续输出泛化动作，才进入 Concrete Choreography Knowledge Audit。

> **Indexes are routing knowledge; leaf files are execution knowledge.**

---

## 17. State Machine Internalized, Choreography Externalized

内部可以完整运行 Range、Advantage、Condition、Tactical、Contact、Kinetic / Camera / Execution Budget 等结构。

Final Prompt 必须转成：

```text
当前身体 / Range 状态
→ 谁用哪个身体部位 / 武器线路移动或攻击
→ 对手如何在动作过程中响应
→ Contact / Evasion / Interception 如何发生
→ Footwork / Axis / Range / Position 如何改变
→ 下一动作怎样从当前状态直接启动
```

优先级：

```text
正向可见 Action Flow
→ 空间 / 环境变化
→ 速度 / 重量 / Character Identity / Intensity / Signature
→ Camera / Audio
→ 少量真正必要的 Continuity / Negative Constraints
```

禁止默认长 Avoid List；禁止自行添加用户没有要求、剧情没有依据的限制。

---

## 18. Ending Coverage Protection

Ending 的**结果意图**可以由用户决定；Ending 占用多少时间、是否吞掉 Active Exchange 属于系统内部 Coverage / Assembly / Preflight 职责。

High Coverage 短 Combat 默认：

- Ending 继承最后一次 Contact / Position / Momentum / Advantage 后果；
- 不提前让双方回到新 Pose 再开始长时间对视；
- 不让呼吸、眼神、静止构图自动占用最后数秒；
- 纯 Ending Pose 参考约 0.5–1s，属于软预算，不是硬配额；
- 用户明确要求长悬停、慢镜、情绪 Ending 时可以扩大。

如果 Ending 描述长度、事件量或静态持续时间明显挤压 Active Exchange，内部先压缩 Ending，而不是重新向用户追问“最后停几秒”。

---

## 19. Combat Final Preflight Gate

Final Prompt 输出前必须过 Gate；失败时内部重写，再检查，不能直接交付。

### A. Action Sufficiency

- Coverage 是否兑现；
- Exchange Depth 是否符合目标；
- 是否存在大量无价值 Downtime / Pose / Control Hold；
- Ending 是否过早吞掉 Active Exchange。

### B. Executable Action Granularity

- 关键数秒是否主要由“连续攻防 / 快速反制 / 贴身缠斗”等抽象动作词承担；
- Character Identity 是否只有打法标签，没有具体动作证据；
- Action Phrase 是否能看出具体动作入口、即时响应、Footwork / Axis / Range / Position 后果和下一动作入口；
- Camera / Audio 是否比身体动作本身写得更具体。

触发失败：**Abstract Action Block / Non-executable Choreography Summary**。

### C. Kinetic Scope

- 是否主要锁在前臂 / 手腕 / 肩部；
- Whole-body / Position / Range / Axis 是否足够；
- Environment 是否推动路线而非锁死。

触发失败：**Upper-body Combat Lock / Kinetic Underfill**。

### D. Temporal Continuity

- 长时间窗是否只有一个宏动作；
- 动作是否通过 Motion Handoff 咬合；
- Neutral Reset 是否过多；
- 是否使用 Continuous Action Spine，而不是硬时间盒把战斗切碎。

触发失败：**Temporal Combat Stretch / Action Underpacking**、**Action Segmentation / Excessive Neutral Reset**、**Timeline-induced Action Segmentation**。

### E. Character / Tactical / Advantage / Initiative

- Character Identity 是否能从动作看出来；
- Tactical Interaction 是否外显；
- 是否只是双方轮流完成独立攻击段；
- Counter / Re-counter 是否在对手动作尚未完成时通过 Contact / Axis / Footwork / Range / Recovery Window 抢走 Initiative；
- Major Advantage Reversal 是否有可见控制权变化；
- 双方抢主动方式是否长期同质化。

触发失败：**Turn-taking Combat / Initiative Segmentation**、**Invisible Advantage / Nominal Reversal**、**Homogeneous Initiative Style**。

### F. Contact / Intensity

- 重要 Contact 是否有 Transfer → Reaction → Consequence；
- 连续 Combat 是否存在可感知的强度变化，而不是全程同速 / 同重量 / 同压力。

触发失败：**Contact Solidity Failure**、**Flat Combat Intensity**。

### G. Camera Coverage

- Kinetic Scope 明显变化时，Camera 是否有足够 Mobility / Reframe；
- `stable / readable` 是否被错误写成长期近似 fixed framing；
- 是否把 Continuous Action Spine 误解为 one-take / 不能 Cut；
- 是否全程几乎只有中全景 / 中景，系统性排斥有信息价值的 Contact / Weapon / Footwork / Reaction 特写；
- Cut 后 Position / Direction / Contact / Momentum / Axis / Range 是否连续；
- 局部 Shot 后是否在需要时 Re-establish 空间关系。

触发失败：**Camera Mobility Underfill**、**Combat Camera Coverage Lock / Medium-wide Overconstraint**、**Cut-induced Action Reset**。

### H. Prompt Externalization

- Final Prompt 是否由具体 Action Language 主导；
- 具体 Choreography 是否被重新压缩成 Meta 摘要；
- 是否 Dump 内部 State / Meta；
- Negative Constraints 是否少而有针对性。

### Gate Failure 行为

```text
定位失败维度
→ 优先重写具体 Action Phrase / Action Spine / Camera Coverage / Prompt Assembly
→ 必要时重新分配执行预算
→ 再次 Preflight
→ 通过后才交付
```

> **规则存在不等于规则生效；Final Preflight 拥有否决权。**

---

## 20. 边界与最终原则

- Core 是 State / Continuity 真源；
- Choreography 不复制专项动作知识；
- Modern / Wuxia 负责具体表现；
- Fighting / Martial / Weapon Libraries 提供专业可组合动作知识；
- Controls 提供通用 Camera / Motion / Spatial / Audio / Prompt Assembly；
- Model Adapter 只改变执行路径与序列化，不改导演意图。

最终原则：

> **动作要足够多，但不是独立动词堆叠。**  
> **关键因果动作要具体，但不是逐招机械枚举。**  
> **连续打斗不是动作排得更近，而是后一个动作从前一个动作的身体与空间状态里长出来。**  
> **Initiative 要在动作链里被抢走，不是在“你的回合结束后”轮到下一方。**  
> **镜头可以稳定，也可以切；Action Continuity ≠ Shot Continuity。**  
> **可读性来自空间锚点与剪辑连续性，不来自全程中全景。**  
> **Ending 服从 Coverage，不让静止收尾吞掉有效交战。**  
> **状态机留在内部，最终 Prompt 交付一条真正连续、具体、可见、可执行的动作主链。**