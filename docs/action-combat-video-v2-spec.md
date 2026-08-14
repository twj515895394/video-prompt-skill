# Action Combat Video Prompt Spec V2

> 状态：设计中（Grill Me 持续收敛）
>
> 基线：`docs/action-combat-video-spec.md`
>
> V1 状态：已完成设计、实现与静态回归
>
> V2 定位：在保留 V1 Combat State / Continuity Engine 的基础上，新增并强化 **Combat Choreography Engine（动作编排引擎 / 动作导演层）**，重点解决实测中“有效交战时间不足、动作交换过少、角色打法同质、动作缺乏电影动作编排感”等问题。

## 1. 背景与问题来源

V1 已经较完整地解决了复杂打斗 Prompt 中的状态与连续性问题，包括：

- Combat Intent；
- Combat Spatial Map；
- Combat Range State；
- Combat Advantage State；
- Combat Condition State；
- Turning Event；
- Action–Reaction Pair；
- Battle Beat；
- Target Handoff；
- Beat State Contract；
- Action / Camera / Audio 三线协同；
- 打击受力、空间连续、镜头轴线与环境状态继承。

但在真实生成测试中出现了一个新的核心问题：

> **Prompt 的 15 秒时间轴虽然被完整描述，但真正发生持续打斗动作的时间只有约 2–3 秒，且有效攻击 / 防守交换只有两三次。**

典型表现：

- 开场对峙占用过长；
- 大量时间用于抓腕、控制、重新站稳、调整重心等低动态状态；
- 一个 Battle Beat 内缺少足够连续的攻防交换；
- “职业杀手”被过度映射到 Tactical Close Combat，导致动作趋向制服 / 控制，而不是电影化高手对决；
- 双方使用相似动作语言，角色打法缺少可见差异；
- 环境虽然参与状态变化，但没有充分转化为动作编排素材；
- V1 强调“宁少而清晰”，在短时长动作片中可能被过度执行，形成动作预算通缩。

因此 V2 不推翻 V1，而是补足 V1 当前较弱的“动作导演 / 动作编排”能力。

## 2. V1 与 V2 的关系

