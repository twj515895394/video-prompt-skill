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
→ Final Prompt Action Externalization
```

核心原则：

> **Combat Choreography Engine 负责“打得好不好看、够不够、实不实”。**  
> **Combat State / Continuity Engine 负责“打得对不对、接不接得上”。**  
> **约束错误，不约束创作。**

---

## 3. V2-01：Combat Choreography Engine

正式新增动作编排引擎，负责：有效交战时间、单位时间攻防交换丰富度、角色打法差异、整场电影动作观感、Action Phrase 组织、节奏变化、环境动作机会、Tactical Interaction、Combat Contact Solidity、Signature Moment，以及可读性与模型可执行性的动态平衡。

它不替代 V1 Range / Advantage / Condition / State Contract。

## 4. V2-02：Active Combat Coverage

新增 **Active Combat Coverage / 有效交战覆盖率**。

> Timeline Coverage ≠ Combat Coverage

Interactive 可表达为：Low 约 40–55%，Medium 约 60–75%，High 约 75–90%。类似“15 秒、高手 1v1、办公室近身对决”默认推荐 High。

High 不等于全程同速高速动作；只要受击、失衡、闪避、恢复、快速重新切入等反馈直接推动下一次攻防，仍属于 Active Combat。

## 5. V2-03：Action Exchange Rhythm

Coverage 决定“有多少时间在打”；Rhythm 决定“持续交战期间如何交换”。基础类型：重击型、均衡型、高手高速交换型、混合型。

## 6. V2-04：Action Phrase

层级：

```text
Action–Reaction Pair
→ Action Phrase
→ Battle Beat
→ Combat Sequence
```

Action Phrase 的核心是：**前一个动作自然制造下一个动作的机会。**

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

角色战斗身份回答“当前这个角色怎么打”。动态判断至少关注 Combat Preference、Movement Signature、Attack Character、Defense / Counter Character；这些只是推导维度，不是固定标签全集。

```text
人物设定 / 体型能力 / 性格
+ Combat Intent
+ 当前环境
+ 对手关系
+ Cinematic Choreography Profile
        ↓
动态推导 Combat Character Identity
        ↓
选择 / 混合 Fighting / Martial / Weapon Profile
        ↓
