# Action Combat Video Prompt Spec V2

> 状态：设计中（Grill Me 持续收敛）  
> 基线：`docs/action-combat-video-spec.md`  
> V1 状态：已完成设计、实现与静态回归

## 1. V2 背景

V1 已较完整解决 Combat Intent、Spatial Map、Range / Advantage / Condition、Turning Event、Action–Reaction Pair、Battle Beat、Target Handoff、Beat State Contract、Action / Camera / Audio 协同，以及受力、空间和环境状态连续性。

真实生成测试暴露的新问题是：

> **15 秒时间轴虽然完整，但真正持续交战只有约 2–3 秒，有效攻防交换也只有两三次。**

典型表现包括：开场对峙过长、抓腕和控制等低动态状态占用大量时长、Battle Beat 内连续攻防不足、职业标签过度映射固定打法、双方打法同质、环境只在事后修改状态、V1“宁少而清晰”被过度执行导致动作预算通缩，以及部分生成打斗接触软绵绵、缺少真实力量和后果。

因此 V2 不推翻 V1，而是在其上增强正式的 **Combat Choreography Engine（动作编排引擎 / 动作导演层）**。

## 2. V1 与 V2 职责拆分

V1：

```text
Combat Intent
→ Spatial Map
→ Range / Advantage / Condition
→ Action–Reaction Pair
→ Turning / Handoff
→ Beat State Contract
→ Continuity / Physics Validation
```

V2：

```text
Combat Choreography Intent
→ Cinematic Choreography Profile
→ Active Combat Coverage
→ Action Exchange Rhythm
→ Combat Character Identity
→ Environment Action Affordance
→ Action Phrase Design
→ Tactical Interaction（按需）
→ Combat Contact Solidity
→ Signature Moment Planning
→ Battle Beat
→ V1 State / Continuity Validation
→ Camera Readability Budget / Camera Coordination
→ Audio Coordination
→ Final Prompt Compression
```

核心原则：

> **Combat Choreography Engine 负责“打得好不好看、够不够、实不实”。**  
> **Combat State / Continuity Engine 负责“打得对不对、接不接得上”。**  
> **约束错误，不约束创作。**

---

## 3. V2-01：Combat Choreography Engine

正式新增动作编排引擎，负责：

- 有效交战时间；
- 单位时间攻防交换丰富度；
- 角色打法差异；
- 整场电影动作观感；
- Action Phrase 组织；
- 节奏变化；
- 环境动作机会；
- Tactical Interaction；
- Combat Contact Solidity；
- Signature Moment；
- 可读性与模型可执行性的动态平衡。

它不替代 V1 Range / Advantage / Condition / State Contract。

## 4. V2-02：Active Combat Coverage

新增 **Active Combat Coverage / 有效交战覆盖率**。

> Timeline Coverage ≠ Combat Coverage

Interactive 可表达为：

- **Low**：约 40–55%，剧情 / 对峙倾向；
- **Medium**：约 60–75%，标准电影动作戏；
- **High**：约 75–90%，持续高手对决。

类似“15 秒、高手 1v1、办公室近身对决”默认推荐 High。

High 不等于全程同速高速动作；只要受击、失衡、闪避、恢复、快速重新切入等反馈直接推动下一次攻防，仍属于 Active Combat。

## 5. V2-03：Action Exchange Rhythm

Coverage 决定“有多少时间在打”；Rhythm 决定“持续交战期间如何交换”。

基础类型：

1. **重击型**：交换较少，但重量、失衡、碰撞和恢复明显；
2. **均衡型**：连续攻防与关键重击均衡；
3. **高手高速交换型**：高频 Attack / Defense / Counter / Re-counter；
4. **混合型**：高速交换 → 重型 / 环境 Payoff → 再进入高速交换。

## 6. V2-04：Action Phrase

层级：

```text
Action–Reaction Pair
→ Action Phrase
→ Battle Beat
→ Combat Sequence
```

- Action–Reaction Pair：原子攻防交互；
- Action Phrase：连续攻防段；
- Battle Beat：一个战术 / 剧情攻防阶段；
- Combat Sequence：整场动作戏。

Action Phrase 的核心是：

> **前一个动作自然制造下一个动作的机会。**

可参考但不强制：

```text
Setup / Entry
→ Attack
→ Defensive Answer
→ Counter
→ Re-counter / Continuation
→ Phrase Payoff
```