V1 继续作为底层的 **Combat State / Continuity Engine**：

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
→ Active Combat Coverage
→ Action Exchange Rhythm
→ Combat Character Identity
→ Cinematic Choreography Profile
→ Action Phrase Design
→ Battle Beat
→ V1 Combat State / Continuity Engine
→ Camera / Audio Coordination
→ Final Prompt Compression
```

核心职责拆分：

> **Combat Choreography Engine 负责“打得好不好看”。**
>
> **Combat State / Continuity Engine 负责“打得对不对、接不接得上”。**

V2 必须继续遵守 V1 的上位原则：

> **约束错误，不约束创作。**

新增的 Coverage、Rhythm、Identity、Profile、Action Phrase 均属于创作与动作编排工具，不应被实现为所有场景固定套用的动作模板。

## 3. 已确认决策一：新增 Combat Choreography Engine

确认 V2 的核心不是继续堆叠更多状态连续性规则，而是在 V1 上新增一层正式的 **Combat Choreography Engine（动作编排引擎 / 动作导演层）**。

该层主要负责：

- 控制整段视频真正处于交战状态的时间比例；
- 控制单位时间内攻防交换的节奏和丰富度；
- 为主要战斗角色建立差异化打法；
- 决定整场动作戏的电影动作编排观感；
- 将原子级 Action–Reaction Pair 组织成连续 Action Phrase；
- 生成具有视觉记忆点、节奏变化和环境利用的动作设计；
- 在保证可读性的前提下避免“动作过少”。

该层不负责替代 V1 的 Range / Advantage / Condition / Continuity State。

## 4. 已确认决策二：Active Combat Coverage

新增 **Active Combat Coverage / 有效交战覆盖率**。

它解决的问题不是“时间轴有没有填满”，而是：

> **整段视频有多少有效时长真正处于攻击、防守、闪避、反击、换位、缠斗、追击或其他持续交战状态。**

必须区分：

> Timeline Coverage ≠ Combat Coverage

一个 15 秒 Prompt 即使从 0.0s 写到 15.0s，也可能只有 2–3 秒属于真正的有效交战。

Interactive Mode 下可以让用户选择三档，并同时给出推荐：

### Low｜剧情 / 对峙型

- 约 40–55% 有效交战；
- 更多观察、试探、剧情信息和停顿；
- 适合悬疑、压迫、蓄势型动作戏。

### Medium｜标准电影动作戏

- 约 60–75% 有效交战；
- 建立、交锋、反转、收尾相对均衡。

### High｜持续高手对决

- 约 75–90% 有效交战；
- 开场只保留必要建立；
- 中段绝大多数时间保持持续攻防；
- 最后才进入短暂落点。

对于类似“15 秒、两个职业杀手、办公室近身对决”的短时长高手动作片，默认推荐 **High**。

注意：High Coverage 不等于全片高速挥拳。短暂停顿、僵持、重击反馈和节奏变化允许存在，但不应让角色长时间退出交战状态。

## 5. 已确认决策三：Action Exchange Rhythm

新增 **Action Exchange Rhythm / 攻防交换节奏类型**。

它与 Active Combat Coverage 不同：

- Coverage 决定“有多少时间在打”；
- Exchange Rhythm 决定“持续打斗期间，攻防交换如何组织”。

Interactive Mode 下不使用第二套抽象 Low / Medium / High，而使用用户更容易理解的动作节奏类型：

### 1. 重击型

动作数量较少，但单次交换重量、失衡、碰撞和恢复更明显。

### 2. 均衡型

连续攻防与关键重击相对均衡。

### 3. 高手高速交换型

强调短促、连续的 Attack / Defense / Counter / Re-counter，单位时间交换更多。

### 4. 混合型（默认推荐）

高速交换 → 重击或环境爆点 → 再进入高速交换，通过节奏反差避免全片同速。

对于短时长职业杀手高手对决，默认推荐 **混合型**。

## 6. 已确认决策四：Action Phrase

正式新增 **Action Phrase / 动作句 / 连续攻防段**，作为 Combat Choreography Engine 的核心动作编排单位。

V1 当前主要粒度为：

```text
Action–Reaction Pair
→ Battle Beat
```

V2 调整为：

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

也可以根据场景省略、替换或扩展节点。

禁止把该结构实现成固定六步动作模板。

## 7. 已确认决策五：Combat Character Identity

新增角色级 **Combat Character Identity / 角色战斗身份**。

V1 Fighting Profile 主要回答 Boxing、Muay Thai、Sanda、MMA、Tactical Close Combat 等“动作语言可以是什么”；V2 不再让整场战斗只依赖统一 Profile，而允许主要战斗角色分别拥有自己的打法身份。

角色战斗身份至少考虑：

- **Combat Preference**：主动压迫、反击、控制、保持距离、快速切入等；
- **Movement Signature**：直线压迫、侧向切角、灵活绕位、稳定低重心等；
- **Attack Character**：速度、力量、精准、欺骗、控制等倾向；
- **Defense / Counter Character**：闪避反击、硬格挡、截击、抓控、借力换位等。

这些维度属于动态推导时的判断框架，不是固定标签全集，也不要求把所有角色映射到预设职业模板。

角色身份高于具体 Fighting Profile：

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

该概念与 Combat Character Identity 明确拆开：

- Combat Character Identity：决定“这个角色自身怎么打”；
- Cinematic Choreography Profile：决定“整场动作戏看起来怎么打”。

候选方向可包含：

- 写实战术型；
- 凌厉电影动作型；
- 高手连续编排型；
- 重型硬派型；
- 环境技巧型。

允许在需要时采用“主动作编排风格 + 辅助倾向”，但不得堆叠互斥风格。

### 架构落位确认

该能力 **不进入 `references/styles/` 一级视觉 Style 层**。

原因：现有 Style 继续回答“画面长什么样”，例如 cinematic-live-action、documentary、anime 等；Cinematic Choreography Profile 回答的是“动作怎么被编排”。

当前落位方向：

- Combat Playbook：负责选择、组合与协调 Choreography Profile；
- `combat-choreography-profiles` Library：提供少量稳定、可复用的电影动作编排基础原型。

Library 只负责“有哪些稳定的动作编排语法与倾向”，不替代 Playbook 的动态判断，也不替代角色级 Combat Character Identity。

## 9. 当前 V2 核心层级

当前已确认的建议结构：

```text
Combat Sequence
└─ Battle Beat
   └─ Action Phrase
      └─ Action–Reaction Pair
