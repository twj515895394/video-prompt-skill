# Action Combat Video Task Router

## 1. 何时进入本任务

当用户的主要目标是生成或设计**动作格斗 / 武术 / 武侠战斗视频 Prompt**，且成败高度依赖持续攻防、动作因果、距离变化、空间站位、受力反馈、多人目标切换、兵器连续性或动作导演质量时，读取本任务。

典型信号：

- 近身格斗、拳脚、摔投、缠斗、制服；
- 1v1 / 1vN 动作戏；
- 武术、武侠、刀剑枪棍交锋；
- 用户明确要求动作连续、高手对决、拳拳到肉、兵器轨迹、长镜头打斗；
- 普通 `text-to-video` / `image-to-video` 已不足以表达 Combat State + Choreography 双重要求。

本任务是执行差异明显的专项工作流，不只是题材标签。

---

## 2. 不进入本任务的情况

- 只有一个简单挥拳、跑动或体育动作：继续使用原主任务 + `action-motion`；
- 用户主要提供故事板并要求管理整部多镜头片段：主任务仍可为 `storyboard-and-multi-shot-video`，Combat 作为专项编排知识按需引用；
- 用户主要要求视频局部编辑 / 延长：主任务仍由对应编辑 / 延长 Playbook 决定；
- 枪战：当前没有正式 Gunfight 专项 Playbook，除非后续扩展，否则只复用可迁移的 Combat Core / Choreography 原则，不伪装成已完整支持分支。

---

## 3. Combat 运行结构

进入本任务后，运行时骨架固定为：

```text
core-playbook.md
+ choreography-playbook.md
+ 1 个当前专项 Playbook
+ Planning Gate
+ Stage-2 Pattern Hit Evidence Gate
+ Persistent Combat Signature Contract（存在明确 Character / Technique Identity 时必经）
+ subject-motion/control.md（短时 High Kinetic / Whole-body 条件命中时必经）
+ 按缺口选择的其余少量 Controls
+ 按需展开的少量 Library Detail
+ action-camera-handoff-playbook.md（Camera 允许 Cut / Reframe / 景别变化时必经；one-take 仍用于 Movement/Reframe Handoff）
+ 可选 Model Adapter
+ prompt-assembly/control.md（Combat 必经）
+ Combat Final Preflight（必经）
+ Prompt QA / Self-Repair Gate（必经）
+ 当前输出模板 / Model Serialization
```

其中 `prompt-assembly/control.md` 在普通任务中仍可按需读取；**一旦进入 Action Combat，则不占普通 `0-3 Controls` 可选预算，必须在最终交付前读取并执行。**

当 Combat Camera 允许 Cut、明显景别变化、Impact / Insert / Re-establish 或动态 Reframe 时，必须读取并执行：

`action-camera-handoff-playbook.md`

如果用户明确要求严格 one-take，也不需要 Editorial Cut，但仍应使用该文件的 Motion / Energy Carry-over 与 Action-triggered Camera Movement / Reframe 规则。

### `core-playbook.md`

负责 Combat State / Continuity / Battle Runtime Skeleton：Combat Intent、Spatial Map、Range / Advantage / Condition、Turning Event、Target Handoff、Beat State Contract、Position / Environment / Weapon State 与连续性验证。

### `choreography-playbook.md`

负责 Combat Choreography Engine：Fighting Direction / Choreography 执行属性、Active Combat Coverage、Rhythm、Action Phrase、Executable Granularity、Exchange Depth、Character Identity、Tactical Interaction、Environment Affordance、Contact Solidity、Signature Moment、Action Sufficiency / Execution Budget、Kinetic / Temporal / Motion Continuity、Camera Readability / Mobility / Coverage、Combat Audio、Ending Coverage Protection 与 Final Preflight Criteria。

### `action-camera-handoff-playbook.md`

负责 Stage-2 Pattern Hit Evidence、Motion / Energy Carry-over 与 Action ↔ Camera Bridge：关键 Cut / Reframe 为什么发生、Shot 如何从仍在发生的 Motion / Contact / Pressure / Recovery 中进入，以及 Camera 如何随 Fight-space / Initiative / Level / Support 的真实变化组织 Coverage。

