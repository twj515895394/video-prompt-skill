# Action Combat Video Prompt Spec V2

> 状态：设计中（Grill Me 持续收敛）
>
> 基线：`docs/action-combat-video-spec.md`
>
> V1 状态：已完成设计、实现与静态回归
>
> V2 定位：在保留 V1 Combat State / Continuity Engine 的基础上，新增并强化 **Combat Choreography Engine（动作导演 / 武术指导层）**，重点解决实测中“有效交战时间不足、动作交换过少、角色打法同质、动作缺乏电影编排感”等问题。

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

因此 V2 不推翻 V1，而是补足 V1 当前较弱的“动作导演 / 武术指导”能力。

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

新增的 Coverage、Rhythm、Identity、Profile、Action Phrase 均属于创作与编排工具，不应被实现为所有场景固定套用的动作模板。

## 3. 已确认决策一：新增 Combat Choreography Engine

确认 V2 的核心不是继续堆叠更多状态连续性规则，而是在 V1 上新增一层正式的 **Combat Choreography Engine**。

该层主要负责：

- 控制整段视频真正处于交战状态的时间比例；
- 控制单位时间内攻防交换的节奏和丰富度；
- 为主要战斗角色建立差异化打法；
- 决定整场动作戏的电影编排观感；
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

正式新增 **Action Phrase / 动作句**，作为 Combat Choreography Engine 的核心编舞单位。

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
- **Action Phrase**：多个连续攻防交互组成的一段完整动作句；
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

角色身份高于具体 Fighting Profile：

```text
Combat Character Identity
→ 选择适合该角色的 Fighting / Martial Profile
→ Action Phrase 编排
```

这用于避免“职业杀手 = Tactical Close Combat = 双方抓腕控制”的同质化结果。

## 8. 已确认决策六：Cinematic Choreography Profile

新增 **Cinematic Choreography Profile / 电影动作编排观感**。

该概念与 Combat Character Identity 明确拆开：

- Combat Character Identity：决定“这个角色自身怎么打”；
- Cinematic Choreography Profile：决定“整场动作戏看起来怎么打”。

候选方向可包含：

- 写实战术型；
- 凌厉电影动作型；
- 高手连续编舞型；
- 重型硬派型；
- 环境技巧型。

允许在需要时采用“主编排观感 + 辅助倾向”，但不得堆叠互斥风格。

### 架构落位确认

该能力 **不进入 `references/styles/` 一级视觉 Style 层**。

原因：现有 Style 继续回答“画面长什么样”，例如 cinematic-live-action、documentary、anime 等；Cinematic Choreography Profile 回答的是“动作怎么被编排”。

当前推荐落位方向：

- Combat Playbook：负责选择与协调 Choreography Profile；
- Combat Library：负责提供可选动作编排画像。

是否最终新增 `combat-choreography-profiles` Library，待后续设计树继续确认。

## 9. 当前 V2 核心层级

当前已确认的建议结构：

```text
Combat Sequence
└─ Battle Beat
   └─ Action Phrase
      └─ Action–Reaction Pair
```

生成前的上游编排变量：

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

其中 **Cinematic Choreography Profile 位于 Coverage / Rhythm 之前**，因为整场编舞观感应先决定后续推荐倾向。例如：

- “高手连续编舞型”通常更适合推荐 High Coverage + 混合型 / 高速交换 Rhythm；
- “重型硬派型”可能更适合 Medium / High Coverage + 重击型或混合型 Rhythm；
- “写实战术型”可以保持较低动作数量，但仍需根据用户的观看目标判断是否需要较高 Active Combat Coverage。

### 上游选择驱动下游推荐

Interactive Mode 不要求机械地把链路中每一项都问一遍。

规则：

- 上游选择应主动缩小下游候选范围；
- 每个下游问题都应给出基于已确认上游条件的推荐；
- 如果某项可以高置信度从已确认信息推断，且不会明显改变成片，则允许自动补全而不追问；
- 只有会实质改变编舞、持续交战、角色打法、环境利用、Camera Mode 或最终落点的变量才继续询问；
- 始终遵守“一次只问一个最关键问题”。

例如用户确认“高手连续编舞型 + High Coverage + 混合型 Rhythm”后，后续 Combat Character Identity 的推荐应主动服务于角色打法差异，而不是重新从全部 Fighting Profile 无差别询问。

该决策链仍服从全局 Interactive Contract：