禁止实现成固定六步模板。

## 7. V2-05：Combat Character Identity

角色战斗身份回答“当前这个角色怎么打”。动态判断至少关注：

- Combat Preference；
- Movement Signature；
- Attack Character；
- Defense / Counter Character。

这些只是推导维度，不是固定标签全集。

```text
人物设定 / 体型能力 / 性格
+ Combat Intent
+ 当前环境
+ 对手关系
+ Cinematic Choreography Profile
        ↓
动态推导 Combat Character Identity
        ↓
选择 / 混合适合的 Fighting / Martial / Weapon Profile
        ↓
Action Phrase
```

## 8. V2-06：Cinematic Choreography Profile

新增 **Cinematic Choreography Profile / 电影动作编排风格**：

- Combat Character Identity：决定“角色自身怎么打”；
- Cinematic Choreography Profile：决定“整场动作戏看起来怎么打”。

第一版基础方向可包含：

- 写实战术型；
- 凌厉电影动作型；
- 高手连续攻防型；
- 重型硬派型；
- 环境技巧型。

允许“主动作编排风格 + 少量辅助倾向”，禁止堆叠互斥风格。

它不进入 `references/styles/` 一级视觉 Style；由 Combat Playbook 选择 / 协调，由 `combat-choreography-profiles` Library 提供约 5–7 个稳定基础原型，不建设无限扩张的动作片风格百科。

## 9. V2-07：Combat Interactive Mode 专属决策链

```text
核心战斗目的 / 观看目标
→ Cinematic Choreography Profile
→ Active Combat Coverage
→ Action Exchange Rhythm
→ Combat Character Identity
→ 环境参与程度
→ Camera Mode
→ 战斗结果 / 收尾
```

规则：

- 上游选择驱动下游推荐；
- 可高置信度推断且不会明显改变成片的变量自动补全；
- 只询问会实质改变动作编排、持续交战、角色打法、环境、Camera 或结局的变量；
- 始终一次只问一个最关键问题。

## 10. V2-08：Coverage 四类时间预算

Active Combat Coverage 映射为：

1. **Setup Budget**；
2. **Active Exchange Budget**；
3. **Combat Downtime Budget**；
4. **Ending Budget**。

对于“15 秒、高手 1v1、High Coverage”可采用内部参考：

- Setup：约 0.5–1.5 秒；
- Active Exchange：约 11–13 秒；
- 累计 Downtime：尽量 ≤ 1–2 秒；
- 纯 Ending Pose：约 0.5–1 秒。

均为软预算，不是硬秒表。Ending 不应提前终止交战；最后一轮 Action Phrase 可以直接延伸进入 Ending。

## 11. V2-09：Exchange Depth

新增 **Exchange Depth / 攻防交换深度**。

> **Exchange Depth ≠ Action Verb Count**

衡量一次发起后连续 Defense → Counter → Re-counter → Continuation 的因果深度，而不是招式名数量。

主要受 Rhythm、Phrase 时长、Choreography Profile、Character Identity、Range / Advantage / Condition、环境复杂度、Camera Complexity 和视频模型可执行性共同决定。

倾向：重击型低～中，均衡型中等，高速交换型高，混合型在多个 Phrase 间形成节奏反差。“1–2 / 2–3 / 3–5 轮”等只能作为软倾向。

## 12. V2-10：Battle Beat 与 Action Phrase 动态一对多

确认 **Battle Beat : Action Phrase 动态一对多**，不默认 `1 Beat = 1 Phrase`。

- Phrase 切分服务局部连续攻防组织；
- Beat 切分服务更高层战术状态变化。

Phrase 可因局部 Payoff、重新建立攻击窗口、Range / 路线 / 环境方式变化、节奏切换或模型可执行性而结束；Phrase 之间可以无缝衔接，不要求 Downtime。

Beat 只在战术目标、Advantage、关键 Condition、主交战对象、战斗阶段或 Turning Event 实质变化时切换。

## 13. V2-11：Combat 中文术语统一

英文保留 Choreography；中文统一：

- Combat Choreography Engine → **动作编排引擎 / 动作导演层**；
- Cinematic Choreography Profile → **电影动作编排风格**；
- Action Choreography → **动作编排**；
- Action Phrase → **动作句 / 连续攻防段**。

不再以“编舞”作为 Combat 的主要中文翻译。

