# Action Combat Video Prompt Spec V2

> 状态：设计中（Grill Me 持续收敛）  
> 基线：`docs/action-combat-video-spec.md`  
> V1 状态：已完成设计、实现与静态回归

## 1. V2 背景

V1 已较完整解决 Combat Intent、Spatial Map、Range / Advantage / Condition、Turning Event、Action–Reaction Pair、Battle Beat、Target Handoff、Beat State Contract、Action / Camera / Audio 协同，以及受力、空间和环境状态连续性。

真实生成测试暴露的新问题是：

> **15 秒时间轴虽然完整，但真正持续交战只有约 2–3 秒，有效攻防交换也只有两三次。**

典型表现包括：开场对峙过长、抓腕和控制等低动态状态占用大量时长、Battle Beat 内连续攻防不足、职业标签过度映射固定打法、双方打法同质、环境只在事后修改状态、V1“宁少而清晰”被过度执行导致动作预算通缩。

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
→ Signature Moment Planning
→ Battle Beat
→ V1 State / Continuity Validation
→ Camera Readability Budget / Camera Coordination
→ Audio Coordination
→ Final Prompt Compression
```

核心原则：

> **Combat Choreography Engine 负责“打得好不好看”。**  
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

High 不等于全程同速高速挥拳；只要受击、失衡、闪避、恢复等反馈直接推动下一次攻防，仍属于 Active Combat。

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

它不进入 `references/styles/` 一级视觉 Style；由 Combat Playbook 选择 / 协调，由 `combat-choreography-profiles` Library 提供稳定基础原型。

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
- 一次只问一个最关键问题。

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

均为软预算，不是硬秒表。

Ending 不应提前数秒终止交战；最后一轮 Action Phrase 可以直接延伸进入 Ending。

## 11. V2-09：Exchange Depth

新增 **Exchange Depth / 攻防交换深度**。

> **Exchange Depth ≠ Action Verb Count**

衡量一次发起后连续 Defense → Counter → Re-counter → Continuation 的因果深度，而不是招式名数量。

主要受以下变量共同决定：

- Rhythm；
- Phrase 时长；
- Choreography Profile；
- Character Identity；
- Range / Advantage / Condition；
- 环境复杂度；
- Camera Complexity；
- 视频模型可执行性。

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

原因是角色、职业、体型、性格、能力、环境和目的组合近乎无限，而且固定职业模板会重复 V1 的过拟合问题。

Combat Character Identity 是当前 Combat Sequence 的动态推导结果。

Library 只保存相对稳定、可复用的专业动作知识，例如 Boxing、Muay Thai、Sanda、MMA、Grappling、Tactical Close Combat、传统 Martial Profile、兵器动作知识等。

## 15. V2-13：小型 `combat-choreography-profiles` Library

正式新增该 Library，但第一版只维护约 5–7 个稳定基础原型。

每个 Profile 主要描述：

- Coverage 倾向；
- Rhythm；
- Exchange Depth；
- 重量与受力反馈；
- Range 变化；
- 环境利用程度；
- Phrase 节奏；
- Camera Complexity；
- 冲突 / 不适用条件。

禁止演化成“所有动作电影风格百科”。特殊观感允许 Playbook 基于基础原型动态扩展。

## 16. V2-14：Environment Action Affordance

新增 **Environment Action Affordance / 环境动作机会**。

环境在 Action Phrase 设计之前先回答“当前场景可以为攻防提供什么机会”。

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

必须区分：

- **Phrase Payoff**：局部连续攻防段结果；
- **Signature Moment**：整场中少数真正具有记忆度的动作高潮 / 设计节点。

它可以来自 Counter / Re-counter、环境反制、力量差异、兵器交错、空间轴线变化、主导权翻转或角色打法差异。

约 15 秒短动作片默认只追求 **1 个主要 Signature Moment**；必要时可有 1 个辅助记忆点。禁止每个 Phrase / Beat 都强制高潮。

Signature Moment 不等于慢动作。

默认由系统内部规划，不作为 Interactive Mode 固定追问项；用户明确指定特技、标志动作或名场面参考时再锁定 / 询问。

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

运行时：

```text
当前场景 / 空间
+ Character Identity
+ Choreography Profile
+ Environment Affordance
+ Rhythm / Exchange Depth
        ↓