> **Core 负责“打得对、接得上”；Choreography 负责“打得够、连续、丰富、具体、好看、有实感”；Persistent Combat Signature 负责“角色已确认的打法差异不能打一半就消失”；Subject Motion 负责在 High Kinetic 条件下把重心、支撑、惯性、受力与 Whole-body Driver 真正落实；Action–Camera Handoff 负责“动作怎样自然交给镜头、镜头怎样继续同一个动作”；Prompt Assembly 负责“把内部具体设计原样保真地序列化成模型可执行的最终 Prompt”；Prompt QA / Self-Repair 负责“交付前发现实现问题并自动修正”。**

---

## 4. 专项分支路由

Core + Choreography 之后只选择一个主要专项 Playbook。

### 现代格斗

读取：`modern-combat-playbook.md`

包括写实近身格斗、电影化动作片、拳击 / 泰拳 / 散打 / MMA / 摔跤 / 缠斗等动作语言。

### 电影武侠

读取：`cinematic-wuxia-playbook.md`

包括空手武术与刀 / 剑 / 枪 / 棍，默认是电影武侠而非仙侠。

专项 Playbook 只负责具体动作语言、物理尺度、默认 Range / Rhythm / Contact 表现与专业 Profile 使用方式，不得反向重定义 Core / Choreography 的通用质量合同。

---

## 5. Two-stage On-demand Loading

Combat V2 使用：

> **Plan First, Load Detail Second / 先规划，再加载详情。**

### Stage 1：Planning

使用：

```text
Task Router
+ Core
+ Choreography
+ 当前专项 Playbook
+ 必要轻量 Index
+ 可选 Model Capability 摘要
→ Combat Planning Context
→ Planning Gate
```

Planning Context 只保留当前任务需要的轻量变量，例如：

- Combat Branch；
- **Fighting Direction / 怎么打；**
- Coverage；
- Rhythm / Realism / Impact 等执行属性；
- Character Identity 倾向；
- **用户已确认的 Technique Identity / Persistent Combat Signature；**
- Contact Modality；
- Environment Importance；
- Signature Moment Need；
- Camera / Model 风险。

不把所有 Library 正文一次性加载。

Planning Gate 必须先检查：

- Fighting Direction 是否已经由用户明确；若未明确且不同打法会显著改变成片，Interactive 应优先直接询问“怎么打”；
- 是否过早锁定结局；
- Character Identity 是否被职业、性别、年龄、外貌或体型快捷映射；
- 用户已经明确的角色打法 / Technique Identity 是否被保留为后续 Persistent Combat Signature，而不是一次性标签；
- 是否把系统应自动保证的质量条件错误变成用户问卷。

### Stage 2：Execution Knowledge — Gap-driven Routing

Stage-2 不再固定使用“Technique Slot + Enhancement Slot”的机械结构；先检查当前 Phrase / Planning Context 真正缺什么，再选择 Pattern Slot。

```text
Planning / Phrase Gap
├─ 缺路线、身法、高低位、重心、轴线、空间变化
│  → Movement Pattern Slot
├─ 缺具体攻击、防守、腿法、摔控、兵器动作
│  → Technique Pattern Slot
└─ 缺前后动作如何从 Contact / Range / Axis / Momentum 连续接上
   → Transition Pattern Slot
```

每个被命中的 Slot 默认：

```text
1 个主 Pattern
+ 必要时 1 个辅助 Pattern
```

不是必须填满的配额，也不要求三槽全部读取。

当前最小验证知识源：

`references/libraries/combat-choreography-patterns/minimum-validation-set.md`

只有当前 Gap 与 Fighting Direction 真正需要时才读取。现有 Fighting / Martial / Weapon Profile 仍可作为 Technique Detail 或 source/style evidence 按需使用，但不能只增加打法标签。

#### Stage-2 Pattern Hit Evidence Gate

Stage-2 不能只完成“脑内判断”却没有真实 leaf knowledge hit。进入最终 Concrete Action Phrase 前，内部必须能回答：

```text
当前 Execution Gap 是什么
→ 命中哪个 Pattern Slot
→ 实际读取哪个 leaf knowledge
→ 哪个 Pattern / Detail 被实例化进动作
```

