# Action Combat Video Prompt Spec V2

> 状态：设计中（Grill Me 持续收敛）  
> 基线：`docs/action-combat-video-spec.md`  
> V1 状态：已完成设计、实现与静态回归

## 1. V2 背景

V1 已较完整解决 Combat Intent、Spatial Map、Range / Advantage / Condition、Turning Event、Action–Reaction Pair、Battle Beat、Target Handoff、Beat State Contract、Action / Camera / Audio 协同，以及受力、空间和环境状态连续性。

真实生成测试暴露的新问题是：15 秒时间轴虽然完整，但真正持续交战只有约 2–3 秒，有效攻防交换也只有两三次；同时存在开场对峙过长、控制 / 僵持占时、双方打法同质、环境只做装饰、动作预算通缩、接触软绵绵等问题。

因此 V2 不推翻 V1，而是在其上增强正式的 **Combat Choreography Engine（动作编排引擎 / 动作导演层）**。

核心分工：

> **Combat Choreography Engine 负责“打得好不好看、够不够、实不实”。**  
> **Combat State / Continuity Engine 负责“打得对不对、接不接得上”。**  
> **约束错误，不约束创作。**

## 2. V2 总运行链

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
→ Final Prompt Action Externalization
```

---

## 3. V2-01：Combat Choreography Engine

正式新增动作编排引擎，负责有效交战时间、单位时间攻防交换丰富度、角色打法差异、电影动作观感、Action Phrase、节奏、环境机会、Tactical Interaction、Combat Contact Solidity、Signature Moment，以及可读性与模型可执行性的动态平衡。

## 4. V2-02：Active Combat Coverage

新增 **Active Combat Coverage / 有效交战覆盖率**：Low 约 40–55%，Medium 约 60–75%，High 约 75–90%。

Timeline Coverage ≠ Combat Coverage。High 不等于全程同速高速动作；只要受击、失衡、闪避、恢复、快速重新切入等反馈直接推动下一次攻防，仍属于 Active Combat。

## 5. V2-03：Action Exchange Rhythm

Coverage 决定“有多少时间在打”；Rhythm 决定“持续交战期间怎么交换”。基础方向：重击型、均衡型、高手高速交换型、混合型。

## 6. V2-04：Action Phrase

```text
Action–Reaction Pair
→ Action Phrase
→ Battle Beat
→ Combat Sequence
```

Action Phrase 的核心是：**前一个动作自然制造下一个动作的机会。** 可参考 `Setup / Entry → Attack → Defensive Answer → Counter → Re-counter / Continuation → Phrase Payoff`，但禁止固定六步模板。

## 7. V2-05：Combat Character Identity

Character Identity 回答“当前这个角色怎么打”，动态关注 Combat Preference、Movement Signature、Attack Character、Defense / Counter Character 等维度。

```text
人物设定 / 体型能力 / 性格
+ Combat Intent
+ 环境 / 对手关系
+ Cinematic Choreography Profile
→ Combat Character Identity
→ 选择 / 混合 Fighting / Martial / Weapon Profile
→ Action Phrase
```

## 8. V2-06：Cinematic Choreography Profile

新增 **Cinematic Choreography Profile / 电影动作编排风格**，第一版基础方向可包含：写实战术型、凌厉电影动作型、高手连续攻防型、重型硬派型、环境技巧型。

它不进入一级视觉 `styles/`；由 Combat Playbook 协调，由小型 `combat-choreography-profiles` Library 提供稳定基础原型。

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

高置信度低风险项自动补全；只询问真正改变成片的变量；一次只问一个问题。

## 10. V2-08：Coverage 四类时间预算

Coverage 映射为 Setup Budget、Active Exchange Budget、Combat Downtime Budget、Ending Budget。

对于约 15 秒 High Coverage 高手 1v1，可参考：Setup 0.5–1.5s、Active Exchange 11–13s、累计 Downtime 尽量 ≤1–2s、纯 Ending Pose 0.5–1s。均为软预算。

## 11. V2-09：Exchange Depth

新增 **Exchange Depth / 攻防交换深度**，衡量 Defense → Counter → Re-counter → Continuation 的因果深度，而不是动作词数量。

主要由 Rhythm、Phrase 时长、Profile、Character Identity、Range / Advantage / Condition、环境、Camera Complexity、模型可执行性共同决定。

## 12. V2-10：Battle Beat 与 Action Phrase 动态一对多

Battle Beat : Action Phrase 动态一对多。Phrase 服务局部连续攻防组织；Beat 只在战术目标、Advantage、关键 Condition、主交战对象、战斗阶段或 Turning Event 实质变化时切换。

Phrase 之间可以无缝衔接，不要求 Downtime。

## 13. V2-11：Combat 中文术语统一

中文统一使用“动作编排 / 动作导演”；Action Phrase 使用“动作句 / 连续攻防段”。不再以“编舞”作为主要中文翻译。

## 14. V2-12：Combat Character Identity 动态推导，不建角色画像库

不建立“杀手 / 军人 / 警察 / 拳手”等职业到固定打法的模板映射。Character Identity 是当前 Combat Sequence 的动态推导结果。

Library 只保存相对稳定、可复用的 Fighting / Martial / Weapon 专业动作知识。

## 15. V2-13：小型 `combat-choreography-profiles` Library

第一版维护约 5–7 个稳定基础原型，描述 Coverage 倾向、Rhythm、Exchange Depth、动作重量与受力、Range 变化、环境利用、Phrase 节奏、Camera Complexity、冲突 / 不适用条件。

## 16. V2-14：Environment Action Affordance

```text
场景对象 / 空间结构 / 障碍
→ Environment Action Affordance
→ Intent / Identity / Range / Advantage 过滤
→ Action Phrase
→ 更新 Position / Range / Advantage / Condition / Environment State
```

只有环境利用真正改变攻击路线、移动路线、Range、Advantage、战术选择或 Phrase Payoff 时才值得使用，禁止装饰性随机破坏。

## 17. V2-15：Signature Moment / 标志性动作时刻

Signature Moment 是 Combat Sequence 级显式动作设计目标；Phrase Payoff 是局部结果，Signature Moment 是整场少数真正有记忆度的动作高潮 / 设计节点。

约 15 秒短动作片默认追求 1 个主要 Signature Moment，必要时可有 1 个辅助记忆点。Signature Moment 不等于慢动作，也不作为 Interactive Mode 固定追问项。

## 18. V2-16：经典影视 Signature Moment 参考体系按 Pattern 组织

经典影视打斗作为知识来源，但一级组织方式是 **可复用动作设计模式（Signature Moment Pattern）**，不是作品目录。作品名场面只是来源案例 / metadata。

运行时只吸收设计机制，再重新生成当前 Sequence 独有的 Signature Moment，不复刻完整影视动作段落。

## 19. V2-17：Signature Moment Pattern 单条知识结构

Pattern 采用 **抽象动作因果骨架 + 适用条件 + 可变化参数 + 案例证据**，核心字段包括 Pattern Intent、Trigger Conditions、Character Relationship、Core Mechanism、Action Causality Skeleton、Environment Role、Payoff Type、Rhythm / Exchange Fit、Camera Readability Hint、Adaptation Variables、Do Not Copy、Source Case IDs。

Source Case Facts 应核实；Pattern Abstraction 属于动作设计分析与归纳，不冒充影视官方定义。

## 20. V2-18：Signature Moment Pattern 轻量索引与按需加载

```text
references/libraries/signature-moment-patterns/
├─ index.md
├─ patterns/<pattern-id>.md
└─ source-cases/<case-id>.md
```

`index.md` 只存轻量路由信息；Agent 根据索引只加载最相关的 1–3 个 Pattern；正常生成默认不加载 `source-cases/`。

> **运行时加载设计知识，不加载研究档案。**

## 21. V2-19：`patterns/` 与 `source-cases/` 正式职责分离

- `patterns/`：存可迁移、可执行的动作设计生产知识；
- `source-cases/`：存作品 / 场景事实、核实来源、案例分析、可信度、关联 Pattern IDs。

> **Pattern 是生产知识；Source Case 是研究证据。**

## 22. V2-20：Tactical Interaction / 攻防博弈机制

新增 Tactical Interaction 作为 Action Phrase 内部可选战术因果层。

Exchange Depth 回答“有多深”；Tactical Interaction 回答“为什么进入下一层”。第一版 Playbook 维护少量稳定机制：Feint、Probe & Read、Bait、Anticipation、Counter-to-Counter、Pattern Break、Forced Response。

是否使用由 Character Identity、双方能力关系、Profile、Depth、Rhythm、当前状态、Phrase 时长、模型可执行性动态判断。

## 23. V2-21：Camera Readability Budget / 镜头可读性预算

```text
Action Complexity
+ Spatial Complexity
+ Camera Complexity
≈ 有限 Perceptual / Execution Budget
```

高 Coverage、高 Exchange Depth、高 Tactical Interaction、多人 / 高速换位、环境与空间复杂时，默认降低无必要 Camera Complexity，优先保持双方身体关系和动作因果可见。

重型 Payoff、环境换位、Signature Moment 等时机可以有目的释放镜头表现力。

> **镜头为动作服务；复杂动作先保证看清，简单爆点再释放镜头表现力。**

## 24. V2-22：Action Execution Budget / 动作执行复杂度预算

正式废除 V1 `1 个主攻防目标 + 2–4 个连续攻防交互节点 + 1 个结束状态` 作为 Battle Beat 全局默认动作数量锚点。

> **限制的是同一时间窗口内模型需要理解和执行的复杂信息量，不是整个 Battle Beat 最多允许多少动作。**

Battle Beat 不设置统一动作数量上限；一个 Beat 可以包含 1～多个无缝连续 Action Phrase。

同时增加 **Action Sufficiency Check** 防止取消上限后反而过少：检查 Coverage、Rhythm、Exchange Depth、Active Exchange Budget、无价值 Downtime 是否兑现。过载时优先删无价值动作 → 降低单 Phrase Depth / Tactical Complexity → 降低 Camera Complexity → 拆为无缝连续 Phrase → 最后才削减次要有效攻防。

## 25. V2-23：Combat Contact Solidity / 战斗接触实感

作为所有 Combat Contact Event 的通用动作质量维度，覆盖 Strike、Grapple / Control、Takedown / Throw、Blunt Weapon、Blade / Edge / Thrust、Weapon Clash / Parry、Environment Impact 等。

通用实感链：

```text
Commitment
→ Contact Event
→ Force / Energy / Pressure Transfer
→ Reaction Propagation
→ State Consequence
→ Recovery / Continuation
```

不同 Contact Modality 使用不同实感证据，不能把“重拳反馈”机械套到刀剑、摔控或兵器交击。

内部可动态区分 Light / Solid / Heavy，表示当前 Contact Event 的感知强度与战术后果等级。有效接触必须产生可见、可继承的身体 / 兵器 / 空间 / 状态后果；Camera / Audio 只能强化，不能替代真实受力。

## 26. V2-24：Clarity Through Structure, Not Action Reduction

正式替换 V1 “宁少而清晰”。

> **Clarity Through Structure, Not Action Reduction.**  
> **通过结构获得清晰，而不是通过动作通缩获得清晰。**

优秀动作戏天然是高信息密度内容；问题不在元素多，而在能否组织成清楚因果层级并被模型稳定执行。

> **高信息密度，但低混乱度。**  
> **清晰优先，但不以削减有效攻防换取清晰。**  
> **宁可少冗余，不可少有效攻防。**

复杂度风险优先通过去冗余、Phrase 结构化、降低 Camera Complexity、连续 Phrase 切分解决。

## 27. V2-25：State Machine Internalized, Choreography Externalized

Final Prompt 正式采用：

> **State Machine Internalized, Choreography Externalized.**  
> **状态机内化，动作编排外显。**

内部完整运行 Range、Advantage、Condition、Exchange Depth、Tactical Interaction、Combat Contact Solidity、Environment Affordance、Camera Readability Budget 等机制；Final Prompt 则把这些状态转译成视频模型可执行、观众可见的动作事实。

信息优先级：正向可见动作 → 空间与环境动作 → 动作质感 → Camera / Audio → 少量必要连续性 / Negative Constraints。

Final Prompt 应由 Action Language 主导；不得默认追加通用禁止清单或无根据限制。

## 28. V2-26：Combat Quality Benchmark / 打斗成片质量基准集

建立 **静态结构回归 + 实际生成视频质量回归** 双层验证体系。

> **最终生成视频动作质量是第一验收目标；静态规则正确只是必要条件，不是充分条件。**

第一版维护约 6–10 个 Golden Combat Scenarios，覆盖高手近身、力量差、受限空间、硬派拳脚、短兵器、长兵器、抓控摔投、多人战等。

成片至少评价 Active Combat Coverage Realization、Exchange / Choreography Richness、Character Distinction、Tactical Interaction Realization、Combat Contact Solidity、Environment Integration、Signature Moment、Camera Readability、Spatial / Physical Continuity、Rhythm Variation。

显式记录 **Prompt Intent → Generated Result Gap**；“Prompt 写了某条规则”不等于“成片兑现了该规则”。

## 29. V2-27：Golden Combat Scenario 使用质量合同，不锁固定动作答案

Golden Scenario 采用：

```text
Fixed Input
+ Quality Contract
+ Failure Contract
+ Optional Test Anchor
```

Fixed Input 保证可比性；Quality Contract 定义必须兑现的质量；Failure Contract 定义禁止退化模式；Optional Test Anchor 只在专门测试某能力时要求该抽象能力必须出现。

> **Benchmark 锁质量，不锁创意。**

## 30. V2-28：Combat Core 与专项实现层解耦

正式确立一级架构边界：**Combat Core 保持 Combat-agnostic / 战斗形式无关；Modern Combat、Cinematic Wuxia、Weapon / Fighting / Martial 等专项层只负责把 Core 机制实例化为不同动作语言、物理尺度、默认节奏和 Contact Modality 表现。**

推荐结构：

```text
Combat Core
├─ Coverage
├─ Rhythm
├─ Action Phrase
├─ Exchange Depth
├─ Combat Character Identity
├─ Tactical Interaction
├─ Environment Action Affordance
├─ Signature Moment
├─ Combat Contact Solidity
├─ Action Execution Budget
├─ Camera Readability Budget
└─ State / Continuity Contract
        ↓