匹配 Signature Moment Pattern
        ↓
吸收设计机制
        ↓
重新生成当前 Sequence 独有的 Signature Moment
```

目标是学习设计规律，而不是复刻影视完整动作段落。

## 19. V2-17：Signature Moment Pattern 单条知识结构

单条 Pattern 采用 **抽象动作因果骨架 + 适用条件 + 可变化参数 + 案例证据** 的结构，不保存可直接复刻的完整影视动作序列。

建议字段：

- **Pattern ID / Name**：稳定标识与名称；
- **Pattern Intent**：希望制造的动作观感 / 戏剧功能；
- **Trigger Conditions**：适用空间、距离、人物关系、武器或环境前提；
- **Character Relationship**：适合的打法关系，例如速度型 vs 力量型，但不做职业限制；
- **Core Mechanism**：真正可复用的设计机制；
- **Action Causality Skeleton**：抽象因果骨架，例如 `Pressure → Boundary Constraint → Direction Change → Counter Window → Reversal`；
- **Environment Role**：Boundary / Obstacle / Support / Route Modifier / Impact Surface 等功能；
- **Payoff Type**：空间逆转、主导权翻转、力量落空、换轴、距离切换等；
- **Rhythm / Exchange Fit**：适合的 Rhythm 与 Exchange Depth 倾向；
- **Camera Readability Hint**：只描述需要看清什么，不固化镜头脚本；
- **Adaptation Variables**：可以自由替换的环境、攻击方式、人物差异等；
- **Do Not Copy**：明确禁止直接迁移具体影视招式顺序、逐镜头设计、台词、独特特技；
- **Source Case IDs**：指向独立 `source-cases/` 证据层的案例 ID；Pattern 文件只保留短引用，不内嵌完整案例资料。

其中 **Action Causality Skeleton** 是核心知识，不保存影视片段的逐招还原。

数据准确性分两层：

1. **Source Case Facts**：作品、人物、场景、名场面基本事实，应尽量通过可靠公开资料核实；
2. **Pattern Abstraction**：Core Mechanism、Causality Skeleton、适用条件等属于动作设计抽象与归纳，应明确是设计分析，不冒充影视官方定义。

因此第一版种子数据可以由 AI 调研、核实、归纳生成，不要求用户手工收集；用户后续更适合补充特别认可、冷门或本地化影视案例。

## 20. V2-18：Signature Moment Pattern 轻量索引与按需加载

Signature Moment 参考体系必须支持 **轻量索引 + 按需展开**，禁止 Agent 为了选择一个 Pattern 而全量加载整个知识库。

推荐三级结构：

```text
references/libraries/signature-moment-patterns/
├─ index.md
├─ patterns/
│  ├─ constrained-space-reversal.md
│  ├─ environment-assisted-counter.md
│  ├─ rapid-counter-recounter.md
│  └─ ...
└─ source-cases/
   ├─ <case-id>.md
   └─ ...
```

### 20.1 `index.md`：常驻轻量路由索引

只保存足以完成候选筛选的紧凑信息，例如：

- pattern_id；
- name / short_summary；
- combat_context_tags；
- spatial_tags；
- environment_tags；
- character_relation_tags；
- weapon / unarmed compatibility；
- rhythm_fit；
- exchange_depth_fit；
- payoff_type；
- detail_path。

索引禁止塞入完整动作因果说明和影视案例细节。

### 20.2 `patterns/<id>.md`：按需加载的动作设计知识

Agent 根据当前场景与索引选出少量候选后，只加载最相关的 **1–3 个 Pattern 详情**。

详情包含 V2-17 的 Pattern Intent、Trigger Conditions、Core Mechanism、Action Causality Skeleton、Environment Role、Adaptation Variables、Do Not Copy 等字段。

### 20.3 `source-cases/`：证据 / 调研层

影视案例详细资料与核实来源单独存放。

正常生成 Prompt 时 **默认不加载 source-cases**；只有以下情况才需要读取：

- 维护 / 扩充 Pattern；
- 校验 Pattern 的案例依据；
- 用户明确要求参考某部作品 / 某个名场面；
- 需要重新审查某个 Pattern 的抽象是否准确。

这样做到：

> **运行时加载设计知识，不加载研究档案。**

推荐运行链：

```text
当前 Combat Context
        ↓
