# Action Combat Choreography Playbook

## 1. 职责

本文件是 `action-combat-video` Task 内的 **Combat Choreography Engine / 动作编排引擎**。

它负责：

- 战斗真正打多久；
- 有效攻防是否足够丰富；
- Action Phrase 如何连续组织；
- 双方打法是否有明显身份差异；
- 环境如何参与战术与空间变化；
- 接触是否有可信受力 / 压力 / 兵器反馈；
- 是否形成值得记住的 Signature Moment；
- 动作、Camera、Audio 与模型执行预算如何协调；
- 最终 Prompt 如何把内部状态转译成正向、可见、可执行的动作语言。

它**不替代** `core-playbook.md` 的 Combat State / Continuity Runtime Skeleton，也不替代 Modern / Wuxia 等专项 Playbook 的具体动作语言。

核心分工：

> **Core 负责“打得对、接得上”。**  
> **Choreography 负责“打得够、丰富、好看、有实感”。**  
> **专项 Playbook 负责“这种战斗具体怎么表现”。**

---

## 2. Combat Planning Graph

Quick 与 Interactive 共用同一规划图：

```text
理解 Combat Intent / 观看目标
→ 判断 Combat Branch
→ Cinematic Choreography Profile
→ Active Combat Coverage
→ Action Exchange Rhythm
→ Combat Character Identity
→ Contact Modality / Environment Affordance
→ Camera Intent
→ Model Combat Capability Input（如有）
→ Action Execution / Camera Readability Budget
→ Signature Moment
→ Action Phrase / Battle Beat
→ Core State / Continuity Validation
→ Combat Audio Coordination
→ Final Prompt Action Externalization
```

Quick Mode：完整规划但静默解决低风险、高置信度决策。  
Interactive Mode：只把高影响、低置信度、真正存在明显分叉的决策暴露给用户。

> **Quick 与 Interactive 的成片质量上限相同，区别只是用户控制程度。**

---

## 3. Cinematic Choreography Profile

Profile 回答“整场动作戏看起来怎么打”，不是角色职业，也不是视觉 Style。

第一版稳定基础方向可包括：

- 写实战术型；
- 凌厉电影动作型；
- 高手连续攻防型；
- 重型硬派型；
- 环境技巧型。

可主次混合，但禁止一次叠加大量互相冲突 Profile。

Profile 主要影响：

- Coverage 倾向；
- Rhythm；
- Exchange Depth；
- Contact Solidity 的表现重点；
- Range 变化方式；
- Environment 使用程度；
- Phrase 节奏；
- Camera Complexity 倾向。

具体稳定知识由 `combat-choreography-profiles` Library 提供；本 Playbook 只负责选择和协调。

---

## 4. Active Combat Coverage

Timeline 写满不等于 Combat 写满。

内部使用 **Active Combat Coverage / 有效交战覆盖率**：

- Low：约 40–55%；
- Medium：约 60–75%；
- High：约 75–90%。

Coverage 是软目标，不是机械百分比。关键是判断整段时间中有多少内容真正推动下一次攻防。

High Coverage 允许：

- 受击反馈；
- 失衡；
- 闪避；
- 恢复；
- 抓控中的主动争夺；
- 快速重新切入；
- Range 改变；
- 直接制造下一次攻击机会的短促反应。

只要这些反馈仍在推动战斗，就属于 Active Combat，不算真正 Downtime。

### 4.1 四类时间预算

内部可将总时长粗分为：

- Setup Budget；
- Active Exchange Budget；
- Combat Downtime Budget；
- Ending Budget。

约 15 秒、High Coverage、高手 1v1 可参考：

- Setup：0.5–1.5s；
- Active Exchange：11–13s；
- 累计真实 Downtime：尽量 ≤1–2s；
- 纯 Ending Pose：约 0.5–1s。

这些只用于规划，不要求最终 Prompt 暴露计算过程。

---

## 5. Action Exchange Rhythm

Coverage 回答“打多久”；Rhythm 回答“持续交战期间怎么交换”。

基础方向：

- 重击型；
- 均衡型；
- 高手高速交换型；
- 混合型。

混合型不是随机切换，而是让不同 Action Phrase 承担不同节奏角色，例如快速 Counter-to-Counter 后接一次有明显重量的 Payoff，再重新进入高速交换。