出现以下任一情况时，不能在没有 leaf execution knowledge 的状态下直接进入最终 Phrase：

- High / Expert Combat 且目标是连续高手对决；
- Fighting Direction 明确要求 Movement / Level / Axis / Route / Support 发生显著变化；
- 中国武术电影化近身、身法角度争夺、腿法全身攻防、摔控反摔等方向需要具体动作构造差异；
- 连续多个关键 Phrase 主要由 Upper-body Contact 驱动；
- Movement 只是“给上肢动作补脚步”；
- Transition 缺少 Contact / Momentum / Axis / Range / Recovery Handoff；
- Final Preflight 已触发 `Static Standing Combat / Upper-body Technique Dominance`。

当前 CK 最小验证阶段，如果没有更具体且已经读取的专业 leaf knowledge 能完整覆盖对应 Gap：

> **必须读取 `references/libraries/combat-choreography-patterns/minimum-validation-set.md`。**

如果 Phrase 已经生成后才发现 Pattern Hit Evidence 缺失，判 `Stage-2 Routing Evidence Missing`，必须回到 Stage-2 Read + Pattern Selection + Phrase Rewrite；不能只在旧动作上追加“侧切 / 转髋 / 重心变化”等词。

#### Movement 缺席风险

对于 High / Expert Combat，如果连续多个关键 Phrase 都由 Upper-body Technique 主导，而 Movement 只剩附属脚步说明，应将其视为：

`Movement Knowledge Gap / Static Standing Combat Risk`

此时提高 Movement Pattern Slot 的路由优先级，但**不使用“每段必须几次换位 / 踢腿”的固定配额**。

#### Persistent Combat Signature Gate

只要用户、Interactive 或高置信度 Planning 已经明确某个角色的 Technique Identity / 打法差异，就必须把它升级为：

> **Persistent Combat Signature / 持续打法特征**

它不是动作次数配额，也不是要求重复同一 Combo；它回答的是：

> **这个角色持续通过什么动作逻辑创造下一状态、抢 Initiative、改变 Range / Support / Position？**

内部至少从以下维度中选取当前真正有区分度的组合：

- Entry / Range Creation：怎样进入或维持距离；
- State-change Method：通过 Strike / Kick / Grapple / Throw / Weapon / Movement 如何改变 Guard、Support、Axis、Range、Position；
- Initiative Method：怎样抢、续、夺回主动权；
- Continuation Logic：前一动作后果怎样进入下一动作；
- Recovery / Re-entry：受阻或被反制后怎样继续保持角色打法特征。

例如用户明确：

```text
女方：拳腿组合
男方：拳肘 + 抱摔
```

不能只实现成：

```text
女方出现一次低踢
男方尝试一次 body lock
→ 后续双方全部回到同一种前臂 / 抓臂 / 肩线短打
```

应让角色打法在 Combat Spine 的不同阶段持续改变状态，例如：

```text
拳法制造高位 Guard / Reaction
→ 腿法攻击 Support / Range
→ 借 Footwork / Angle 继续进入拳法
```

以及：

```text
短打 / 肘击压缩距离
→ 创造 Clinch / Body-lock Entry
→ 成功摔控、被反摔、被迫换位，或至少迫使对手改变 Support / Position
→ 从这个结果继续下一次贴身进入
```

`Grapple / Throw` 不要求每次成功摔倒，但必须产生真实状态后果；只有“尝试抱住”而没有改变 Balance / Position / Range / Response，不算 Signature Realization。

不做机械次数配额；判断标准是：

- 角色打法是否在整条 Combat Spine 中持续可辨认；
- Concrete Technique 可以变化，但创造状态和抢主动的逻辑不能中途蒸发；
- Major Reversal 前后角色仍然以自己的方式解决问题，而不是双方长期塌成同一种 Counter 模板。

失败判定：

`Technique Identity Evaporation / Persistent Signature Collapse`

修复：回到后续 Concrete Action Phrase / Transition 重写，让打法差异继续产生状态后果；**禁止只补一个孤立踢腿 / 抱摔词来“打卡”。**

#### Subject Motion 条件必读 Gate

当任务同时满足以下条件时，必须在 Concrete Action Phrase 定稿前读取：

`references/controls/subject-motion/control.md`

条件：