加载 signature-moment-patterns/index.md
        ↓
筛选 Top 1–3 Pattern IDs
        ↓
仅加载对应 patterns/<id>.md
        ↓
结合当前场景重新生成 Signature Moment
        ↓
一般不读取 source-cases/
```

## 21. V2-19：`patterns/` 与 `source-cases/` 正式职责分离

确认将 **运行时动作设计知识** 与 **影视案例研究证据** 正式拆成两个独立层。

### `patterns/`

用于 Agent 正常生成时按需加载，只保存可迁移的动作设计知识，包括 Pattern Intent、Trigger Conditions、Core Mechanism、Action Causality Skeleton、Environment Role、Rhythm / Exchange Fit、Camera Readability Hint、Adaptation Variables、Do Not Copy，以及 `source_case_ids` 和极短案例备注。

### `source-cases/`

作为研究 / 核实层，保存作品与场景标识、角色 / 对战双方、名场面事实摘要、公开资料核实来源、案例分析笔记、事实可信度 / 待核实项和关联 Pattern IDs。

> **Pattern 是生产知识；Source Case 是研究证据。**

正常生成只走 `index.md → patterns/<id>.md`，不因存在 source_case_id 就自动加载案例文件。

## 22. V2-20：Tactical Interaction / 攻防博弈机制

正式新增 **Tactical Interaction / 攻防博弈机制**，作为 Action Phrase 内部的可选战术因果层，用来表现高手之间“互相读取、诱导、预判和反制”，而不是单纯增加动作数量。

它与 Exchange Depth 明确区分：

- **Exchange Depth**：回答“一轮连续攻防有多深”；
- **Tactical Interaction**：回答“为什么会自然进入下一层攻防”。

基础机制第一版只在 Playbook 中维护少量稳定类型，不建设大型独立 Library：

- Feint / 假动作；
- Probe & Read / 试探与读取；
- Bait / 诱导；
- Anticipation / 预判；
- Counter-to-Counter / 反制对反制；
- Pattern Break / 模式打破；
- Forced Response / 强迫反应。

这些机制只描述战术因果，不是固定招式模板。

是否使用及复杂度主要由 Character Identity、双方能力关系、Choreography Profile、Exchange Depth、Rhythm、Range / Advantage / Condition、Phrase 可用时长、模型可执行性和动作可读性动态判断。

典型倾向：

- 高手连续攻防型 + 高 Exchange Depth + 双方实力接近：明显提高使用概率；
- 写实战术型：适合短、直接的 Probe / Feint / Forced Response；
- 重型硬派型 / 普通人互殴：默认降低复杂战术博弈。

最终 Prompt 不应堆角色心理解释，而应通过可见动作、时机、线路和反应外显博弈。

## 23. V2-21：Camera Readability Budget / 镜头可读性预算

新增 **Camera Readability Budget / 镜头可读性预算**，用于协调动作复杂度、空间复杂度和 Camera Complexity，防止 V2 提高动作密度后出现“动作很多但观众和模型都看不清”的新问题。

核心判断：

```text
Action Complexity
+ Spatial Complexity
+ Camera Complexity
≈ 有限的 Perceptual / Execution Budget
```

因此 Camera Complexity 不能脱离动作本身独立拉满。

### 与 Camera Mode 的边界

- **Camera Mode**：回答用户希望采用什么观看方式 / 镜头观感；
- **Camera Complexity**：回答当前动作在保证可读性和模型可执行性的前提下，实际承受得住多复杂的运镜、切镜和构图变化。

即使用户要求“动态电影镜头”，也不能自动解释为全程快速环绕、频繁推拉、连续切镜和极近特写。

### 默认联动原则

当以下因素同时较高时，应默认降低 Camera Complexity：

- Active Combat Coverage 高；
- Exchange Depth 高；
- Tactical Interaction 复杂；
- 双角色高速换位；
- Environment Action Affordance 参与较多；
- 空间关系本身复杂。

这时优先使用能够保留双方身体关系和动作因果的中景 / 中全景、稳定跟随、有限切镜或其他清晰观看方式。

> **动作复杂度上升时，默认优先减少无必要的 Camera Complexity，而不是为了镜头炫技牺牲动作可读性。**

该原则是默认倾向，**不是机械反比公式**。

### 可以释放 Camera Complexity 的时机

动作导演层可以在动作复杂度暂时下降、需要强化单一视觉信息时，有目的地释放镜头表现力，例如：

- **重型 Phrase Payoff**：动作链短暂收束，可使用一次短促推进、近侧角度或明确切镜强化重量；
- **环境换位 / 空间关系变化**：适当扩宽或调整角度，让观众看清路线和位置变化；
- **Signature Moment**：获得最高的“可读性优先级”，选择最能看清核心机制和冲击力的观看角度；
- **短暂战术停顿 / 重建距离**：若不损害 Coverage，可用有限镜头变化建立下一轮空间关系。

Signature Moment 不要求最复杂镜头。很多情况下，一个干净、清晰的中景或侧面角度比多次快速切镜更有效。

### Phrase 级 Camera Readability Budget

Camera 不再只在 Sequence 级设一个固定模式，而应根据 Phrase 动作负载动态分配复杂度：

```text
高速高 Depth Phrase
→ Camera 稳定、保持双方关系可见