```

生成前的上游动作编排变量：

```text
Combat Intent
+ Active Combat Coverage
+ Action Exchange Rhythm
+ Combat Character Identity
+ Cinematic Choreography Profile
+ Environment / Spatial Context
        ↓
Action Phrase Design
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

Combat Interactive Mode 不再直接套用通用文生视频的“核心观看目标 → 开场 → 主体动作 → 镜头 → 节拍 → 收尾”顺序，而采用 Combat 专属的上游决策链。

确认顺序：

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

其中 **Cinematic Choreography Profile 位于 Coverage / Rhythm 之前**，因为整场动作编排风格应先决定后续推荐倾向。例如：

- “高手连续编排型”通常更适合推荐 High Coverage + 混合型 / 高速交换 Rhythm；
- “重型硬派型”可能更适合 Medium / High Coverage + 重击型或混合型 Rhythm；
- “写实战术型”可以保持较低动作数量，但仍需根据用户的观看目标判断是否需要较高 Active Combat Coverage。

### 上游选择驱动下游推荐

Interactive Mode 不要求机械地把链路中每一项都问一遍。

规则：

- 上游选择应主动缩小下游候选范围；
- 每个下游问题都应给出基于已确认上游条件的推荐；
- 如果某项可以高置信度从已确认信息推断，且不会明显改变成片，则允许自动补全而不追问；
- 只有会实质改变动作编排、持续交战、角色打法、环境利用、Camera Mode 或最终落点的变量才继续询问；
- 始终遵守“一次只问一个最关键问题”。

例如用户确认“高手连续编排型 + High Coverage + 混合型 Rhythm”后，后续 Combat Character Identity 的推荐应主动服务于角色打法差异，而不是重新从全部 Fighting Profile 无差别询问。

该决策链仍服从全局 Interactive Contract：

- 每次只问一个最影响结果的问题；
- 每个问题给出推荐答案；
- 已确认项不重复追问；
- 能推断的低风险内容不追问；
- 用户要求收口时立即生成最终 Prompt。

## 11. 已确认决策八：Coverage 四类时间预算

Active Combat Coverage 不能只停留在 Low / Medium / High 的总比例，还需要进一步映射为 **Combat Sequence 时间预算结构**。

新增四类内部时间预算：

1. **Setup Budget**：真正开打前用于建立人物、空间、冲突和第一攻击触发点的时间；
2. **Active Exchange Budget**：持续 Attack / Defense / Counter / Re-counter、追击、换位、缠斗和直接服务下一次攻防的反馈过程；
3. **Combat Downtime Budget**：交战过程中暂时退出有效攻防的观察、纯喘息、长僵持、无攻防目的的绕圈或等待；
4. **Ending Budget**：最后收招、结果确认、悬念姿态或自然停止所需时间。

必须区分 **Active Combat Feedback** 与 **Downtime**：

> 受击反馈、失衡、快速恢复、闪避后重新切入、短暂缠斗、推开后立即追击等，只要直接制造下一次攻防窗口，仍属于 Active Exchange，而不是 Downtime。

真正的 Downtime 是双方明显退出当前攻防链、没有直接制造下一动作机会的停顿。

### High Coverage 默认预算倾向

对于类似“15 秒、高手 1v1、High Coverage”的短动作片，可采用以下内部参考，而不是硬秒表：

- Setup：约 0.5–1.5 秒；
- Active Exchange：约 11–13 秒；
- 累计 Combat Downtime：尽量不超过约 1–2 秒，并优先拆散在 Action Phrase 之间；
- 纯 Ending Pose / 静止落点：约 0.5–1 秒。