- 约 `10–20s` 的短时 Combat；
- 以持续近身攻防 / High Kinetic Scope 为主体；
- Fighting Direction / Character Identity 明确依赖 Whole-body、Footwork、Support / Balance、Range / Position / Axis / Route；
- 或已有上肢锁死、动作断裂、脚步 / 重心只作为上肢动作修饰语的风险。

命中后 `subject-motion/control.md` 占普通 `0-3 Controls` 中 `1` 个名额；不能因为 Core / Choreography 已经描述了 Motion / Continuity 就跳过。

如果命中条件但 Runtime Read List 没有它，判：

`Subject Motion Routing Missing`

必须在 Final Prompt 前补读并重新检查 Whole-body Motor Driver、Support Transfer、Momentum / Recovery、Contact Reaction 与 Continuation。

Stage-2 读取之后必须进入：

```text
Execution Knowledge
→ Persistent Combat Signature Realization（如存在明确角色打法差异）
→ 必要时读取 subject-motion/control.md
→ Movement / Technique / Transition 按当前状态组合
→ Concrete Action Phrase Construction
→ State / Continuity Validation
→ Motion / Energy Carry-over Check
→ Action–Camera Handoff Planning
→ Prompt Assembly
```

**Stage-2 的职责不是只增加打法标签，而是帮助把当前 Planning Context 实例化成具体身体 / 武器动作、Contact / Evasion、即时响应、Footwork / Axis / Range / Position 后果和下一动作入口。**

> **能力很多，不等于每次加载很多；按缺口补知识，而不是按目录读知识。**

---

## 6. Quick / Interactive 共享规划图

Quick 与 Interactive 使用同一个 Combat Planning Graph 和同一套质量标准。

### Quick Mode

> **Quick = Full Planning + Silent Resolution.**

Quick 不因输入简短而跳过：Coverage、Rhythm、Character Identity、Persistent Combat Signature（如命中）、Contact Solidity、Environment、Signature Moment、Camera / Execution Budget、Stage-2 Execution Knowledge、条件命中的 Subject Motion、Concrete Action Phrase、State / Continuity Validation、Action–Camera Handoff、Final Assembly / Final Preflight、Prompt QA / Self-Repair。

如果 Fighting Direction 未明确但当前只有一个明显合理方向，Quick 静默推导；如果存在多个方向，也不进入多轮问答，而按上下文选择基线方案。

### Interactive Mode

只在以下条件同时成立时暴露一个决策：

- 存在多个明显不同方向；
- 方向会显著改变成片；
- 当前信息不足以高置信度选择。

`Fighting Direction / 怎么打` 是上游高价值候选问题：当用户未明确且不同打法会显著改变 Movement / Technique / Range / Physical Scale 时直接询问。候选答案至少 5 个，正常 6–8 个，复杂可到 10 个，并支持自定义；不与旧“核心动作风格 / Choreography Profile”重复询问。

不把 Contact Solidity、Kinetic Scope、Temporal Packing、Motion Handoff、Action Sufficiency、Executable Granularity、Stage-2 Evidence、Persistent Combat Signature QA、Subject Motion Gate、Action–Camera Handoff、Camera Readability、Final Preflight 等基础质量机制变成固定问卷。

Camera Intent 属于条件高价值节点：只有多个观看策略都合理且会显著改变成片时才暴露，不固定必问。

推荐答案不得把人口属性当打法模板。

---

## 7. Combat 必经 Final Assembly / Preflight / QA

输入仍由 `references/inputs/` 判断，不在本任务复制素材规则；输出仍挂接现有 single-shot / multi-shot / model-adapted 模板，不建立平行 Combat 模板。

Action Combat 的最终运行链必须是：

