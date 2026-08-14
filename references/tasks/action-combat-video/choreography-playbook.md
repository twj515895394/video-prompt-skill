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
> **Choreography 负责“打得够、连续、丰富、好看、有实感”。**  
> **专项 Playbook / Library 负责“具体怎么打”。**

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
→ Action Phrase / Battle Beat
→ Core State / Continuity Validation
→ Final Prompt Externalization
```

### Planning Gate

进入具体 Phrase 设计前必须检查：

- 是否先解决 Profile / Coverage / Rhythm / Character Identity 等上游高影响决策；
- 高手连续对决是否遗漏“高手连续攻防型”等明显相关 Profile；
- Character Identity 是否动态推导，而不是按职业、性别、年龄、体型直接套模板；
- Interactive 是否把真正改变成片的分叉暴露给用户，而不是浪费问题在可自动推导的 Contact / Sufficiency / Camera 基础质量上；
- 目标战斗结果是否没有过早锁死整个编排路径。

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

## 5. Action Phrase：连续动作主单元

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

## 8. Tactical Interaction + Visible Advantage

Tactical Interaction 是 Phrase 内可选战术因果，可使用 Feint、Probe & Read、Bait、Anticipation、Counter-to-Counter、Pattern Break、Forced Response 等机制。

最终 Prompt 必须外显为可见动作与时机，禁止只写“她提前预判”。

### Visible Advantage Dynamics

`Advantage` 由 Core State Engine 维护，但主要 Advantage 变化必须通过可见控制事实表现，例如：

- Attack Initiative；
- Forced Defense；
- Range / Angle / Axis Control；
- Route / Position Control；
- Environment Control；
- Recovery Burden。

Major Advantage Reversal 必须真实改变至少一类控制关系，并由后续 Phrase 继承，而不是一句“局势逆转”。

### Initiative Handoff

在高手 Counter / Re-counter 中，主动权应优先在动作执行过程中转移，而不是一方做完整段动作后“轮到”另一方。

可通过 Interception、Forced Response、Line / Range / Axis Control、Contact Handoff、Recovery Window 等发生转移。

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

## 13. Camera Readability + Mobility Coupling

必须区分：

```text
Camera Complexity ≠ Camera Mobility
```

高动作 / 空间复杂度时可以降低不必要 Camera Complexity，但**不等于降低 Camera Mobility**。

正式原则：

> **Stable Camera ≠ Static Camera.**

当 Kinetic Scope 出现明显 Position / Range / Axis / Route 变化时，Camera 应使用简单、连续、可预测的 tracking / dolly / small arc / reframe 跟随；高密度动作常用目标是：

> **Low Camera Complexity + Medium / High Camera Mobility。**

不要为了“保持构图”反向把人物锁在画面中央小区域。

Camera 具体语言继续由通用 `camera-direction` Control 提供。

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

过载时依次：

1. 删除重复 / 装饰性 / 无状态价值动作；
2. 降低单 Phrase 次要 Tactical 分支；
3. 降低无必要 Camera Complexity；
4. 拆成多个无缝连续 Phrase；
5. 最后才缩减次要有效攻防。

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

> **Indexes are routing knowledge; leaf files are execution knowledge.**

---

## 17. State Machine Internalized, Choreography Externalized

内部可以完整运行 Range、Advantage、Condition、Tactical、Contact、Kinetic / Camera / Execution Budget 等结构。

Final Prompt 必须转成：

```text
谁移动 / 攻击
→ 对手如何在动作过程中响应
→ 接触与受力如何发生
→ 身体 / Range / Position 如何改变
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

## 18. Combat Final Preflight Gate

Final Prompt 输出前必须过 Gate；失败时内部重写，再检查，不能直接交付。

### A. Action Sufficiency

- Coverage 是否兑现；
- Exchange Depth 是否符合目标；
- 是否存在大量无价值 Downtime / Pose / Control Hold。

### B. Kinetic Scope

- 是否主要锁在前臂 / 手腕 / 肩部；
- Whole-body / Position / Range / Axis 是否足够；
- Environment 是否推动路线而非锁死。

触发失败：**Upper-body Combat Lock / Kinetic Underfill**。

### C. Temporal Continuity

- 长时间窗是否只有一个宏动作；
- 动作是否通过 Motion Handoff 咬合；
- Neutral Reset 是否过多；
- 是否使用 Continuous Action Spine，而不是硬时间盒把战斗切碎。

触发失败：**Temporal Combat Stretch / Action Underpacking**、**Action Segmentation / Excessive Neutral Reset**、**Timeline-induced Action Segmentation**。

### D. Character / Tactical / Advantage

- Character Identity 是否能从动作看出来；
- Tactical Interaction 是否外显；
- 是否只是双方轮流完成独立攻击段；
- Major Advantage Reversal 是否有可见控制权变化；
- 双方抢主动方式是否长期同质化。

触发失败：**Turn-taking Combat / Initiative Segmentation**、**Invisible Advantage / Nominal Reversal**、**Homogeneous Initiative Style**。

### E. Contact / Intensity

- 重要 Contact 是否有 Transfer → Reaction → Consequence；
- 连续 Combat 是否存在可感知的强度变化，而不是全程同速 / 同重量 / 同压力。

触发失败：**Contact Solidity Failure**、**Flat Combat Intensity**。

### F. Camera

- Kinetic Scope 明显变化时 Camera 是否跟随；
- `stable / readable` 是否被错误写成长期近似 fixed framing。

触发失败：**Camera Mobility Underfill**。

### G. Prompt Externalization

- Final Prompt 是否由 Action Language 主导；
- 是否 Dump 内部 State / Meta；
- Negative Constraints 是否少而有针对性。

### Gate Failure 行为

```text
定位失败维度
→ 优先重写 Action Phrase / Action Spine / Camera Path / Prompt Assembly
→ 必要时重新分配执行预算
→ 再次 Preflight
→ 通过后才交付
```

> **规则存在不等于规则生效；Final Preflight 拥有否决权。**

---

## 19. 边界与最终原则

- Core 是 State / Continuity 真源；
- Choreography 不复制专项动作知识；
- Modern / Wuxia 负责具体表现；
- Fighting / Martial / Weapon Libraries 提供专业可组合动作知识；
- Controls 提供通用 Camera / Motion / Spatial / Audio / Prompt Assembly；
- Model Adapter 只改变执行路径与序列化，不改导演意图。

最终原则：

> **动作要足够多，但不是独立动词堆叠。**  
> **连续打斗不是动作排得更近，而是后一个动作从前一个动作的身体与空间状态里长出来。**  
> **镜头要稳定可读，但 Stable ≠ Static。**  
> **连续不等于匀速；高密度不等于同强度。**  
> **状态机留在内部，最终 Prompt 交付一条真正连续、可见、可执行的动作主链。**