不要因为 High Coverage 就把整段写成同一种速度。

---

## 6. Action Phrase

层级：

```text
Action–Reaction Pair
→ Action Phrase
→ Battle Beat
→ Combat Sequence
```

Action Phrase 是 V2 的主要连续动作组织单元。

可参考：

```text
Setup / Entry
→ Attack
→ Defensive Answer
→ Counter
→ Re-counter / Continuation
→ Phrase Payoff
```

但这只是可选语法，**禁止固定六步模板**。

Phrase 的关键判断：

> **前一个动作是否自然制造了下一个动作的机会。**

Phrase 边界可出现在：

- 局部 Payoff；
- 新攻击窗口形成；
- Range / Position / Environment 关系显著改变；
- 节奏切换；
- 单个 Phrase 已接近模型执行 / 可读性上限。

Phrase 结束不等于停战。多个 Phrase 可以无缝连接在同一个 Battle Beat 中。

Battle Beat 只有在战术目标、主导权、关键 Condition、主目标、战斗阶段或 Turning Event 实质变化时才应切换。

---

## 7. Exchange Depth

Exchange Depth 衡量：

```text
Defense
→ Counter
→ Re-counter
→ Continuation
```

的因果深度，而不是动作动词数量。

软倾向：

- 重击型：低到中深度；
- 均衡型：中深度；
- 高手高速交换型：更高深度；
- 混合型：不同 Phrase 交替深浅。

实际 Depth 由以下因素动态决定：

- Phrase 可用时长；
- Coverage；
- Profile；
- Character Identity；
- Range / Advantage / Condition；
- Tactical Interaction；
- Environment / Spatial Complexity；
- Camera Readability Budget；
- Model Capability。

如果单个 Phrase 过载，优先拆成多个无缝 Phrase，而不是把整个 Beat 的有效交换压缩到很少。

---

## 8. Combat Character Identity

Character Identity 回答：**当前这个角色怎么打。**

它必须动态推导，不能按职业模板映射。

输入可包括：

```text
人物明确设定
+ 体型 / 能力 / 经验（如已知）
+ 性格 / 行为倾向（如已知）
+ Combat Intent
+ 环境 / 空间限制
+ 对手打法 / 双方差异
+ Choreography Profile
+ Range / Advantage / Condition
→ Combat Character Identity
```

可关注：

- Combat Preference；
- Movement Signature；
- Attack Character；
- Defense / Counter Character。

这些维度是动态推理维度，不是封闭字段表。

随后才根据需要选择 / 混合 Fighting / Martial / Weapon Profile。

> **职业 ≠ Character Identity ≠ Fighting Profile。**

例如“职业杀手”不能自动等于 Tactical Close Combat。

---

## 9. Tactical Interaction

Tactical Interaction 是 Action Phrase 内部可选的战术因果层。

Exchange Depth 回答“有多深”；Tactical Interaction 回答“为什么进入下一层”。

可用机制包括：

- Feint；
- Probe & Read；
- Bait；
- Anticipation；
- Counter-to-Counter；
- Pattern Break；
- Forced Response。

是否启用取决于：

- 角色能力与双方水平关系；
- Profile；
- Rhythm；
- Exchange Depth；
- 当前 Range / Advantage / Condition；
- Phrase 时长；
- 模型执行与可读性。

高手 / 势均力敌 / 高 Exchange Depth 场景更适合增加 Tactical Interaction；重型硬派、经验不足、单纯压制型场景可以很少甚至不使用。

不要在每个 Phrase 都强行加入假动作或诱导。

最终 Prompt 应描述可见动作与时机，而不是解释角色“心里预判了什么”。

---

## 10. Environment Action Affordance

环境先作为“可以怎样参与动作”的机会进入规划，而不是先决定随机破坏物体。

```text
场景对象 / 空间结构 / 障碍
→ Environment Action Affordance
→ Intent / Identity / Range / Advantage 过滤
→ Action Phrase
→ 更新 Position / Range / Advantage / Condition / Environment State
```

有效 Environment Action 至少应改变一项：

- 攻击路线；
- 移动路线；
- Range；
- Advantage；
- 战术选择；
- Phrase Payoff；
- Camera Handoff。