## 14. V2-12：Combat Character Identity 动态推导，不建角色画像库

不建立“杀手 / 军人 / 警察 / 拳手”等职业画像到固定打法的模板映射。

Combat Character Identity 是当前 Combat Sequence 的动态推导结果。Library 只保存相对稳定、可复用的专业动作知识，例如 Boxing、Muay Thai、Sanda、MMA、Grappling、Tactical Close Combat、传统 Martial Profile、兵器动作知识等。

> **人物 / 职业提供背景线索；Combat Character Identity 决定当前角色怎么打；Fighting / Martial / Weapon Profile 提供专业动作语言。**

## 15. V2-13：小型 `combat-choreography-profiles` Library

正式新增该 Library，但第一版只维护约 5–7 个稳定基础原型。

每个 Profile 主要描述 Coverage 倾向、Rhythm、Exchange Depth、动作重量与受力反馈、Range 变化、环境利用、Phrase 节奏、Camera Complexity 和冲突 / 不适用条件。

禁止因新角色、新职业或单个影视案例不断新增 Profile；特殊观感允许 Playbook 基于基础原型动态扩展。

## 16. V2-14：Environment Action Affordance

新增 **Environment Action Affordance / 环境动作机会**。

```text
场景对象 / 空间结构 / 障碍
→ Environment Action Affordance
→ 结合 Intent / Identity / Range / Advantage 过滤
→ Action Phrase
→ 更新 Position / Range / Advantage / Condition / Environment State
```

只有环境利用至少改变攻击路线、移动路线、Range、Advantage、战术选择或 Phrase Payoff 之一时，才值得使用。

> V2 Affordance 负责“环境怎么参与设计”；V1 Environment State 负责“参与后状态怎么正确继承”。

禁止退化成随机踢椅子、扔文件、砸显示器等装饰性破坏。

## 17. V2-15：Signature Moment / 标志性动作时刻

新增 **Signature Moment** 作为 Combat Sequence 级显式动作设计目标。

- **Phrase Payoff**：局部连续攻防段结果；
- **Signature Moment**：整场中少数真正具有记忆度的动作高潮 / 设计节点。

它可以来自 Counter / Re-counter、环境反制、力量差异、兵器交错、空间轴线变化、主导权翻转或角色打法差异。

约 15 秒短动作片默认只追求 **1 个主要 Signature Moment**；必要时可有 1 个辅助记忆点。禁止每个 Phrase / Beat 都强制高潮。

Signature Moment 不等于慢动作；默认由系统内部规划，不作为 Interactive Mode 固定追问项。

## 18. V2-16：经典影视 Signature Moment 参考体系按 Pattern 组织

经典影视打斗可以作为 Signature Moment 的知识来源，但一级组织方式是 **可复用动作设计模式（Signature Moment Pattern）**，不是作品目录。

示例 Pattern：

- constrained-space-reversal｜狭窄空间反制；
- environment-assisted-counter｜环境辅助反击；
- size-difference-payoff｜体型 / 力量差视觉爆点；
- rapid-counter-recounter｜高速 Counter / Re-counter；
- weapon-distance-transition｜兵器距离切换；
- false-opening-trap｜假破绽诱导反制；
- momentum-redirection｜动量 / 冲势借力改变；
- dominance-reversal｜主导权瞬间翻转。

作品名场面只作为来源案例 / metadata。同一个 Pattern 可挂多个案例；新增案例不自动产生新 Pattern。

运行时只吸收设计机制，再重新生成当前 Sequence 独有的 Signature Moment，不复刻影视完整动作段落。

## 19. V2-17：Signature Moment Pattern 单条知识结构

单条 Pattern 采用 **抽象动作因果骨架 + 适用条件 + 可变化参数 + 案例证据** 的结构，不保存可直接复刻的完整影视动作序列。

建议字段：

- Pattern ID / Name；
- Pattern Intent；
- Trigger Conditions；
- Character Relationship；
- Core Mechanism；
- **Action Causality Skeleton**；
- Environment Role；
- Payoff Type；
- Rhythm / Exchange Fit；
- Camera Readability Hint；
- Adaptation Variables；
- Do Not Copy；
- Source Case IDs。

其中 **Action Causality Skeleton** 是核心知识，例如：

```text
Pressure
→ Boundary Constraint
→ Direction Change
→ Counter Window
→ Reversal
```

数据准确性分两层：