```text
Combat Planning Context
→ Stage-2 Gap-driven Execution Knowledge
→ Stage-2 Pattern Hit Evidence Gate
→ Persistent Combat Signature Realization（如命中）
→ 条件命中时读取 subject-motion/control.md
→ Concrete Action Phrase / Battle Beat
→ Core State Validation
→ Motion / Energy Carry-over Check
→ 读取并执行 action-camera-handoff-playbook.md
→ Action–Camera Handoff Planning
→ Camera / Audio / Spatial Coordination
→ 读取并执行 prompt-assembly/control.md
→ Combat-aware Final Prompt Assembly
→ Combat Final Preflight
→ FAIL：内部回到 Stage-2 Read / Persistent Signature / Subject Motion / Concrete Action Phrase / Pattern Selection / Character Identity / Action–Camera Handoff / Prompt Assembly，并重新检查
→ PASS：进入 Prompt QA / Self-Repair Gate
→ QA FAIL（实现质量问题）：静默修复对应层并重新 QA
→ QA FAIL（必须改变用户已确认创作决策）：Interactive 重新暴露当前唯一必要决策；Quick 不得偷改决策
→ QA PASS：挂接当前输出模板 / Model Adapter
→ Delivery
```

### Final Preflight 最小合并 Gate

最终只回答这些高价值问题：

1. **动作是否够**：Coverage / Exchange Depth / Kinetic Scope 是否与观看目标匹配；Ending 是否吞掉 Active Exchange；
2. **动作是否具体**：关键数秒是否由具体身体 / 武器动作、Contact / Evasion、即时响应、Footwork / Axis / Range / Position 后果与下一动作入口构成，而不是抽象“连续攻防”；
3. **Stage-2 是否真的命中**：存在明显 Movement / Technique / Transition Gap 时是否真实读取 leaf knowledge，并把 Pattern / Detail 变成 Concrete Action；否则判 `Stage-2 Routing Evidence Missing`；
4. **Subject Motion 是否按条件命中**：短时 High Kinetic / Whole-body Combat 命中 Gate 时是否真实读取 `subject-motion/control.md`；若没读，判 `Subject Motion Routing Missing`；
5. **动作是否连续**：是否存在明显 Action Underpacking、Neutral Reset、Turn-taking Combat；Initiative 是否在动作链内转移；关键 Transition 是否有 Motion / Energy Carry-over；
6. **Persistent Combat Signature 是否持续**：角色已确认的 Technique / Character Identity 是否在整条 Combat Spine 中持续通过不同的 State-change / Initiative / Continuation 逻辑体现；如果只在前段出现一次，后续双方塌成同一种打法，判 `Technique Identity Evaporation / Persistent Signature Collapse`；
7. **Movement 是否真的在编排战斗**：High / Expert Combat 中若连续多个关键 Phrase 主要由上肢 Contact 主导，而 Movement 没有主动创造 Level / Route / Axis / Range / Position / Support / Ground-State 变化，则判 `Static Standing Combat / Upper-body Technique Dominance` FAIL；
8. **动作是否有实感和空间后果**：Contact / Range / Position / Environment 是否真正改变下一拍；
9. **镜头是否由动作触发并继续同一个运动**：关键 Cut / Reframe 是否有 Motion / Contact / Consequence / Initiative / Range / Level / Environment Trigger；Cut 后是否继承 Active Motion，而不只保持位置；否则判 `Action–Camera Decoupling / Dead-motion Cut / Kinetic Handoff Loss`；
10. **Camera Coverage 是否跟着战斗空间和观看体验走**：Stable ≠ Static；Action Continuity ≠ Shot Continuity；不机械形成 `Medium → Close → Medium → Close`；Perceptual Impact 不过少也不过密；Hard Constraint 不被违反；
11. **最终序列化是否正确**：高密度 Combat 默认 Continuous Action Spine + Soft Time Anchors，Concrete Choreography、Persistent Signature 与关键 Camera Handoff 不被 Prompt Assembly 压回抽象摘要；
12. **Prompt 是否 Action-first**：Negative 少而有依据，不添加用户未要求的剧情禁止项；
13. **Model Execution Realizability 是否通过**：没有 Effective High Granularity Everywhere、Instruction Saturation 或明显 Prompt–Video Execution Divergence 高风险结构。

任一关键项 FAIL，不允许直接交付。

### Prompt QA / Self-Repair Gate

Combat Final Preflight PASS 后仍执行最后一次成品级 QA。该 Gate 不是重复整个 Planning，而是检查**最终序列化后的成品 Prompt 是否重新引入了问题**。

