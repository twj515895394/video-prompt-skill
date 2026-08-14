# Action Combat Video Prompt Spec V2

> 状态：设计中（Grill Me 持续收敛）
>
> 基线：`docs/action-combat-video-spec.md`
>
> V1 状态：已完成设计、实现与静态回归
>
> V2 定位：在保留 V1 Combat State / Continuity Engine 的基础上，新增并强化 **Combat Choreography Engine（动作编排引擎 / 动作导演层）**，重点解决实测中“有效交战时间不足、动作交换过少、角色打法同质、动作缺乏电影动作编排感”等问题。

## 1. 背景与问题来源

V1 已较完整地解决复杂打斗 Prompt 中的状态与连续性问题，包括：

- Combat Intent；
- Combat Spatial Map；
- Range / Advantage / Condition；
- Turning Event；
- Action–Reaction Pair；
- Battle Beat；
- Target Handoff；
- Beat State Contract；
- Action / Camera / Audio 三线协同；
- 打击受力、空间连续、镜头轴线与环境状态继承。

但在真实生成测试中出现新的核心问题：

> **Prompt 的 15 秒时间轴虽然被完整描述，但真正发生持续打斗动作的时间只有约 2–3 秒，且有效攻击 / 防守交换只有两三次。**

典型表现：

- 开场对峙占用过长；
- 大量时间用于抓腕、控制、重新站稳、调整重心等低动态状态；
- 一个 Battle Beat 内缺少足够连续的攻防交换；
- “职业杀手”被过度映射到 Tactical Close Combat，导致动作趋向制服 / 控制，而不是电影化高手对决；
- 双方使用相似动作语言，角色打法缺少可见差异；
- 环境虽然参与状态变化，但没有充分转化为动作设计素材；
- V1 强调“宁少而清晰”，在短时长动作片中可能被过度执行，形成动作预算通缩。

因此 V2 不推翻 V1，而是补足 V1 当前较弱的“动作导演 / 动作编排”能力。

## 2. V1 与 V2 的关系

V1 继续作为底层 **Combat State / Continuity Engine**：

```text
Combat Intent
→ Spatial Map
→ Range / Advantage / Condition
→ Action–Reaction Pair
→ Turning / Handoff
→ Beat State Contract
→ Continuity / Physics Validation
```