1. **Source Case Facts**：作品、人物、场景等事实，应通过可靠公开资料核实；
2. **Pattern Abstraction**：Core Mechanism、Causality Skeleton、适用条件等属于动作设计分析与归纳，不冒充影视官方定义。

第一版种子数据可以由 AI 调研、核实、归纳生成，不要求用户手工收集。

## 20. V2-18：Signature Moment Pattern 轻量索引与按需加载

必须支持 **轻量索引 + 按需展开**，禁止 Agent 为选择一个 Pattern 全量加载知识库。

```text
references/libraries/signature-moment-patterns/
├─ index.md
├─ patterns/
│  ├─ constrained-space-reversal.md
│  ├─ environment-assisted-counter.md
│  └─ ...
└─ source-cases/
   ├─ <case-id>.md
   └─ ...
```

### `index.md`

只保存候选筛选需要的紧凑信息，例如 pattern_id、name / short_summary、combat / spatial / environment / character_relation tags、weapon compatibility、rhythm_fit、exchange_depth_fit、payoff_type、detail_path。

### `patterns/<id>.md`

Agent 根据索引选出少量候选后，只加载最相关的 **1–3 个 Pattern 详情**。

### `source-cases/`

影视案例详细资料与核实来源单独存放，正常生成 Prompt 时默认不加载。

> **运行时加载设计知识，不加载研究档案。**

## 21. V2-19：`patterns/` 与 `source-cases/` 正式职责分离

确认将 **运行时动作设计知识** 与 **影视案例研究证据** 正式拆成两个独立层。

- `patterns/`：存可迁移、可执行的动作设计知识；
- `source-cases/`：存作品 / 场景事实、核实来源、案例分析、可信度和关联 Pattern IDs。

> **Pattern 是生产知识；Source Case 是研究证据。**

正常生成只走 `index.md → patterns/<id>.md`，不因存在 source_case_id 就自动加载案例文件。

## 22. V2-20：Tactical Interaction / 攻防博弈机制

正式新增 **Tactical Interaction / 攻防博弈机制**，作为 Action Phrase 内部的可选战术因果层。

- **Exchange Depth**：回答“一轮连续攻防有多深”；
- **Tactical Interaction**：回答“为什么会自然进入下一层攻防”。

第一版只在 Playbook 中维护少量稳定类型，不建设大型独立 Library：

- Feint / 假动作；
- Probe & Read / 试探与读取；
- Bait / 诱导；
- Anticipation / 预判；
- Counter-to-Counter / 反制对反制；
- Pattern Break / 模式打破；
- Forced Response / 强迫反应。

是否使用主要由 Character Identity、双方能力关系、Choreography Profile、Exchange Depth、Rhythm、当前状态、Phrase 时长和模型可执行性动态判断。

最终 Prompt 不堆心理解释，而通过可见动作、时机、线路和反应外显博弈。

## 23. V2-21：Camera Readability Budget / 镜头可读性预算

新增 **Camera Readability Budget / 镜头可读性预算**：

```text
Action Complexity
+ Spatial Complexity
+ Camera Complexity
≈ 有限的 Perceptual / Execution Budget
```

- Camera Mode：用户希望采用什么观看方式 / 镜头观感；
- Camera Complexity：当前动作实际承受得住多复杂的运镜、切镜和构图变化。

高 Coverage、高 Exchange Depth、高 Tactical Interaction、多人 / 高速换位、环境和空间复杂度较高时，默认降低无必要 Camera Complexity，优先保持双方身体关系和动作因果可见。

该原则不是机械反比。重型 Phrase Payoff、环境换位、Signature Moment 或短暂重建空间关系时，可以有目的地释放镜头表现力。

> **镜头为动作服务；复杂动作先保证看清，简单爆点再释放镜头表现力。**

## 24. V2-22：Action Execution Budget / 动作执行复杂度预算

正式废除 V1 中 `1 个主攻防目标 + 2–4 个连续攻防交互节点 + 1 个结束状态` 作为 Battle Beat 的全局默认动作数量锚点。

V2 改为 **Action Execution Budget / 动作执行复杂度预算**：

> **限制的是同一时间窗口内模型需要理解和执行的复杂信息量，不是整段 Battle Beat 最多允许多少动作。**