```text
Final Prompt Draft
→ QA
→ PASS：Delivery
→ FAIL：定位主失败项
   ├─ 实现质量问题
   │  → Silent Self-Repair
   │  → Re-run QA
   └─ 只有改变用户已确认 Creative Decision 才能修复
      → 不得静默改
      → Interactive：重新问当前唯一必要问题
      → Quick：保留决策并输出约束内最佳结果 / 最简冲突说明
```

Combat QA 特别检查：

- Stage-2 Pattern / Detail 是否在 Assembly 后消失；
- Persistent Combat Signature 是否中后段蒸发；
- Subject Motion / Whole-body Driver 是否又被压成上肢主导；
- Action–Camera Handoff / Perceptual Impact 是否被压回一个泛化 Camera 段；
- Base Viewing Priority 是否被错误固化成固定 Shot Pattern；
- Camera Hard Constraint 是否被动态镜头偷偷违反；
- Instruction Saturation 是否因为最终合并 Camera / Audio / Negative 再次出现；
- Ending / Negative / Continuity 是否吞掉 Active Exchange；
- 用户确认的 Technique Identity、Camera 选择和剧情约束是否有任何漂移。

### Self-Repair 权限边界

可以静默修：Phrase 组织、动作 / Camera Handoff 外显、Granularity、重复描述、Instruction Saturation、低价值 Negative / Camera / Audio、Ending 占比，以及已经确认内容在序列化中的遗漏。

不能静默改：Fighting Direction、Persistent Combat Signature / Technique Identity、Base Viewing Priority、Camera Hard Constraint、人物身份、剧情关系、胜负 / Ending 意图、用户明确必须保留 / 禁止项。

默认发现问题先执行 `1` 次静默修复并重新 QA；复杂依赖问题可再修一次，但不做无止境循环。

> **质量问题修实现；创作决策要么保留，要么重新问。**

---

## 8. Lightweight Action Phrase Budget

Granularity 只控制信息展开深度，不控制动作数量配额：

```text
Major Reversal / Initiative Theft / Signature Moment
→ High Granularity

普通 Exchange / Re-counter / Range Change
→ Medium Granularity

纯连接 / 非关键过渡
→ Low Granularity
```

如果连续两个 Phrase 已经使用 High Granularity，后续普通 Exchange 优先压缩为 Medium / Low，给更多真实 Exchange 留执行空间。

Medium / Low 仍必须保留基本动作因果，不能退回“连续格挡 / 快速反制 / 持续缠斗”。

明确禁止：固定动作数、固定字数、固定秒数、固定 High/Medium/Low 占比。

---

## 9. 输出模板覆盖关系

Combat 不建立独立 single-shot / multi-shot 模板副本，但**专项 Task 规则优先于通用模板默认规则**。

高密度 Combat 默认继承 `Continuous Action Spine + Soft Time Anchors`；只有用户明确逐秒、外部同步、多镜头边界或 Model Adapter 有实测依据时才使用 Hard Time Blocks。即使使用 Hard Time Blocks，也必须跨块保持 Motion Handoff。

如果 Final Prompt 包含关键 Cut / 景别变化 / Reframe，Camera 不能只在动作段后写一句“关键接触切近”；关键 Handoff 应锚定到具体 Action Moment，并保持 Action State / Active Motion 连续。

最终 Prompt 遵循：

> **State Machine Internalized, Choreography Externalized.**  
> **Concrete Choreography In, Concrete Choreography Out.**  
> **Persistent Combat Signature Across the Spine.**  
> **Action Drives Camera; Camera Preserves Live Motion.**  
> **时间码服从动作连续性，而不是动作服从时间码。**

---

## 10. 上位原则

> **约束错误，不约束创作。**  
> **Clarity Through Structure, Not Action Reduction.**  
> **高信息密度，但低混乱度。**  
> **质量问题自动修实现，已确认创作决策不偷改。**  
> **少建运行时概念，多做高价值质量检查。**

Battle Beat、Action Phrase、Pattern、Persistent Combat Signature、Action–Camera Handoff、Golden Scenario 都不是固定动作 / 镜头模板。

禁止为了“清晰”默认削减有效攻防；复杂度优先通过结构、Phrase 切分、Camera Readability、Action-triggered Handoff、Persistent Signature 与模型执行预算处理。新增 Failure Signature 不自动意味着新增 Runtime 模块。