- 每次只问一个最影响结果的问题；
- 每个问题给出推荐答案；
- 已确认项不重复追问；
- 能推断的低风险内容不追问；
- 用户要求收口时立即生成最终 Prompt。

## 11. V2 设计原则补充

在 V1 原则基础上增加：

1. **时间轴写满不代表动作写满。** 必须检查 Active Combat Coverage。
2. **持续交战不代表动作丰富。** 必须检查 Action Exchange Rhythm 与 Action Phrase。
3. **动作合理不代表动作好看。** Choreography Engine 必须负责视觉节奏与动作设计。
4. **高手身份应通过打法表现，而不是只靠人物设定文字。**
5. **不同角色应允许有不同 Combat Character Identity。**
6. **Action Phrase 负责连续编舞，State Contract 负责连续性，两者不能互相替代。**
7. **High Coverage 不等于全程同速高速动作。** 必须允许节奏反差。
8. **V2 不通过增加大量 Negative Constraints 解决动作不足问题。** 优先增强正向动作编排。
9. **最终 Prompt 应外显精彩动作，内部状态检查应尽量压缩。**
10. **不因追求可读性而默认把短动作片压缩成少数几次控制动作。**
11. **Interactive Mode 的上游选择必须驱动下游推荐，而不是参数问卷式逐项询问。**

## 12. 已确认决策记录

| # | 决策 | 当前结论 |
|---|---|---|
| V2-01 | V2 核心升级方向 | 新增 Combat Choreography Engine；保留 V1 State / Continuity Engine |
| V2-02 | 有效交战时间 | 新增 Active Combat Coverage；Interactive 可选 Low / Medium / High |
| V2-03 | 持续交战内部节奏 | 新增 Action Exchange Rhythm；重击 / 均衡 / 高速交换 / 混合型 |
| V2-04 | 动作编排核心单位 | 新增 Action Phrase，位于 Action–Reaction Pair 与 Battle Beat 之间 |
| V2-05 | 角色打法 | 新增角色级 Combat Character Identity |
| V2-06 | 整场动作观感 | 新增 Cinematic Choreography Profile；不放入一级视觉 Styles |
| V2-07 | Interactive Mode | 建立 Combat 专属决策链；Choreography Profile 位于 Coverage / Rhythm 之前；上游选择驱动下游推荐 |

## 13. 尚待继续 Grill Me 的设计树

以下内容尚未确认，必须继续按“一次一个问题”的方式推进：

1. Active Combat Coverage 如何映射到具体时间预算与收尾预算；
2. 不同 Exchange Rhythm 下，一个 Action Phrase 的默认复杂度与节奏如何动态变化；
3. Action Phrase 与 Battle Beat 的数量关系如何控制，避免再次形成新死模板；
4. Combat Character Identity 是否需要预设画像库，以及画像库应包含哪些维度；
5. Cinematic Choreography Profile 是否正式新增 `combat-choreography-profiles` Library；
6. Environment Interaction 如何升级为 Environment Choreography，而不是仅作为状态修改器；
7. 视觉记忆点 / Signature Moment 是否作为 Choreography Engine 的显式设计目标；
8. 假动作、预判、诱导、Counter / Re-counter 是否需要形成独立编舞规则；
9. Combat Density / Coverage / Rhythm 与 Camera Complexity 如何联动；
10. V1 “动作复杂度预算”如何调整，避免 `2–4` 交互节点被过度保守执行；
11. V1 “宁可少而清晰”原则如何重新表述，避免动作预算通缩；
12. Final Prompt 如何减少状态规范语言、提高正向动作编排权重；
13. Combat Quality Regression 如何从静态规则覆盖升级为实际生成质量评价；
14. V2 最终需要修改哪些 Playbook / Library / Contract / Diagnostic，以及是否需要新增 Control。

## 14. 当前阶段结论

V1 的核心问题不是状态连续性设计错误，而是系统在真实生成中表现出明显的“防错强、编舞弱”倾向。

V2 当前目标可以概括为：

> **在 V1 已经能够“把战斗写对”的基础上，让 Skill 进一步能够“把战斗设计得持续、丰富、有角色差异、具有电影动作编排感”。**

本文件继续作为 V2 Grill Me 的单一设计记录。后续每确认一个关键决策，应同步更新“已确认决策记录”和“尚待继续 Grill Me 的设计树”，直到 V2 设计收口。