Action Phrase
```

## 8. V2-06：Cinematic Choreography Profile

新增 **Cinematic Choreography Profile / 电影动作编排风格**。第一版基础方向可包含：写实战术型、凌厉电影动作型、高手连续攻防型、重型硬派型、环境技巧型。

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

上游选择驱动下游推荐；高置信度低风险项自动补全；只询问真正改变成片的变量；始终一次只问一个最关键问题。

## 10. V2-08：Coverage 四类时间预算

Active Combat Coverage 映射为 Setup Budget、Active Exchange Budget、Combat Downtime Budget、Ending Budget。

对于“15 秒、高手 1v1、High Coverage”可采用内部参考：Setup 约 0.5–1.5 秒、Active Exchange 约 11–13 秒、累计 Downtime 尽量 ≤ 1–2 秒、纯 Ending Pose 约 0.5–1 秒。均为软预算。

## 11. V2-09：Exchange Depth

新增 **Exchange Depth / 攻防交换深度**。

> **Exchange Depth ≠ Action Verb Count**

衡量一次发起后连续 Defense → Counter → Re-counter → Continuation 的因果深度。主要受 Rhythm、Phrase 时长、Choreography Profile、Character Identity、Range / Advantage / Condition、环境复杂度、Camera Complexity 和模型可执行性共同决定。

## 12. V2-10：Battle Beat 与 Action Phrase 动态一对多

确认 **Battle Beat : Action Phrase 动态一对多**，不默认 `1 Beat = 1 Phrase`。Phrase 按局部连续攻防组织切分，Beat 只在战术目标、Advantage、关键 Condition、主交战对象、战斗阶段或 Turning Event 实质变化时切换。

Phrase 之间可以无缝衔接，不要求 Downtime。

## 13. V2-11：Combat 中文术语统一

英文保留 Choreography；中文统一使用“动作编排 / 动作导演”。Action Phrase 统一为“动作句 / 连续攻防段”。

## 14. V2-12：Combat Character Identity 动态推导，不建角色画像库

不建立职业到固定打法的模板映射。Combat Character Identity 是当前 Combat Sequence 的动态推导结果。Library 只保存相对稳定、可复用的 Fighting / Martial / Weapon 专业动作知识。

## 15. V2-13：小型 `combat-choreography-profiles` Library

正式新增该 Library，第一版只维护约 5–7 个稳定基础原型。每个 Profile 描述 Coverage 倾向、Rhythm、Exchange Depth、动作重量与受力反馈、Range 变化、环境利用、Phrase 节奏、Camera Complexity 和冲突 / 不适用条件。

## 16. V2-14：Environment Action Affordance

新增 **Environment Action Affordance / 环境动作机会**。

```text
场景对象 / 空间结构 / 障碍
→ Environment Action Affordance
→ 结合 Intent / Identity / Range / Advantage 过滤
→ Action Phrase
→ 更新 Position / Range / Advantage / Condition / Environment State
```

只有环境利用至少改变攻击路线、移动路线、Range、Advantage、战术选择或 Phrase Payoff 之一时才值得使用。禁止装饰性随机破坏。

## 17. V2-15：Signature Moment / 标志性动作时刻

新增 **Signature Moment** 作为 Combat Sequence 级显式动作设计目标。Phrase Payoff 是局部结果；Signature Moment 是整场少数真正具有记忆度的动作高潮 / 设计节点。

约 15 秒短动作片默认只追求 1 个主要 Signature Moment，必要时 1 个辅助记忆点。Signature Moment 不等于慢动作，也不作为 Interactive Mode 固定追问项。

## 18. V2-16：经典影视 Signature Moment 参考体系按 Pattern 组织

经典影视打斗作为 Signature Moment 的知识来源，但一级组织方式是 **可复用动作设计模式（Signature Moment Pattern）**，不是作品目录。作品名场面只作为来源案例 / metadata。

运行时吸收设计机制，再重新生成当前 Sequence 独有的 Signature Moment，不复刻影视完整动作段落。

## 19. V2-17：Signature Moment Pattern 单条知识结构

单条 Pattern 采用 **抽象动作因果骨架 + 适用条件 + 可变化参数 + 案例证据** 的结构，不保存可直接复刻的完整影视动作序列。

核心字段包括 Pattern Intent、Trigger Conditions、Character Relationship、Core Mechanism、Action Causality Skeleton、Environment Role、Payoff Type、Rhythm / Exchange Fit、Camera Readability Hint、Adaptation Variables、Do Not Copy、Source Case IDs。

Source Case Facts 应核实；Pattern Abstraction 属于动作设计分析与归纳，不冒充影视官方定义。

## 20. V2-18：Signature Moment Pattern 轻量索引与按需加载

```text
references/libraries/signature-moment-patterns/
├─ index.md
├─ patterns/
│  └─ <pattern-id>.md
└─ source-cases/
   └─ <case-id>.md