Battle Beat 不再设置统一动作数量上限。一个 Beat 可以包含 1～多个无缝连续的 Action Phrase；每个 Phrase 的 Exchange Depth 和动作负载由时长、Coverage、Rhythm、Exchange Depth、Tactical Interaction、Choreography Profile、Character Identity、状态、环境、Camera Readability Budget 和目标模型能力共同决定。

### Action Sufficiency Check / 动作充分性检查

取消全局动作数量上限，不代表取消最低充分性检查。以下情况应视为 Combat Underfill 并触发重新规划：

- High / Medium Coverage 下仍存在大段未被 Active Exchange 使用的时间；
- “高手高速交换型 / 混合型”实际 Exchange Depth 明显偏低；
- 有足够时长的 Beat 只有极少有效攻防且无合理原因；
- Phrase 之间存在大量无直接攻防目的的站立、观察、摆姿势；
- 用户明确要求持续对打、高手对决、拳拳到肉等观感，但计划仍主要由僵持、控制和摆位占据。

Action Sufficiency 不采用新的固定最低招数，而检查 Coverage、Rhythm、Exchange Depth、Active Exchange Budget 和无价值 Downtime 是否兑现。

过载时优先：删除无价值附属动作 → 降低单 Phrase Depth / Tactical Complexity → 降低 Camera Complexity → 拆成仍无缝连续的 Phrase → 只有战术状态真正变化才拆 Beat。

> **拆 Phrase 不等于停下来。**

## 25. V2-23：Combat Contact Solidity / 战斗接触实感

正式新增 **Combat Contact Solidity / 战斗接触实感**，作为所有 Combat Contact Event 的通用动作质量维度，用于防止打斗“软绵绵、像套动作或小孩过家家”。

它不只针对拳击，而覆盖所有会发生力量、动量、压力、兵器作用或身体控制后果的接触，包括：

- 拳、掌、肘、膝、腿、踢击等 Strike；
- 抓控、缠斗、推撞、压迫；
- Takedown / Throw / 摔投；
- 钝器打击；
- 刀剑、切割、刺击等 Edge / Thrust；
- Weapon Clash / Parry / 格挡、偏转、交击、缴械；
- Environment Impact / 环境撞击与二次冲击。

### 通用 Combat Contact Chain

不同接触类型共享的不是同一种“重拳表现”，而是 **接触必须有可信投入、传递和后果**：

```text
Commitment
发力 / 投入 / 切入 / 压入 / 逼近
        ↓
Contact Event
命中 / 格挡 / 交击 / 抓控 / 撞击 / 切割 / 刺入 / 压制
        ↓
Force / Energy / Pressure Transfer
力量、动量、压力或兵器作用发生传递
        ↓
Reaction Propagation
受力从接触点传播到身体、兵器、姿态或空间关系
        ↓
State Consequence
Range / Advantage / Condition / 平衡 / 呼吸 / Guard / 兵器状态发生后果
        ↓
Recovery / Continuation
带着该后果进入下一动作
```

### Contact Modality / 接触类型差异

`Combat Contact Solidity` 是通用质量规则，但不同 Contact Modality 的“实感证据”不同：

- **Strike**：身体整体发力、明确命中、受力传播、重心 / Guard / 呼吸变化；
- **Grapple / Control**：接触建立、身体压迫、杠杆 / 方向、重心被夺、挣脱需要动作代价；
- **Takedown / Throw**：夺重心过程、失衡方向、落地结果、落地后位置 / Advantage 延续；
- **Blunt Weapon**：挥击惯性、接触重量、格挡负担、持械手臂与站位受力；
- **Blade / Edge / Thrust**：重点不是“重”，而是危险线路、距离约束、躲避 / 偏转必要性和接触后的明确战术后果；
- **Weapon Clash / Parry**：接触点、兵器线路偏移、手臂 / 身体承担、下一拍主动权变化；
- **Environment Impact**：撞击方向、身体与环境共同反馈、反弹 / 停滞 / 支撑 / 二次状态后果。

因此不能把“拳拳到肉”的表现模板机械套到刀剑、摔控或兵器交击上。

### Contact Weight / 接触重量

内部可按场景动态区分：

- **Light**：试探、截击、轻触、快速格挡、建立接触；
- **Solid**：明确有效接触，有可见的身体 / 兵器 / 空间反馈；
- **Heavy**：Phrase Payoff、重型撞击、强制失衡或明显改变状态的关键接触。