例如桌子可以改变线路、边界、支撑或绕位；椅子可以扰乱追击 / 步法；隔断可以成为压力边界。

禁止为“丰富”而让角色随机使用多个无关物件。

---

## 11. Combat Contact Solidity

Combat Contact Solidity 控制所有主要战斗接触的**物理 / 材质 / 战术可信度**。

通用链：

```text
Commitment
→ Contact Event
→ Force / Energy / Pressure Transfer
→ Reaction Propagation
→ State Consequence
→ Recovery / Continuation
```

动态 Contact Modality 可包括：

- Strike；
- Grapple / Control；
- Takedown / Throw；
- Blunt Weapon；
- Blade / Edge / Thrust；
- Weapon Clash / Parry；
- Environment Impact。

这不是封闭分类，可按任务合并 / 扩展。

内部可区分 Light / Solid / Heavy，表示当前接触的感知强度与战术后果，不代表所有模态都追求“越重越好”。

### 11.1 通用检查

- Commitment 是否看得到；
- Contact 是否清楚；
- Force / Pressure Transfer 是否成立；
- Reaction 是否从接触位置传播；
- 是否留下可继承 Consequence；
- Recovery / Continuation 是否自然进入下一拍。

### 11.2 不同模态

Strike：身体驱动、接触清晰、守架 / 重心 / 呼吸反馈。  
Grapple / Control：持续连接、压力方向、杠杆、夺重心、逃脱代价。  
Takedown / Throw：破坏平衡、轨迹、落地与位置后果。  
Blunt Weapon：挥动惯性、接触负载、兵器 / 身体位移。  
Blade：危险线路、距离、躲避 / 偏转、接触后果，不使用“重拳感”模板。  
Weapon Clash：接触点 / 角度、偏转 / bind、兵器与身体反应、主动权变化。  
Environment Impact：具体材质接触、反弹 / 支撑 / 位移与空间后果。

> **Camera / Audio 可以强化 Contact，但不能替代真实动作接触。**

---

## 12. Signature Moment

Signature Moment 是 Combat Sequence 级少量记忆点，不是每个 Beat / Phrase 都要有的“特技动作”。

约 15 秒短片默认追求 1 个主要 Signature Moment；有充分理由时可增加辅助记忆点。

来源可包括：

- Counter / Re-counter 高潮；
- 环境反制；
- 力量 / 体型差异视觉 Payoff；
- Weapon Distance Transition；
- 假破绽诱导；
- 动量重定向；
- 主导权瞬间翻转；
- 身体轴线 / 空间关系明显变化。

Signature Moment 必须由前后 Phrase 因果“挣来”，不能随机插入一个炫技动作。

Signature Moment ≠ slow motion。Camera 只负责让它更清楚、更有冲击。

若使用 `signature-moment-patterns` Library，吸收的是可迁移 Pattern 机制，不复制影视完整动作段。

---

## 13. Action Execution Budget

V2 不再使用 Battle Beat 全局固定动作数量上限。

> **限制的是同一短时间窗口中模型需要同时理解与执行的复杂信息，不是整个 Beat 最多能发生多少动作。**

Action Phrase 是主要复杂度控制单元。

动态输入：

- Phrase / Beat 可用时长；
- Active Exchange Budget；
- Rhythm；
- Exchange Depth；
- Tactical Interaction；
- Profile；
- Character Identity；
- Range / Advantage / Condition；
- Environment / Spatial Complexity；
- Camera Readability Budget；
- Model Capability。

### 13.1 过载处理顺序

1. 删除重复、装饰性、无状态价值动作；
2. 降低单个 Phrase 的次要分支 / Tactical Complexity；
3. 降低不必要 Camera Complexity；
4. 把过载 Phrase 拆成两个或多个无缝连续 Phrase；
5. 只有仍无法稳定执行时，才缩减次要有效交换。

Phrase 拆分不等于停战。

---

## 14. Action Sufficiency Check

Action Execution Budget 防止同一窗口过载；Action Sufficiency Check 防止整段动作不足。

触发信号：