具体数值必须根据总时长、Choreography Profile、Exchange Rhythm、战斗结果和模型能力动态调整，不得把上述区间实现为固定模板。

### 预算约束原则

- High Coverage 尤其限制过长 Setup；
- Downtime 不能被“电影感”“重新站稳”“互相观察”之类描述无意扩张；
- Ending 不应提前数秒让人物停止交锋；
- 最后一轮 Action Phrase 可以延伸进入 Ending，使“最后一拍才停住”成为默认倾向；
- Coverage 检查必须发生在最终 Prompt 组装前，防止时间轴完整但有效交战不足。

## 12. 已确认决策九：Exchange Depth 动态控制 Action Phrase 复杂度

新增 **Exchange Depth / 攻防交换深度**，用于控制一个 Action Phrase 内部到底发生多少层有因果关系的攻防回应。

Exchange Depth 不统计“招式数量”或动作动词数量，而关注：

> **一次主动发起之后，双方发生了多少层连续的 Defense → Counter → Re-counter → Continuation，以及这些动作是否由前一动作自然制造。**

因此必须明确：

> **Exchange Depth ≠ Action Verb Count**

例如“出拳、踢腿、肘击、膝击、抱摔”并不因为动作名很多就自动形成高 Exchange Depth；如果彼此没有攻防因果，仍然只是招式堆叠。

### 与 Action Exchange Rhythm 的动态映射

Exchange Depth 不独立作为用户必须选择的参数，而主要由 **Action Exchange Rhythm + Action Phrase 可用时长 + Choreography Profile + Combat Character Identity** 自动决定。

#### 重击型

- 默认低～中 Exchange Depth；
- 倾向约 1–2 轮主要攻防回应；
- 将更多时间预算分配给蓄力、重击、环境碰撞、明显失衡、受力和恢复；
- 重点是每次交换有重量，而不是动作数量。

#### 均衡型

- 默认中等 Exchange Depth；
- 倾向约 2–3 轮有明确因果的 Response / Counter；
- 之后进入一个清晰 Phrase Payoff；
- 兼顾连续性、重量和节奏推进。

#### 高手高速交换型

- 默认高 Exchange Depth；
- 倾向约 3–5 轮短促 Attack / Defense / Counter / Re-counter；
- 单次反馈可以更短，但不能删除真实的接触、闪避、受力或空间因果；
- 目标是让高手感来自连续读取对方动作并立刻形成下一层反制，而不是简单提高播放速度。

#### 混合型

混合型不要求一个 Phrase 内同时包含所有节奏，而是在多个 Phrase 之间形成节奏反差，例如：

```text
高 Exchange Depth 的短促连续 Phrase
→ 低 / 中 Depth 的重型 Payoff Phrase
→ 再进入高 Exchange Depth Phrase
```

这种组织方式用于避免全片同速，同时保证短时长动作片仍拥有足够有效交换。

### 软预算原则

以上“1–2 / 2–3 / 3–5 轮”只作为内部动作编排倾向，不得变成固定模板或硬计数器。

实际 Exchange Depth 必须受以下变量共同影响：

- Action Phrase 时长；
- Active Combat Coverage；
- Choreography Profile；
- 角色能力差与 Combat Character Identity；
- 当前 Range / Advantage / Condition；
- 环境复杂度；
- Camera Complexity；
- 视频模型可执行性。

当动作过载时，优先降低单个 Phrase 的 Exchange Depth、缩短支线动作或拆分 Phrase，而不是退回“所有战斗统一 2–4 个动作节点”的全局保守上限。

## 13. 已确认决策十：Battle Beat 与 Action Phrase 动态一对多

确认 **Battle Beat : Action Phrase 采用动态一对多关系**，不默认 `1 Beat = 1 Phrase`，也不规定一个 Beat 必须包含固定数量的 Phrase。

职责边界：

> **Battle Beat 负责一个战术 / 剧情攻防阶段。**
>
> **Action Phrase 负责该阶段内部的一段局部连续攻防。**