专项实现层
├─ Modern Combat
├─ Cinematic Wuxia
├─ Fighting / Martial Profiles
└─ Weapon Profiles / Weapon-specific execution
```

Core 规定的是 **机制与质量合同**，例如：

- 接触必须有 Commitment → Contact → Transfer → Reaction → Consequence；
- Phrase 必须有因果连续性；
- Coverage / Rhythm / Exchange Depth 必须兑现；
- 环境利用必须改变战术或空间关系；
- Signature Moment 必须由前后动作因果支撑；
- Camera 必须服务动作可读性。

专项层规定的是 **这种战斗形式如何表现上述机制**：

- Modern Combat：更强调重心、身体发力、直接压迫、真实失衡、短距离 Contact；
- Cinematic Wuxia：可采用借力、身法、兵器轨迹、电影化腾跃、节奏留白等不同物理尺度，但仍必须保持动作因果与状态继承；
- Grapple / Takedown：以杠杆、压迫、夺重心、控制与挣脱代价体现 Contact Solidity；
- Blade / Weapon：以危险线路、距离约束、格挡偏转、兵器震荡、主动权与 Weapon State 变化体现 Contact Solidity；
- 其他 Fighting / Martial / Weapon Profile 继续作为专业动作语言来源，而不是改写 Core 规则。

禁止以下反向污染：

- 把现代拳脚的“拳拳到肉”表现模板强制套到刀剑 / 武侠 / 摔控；
- 把某一职业 / 流派直接映射为唯一 Character Identity；
- 因某专项默认节奏修改 Core 的 Coverage / Phrase / State Contract 基本定义；
- 为适配某一种动作形式在 Core 中塞入大量专项招式或影视表现细节。

原则：

> **Core 规定“必须成立什么”；专项层规定“在这种战斗里它具体长什么样”。**  
> **专项可以覆盖默认表现，但不能反向重定义 Combat Core。**

---

## 31. V2 设计原则汇总

1. 时间轴写满不代表动作写满，必须检查 Coverage；
2. 持续交战不代表动作丰富，必须检查 Rhythm / Phrase / Exchange Depth；
3. 动作合理不代表好看，动作导演层负责视觉动作设计；
4. 高手身份必须通过打法表现；Character Identity 动态推导；
5. Phrase 负责连续动作，State Contract 负责连续性；Phrase 与 Beat 不绑定 1:1；
6. High Coverage 不等于全程同速，Active Combat Feedback 与 Downtime 必须区分；
7. Exchange Depth 衡量因果深度，不衡量动作词数量；Tactical Interaction 回答攻防为何进入下一层；
8. 环境先作为动作机会参与设计，再由 V1 继承状态；
9. Choreography Profile 只维护少量稳定原型；
10. Signature Moment 是少量 Sequence 级记忆点；影视参考用于抽象机制，不复制完整动作；
11. Pattern Library 轻量索引、按需加载；Pattern 与 Source Case 分层；
12. Camera Complexity 与动作 / 空间复杂度共享有限执行预算；高动作复杂度优先可读性；
13. Battle Beat 不使用固定 `2–4` 节点动作锚点；Action Sufficiency Check 防止动作不足；
14. Combat Contact Solidity 适用于所有主要接触形式，不同 Contact Modality 使用不同实感证据；
15. 优秀动作戏追求高信息密度而非少元素；清晰来自层级、因果、Phrase 结构和镜头组织；
16. State Machine Internalized, Choreography Externalized；Final Prompt 由正向动作语言主导；
17. Combat 回归同时包含静态结构与真实成片质量回归，并评价 Prompt Intent → Generated Result Gap；
18. Golden Scenario 采用 Fixed Input + Quality Contract + Failure Contract + Optional Test Anchor，锁质量不锁创意；
19. Combat Core 只定义跨战斗形式稳定成立的机制 / 质量合同；Modern / Wuxia / Weapon 等专项层负责具体表现，不允许专项反向污染 Core。

## 32. 已确认决策记录

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
| V2-17 | Pattern 数据结构 | 抽象因果骨架 + 适用条件 + 可变化参数 + 案例证据 |
| V2-18 | Pattern 加载架构 | 轻量 `index.md` → 按需加载 1–3 个 Pattern → source-cases 默认不加载 |
| V2-19 | Pattern / Source Case 分层 | `patterns/` 存生产知识；`source-cases/` 存研究证据 |
| V2-20 | Tactical Interaction | 假动作、试探、诱导、预判、Counter-to-Counter 等作为 Phrase 可选战术因果层 |
| V2-21 | Camera Readability Budget | Camera Complexity 与动作 / 空间复杂度共享执行预算 |
| V2-22 | Action Execution Budget | 废除 Battle Beat 全局 `2–4` 交互节点锚点；改为 Phrase 级动态执行预算，并增加 Action Sufficiency Check |
| V2-23 | Combat Contact Solidity | 全战斗接触共享 Contact 实感链，并按 Contact Modality 适配 |
| V2-24 | Clarity Through Structure | 正式替换“宁少而清晰”；高信息密度通过结构保证清晰 |
| V2-25 | Final Prompt 输出原则 | 状态机内化、动作编排外显；最小化状态术语与无根据 Negative Constraints |
| V2-26 | Combat Quality Benchmark | 静态结构回归 + 真实成片质量回归；评价 Prompt→成片执行差距 |
| V2-27 | Golden Scenario Contract | Fixed Input + Quality Contract + Failure Contract + Optional Test Anchor；锁质量不锁创意 |
| V2-28 | Core / 专项边界 | Combat Core 定义通用机制与质量合同；Modern / Wuxia / Weapon 等专项层实例化动作语言、物理尺度、节奏和 Contact 表现，禁止专项反向污染 Core |

## 33. 全局复盘后待继续 Grill Me 的设计树

1. **运行时编排与 Reference 加载预算**：V2 新增 Choreography Profile、Signature Moment Pattern、Environment Affordance、Fighting / Martial / Weapon Profile 等知识，需要确认实际按需路由链，避免运行时全量加载；
2. **模型能力如何正式进入动作预算**：是否形成轻量 Model Capability Contract，为 Exchange Depth、Action Execution Budget、Camera Complexity 等提供能力输入；
3. **Quick / Interactive 的运行闭环**：Interactive 已有决策链，Quick Mode 的自动推导顺序仍需确认；
4. **Action / Camera / Audio 三线职责平衡**：确认 V2 Audio 是继承 V1 即可，还是需要动作节奏 / Contact / Signature Moment 的专项增强；
5. **实现层归属**：最终确认哪些内容属于 Task Playbook、Control、Library、Diagnostic、Output Contract、Model Adapter，以及是否新增独立 Control。

## 34. 当前阶段结论

V2 已基本补齐“持续性、丰富度、角色差异、环境设计、博弈、接触实感、记忆点、镜头可读性、动作化 Prompt、成片验证”等核心质量层，并正式建立 Combat Core 与专项实现层的边界。

下一步应优先解决 **运行时按需加载与 Reference 预算**，再进入模型能力输入、Quick / Interactive 闭环、Audio 协同和最终实现归属。

本文件继续作为 V2 Grill Me 的单一设计记录。