该分级不是让每种武器都按“物理重量”理解，而是表达 **当前 Contact Event 的感知强度与战术后果等级**。

并非所有攻击都应 Heavy。连续高手攻防中应允许 Light / Solid / Heavy 形成层次；否则全程同强度会失去真实节奏和高潮。

### 六个通用检查维度

1. **Commitment / Kinetic Commitment**：攻击、推撞、摔控或武器动作是否有身体 / 步法 / 惯性上的真实投入；
2. **Contact Clarity**：关键接触是否能看清“哪里、何时、以什么关系发生”；
3. **Force / Pressure Transfer**：力量、压力、动量或兵器作用是否真正传递，而不是只做表面触碰；
4. **Reaction Propagation**：反应是否从接触点传播到身体、兵器、姿态、重心或空间关系，而不是单一局部摆动；
5. **Persistent Consequence**：有效接触必须至少在后续一个动作窗口留下 Range / Advantage / Condition / Guard / Balance / Weapon State 等可见后果，禁止下一帧无理由 Reset；
6. **Audio / Camera Accent**：声音和镜头可以强化接触，但不能代替身体 / 兵器本身的真实受力与状态变化。

### 与 V1 State Engine 的关系

```text
Combat Contact Event
→ Combat Contact Solidity 检查接触是否“打实 / 控实 / 撞实 / 交击实”
→ 生成 Contact / Reaction / Consequence
→ V1 Range / Advantage / Condition / Weapon / Environment State 继承
→ 下一 Action Phrase 从真实后果继续
```

因此 `Combat Contact Solidity` 不取代 V1 的物理与状态连续性，而是把 V1 已有的“命中有因果”进一步提升为：

> **接触有重量 / 压力 / 危险感，受力会传播，后果会留下，并影响下一动作。**

### 防止假实感

禁止仅靠以下手段伪造“有力”：

- 每次接触都 Camera Shake；
- 每次命中都 Slow Motion；
- 每次都巨大音效；
- 每次都夸张飞退；
- 用 Motion Blur 掩盖实际未接触；
- 用痛苦表情代替真实身体 / 兵器反馈。

正确顺序是：

```text
动作与接触本身成立
→ 力量 / 压力 / 危险关系成立
→ 身体 / 兵器 / 状态后果成立
→ Camera / Audio 再做强化
```

---

## 26. V2 设计原则汇总

1. 时间轴写满不代表动作写满，必须检查 Coverage；
2. 持续交战不代表动作丰富，必须检查 Rhythm / Phrase / Exchange Depth；
3. 动作合理不代表好看，动作导演层负责视觉动作设计；
4. 高手身份必须通过打法表现；
5. Character Identity 是动态推导，不是职业画像；
6. Phrase 负责连续动作，State Contract 负责连续性；
7. Phrase 与 Beat 不绑定 1:1；
8. High Coverage 不等于全程同速；
9. Active Combat Feedback 与 Downtime 必须区分；
10. Ending 不应提前终止战斗；
11. Exchange Depth 衡量因果深度，不衡量动作词数量；
12. Tactical Interaction 负责攻防为何进入下一层，不能与 Exchange Depth 混为一谈；
13. 战术博弈按角色能力和场景动态触发，不要求每个 Phrase 都有；
14. 环境先作为动作机会参与设计，再由 V1 继承状态；
15. Choreography Profile 只维护少量稳定原型；
16. 15 秒短动作片默认只有少量 Signature Moment；
17. 经典影视参考用于抽象动作设计规律，不用于复制完整动作段落；
18. Pattern 是知识主体，作品只作为来源案例；
19. Pattern 保存抽象因果骨架，不保存可直接复刻的完整影视动作；
20. Pattern Library 必须通过轻量索引按需加载；
21. 正常生成加载设计知识，不加载影视调研证据层；
22. Pattern 与 Source Case 正式分层，生产知识与研究证据独立维护；
23. Camera Complexity 与动作 / 空间复杂度共享有限执行预算，不能同时无上限拉高；
24. 高动作复杂度默认优先镜头可读性，Payoff / 环境换位 / Signature Moment 再有目的释放镜头表现力；
25. Battle Beat 不再使用固定 `2–4` 交互节点作为动作数量锚点；动作复杂度在 Phrase 级动态预算；
26. 取消动作数量上限后必须执行 Action Sufficiency Check，既防止过载，也防止动作不足；
27. Combat Contact Solidity 适用于拳脚、摔控、钝器、刀剑、武器交击和环境冲击等全部接触形式；
28. 不同 Contact Modality 使用不同实感证据，不能把“重拳反馈”套到所有打斗形式；
29. 有效接触必须产生可见、可继承的身体 / 兵器 / 空间 / 状态后果，Camera / Audio 只能强化、不能替代；
30. 最终 Prompt 应外显精彩动作、可见战术博弈和关键接触后果，内部状态规范尽量压缩。