V2 在其上新增 **Combat Choreography Engine**：

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
→ V1 Combat State / Continuity Engine
→ Camera / Audio Coordination
→ Final Prompt Compression
```

核心职责拆分：

> **Combat Choreography Engine 负责“打得好不好看”。**
>
> **Combat State / Continuity Engine 负责“打得对不对、接不接得上”。**

V2 必须继续遵守 V1 上位原则：

> **约束错误，不约束创作。**

新增的 Coverage、Rhythm、Identity、Profile、Action Phrase、Signature Moment 均属于创作与动作编排工具，不应被实现为所有场景固定套用的动作模板。

## 3. 已确认决策一：新增 Combat Choreography Engine

确认 V2 核心不是继续堆叠更多状态连续性规则，而是在 V1 上新增正式的 **Combat Choreography Engine（动作编排引擎 / 动作导演层）**。

该层主要负责：

- 控制整段视频真正处于交战状态的时间比例；
- 控制单位时间内攻防交换节奏和丰富度；
- 为主要战斗角色建立差异化打法；
- 决定整场动作戏的电影动作编排观感；
- 将原子级 Action–Reaction Pair 组织成连续 Action Phrase；
- 生成具有视觉记忆点、节奏变化和环境利用的动作设计；
- 在保证可读性的前提下避免“动作过少”。

该层不替代 V1 的 Range / Advantage / Condition / Continuity State。

## 4. 已确认决策二：Active Combat Coverage

新增 **Active Combat Coverage / 有效交战覆盖率**。

它解决的问题不是“时间轴有没有填满”，而是：

> **整段视频有多少有效时长真正处于攻击、防守、闪避、反击、换位、缠斗、追击或其他持续交战状态。**

必须区分：

> Timeline Coverage ≠ Combat Coverage

Interactive Mode 下可以让用户选择三档，并给出推荐：

- **Low｜剧情 / 对峙型**：约 40–55% 有效交战；
- **Medium｜标准电影动作戏**：约 60–75%；
- **High｜持续高手对决**：约 75–90%。

对于类似“15 秒、两个职业杀手、办公室近身对决”的短时长高手动作片，默认推荐 **High**。

High Coverage 不等于全片高速挥拳。短暂停顿、僵持、重击反馈和节奏变化允许存在，但不应让角色长时间退出交战状态。

## 5. 已确认决策三：Action Exchange Rhythm

新增 **Action Exchange Rhythm / 攻防交换节奏类型**。

- Coverage 决定“有多少时间在打”；
- Exchange Rhythm 决定“持续打斗期间，攻防交换如何组织”。

Interactive Mode 下使用用户可理解的节奏类型：

1. **重击型**：动作数量较少，但单次交换重量、失衡、碰撞和恢复更明显；
2. **均衡型**：连续攻防与关键重击相对均衡；
3. **高手高速交换型**：强调短促、连续 Attack / Defense / Counter / Re-counter；
4. **混合型（默认推荐）**：高速交换 → 重击或环境爆点 → 再进入高速交换。

## 6. 已确认决策四：Action Phrase

新增 **Action Phrase / 动作句 / 连续攻防段**，作为 Combat Choreography Engine 的核心动作编排单位。

V2 层级：

```text
Action–Reaction Pair
→ Action Phrase
→ Battle Beat
→ Combat Sequence
```

职责分层：

- **Action–Reaction Pair**：原子级攻防交互单位；
- **Action Phrase**：多个连续攻防交互组成的一段完整动作句 / 连续攻防段；
- **Battle Beat**：承担一个战术 / 剧情攻防目标；
- **Combat Sequence**：整场动作戏。

Action Phrase 的核心不是固定“几招”，而是：

> **前一个动作自然制造下一个动作的机会。**

可参考但不强制的内部逻辑：

```text
Setup / Entry
→ Attack
→ Defensive Answer
→ Counter
→ Re-counter / Continuation
→ Phrase Payoff
```

禁止把该结构实现成固定六步动作模板。

## 7. 已确认决策五：Combat Character Identity

新增角色级 **Combat Character Identity / 角色战斗身份**。

角色战斗身份至少考虑：

- Combat Preference；
- Movement Signature；
- Attack Character；
- Defense / Counter Character。

这些维度属于动态推导时的判断框架，不是固定标签全集。

关系：

```text
人物设定 / 体型能力 / 性格
+ Combat Intent
+ 当前环境
+ 对手关系
+ Cinematic Choreography Profile
        ↓
动态推导 Combat Character Identity
        ↓
选择适合该角色的 Fighting / Martial Profile
        ↓
Action Phrase 动作编排
```

这用于避免“职业杀手 = Tactical Close Combat = 双方抓腕控制”的同质化结果。

## 8. 已确认决策六：Cinematic Choreography Profile

新增 **Cinematic Choreography Profile / 电影动作编排风格**。

- Combat Character Identity：决定“这个角色自身怎么打”；
- Cinematic Choreography Profile：决定“整场动作戏看起来怎么打”。

基础方向可包含：

- 写实战术型；
- 凌厉电影动作型；
- 高手连续攻防型；
- 重型硬派型；
- 环境技巧型。

允许“主动作编排风格 + 辅助倾向”，但不得堆叠互斥风格。

### 架构落位

该能力 **不进入 `references/styles/` 一级视觉 Style 层**。

- Combat Playbook：负责选择、组合与协调 Choreography Profile；
- `combat-choreography-profiles` Library：提供少量稳定、可复用的电影动作编排基础原型。

## 9. 当前 V2 核心层级

```text
Combat Sequence
└─ Battle Beat
   └─ Action Phrase
      └─ Action–Reaction Pair
