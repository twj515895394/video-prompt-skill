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
→ Signature Moment Planning
→ Battle Beat
→ V1 State / Continuity Validation
→ Camera / Audio Coordination
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

该设计遵守 V2 总体的按需加载原则，避免 Pattern 数量增长后造成 Token 膨胀。

## 21. V2-19：`patterns/` 与 `source-cases/` 正式职责分离

确认将 **运行时动作设计知识** 与 **影视案例研究证据** 正式拆成两个独立层，不把完整影视案例 metadata 和研究笔记塞入 Pattern 文件。

职责明确如下：

### `patterns/`

用于 Agent 正常生成时按需加载，只保存可迁移的动作设计知识：

- Pattern Intent；
- Trigger Conditions；
- Core Mechanism；
- Action Causality Skeleton；
- Environment Role；
- Rhythm / Exchange Fit；
- Camera Readability Hint；
- Adaptation Variables；
- Do Not Copy；
- `source_case_ids` 与极短案例备注。

### `source-cases/`

作为研究 / 核实层，保存：

- 作品与场景标识；
- 角色 / 对战双方；
- 名场面事实摘要；
- 公开资料核实来源；
- 案例为什么支持某个 Pattern 的分析笔记；
- 事实可信度 / 待核实项；
- 可关联的 Pattern IDs。

运行时原则：

> **Pattern 是生产知识；Source Case 是研究证据。**

正常 Prompt 生成只通过 `index.md → patterns/<id>.md` 路由，不因为 Pattern 引用了 source_case_id 就自动加载案例文件。只有维护、核实、用户明确点名作品 / 名场面等情形才进入 `source-cases/`。

这样可以同时保证：

- Agent 运行上下文精简；
- 影视事实和动作设计抽象可独立维护；
- Pattern 不被某个具体作品的细节污染；
- 后续更换 / 增补案例时不需要重写 Pattern 主体；
- 可以追溯 Pattern 的案例依据，但不把证据层变成运行时依赖。

---

## 22. V2 设计原则汇总

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
12. 环境先作为动作机会参与设计，再由 V1 继承状态；
13. Choreography Profile 只维护少量稳定原型；
14. 15 秒短动作片默认只有少量 Signature Moment；
15. 经典影视参考用于抽象动作设计规律，不用于复制完整动作段落；
16. Pattern 是知识主体，作品只作为来源案例；
17. Pattern 保存抽象因果骨架，不保存可直接复刻的完整影视动作；
18. Pattern Library 必须通过轻量索引按需加载；
19. 正常生成加载设计知识，不加载影视调研证据层；
20. Pattern 与 Source Case 正式分层，生产知识与研究证据独立维护；
21. 最终 Prompt 应外显精彩动作，内部状态规范尽量压缩。

## 23. 已确认决策记录

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

## 24. 尚待继续 Grill Me 的设计树

1. 假动作、预判、诱导、Counter / Re-counter 是否形成独立动作编排规则；
2. Combat Density / Coverage / Rhythm 与 Camera Complexity 如何联动；
3. V1 “动作复杂度预算”如何调整，避免 `2–4` 交互节点被过度保守执行；
4. V1 “宁少而清晰”如何重述，避免动作预算通缩；
5. Final Prompt 如何减少状态规范语言、提高正向动作编排权重；
6. Combat Quality Regression 如何从静态覆盖升级为真实生成质量评价；
7. V2 最终修改哪些 Playbook / Library / Contract / Diagnostic，是否新增 Control。

## 25. 当前阶段结论

V1 已能够较好地“把战斗写对”；V2 的目标是在此基础上进一步做到：

> **把战斗设计得持续、丰富、有角色差异、有环境逻辑、有电影动作编排感，并拥有真正值得记住的动作时刻，同时通过索引化知识结构控制运行时 Token 成本。**

本文件继续作为 V2 Grill Me 的单一设计记录。后续每确认一个关键决策，同步更新已确认决策与待讨论设计树，直到 V2 设计收口。