重型 Payoff Phrase
→ 允许一次有目的的镜头强化

环境换位 Phrase
→ 优先交代空间变化

Signature Moment
→ 优先最清晰、最具冲击力的角度

重新进入高速交换
→ Camera 再次收敛复杂度
```

### 与模型能力的关系

Camera Readability Budget 必须同时考虑目标视频模型的可执行性。模型越难同时稳定处理多人、高速动作、复杂空间与复杂运镜，越应优先保留动作和空间信息，削减装饰性镜头复杂度。

因此 V2 的 Camera 原则不是“动作片必须镜头更炫”，而是：

> **镜头为动作服务；复杂动作先保证看清，简单爆点再释放镜头表现力。**

## 24. V2-22：Action Execution Budget / 动作执行复杂度预算

正式废除 V1 中 `1 个主攻防目标 + 2–4 个连续攻防交互节点 + 1 个结束状态` 作为 Battle Beat 的全局默认动作数量锚点。

该数字虽然原本只是“可读性参考”，但在 V2 的实测问题背景下容易被 Agent 保守执行，导致一个较长 Battle Beat 也只发生两三次有效交换。

V2 改为 **Action Execution Budget / 动作执行复杂度预算**：

> **限制的是同一时间窗口内模型需要理解和执行的复杂信息量，不是整段 Battle Beat 最多允许多少动作。**

### Phrase 级动态预算

Battle Beat 不再设置统一动作数量上限。一个 Beat 可以包含 1～多个无缝连续的 Action Phrase；每个 Phrase 的 Exchange Depth 和动作负载由以下变量共同决定：

- Beat / Phrase 可用时长；
- Active Combat Coverage 与 Active Exchange Budget；
- Action Exchange Rhythm；
- Exchange Depth；
- Tactical Interaction；
- Cinematic Choreography Profile；
- Combat Character Identity；
- Range / Advantage / Condition；
- Environment Action Affordance 与空间复杂度；
- Camera Readability Budget；
- 目标视频模型可执行性。

因此一个较长的高手连续攻防 Beat 可以自然包含多个 Phrase 和明显超过 4 次的有效攻防交换，而一个短促重击 Phrase 仍然可以只承担少数关键交互。

### 防止“取消上限后反而太少”：Action Sufficiency Check

取消全局动作数量上限，不代表取消最低动作充分性检查。V2 在 Phrase / Beat 规划完成后增加 **Action Sufficiency Check / 动作充分性检查**，用于识别 Combat Underfill。

以下情况应视为动作可能不足并触发重新规划：

- High / Medium Coverage 下仍存在大段未被 Active Exchange 使用的时间；
- 选择“高手高速交换型 / 混合型”但实际 Phrase 内 Exchange Depth 明显偏低；
- 一个有足够时长的 Battle Beat 只有极少有效攻防，却没有重击、环境、剧情或状态理由；
- Phrase 之间存在长时间站立、观察、重新摆姿势等无直接攻防目的的空档；
- 用户明确要求持续对打、高手对决、拳拳到肉等观感，但计划仍主要由控制、僵持、摆位占据。

Action Sufficiency 不采用新的固定“最低几招”数字，而是检查：

```text
Coverage 是否兑现
+ Rhythm 是否兑现
+ Exchange Depth 是否符合当前 Phrase
+ Active Exchange Budget 是否真正被使用
+ 是否存在无价值 Downtime
```

如果不满足，则优先补足有效 Action Phrase / 攻防因果，而不是通过增加空洞动作词数量凑数。

### 信息过载时的处理顺序

当动作计划超过模型可执行预算时，优先按以下顺序处理：

1. 删除不改变战斗关系的附属 / 装饰动作；
2. 降低单个 Phrase 的 Exchange Depth 或 Tactical Interaction 复杂度；
3. 降低 Camera Complexity；
4. 将一个过载 Phrase 拆成两个仍然无缝连续的 Phrase；
5. 只有战术目标、Advantage、关键 Condition 或阶段真正改变时，才拆 Battle Beat。

> **拆 Phrase 不等于停下来。** Phrase 之间可以保持持续交战，不自动产生 Downtime。

---

## 25. V2 设计原则汇总

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
24. 高动作复杂度默认优先镜头可读性，重型 Payoff / 环境换位 / Signature Moment 再有目的地释放镜头表现力；
25. Battle Beat 不再使用固定 `2–4` 交互节点作为动作数量锚点；动作复杂度在 Phrase 级动态预算；
26. 取消动作数量上限后必须执行 Action Sufficiency Check，既防止过载，也防止动作不足；
27. 最终 Prompt 应外显精彩动作与可见战术博弈，内部状态规范尽量压缩。

## 26. 已确认决策记录

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
| V2-19 | Pattern / Source Case 分层 | `patterns/` 存生产知识；`source-cases/` 存影视事实、核实来源和研究笔记；运行时默认只加载 Pattern |
| V2-20 | Tactical Interaction | 假动作、试探、诱导、预判、Counter-to-Counter 等作为 Phrase 可选战术因果层；动态触发，不做用户参数、暂不建大型独立 Library |
| V2-21 | Camera Readability Budget | Camera Complexity 与动作 / 空间复杂度共享执行预算；高动作复杂度优先可读性，Payoff / 环境换位 / Signature Moment 再有目的释放镜头表现力 |
| V2-22 | Action Execution Budget | 废除 Battle Beat 全局 `2–4` 交互节点锚点；改为 Phrase 级动态执行预算，并增加 Action Sufficiency Check 防止动作不足 |

## 27. 尚待继续 Grill Me 的设计树

1. 打击重量 / Impact Solidity 如何设计，防止命中软绵绵、缺少“拳拳到肉”实感；
2. V1 “宁少而清晰”如何重述，避免动作预算通缩；
3. Final Prompt 如何减少状态规范语言、提高正向动作编排权重；
4. Combat Quality Regression 如何从静态覆盖升级为真实生成质量评价；
5. V2 最终修改哪些 Playbook / Library / Contract / Diagnostic，是否新增 Control。

## 28. 当前阶段结论

V1 已能够较好地“把战斗写对”；V2 的目标是在此基础上进一步做到：

> **把战斗设计得持续、丰富、有角色差异、有环境逻辑、有战术博弈、有电影动作编排感，并拥有真正值得记住的动作时刻；同时通过 Action Sufficiency Check 防止动作不足，通过 Action Execution Budget 与 Camera Readability Budget 控制模型负载。**

本文件继续作为 V2 Grill Me 的单一设计记录。后续每确认一个关键决策，同步更新已确认决策与待讨论设计树，直到 V2 设计收口。