只要战术目标和主要攻防关系没有发生实质变化，同一个 Battle Beat 内可以连续存在多个 Action Phrase。

例如：

```text
Battle Beat A：第一次争夺，男方轻度占优
├─ Phrase A1：第一次高速接触
├─ Phrase A2：连续追击与换位
└─ Phrase A3：环境压迫 → Turning Event

Battle Beat B：女方夺回主动
├─ Phrase B1：反制后连续攻防
└─ Phrase B2：扩大空间优势
```

### Action Phrase 的结束条件

一个 Phrase 可以在以下情况形成局部结束：

- 当前连续攻防形成一个局部 Payoff；
- 双方在极短时间内重新建立新的攻击窗口；
- 动作路线、Range 或环境利用方式明显改变；
- 需要从高速交换切换到重型爆点，或反向切换；
- 当前 Phrase 继续增加动作会导致可读性或模型执行风险明显下降。

Phrase 结束不代表战斗暂停，也不代表必须产生 Downtime；下一个 Phrase 可以无缝继续。

### Battle Beat 的结束条件

Battle Beat 只在更高层状态发生实质变化时切换，例如：

- 战术目标改变；
- Advantage 发生主要反转；
- 关键 Condition 改变后续打法；
- 主交战对象切换；
- 战斗阶段从争夺转为追击、脱身、终结等；
- 明确 Turning Event 改变双方关系。

因此：

> **Phrase 切分服务局部动作组织；Beat 切分服务战术状态变化。**

Phrase 数量由 Beat 可用时长、Active Combat Coverage、Exchange Rhythm、Exchange Depth、Turning Event、环境变化、Camera Complexity 和模型执行性共同动态决定。

## 14. 已确认决策十一：Combat 中文术语统一

英文专业术语继续保留 `Choreography`，因为 `Fight Choreography / Action Choreography` 在电影动作设计语境中表示打斗动作的设计、串联、节奏、空间和镜头协同。

但中文正文不再使用容易产生舞蹈语义的“编舞”作为 Combat 的主要翻译，统一采用：

- **Combat Choreography Engine** → **动作编排引擎 / 动作导演层**；
- **Cinematic Choreography Profile** → **电影动作编排风格**；
- **Action Choreography** → **动作编排**；
- **Action Phrase** → **动作句 / 连续攻防段**。

原则：

> **英文保留行业语义，中文优先表达“动作设计与连续攻防编排”，避免让文档读起来像舞蹈设计。**

后续新增 V2 文档内容统一遵守这一中文术语规则。

## 15. 已确认决策十二：Combat Character Identity 动态推导，不建角色画像库

确认 **不建立 Combat Character Identity 角色画像库，也不建立“杀手 / 军人 / 警察 / 拳手”等职业到固定打法的模板映射**。

原因：

- 角色类型、职业、年龄、体型、能力、性格和情境组合近乎无限，预设画像库无法合理覆盖；
- 固定职业模板会再次形成“职业 → 固定打法”的过拟合，重复 V1 中“职业杀手 → Tactical Close Combat”的问题；
- 同一职业的不同人物，本就可能拥有完全不同的动作倾向；
- Combat Character Identity 的价值在于当前场景中的角色差异，而不是人物分类本身。

因此 Combat Character Identity 定位为 **当前 Combat Sequence 的动态推导结果**，不是 Library 条目。

建议推导输入：

```text
人物明确设定
+ 体型 / 能力 / 经验（若已知）
+ 性格与行为倾向（若已知）
+ Combat Intent
+ 当前环境与空间限制
+ 对手的打法与双方差异
+ Cinematic Choreography Profile
+ 当前 Range / Advantage / Condition
        ↓
Combat Character Identity
```

如果用户没有给足人物细节，系统可以为了形成可见打法差异进行低风险补全，但不得把职业标签自动等同于某个固定 Fighting Profile。

### 与 Library 的职责边界

Library 继续只保存相对稳定、可复用的专业动作知识，例如：