```

生成前的上游动作编排变量：

```text
Combat Intent
+ Cinematic Choreography Profile
+ Active Combat Coverage
+ Action Exchange Rhythm
+ Combat Character Identity
+ Environment / Spatial Context
        ↓
Environment Action Affordance
        ↓
Action Phrase Design
        ↓
Signature Moment Planning
        ↓
Battle Beat Design
        ↓
V1 Range / Advantage / Condition / State Contract
        ↓
Camera / Audio Coordination
        ↓
Final Prompt
```

## 10. 已确认决策七：Combat Interactive Mode 专属决策链

Combat Interactive Mode 采用 Combat 专属上游决策链：

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

其中 Choreography Profile 位于 Coverage / Rhythm 之前，因为整场动作编排风格应先决定后续推荐倾向。

Interactive Mode 不机械询问每一项：

- 上游选择主动缩小下游候选范围；
- 每个下游问题给出基于已确认上游条件的推荐；
- 可高置信度推断、且不会明显改变成片的变量自动补全；
- 只有实质改变动作编排、持续交战、角色打法、环境利用、Camera Mode 或最终落点的变量才继续询问；
- 始终一次只问一个最关键问题。

## 11. 已确认决策八：Coverage 四类时间预算

Active Combat Coverage 进一步映射为 Combat Sequence 内部时间预算：

1. **Setup Budget**；
2. **Active Exchange Budget**；
3. **Combat Downtime Budget**；
4. **Ending Budget**。

必须区分 **Active Combat Feedback** 与 **Downtime**：

> 受击反馈、失衡、快速恢复、闪避后重新切入、短暂缠斗、推开后立即追击等，只要直接制造下一次攻防窗口，仍属于 Active Exchange。

对于“15 秒、高手 1v1、High Coverage”的短动作片，可采用内部参考：

- Setup：约 0.5–1.5 秒；
- Active Exchange：约 11–13 秒；
- 累计 Downtime：尽量不超过约 1–2 秒；
- 纯 Ending Pose：约 0.5–1 秒。

以上均为软预算，不是硬秒表。

## 12. 已确认决策九：Exchange Depth

新增 **Exchange Depth / 攻防交换深度**，用于控制一个 Action Phrase 内发生多少层有因果关系的攻防回应。

> **Exchange Depth ≠ Action Verb Count**

它主要由：

- Action Exchange Rhythm；
- Action Phrase 时长；
- Choreography Profile；
- Combat Character Identity；
- Range / Advantage / Condition；
- 环境复杂度；
- Camera Complexity；
- 视频模型可执行性；

共同决定。

参考倾向：

- 重击型：低～中 Depth；
- 均衡型：中等 Depth；
- 高手高速交换型：高 Depth；
- 混合型：在多个 Phrase 间形成高 Depth / 重型 Payoff / 高 Depth 的节奏反差。

“1–2 / 2–3 / 3–5 轮”等只能作为软倾向，不得变成固定模板或硬计数器。

## 13. 已确认决策十：Battle Beat 与 Action Phrase 动态一对多

确认 **Battle Beat : Action Phrase 采用动态一对多关系**，不默认 `1 Beat = 1 Phrase`。

- Phrase 切分服务局部动作组织；
- Beat 切分服务更高层战术状态变化。

Action Phrase 可以在以下情况形成局部结束：

- 当前连续攻防形成局部 Payoff；
- 双方在极短时间内重新建立新攻击窗口；
- 动作路线、Range 或环境利用方式明显改变；
- 高速交换与重型爆点之间需要切换；
- 继续增加动作会明显降低可读性或模型执行性。

Battle Beat 只在更高层状态发生实质变化时切换，例如：

- 战术目标改变；
- Advantage 主要反转；
- 关键 Condition 改变后续打法；
- 主交战对象切换；
- 战斗阶段改变；
- 明确 Turning Event 改变双方关系。

## 14. 已确认决策十一：Combat 中文术语统一

英文专业术语继续保留 `Choreography`；中文正文统一采用：

- **Combat Choreography Engine** → **动作编排引擎 / 动作导演层**；
- **Cinematic Choreography Profile** → **电影动作编排风格**；
- **Action Choreography** → **动作编排**；
- **Action Phrase** → **动作句 / 连续攻防段**。

> **英文保留行业语义，中文优先表达“动作设计与连续攻防编排”。**

## 15. 已确认决策十二：Combat Character Identity 动态推导，不建角色画像库

确认 **不建立 Combat Character Identity 角色画像库，也不建立“杀手 / 军人 / 警察 / 拳手”等职业到固定打法的模板映射**。

原因：角色、职业、年龄、体型、能力、性格和情境组合近乎无限，固定职业模板会重复 V1 中“职业 → 固定打法”的过拟合问题。

Combat Character Identity 定位为 **当前 Combat Sequence 的动态推导结果**，不是 Library 条目。

Library 继续只保存相对稳定、可复用的专业动作知识，例如 Boxing、Muay Thai、Sanda、MMA、Grappling、Tactical Close Combat、传统 Martial Profile、兵器动作知识等。

```text
动态 Combat Character Identity
→ 按需选择 / 混合稳定的 Fighting / Martial / Weapon Profile
→ Action Phrase 动作编排
```

## 16. 已确认决策十三：建立小型 combat-choreography-profiles Library

确认正式新增 **`combat-choreography-profiles` Library**，用于保存少量稳定、可复用的电影动作编排基础原型。

第一版建议只维护约 5–7 个基础 Profile。

每个 Profile 主要描述：

- Active Combat Coverage 推荐倾向；
- Action Exchange Rhythm；
- Exchange Depth；
- 动作重量与受力反馈；
- Range 变化方式；
- 环境利用程度；
- Phrase 节奏组织；
- Camera Complexity 建议；
- 与哪些角色打法或 Combat Intent 容易冲突。

边界：

- 不建设“所有动作电影风格百科”；
- 不因新角色、新职业或单一案例就新增 Profile；
- Profile 必须表达稳定、可复用的动作编排语法差异；
- Playbook 可以动态混合少量辅助倾向；
- 特殊观感允许模型基于基础原型动态扩展。

## 17. 已确认决策十四：Environment Action Affordance

新增 **Environment Action Affordance / 环境动作机会**。

环境不再只作为动作发生后的状态修改器，而要在 Action Phrase 设计之前，动态推导“当前场景能为攻防提供什么动作机会”。

```text
场景对象 / 空间结构 / 障碍关系
→ Environment Action Affordance
→ 结合 Combat Intent / Character Identity / Range / Advantage 过滤
→ 选择真正有战术或视觉价值的环境动作机会
→ Action Phrase 动作编排
→ 更新 Position / Range / Advantage / Condition / Environment State
```

只有当环境利用至少改变以下一项时，才值得进入 Action Phrase：

- 攻击路线；
- 移动路线；
- Range；
- Advantage；
- 角色战术选择；
- Phrase Payoff。

> **V2 Environment Action Affordance 负责“环境可以怎样参与动作设计”；V1 Environment State 负责“环境参与之后状态怎样正确继承”。**

环境利用不得退化成随机踢椅子、扔文件、砸显示器、撞玻璃等装饰性破坏。

## 18. 已确认决策十五：Signature Moment / 标志性动作时刻

正式新增 **Signature Moment / 标志性动作时刻**，作为 Combat Sequence 级的显式动作设计目标。

它解决的问题不是“每个 Phrase 有没有局部结果”，而是：

> **整段动作戏中是否存在一个观众真正容易记住、能代表这场战斗动作设计特色的时刻。**

必须区分：

- **Phrase Payoff**：局部连续攻防段的结果 / 落点；
- **Signature Moment**：整个 Combat Sequence 中少数真正具有记忆度的动作高潮或动作设计节点。

Signature Moment 可以来自：

- 漂亮的 Counter / Re-counter；
- 环境反制；
- 明显的力量差异或重型碰撞；
- 兵器交错；
- 空间与身体轴线变化；
- 主导权瞬间翻转；
- 角色打法差异碰撞出的独特动作结果。

### 默认数量

对于约 15 秒短动作片，默认只追求 **1 个主要 Signature Moment**；必要时可以有 1 个辅助记忆点。

禁止把 Signature Moment 变成“每个 Phrase / Beat 都必须有高潮”的硬要求，否则会导致动作过载和高潮稀释。

### 它不等于慢动作

Signature Moment 不是 Slow Motion 的同义词。正常速度下一个清晰、独特、因果完整的反制，同样可以成为 Signature Moment。

### 与其他模块关系

```text
Choreography Profile
+ Combat Character Identity
+ Environment Action Affordance
+ 当前战术关系
+ Exchange Rhythm / Depth
        ↓