- Medium / High Coverage 留有大量未使用 Active Exchange 时间；
- 高速 / Mixed Rhythm 但实际 Exchange Depth 很低；
- 足够长的 Beat 只有极少有效交换，且没有重型 Payoff / 环境 / 故事 / 状态理由；
- Phrase 之间频繁站立、观察、摆 Pose、重新起势；
- 用户要求高手持续对决 / 拳拳到肉，但计划主体是长时间控制、僵持或定位。

不设置固定最低动作数量。

修复方式：增加有效 Action Phrase / 因果交换，减少无价值 Downtime，而不是堆独立动词。

---

## 15. Clarity Through Structure, Not Action Reduction

正式原则：

> **Clarity Through Structure, Not Action Reduction.**  
> **通过结构获得清晰，而不是通过动作通缩获得清晰。**

优秀动作戏天然高信息密度。问题不是元素多，而是：

- 是否有因果；
- 是否把过多独立信息塞进同一个短窗口；
- 镜头是否可读；
- 模型是否可执行；
- 动作是否重复 / 装饰性而没有改变战斗关系。

执行口径：

> **高信息密度，但低混乱度。**  
> **清晰优先，但不以削减有效攻防换取清晰。**  
> **宁可少冗余，不可少有效攻防。**

---

## 16. Camera Readability Budget

Camera Complexity 与 Action Complexity、Spatial Complexity 共享有限执行 / 感知预算。

高 Coverage、高 Exchange Depth、高 Tactical Interaction、多人、高速换位、复杂环境时：

- 优先稳定 medium / medium-wide；
- 清楚保留双方身体关系；
- 减少无必要切镜、快速镜头变化与侵略性运镜；
- 让 Camera 跟随动作因果，而不是掩盖动作。

低动作复杂度、重型 Payoff、明显空间翻转或 Signature Moment 时，可有目的释放更多 Camera 表现力。

> **镜头为动作服务；复杂动作先保证看清，简单爆点再释放镜头表现力。**

Camera 仍由通用 `camera-direction` Control 提供镜头语言；本文件只定义 Combat 侧预算与协调原则。

---

## 17. Combat Audio Choreography

Audio 与 Action / Camera 同一因果链设计，但不建立庞大独立 Combat Audio 系统。

Audio 参与：

- Action Phrase Rhythm；
- Combat Contact Solidity；
- Body State / Breath；
- Weapon / Material Feedback；
- Environment / Spatial Feedback；
- Phrase Payoff / Signature Moment。

正式原则：

> **Audio Accent Density ≠ Action Density.**  
> **动作密集，不代表每个微动作都需要独立强化音效。**

声音层级可分：

- 基础动作 / 环境声音；
- 关键 Contact Accent；
- Phrase Payoff Accent；
- Signature Moment Accent。

必要时可以用短暂声音收缩 / 环境底噪变化制造对比，但不能把某种声音套路机械复用。

不同 Contact Modality 使用不同声音证据；禁止用统一低频、Camera Shake 或夸张 Boom 掩盖动作接触不成立。

具体音画同步仍由 `audio-visual-sync` Control 提供通用规则。

---

## 18. Model Combat Capability Input

如果目标 Model Adapter 提供 Combat Capability Contract，则将其作为执行预算输入，典型维度：

- Motion Complexity Capacity；
- Multi-character Stability；
- Contact / Interaction Fidelity；
- Spatial Continuity；
- Camera Complexity Capacity；
- Temporal / Prompt Following。

Model Capability 只能影响“怎么稳定实现”，不能擅自降低用户已经确定的 Combat Intent、Coverage 或观看目标。

降载优先顺序：

```text
保留 Combat Intent / Coverage
→ 降低无必要 Camera Complexity
→ 降低单 Phrase 同时复杂度
→ 拆成更多无缝连续 Phrase
→ 简化次要 Environment / Tactical 分支
→ 最后才缩减次要动作细节
```

没有模型专项能力信息时使用 Generic 保守判断，不凭空声明模型能力。

---

## 19. Two-stage On-demand Loading

### Stage 1：Planning

优先使用：

```text
action-combat-video/index
+ core-playbook
+ choreography-playbook
+ 当前一个专项 Playbook
+ 必要 Library 轻量 index
+ 可选 Model Capability 摘要
→ Combat Planning Context
```

Planning Context 只记录当前任务真正需要的变量，例如：