- Boxing；
- Muay Thai；
- Sanda；
- MMA；
- Wrestling / Grappling；
- Tactical Close Combat；
- 咏春、八极、太极借力等 Martial Profile；
- 兵器动作画像。

这些 Profile 回答“某类动作语言通常如何工作”，而不是“某个角色必须怎么打”。

因此关系确认如下：

```text
动态 Combat Character Identity
→ 按需选择 / 混合稳定的 Fighting / Martial / Weapon Profile
→ Action Phrase 动作编排
```

## 16. 已确认决策十三：建立小型 combat-choreography-profiles Library

确认正式新增 **`combat-choreography-profiles` Library**，用于保存少量稳定、可复用的电影动作编排基础原型。

该 Library 与 Combat Character Identity 的动态推导不同：

- Combat Character Identity 面向“当前角色怎么打”，不建角色模板库；
- Cinematic Choreography Profile 面向“整场动作戏采用什么动作编排语法”，可以沉淀少量稳定原型。

第一版建议只维护约 5–7 个基础 Profile，例如：

- 写实战术型；
- 凌厉电影动作型；
- 高手连续攻防型；
- 重型硬派型；
- 环境技巧型；
- 其他确有稳定差异、实施阶段验证后值得保留的少量原型。

每个 Profile 应主要描述可复用的动作编排倾向，例如：

- Active Combat Coverage 推荐倾向；
- Action Exchange Rhythm 倾向；
- Exchange Depth 倾向；
- 动作重量与受力反馈强度；
- Range 变化方式；
- 环境利用程度；
- Phrase 节奏组织方式；
- Camera Complexity 建议；
- 与哪些角色打法或 Combat Intent 容易形成冲突。

### 边界原则

- 不建设“所有动作电影风格百科”；
- 不因遇到一个新角色、新职业或单个案例就新增 Profile；
- Profile 必须表达稳定、可复用的动作编排语法差异，而不是仅仅换名字；
- 允许 Playbook 在基础 Profile 上动态混合少量辅助倾向；
- 角色打法仍由 Combat Character Identity 动态推导，不能由 Choreography Profile 取代；
- 用户明确提出特殊动作观感时，允许模型基于基础原型动态扩展，而不是必须先新增 Library 条目。

关系确认如下：

```text
Combat Intent / 用户观看目标
→ Playbook 选择或组合少量 Cinematic Choreography Profile
→ 推荐 Coverage / Rhythm / Exchange Depth / Camera Complexity
→ 与动态 Combat Character Identity 协同
→ Action Phrase 动作编排
```

## 17. V2 设计原则补充

在 V1 原则基础上增加：

1. **时间轴写满不代表动作写满。** 必须检查 Active Combat Coverage。
2. **持续交战不代表动作丰富。** 必须检查 Action Exchange Rhythm 与 Action Phrase。
3. **动作合理不代表动作好看。** Choreography Engine 必须负责视觉节奏与动作设计。
4. **高手身份应通过打法表现，而不是只靠人物设定文字。**
5. **不同角色应允许有不同 Combat Character Identity。**
6. **Action Phrase 负责连续动作编排，State Contract 负责连续性，两者不能互相替代。**
7. **High Coverage 不等于全程同速高速动作。** 必须允许节奏反差。
8. **V2 不通过增加大量 Negative Constraints 解决动作不足问题。** 优先增强正向动作编排。
9. **最终 Prompt 应外显精彩动作，内部状态检查应尽量压缩。**
10. **不因追求可读性而默认把短动作片压缩成少数几次控制动作。**
11. **Interactive Mode 的上游选择必须驱动下游推荐，而不是参数问卷式逐项询问。**
12. **Active Combat Feedback 与 Downtime 必须区分。** 只要反馈直接推动下一次攻防，就仍属于有效交战。
13. **收尾预算服务最后一拍，不应提前终止战斗。**
14. **Exchange Depth 衡量攻防因果深度，不衡量动作词数量。**
15. **不同 Rhythm 应动态改变 Phrase 内部交换深度，而不是统一套一个动作数量上限。**
16. **Phrase 与 Beat 不绑定 1:1。** Phrase 负责局部连续攻防，Beat 负责更高层战术阶段。
17. **Combat 中文术语统一使用“动作编排 / 动作导演”，不再用“编舞”作为主要中文翻译。**
18. **Combat Character Identity 是动态推导结果，不是职业或角色类型画像库。**
19. **Cinematic Choreography Profile 只沉淀少量稳定基础原型，禁止演化为无限扩张的风格百科。**