## 27. 已确认决策记录

| # | 决策 | 当前结论 |
|---|---|---|
| V2-01 | 核心升级 | 新增 Combat Choreography Engine，保留 V1 State / Continuity |
| V2-02 | 有效交战 | Active Combat Coverage：Low / Medium / High |
| V2-03 | 攻防节奏 | 重击 / 均衡 / 高速交换 / 混合型 |
| V2-04 | 动作单位 | 新增 Action Phrase |
| V2-05 | 角色打法 | 新增 Combat Character Identity |
| V2-06 | 整场动作观感 | Cinematic Choreography Profile，不进入视觉 Styles |
| V2-07 | Interactive | Combat 专属决策链，上游驱动下游推荐 |
| V2-08 | 时间预算 | Setup / Active Exchange / Downtime / Ending |
| V2-09 | Phrase 复杂度 | Exchange Depth 动态控制 |
| V2-10 | Beat / Phrase | 动态一对多 |
| V2-11 | 中文术语 | 中文统一“动作编排 / 动作导演” |
| V2-12 | Identity 来源 | 不建角色 / 职业画像库，动态推导 |
| V2-13 | Choreography Library | 少量稳定基础 Profile |
| V2-14 | Environment | Environment Action Affordance |
| V2-15 | Signature Moment | Sequence 级显式记忆点；15 秒默认 1 个主记忆点 |
| V2-16 | 影视参考组织 | Pattern 为一级，影视作品是来源案例 |
| V2-17 | Pattern 数据结构 | 抽象因果骨架 + 适用条件 + 可变化参数 + 案例证据，不存完整动作复刻 |
| V2-18 | Pattern 加载架构 | 轻量 `index.md` → 按需加载 1–3 个 Pattern → source-cases 默认不加载 |
| V2-19 | Pattern / Source Case 分层 | `patterns/` 存生产知识；`source-cases/` 存影视事实、核实来源和研究笔记 |
| V2-20 | Tactical Interaction | 假动作、试探、诱导、预判、Counter-to-Counter 等作为 Phrase 可选战术因果层；动态触发 |
| V2-21 | Camera Readability Budget | Camera Complexity 与动作 / 空间复杂度共享执行预算；高动作复杂度优先可读性 |
| V2-22 | Action Execution Budget | 废除 Battle Beat 全局 `2–4` 交互节点锚点；改为 Phrase 级动态执行预算，并增加 Action Sufficiency Check |
| V2-23 | Combat Contact Solidity | 所有战斗接触共享 Commitment → Contact → Transfer → Reaction → Consequence → Continuation 实感链；按 Strike / Grapple / Throw / Blunt / Blade / Weapon Clash / Environment 等 Contact Modality 适配，并动态使用 Light / Solid / Heavy 接触层级 |

## 28. 尚待继续 Grill Me 的设计树

1. V1 “宁少而清晰”如何重述，避免动作预算通缩；
2. Final Prompt 如何减少状态规范语言、提高正向动作编排权重；
3. Combat Quality Regression 如何从静态覆盖升级为真实生成质量评价；
4. V2 最终修改哪些 Playbook / Library / Contract / Diagnostic，是否新增 Control。

## 29. 当前阶段结论

V1 已能够较好地“把战斗写对”；V2 的目标是在此基础上进一步做到：

> **把战斗设计得持续、丰富、有角色差异、有环境逻辑、有战术博弈、有电影动作编排感、有可信接触实感，并拥有真正值得记住的动作时刻；同时通过 Action Sufficiency Check 防止动作不足，通过 Action Execution Budget 与 Camera Readability Budget 控制模型负载。**

可进一步概括为：

> **打得够久 + 打得够丰富 + 打得够实 + 看得够清楚。**

本文件继续作为 V2 Grill Me 的单一设计记录。后续每确认一个关键决策，同步更新已确认决策与待讨论设计树，直到 V2 设计收口。