- Combat Branch；
- Choreography Profile；
- Coverage；
- Rhythm；
- Character Identity 倾向；
- Contact Modality；
- Environment 参与程度；
- Signature Moment Need；
- Camera / Model 风险。

### Stage 2：Execution Knowledge

正常情况下只展开约 2 个主要 Library Detail Slot：

```text
Slot A：Technique / Execution Knowledge
→ Fighting / Martial / Weapon Profile

Slot B：Choreography Enhancement Knowledge
→ Signature Moment Pattern 或其他必要增强知识
```

优先级：

```text
用户明确指定的专业动作 / 武器知识
→ 保证正确执行所需知识
→ Character Identity 差异化知识
→ Signature Moment / 创意增强知识
```

> **Indexes are cheap routing knowledge; leaf files are expensive execution knowledge.**  
> **索引用于选择，正文用于执行。**

`source-cases/` 默认不进入正常运行上下文。

---

## 20. State Machine Internalized, Choreography Externalized

内部继续完整运行：

- Range；
- Advantage；
- Condition；
- Exchange Depth；
- Tactical Interaction；
- Contact Solidity；
- Environment Affordance；
- Execution / Camera Budget；
- State Contract。

最终 Prompt 不应该大量 Dump 这些抽象标签。

优先级：

```text
正向可见 Action Phrase / 因果交换 / Contact / Reaction
→ 空间与环境变化
→ 动作速度 / 重量 / Rhythm / Signature Moment
→ Camera / Audio
→ 少量真正必要的连续性 / Negative Constraints
```

示例内部状态：

```text
Range: Close
Advantage: A slight advantage
B balance compromised
Contact: Solid
Tactical: Counter-to-Counter
```

最终应该写成可见动作：A 压近，B 偏开手臂切线反击；A 提前截住反击窗口用短促攻击打断，接触让 B 半步失衡，B 借桌沿稳住重心并立即重新切入。

> **内部用结构做导演，外部用画面语言让模型演。**

---

## 21. Final Pre-output Check

Combat Final Prompt 组装前至少检查：

### 21.1 Coverage

- Active Exchange 是否兑现？
- 是否存在无价值长对峙 / Pose / reset？

### 21.2 Choreography

- 是否有多个真正因果连续的 Action Phrase？
- Rhythm / Exchange Depth 是否符合目标？
- Character Identity 是否能从动作看出来？

### 21.3 Contact

- 重要接触是否有 Contact → Reaction → Consequence？
- 是否使用了正确 Contact Modality？

### 21.4 Environment / Signature

- 环境参与是否真正改变战术 / 空间？
- Signature Moment 是否由前后动作因果支撑？

### 21.5 Readability / Executability

- 是否同一短窗口塞入过多独立信息？
- Camera 是否抢占动作执行预算？
- 模型能力风险是否已通过结构化降载处理？

### 21.6 Prompt Externalization

- Final Prompt 是否由正向动作语言主导？
- 是否无必要地重复状态解释 / Negative Boilerplate？

---

## 22. 与其他层的边界

### Core Playbook

提供 State / Continuity / Battle Runtime Skeleton，本文件必须服从其 Range / Advantage / Condition / State Contract 真源。

### Modern / Wuxia

负责具体动作语言、物理尺度、默认 Range / Rhythm / Contact 表现；不能反向重定义本文件的通用质量合同。

### Controls

继续使用通用 Controls：

- timeline-rhythm；
- subject-motion；
- camera-direction；
- spatial-blocking；
- continuity-consistency；
- audio-visual-sync；
- prompt-assembly；
- realism-quality（需要时）。

本文件不复制这些 Control 的通用正文。

### Libraries

只读取当前任务需要的 Fighting / Martial / Weapon / Environment / Choreography Profile / Signature Pattern 等知识，不让 Library 反过来承担导演流程。

### Model Adapter

只提供模型能力与序列化差异，不覆盖用户导演意图。

---

## 23. 最终原则

> **动作要足够多，但不是无因果堆叠。**  
> **接触要足够实，但不是每一下都 Heavy。**  
> **镜头要有电影感，但不能抢走动作可读性。**  
> **声音要证明动作，但不能替动作表演。**  
> **状态机留在内部，最终 Prompt 把它变成连续可见的动作。**