Signature Moment Candidate
        ↓
围绕候选组织前后 Action Phrase
        ↓
Camera 优先保证这一刻的可读性与冲击力
        ↓
V1 State / Continuity 验证因果和状态继承
```

Signature Moment 默认由系统内部规划，不作为 Combat Interactive Mode 的固定追问项；只有用户明确指定某个标志动作、特技或名场面参考时，才直接锁定或进一步询问。

### 经典影视打斗参考方向（候选，待后续确认结构）

可以整理电影 / 电视剧中的经典打斗名场面，抽取其中“为什么这一动作时刻能被记住”的设计模式，作为 Signature Moment 的参考来源。

这里的目标不是复制具体影视动作，而是抽象出可复用的动作设计规律，例如：

- 空间限制如何制造独特反制；
- 环境物体如何参与一次真正有意义的动作转折；
- 强弱差、体型差如何形成动作视觉记忆点；
- Counter / Re-counter 如何形成高潮；
- 兵器、距离、轴线如何制造一个清晰动作画面；
- 节奏如何在 Signature Moment 前后形成对比。

该参考体系是否独立建立 Library、如何分类、记录到什么粒度，继续 Grill Me 后再确认。

## 19. V2 设计原则补充

1. **时间轴写满不代表动作写满。** 必须检查 Active Combat Coverage。
2. **持续交战不代表动作丰富。** 必须检查 Action Exchange Rhythm 与 Action Phrase。
3. **动作合理不代表动作好看。** 动作编排引擎必须负责视觉节奏与动作设计。
4. **高手身份应通过打法表现，而不是只靠人物设定文字。**
5. **不同角色应允许有不同 Combat Character Identity。**
6. **Action Phrase 负责连续动作编排，State Contract 负责连续性。**
7. **High Coverage 不等于全程同速高速动作。**
8. **V2 不通过增加大量 Negative Constraints 解决动作不足问题。**
9. **最终 Prompt 应外显精彩动作，内部状态检查应尽量压缩。**
10. **不因追求可读性而默认把短动作片压缩成少数几次控制动作。**
11. **Interactive Mode 的上游选择必须驱动下游推荐。**
12. **Active Combat Feedback 与 Downtime 必须区分。**
13. **收尾预算服务最后一拍，不应提前终止战斗。**
14. **Exchange Depth 衡量攻防因果深度，不衡量动作词数量。**
15. **不同 Rhythm 应动态改变 Phrase 内部交换深度。**
16. **Phrase 与 Beat 不绑定 1:1。**
17. **Combat 中文术语统一使用“动作编排 / 动作导演”。**
18. **Combat Character Identity 是动态推导结果，不是职业或角色类型画像库。**
19. **Cinematic Choreography Profile 只沉淀少量稳定基础原型。**
20. **环境先作为动作机会参与设计，再由 V1 状态层验证和继承。**
21. **短时长动作片应有少量真正值得记忆的 Signature Moment，而不是所有地方同时高潮。**
22. **经典影视动作参考用于抽象动作设计规律，不用于复制某个作品的完整动作段落。**

## 20. 已确认决策记录

| # | 决策 | 当前结论 |
|---|---|---|
| V2-01 | V2 核心升级方向 | 新增 Combat Choreography Engine；保留 V1 State / Continuity Engine |
| V2-02 | 有效交战时间 | 新增 Active Combat Coverage；Interactive 可选 Low / Medium / High |
| V2-03 | 持续交战内部节奏 | 新增 Action Exchange Rhythm；重击 / 均衡 / 高速交换 / 混合型 |
| V2-04 | 动作编排核心单位 | 新增 Action Phrase，位于 Action–Reaction Pair 与 Battle Beat 之间 |
| V2-05 | 角色打法 | 新增角色级 Combat Character Identity |
| V2-06 | 整场动作观感 | 新增 Cinematic Choreography Profile；不放入一级视觉 Styles |
| V2-07 | Interactive Mode | 建立 Combat 专属决策链；上游选择驱动下游推荐 |
| V2-08 | Coverage 时间预算 | 新增 Setup / Active Exchange / Combat Downtime / Ending 四类预算 |
| V2-09 | Action Phrase 复杂度 | 新增 Exchange Depth；由 Rhythm、Phrase 时长等动态决定 |
| V2-10 | Beat / Phrase 关系 | 动态一对多；Phrase 按局部攻防组织，Beat 按战术状态切换 |
| V2-11 | 中文术语 | 英文保留 Choreography；中文统一“动作编排 / 动作导演” |
| V2-12 | Combat Character Identity 来源 | 不建角色 / 职业画像库；动态推导 |
| V2-13 | Choreography Profile Library | 新增 `combat-choreography-profiles`；少量稳定基础原型 |
| V2-14 | Environment Action Affordance | 环境从被动状态修改器升级为 Action Phrase 前的动态动作机会 |
| V2-15 | Signature Moment | 作为 Combat Sequence 级显式动作设计目标；15 秒默认 1 个主记忆点；经典影视名场面可作为抽象设计参考来源 |

## 21. 尚待继续 Grill Me 的设计树

以下内容尚未确认，必须继续按“一次一个问题”的方式推进：

1. 经典影视打斗 Signature Moment 参考体系是否独立建 Library，以及应按“作品”还是按“动作设计模式”组织；
2. 假动作、预判、诱导、Counter / Re-counter 是否需要形成独立动作编排规则；
3. Combat Density / Coverage / Rhythm 与 Camera Complexity 如何联动；
4. V1 “动作复杂度预算”如何调整，避免 `2–4` 交互节点被过度保守执行；
5. V1 “宁可少而清晰”原则如何重新表述，避免动作预算通缩；
6. Final Prompt 如何减少状态规范语言、提高正向动作编排权重；
7. Combat Quality Regression 如何从静态规则覆盖升级为实际生成质量评价；
8. V2 最终需要修改哪些 Playbook / Library / Contract / Diagnostic，以及是否需要新增 Control。

## 22. 当前阶段结论

V1 的核心问题不是状态连续性设计错误，而是系统在真实生成中表现出明显的“防错强、动作编排弱”倾向。

V2 当前目标可以概括为：

> **在 V1 已经能够“把战斗写对”的基础上，让 Skill 进一步能够“把战斗设计得持续、丰富、有角色差异、具有电影动作编排感，并且拥有真正值得记住的动作时刻”。**

本文件继续作为 V2 Grill Me 的单一设计记录。后续每确认一个关键决策，应同步更新“已确认决策记录”和“尚待继续 Grill Me 的设计树”，直到 V2 设计收口。