```

`index.md` 只存轻量路由信息；Agent 根据索引选出候选后只加载最相关的 1–3 个 Pattern；正常生成默认不加载 `source-cases/`。

> **运行时加载设计知识，不加载研究档案。**

## 21. V2-19：`patterns/` 与 `source-cases/` 正式职责分离

- `patterns/`：存可迁移、可执行的动作设计知识；
- `source-cases/`：存作品 / 场景事实、核实来源、案例分析、可信度和关联 Pattern IDs。

> **Pattern 是生产知识；Source Case 是研究证据。**

## 22. V2-20：Tactical Interaction / 攻防博弈机制

新增 **Tactical Interaction / 攻防博弈机制**，作为 Action Phrase 内部的可选战术因果层。

- Exchange Depth：回答“一轮连续攻防有多深”；
- Tactical Interaction：回答“为什么会自然进入下一层攻防”。

第一版只在 Playbook 中维护少量稳定类型：Feint、Probe & Read、Bait、Anticipation、Counter-to-Counter、Pattern Break、Forced Response。是否使用由 Character Identity、双方能力关系、Profile、Depth、Rhythm、当前状态、Phrase 时长和模型可执行性动态判断。

## 23. V2-21：Camera Readability Budget / 镜头可读性预算

```text
Action Complexity
+ Spatial Complexity
+ Camera Complexity
≈ 有限的 Perceptual / Execution Budget
```

高 Coverage、高 Exchange Depth、高 Tactical Interaction、多人 / 高速换位、环境和空间复杂度较高时，默认降低无必要 Camera Complexity，优先保持双方身体关系和动作因果可见。

重型 Phrase Payoff、环境换位、Signature Moment 或短暂重建空间关系时，可以有目的地释放镜头表现力。

> **镜头为动作服务；复杂动作先保证看清，简单爆点再释放镜头表现力。**

## 24. V2-22：Action Execution Budget / 动作执行复杂度预算

正式废除 V1 中 `1 个主攻防目标 + 2–4 个连续攻防交互节点 + 1 个结束状态` 作为 Battle Beat 的全局默认动作数量锚点。

> **限制的是同一时间窗口内模型需要理解和执行的复杂信息量，不是整段 Battle Beat 最多允许多少动作。**

Battle Beat 不设置统一动作数量上限；一个 Beat 可以包含 1～多个无缝连续的 Action Phrase。

### Action Sufficiency Check / 动作充分性检查

取消全局动作数量上限，不代表取消最低充分性检查。High / Medium Coverage 未兑现、高手高速 / 混合型 Exchange Depth 偏低、长 Beat 只有极少有效攻防、Phrase 间有大量无价值站立 / 摆姿势等，均视为 Combat Underfill 并触发重新规划。

Action Sufficiency 不采用固定最低招数，而检查 Coverage、Rhythm、Exchange Depth、Active Exchange Budget 和无价值 Downtime 是否兑现。

过载时优先：删除无价值附属动作 → 降低单 Phrase Depth / Tactical Complexity → 降低 Camera Complexity → 拆成仍无缝连续的 Phrase → 只有战术状态真正变化才拆 Beat。

## 25. V2-23：Combat Contact Solidity / 战斗接触实感

正式新增 **Combat Contact Solidity / 战斗接触实感**，作为所有 Combat Contact Event 的通用动作质量维度，覆盖 Strike、Grapple / Control、Takedown / Throw、Blunt Weapon、Blade / Edge / Thrust、Weapon Clash / Parry、Environment Impact 等。

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

内部可动态区分 Light / Solid / Heavy，表示当前 Contact Event 的感知强度与战术后果等级，而非所有武器都按物理重量理解。

六个通用检查维度：Commitment、Contact Clarity、Force / Pressure Transfer、Reaction Propagation、Persistent Consequence、Audio / Camera Accent。

有效接触必须产生可见、可继承的身体 / 兵器 / 空间 / 状态后果；Camera / Audio 只能强化，不能替代真实受力与状态变化。

## 26. V2-24：Clarity Through Structure, Not Action Reduction

正式替换 V1 容易被过度保守执行的“宁少而清晰”原则。

新的上位原则是：

> **Clarity Through Structure, Not Action Reduction.**  
> **通过结构获得清晰，而不是通过动作通缩获得清晰。**

中文执行语义：

> **清晰优先，但不以削减有效攻防换取清晰。**  
> **宁可少冗余，不可少有效攻防。**

进一步确认：**“宁少而清晰”与优秀动作戏的本质并不相符，不能继续作为动作视频的上位设计原则。** 一段优秀打斗天然就是高信息密度内容，同时包含攻击、反应、防守、反制、受力、重心、空间、环境、镜头、声音、节奏、人物状态和战术关系。问题不在“元素多”，而在这些元素是否被组织成清楚的因果层级、是否在同一窗口内可读、是否能被模型稳定执行。

因此 V2 对动作戏的目标不是“少元素”，而是：

> **高信息密度，但低混乱度。**

“动作多”本身不是错误。真正需要控制的是：动作之间缺少因果、同一时间窗口塞入过多独立信息、镜头无法看清动作关系、模型无法稳定执行、动作虽然多但只是重复或装饰且不改变战斗关系。

当出现可读性 / 模型执行风险时，默认处理顺序：

```text
1. 删除重复、装饰、无状态价值的动作
2. 简化单个 Action Phrase 的复杂结构 / 次要分支
3. 降低 Camera Complexity
4. 将过载 Phrase 拆成多个仍然连续交战的 Phrase
5. 只有仍然无法执行时，才削减次要有效攻防
```

这与 V2-22 的 Action Sufficiency Check 共同形成双向约束。

## 27. V2-25：State Machine Internalized, Choreography Externalized

正式确立 Final Prompt 的输出原则：

> **State Machine Internalized, Choreography Externalized.**  
> **状态机内化，动作编排外显。**

V1 / V2 内部仍完整运行 Range、Advantage、Condition、Combat State、Exchange Depth、Tactical Interaction、Combat Contact Solidity、Environment Affordance、Camera Readability Budget 等机制，用于规划、校验和状态继承；但 Final Prompt 不应大量暴露这些抽象术语，而应把它们转译成视频模型能直接执行、观众能直接看到的动作事实。

Combat Final Prompt 的主体信息优先级：

1. 正向可见动作：Action Phrase、Attack / Defense / Counter / Re-counter、Contact、Reaction、Continuation；
2. 空间与环境动作：换位、距离变化、路线、Environment Affordance、站位后果；
3. 动作质感：速度、重量、节奏、Contact Solidity、Signature Moment；
4. Camera / Audio：只服务动作可读性、空间理解和冲击；
5. 必要连续性 / Negative Constraints：只保留当前场景真正高风险、且正向动作语言无法充分解决的少量约束。

Final Prompt 的主体篇幅和语义重心应该明显落在实际发生的 Action Phrase、Reaction、Contact Consequence 和空间变化上。Negative Constraint 不再默认追加通用防错清单，也不得擅自添加用户没有提出、场景也没有证据支持的限制。

> **内部严谨，外部生动；状态负责校验，动作负责表达。**

## 28. V2-26：Combat Quality Benchmark / 打斗成片质量基准集

正式把 Combat 回归体系从“Prompt / 规则有没有写对”升级为 **静态结构回归 + 实际生成视频质量回归** 的双层验证体系。

核心验收原则：

> **最终生成视频的动作质量是第一验收目标；静态规则正确只是必要条件，不是充分条件。**

### Level 1：Static / Structural Regression

继续保留 V1 已有的静态回归，用于检查规则、路由、状态连续性、Final Prompt 动作化、Negative Constraints 和 Combat Underfill 等。

### Level 2：Generated Video Quality Regression

第一版维护约 6–10 个小而稳定的 Golden Combat Scenarios，覆盖高手近身、力量差、受限空间、硬派拳脚、短兵器、长兵器、抓控摔投、多人战等不同难点。

实际生成视频至少评价：

- Active Combat Coverage Realization；
- Exchange / Choreography Richness；
- Character Distinction；
- Tactical Interaction Realization；
- Combat Contact Solidity；
- Environment Integration；
- Signature Moment；
- Camera Readability；
- Spatial / Physical Continuity；
- Rhythm Variation。

同时显式记录 **Prompt Intent → Generated Result Gap**，不能把“Prompt 写了某条规则”等同于“成片兑现了该规则”。

每次实际生成测试至少记录 Golden Scenario ID、Skill / Spec / Prompt 版本、目标视频模型与版本 / Adapter、关键生成参数与时长、Final Prompt、成片评价、Failure Signature 与版本改善 / 退化。

> **Prompt 写得对，只能说明系统内部设计没有明显违规；视频真正打得好，才说明 Combat V2 达到目标。**

## 29. V2-27：Golden Combat Scenario 使用质量合同，不锁固定动作答案

Golden Combat Scenario 正式采用：

```text
Fixed Input
+ Quality Contract
+ Failure Contract
+ Optional Test Anchor
```

不保存、也不要求模型复现某一套固定“标准动作序列”。Golden Benchmark 测试的是动作导演能力与成片质量，而不是是否背出同一套动作答案。

### Fixed Input

固定用于可重复对比的测试前提，例如人物、场景、时长、战斗目的、必要武器 / 环境条件、目标模型与关键生成参数。

### Quality Contract

定义该场景必须兑现的质量目标，例如 High Coverage、足够连续攻防、角色打法差异、可信 Contact Solidity、环境真正参与、主要 Signature Moment、Camera Readability 与 Ending 时机等。

### Failure Contract

定义必须避免的退化模式，例如长时间对峙、只有两三次攻防、大量无意义僵持、接触无受力、双方打法同质、随机环境破坏、运镜掩盖动作、提前数秒摆 Pose 等。

### Optional Test Anchor

只有当某个 Golden Scenario 专门验证某项能力时，才增加抽象能力锚点，例如：

- 环境测试：环境必须至少一次改变攻击线路 / Range / Advantage；
- 刀战测试：至少一次由兵器线路偏转导致下一拍主动权变化；
- Tactical Interaction 测试：至少出现一次可见的诱导 / 预判 / Counter-to-Counter 机制。

Test Anchor 只规定“能力必须出现”，不规定必须用哪一招、哪件物体、哪套镜头实现。

原则：

> **Benchmark 锁质量，不锁创意。**  
> **固定输入保证可比性，质量 / 失败合同保证验收稳定，动作编排本身继续保留创造空间。**

---

## 30. V2 设计原则汇总

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
12. Tactical Interaction 负责攻防为何进入下一层；
13. 战术博弈动态触发，不要求每个 Phrase 都有；
14. 环境先作为动作机会参与设计，再由 V1 继承状态；
15. Choreography Profile 只维护少量稳定原型；
16. 15 秒短动作片默认只有少量 Signature Moment；
17. 经典影视参考用于抽象动作设计规律，不用于复制完整动作段落；
18. Pattern 是知识主体，作品只作为来源案例；
19. Pattern Library 必须通过轻量索引按需加载；
20. Pattern 与 Source Case 正式分层；
21. Camera Complexity 与动作 / 空间复杂度共享有限执行预算；
22. 高动作复杂度优先镜头可读性；
23. Battle Beat 不再使用固定 `2–4` 节点作为动作数量锚点；
24. Action Sufficiency Check 负责防止动作不足；
25. Combat Contact Solidity 适用于所有主要接触形式；
26. 不同 Contact Modality 使用不同实感证据；
27. 有效接触必须产生可见、可继承的身体 / 兵器 / 空间 / 状态后果；
28. 优秀动作戏追求高信息密度而非少元素；清晰来自层级、因果、Phrase 结构和镜头组织；
29. 复杂度问题优先通过去冗余、Phrase 结构化、降低 Camera Complexity 和连续 Phrase 切分解决；
30. State Machine Internalized, Choreography Externalized：状态机内化、动作编排外显；
31. Final Prompt 以正向可见动作、接触后果和空间变化为主体，状态规范与 Negative Constraint 只保留真正必要部分；
32. Combat 回归必须同时包含静态结构回归与真实成片质量回归；最终生成视频质量是首要验收目标；
33. 回归必须评价 Prompt Intent → Generated Result Gap；
34. Golden Combat Scenario 通过 Fixed Input + Quality Contract + Failure Contract + Optional Test Anchor 定义，锁质量而不锁固定动作答案。

## 31. 已确认决策记录

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
| V2-23 | Combat Contact Solidity | 全战斗接触共享 Commitment → Contact → Transfer → Reaction → Consequence → Continuation 实感链，并按 Contact Modality 适配 |
| V2-24 | Clarity Through Structure | 正式替换“宁少而清晰”；优秀动作戏允许高信息密度，清晰通过层级、因果、Phrase 结构、镜头收敛和连续切分获得，不默认削减有效攻防 |
| V2-25 | Final Prompt 输出原则 | State Machine Internalized, Choreography Externalized；内部状态完整运行，最终 Prompt 以正向可见动作、受力、空间变化和连续攻防为主体，最小化状态术语与 Negative Constraints |
| V2-26 | Combat Quality Benchmark | 建立“静态结构回归 + 真实成片质量回归”双层体系；维护 Golden Combat Scenarios，评价 Coverage、动作丰富度、角色差异、战术博弈、接触实感、环境、Signature Moment、Camera Readability、连续性与 Prompt→成片执行差距 |
| V2-27 | Golden Scenario Contract | Golden Scenario 不锁固定动作答案，采用 Fixed Input + Quality Contract + Failure Contract + Optional Test Anchor，保证可比性同时保留动作编排创造空间 |

## 32. 全局复盘后待继续 Grill Me 的设计树

在进入实现文件映射之前，需要先回到 V2 / V1 / Reference Architecture 全局层面重新审查以下一级问题：

1. **能力适用范围与分支一致性**：V2 当前大量增强来自现代近身格斗案例，但 V1 正式范围同时包含现代格斗、电影武侠、拳脚、抓控与兵器；需要确认 V2 哪些机制是 Combat Core 通用能力，哪些需要 Modern / Wuxia / Weapon 分支适配，避免现代格斗逻辑反向污染武侠与兵器动作；
2. **运行时编排与 Reference 加载预算**：Reference Architecture 要求每次只加载 1 task、0–3 controls、0–2 libraries 等；V2 新增 Choreography Profile、Signature Moment Pattern、Environment Affordance、Fighting / Martial / Weapon Profile 等知识，需要设计实际按需路由链，避免理论能力完整但运行时全量加载；
3. **模型能力如何正式进入动作预算**：V2 多处依赖“目标视频模型可执行性”，但尚未定义模型适配层如何向 Choreography Engine 提供可用的 Action / Camera / Multi-character / Contact Complexity 能力信息；需要确认是否形成轻量 Model Capability Contract；
4. **Quick / Interactive 的运行闭环**：Interactive 已有专属决策链，但 Quick Mode 对 Profile、Coverage、Rhythm、Identity、Environment、Signature Moment、Contact Solidity 等变量的自动推导顺序与默认闭环仍需全局确认；
5. **Action / Camera / Audio 三线在 V2 的职责平衡**：V1 把三线同步作为核心能力，V2 目前重点增强 Action 与 Camera，Audio 更多作为 Contact Accent 存在；需要确认 Audio 是否仅继承 V1，还是 V2 还缺少动作节奏 / Contact / Signature Moment 的声音编排升级；
6. **实现层归属**：最终需要确认哪些内容属于 Task Playbook，哪些属于 Control、Library、Diagnostic、Output Contract、Model Adapter，以及是否真的需要新增独立 Control；应在前述全局问题收口后再做，避免先按文件结构反推动作设计。

## 33. 当前阶段结论

V1 已能够较好地“把战斗写对”；V2 已基本补齐“持续性、丰富度、角色差异、环境设计、博弈、接触实感、记忆点、镜头可读性、动作化 Prompt 与成片验证”等核心质量层。

当前不宜继续下钻单条 Pattern 或测试字段，而应回到全局设计树，优先确认 **V2 Combat Core 与 Modern / Wuxia / Weapon 等分支之间的边界**，然后再依次解决运行时加载、模型能力输入、模式闭环、音画协同和最终实现归属。

本文件继续作为 V2 Grill Me 的单一设计记录。