## 18. 已确认决策记录

| # | 决策 | 当前结论 |
|---|---|---|
| V2-01 | V2 核心升级方向 | 新增 Combat Choreography Engine；保留 V1 State / Continuity Engine |
| V2-02 | 有效交战时间 | 新增 Active Combat Coverage；Interactive 可选 Low / Medium / High |
| V2-03 | 持续交战内部节奏 | 新增 Action Exchange Rhythm；重击 / 均衡 / 高速交换 / 混合型 |
| V2-04 | 动作编排核心单位 | 新增 Action Phrase，位于 Action–Reaction Pair 与 Battle Beat 之间 |
| V2-05 | 角色打法 | 新增角色级 Combat Character Identity |
| V2-06 | 整场动作观感 | 新增 Cinematic Choreography Profile；不放入一级视觉 Styles |
| V2-07 | Interactive Mode | 建立 Combat 专属决策链；Choreography Profile 位于 Coverage / Rhythm 之前；上游选择驱动下游推荐 |
| V2-08 | Coverage 时间预算 | 新增 Setup / Active Exchange / Combat Downtime / Ending 四类预算；High Coverage 限制非交战时间 |
| V2-09 | Action Phrase 复杂度 | 新增 Exchange Depth；由 Rhythm、Phrase 时长等动态决定，不采用固定招式数 |
| V2-10 | Beat / Phrase 关系 | 动态一对多；Phrase 按局部攻防组织，Beat 只在战术状态实质变化时切换 |
| V2-11 | 中文术语 | 英文保留 Choreography；中文统一“动作编排 / 动作导演”，不再使用“编舞”作为主要翻译 |
| V2-12 | Combat Character Identity 来源 | 不建角色 / 职业画像库；根据人物、环境、对手、Intent、状态和动作编排风格动态推导 |
| V2-13 | Choreography Profile Library | 正式新增 `combat-choreography-profiles`；仅维护少量稳定基础原型，Playbook 动态选择 / 组合，不做无限风格百科 |

## 19. 尚待继续 Grill Me 的设计树

以下内容尚未确认，必须继续按“一次一个问题”的方式推进：

1. Environment Interaction 如何升级为 Environment Choreography，而不是仅作为状态修改器；
2. 视觉记忆点 / Signature Moment 是否作为 Choreography Engine 的显式设计目标；
3. 假动作、预判、诱导、Counter / Re-counter 是否需要形成独立动作编排规则；
4. Combat Density / Coverage / Rhythm 与 Camera Complexity 如何联动；
5. V1 “动作复杂度预算”如何调整，避免 `2–4` 交互节点被过度保守执行；
6. V1 “宁可少而清晰”原则如何重新表述，避免动作预算通缩；
7. Final Prompt 如何减少状态规范语言、提高正向动作编排权重；
8. Combat Quality Regression 如何从静态规则覆盖升级为实际生成质量评价；
9. V2 最终需要修改哪些 Playbook / Library / Contract / Diagnostic，以及是否需要新增 Control。

## 20. 当前阶段结论

V1 的核心问题不是状态连续性设计错误，而是系统在真实生成中表现出明显的“防错强、动作编排弱”倾向。

V2 当前目标可以概括为：

> **在 V1 已经能够“把战斗写对”的基础上，让 Skill 进一步能够“把战斗设计得持续、丰富、有角色差异、具有电影动作编排感”。**

本文件继续作为 V2 Grill Me 的单一设计记录。后续每确认一个关键决策，应同步更新“已确认决策记录”和“尚待继续 Grill Me 的设计树”，直到 V2 设计收口。