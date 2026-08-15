# Action Combat Regression Fix Runtime Policy

> 状态：Runtime Active  
> 来源：`docs/action-combat-video-regression-fix-spec.md`  
> 适用：Action Combat Interactive 在 Round 1 / Round 2 完成后、进入 Derived Choreography Direction / Stage-2 / Final Assembly 之前必须读取。

本文件是本轮 G01 Regression 的轻量运行期修复层。它不建立第二套 Combat Engine，不替代 `core-playbook.md`、`choreography-playbook.md`、`advantage-structure-contract.md`、`action-camera-handoff-playbook.md` 或 `prompt-assembly/control.md`；它负责把已经确认但此前容易在 Runtime 中丢失的消费 / 验收链固定下来。

核心原则：

> **Routing First, Knowledge Second.**
>
> **Plan the whole exchange spine before expanding local detail.**
>
> **Concrete but compressed; rich in exchanges, not rich in redundant explanation.**

---

## 1. 强制运行顺序

Interactive Round 1 / Round 2 完成后，按以下顺序执行：

```text
Confirmed Per-Character Planning Context
→ Archetype Mandatory Consumption
→ Derived Choreography Direction
→ Duration-aware Choreography Budget
→ Pass 1: Exchange Spine / Battle Beat Skeleton
→ Per-Character Signature + Advantage / Ending Compatibility Check
→ Stage-2 Gap Detection
→ Archetype-weighted Pattern Selection
→ Stage-2 Pattern Trace
→ Pass 2: Selective Concrete Expansion
→ Movement Causality Check
→ Concrete Technique Resolution Gate
→ Impact Aftermath / Damage Continuity Gate
→ Granularity / Exchange Density Check
→ Concrete Compression
→ Action–Camera Handoff（沿用现有 Runtime，不修改）
→ Prompt Assembly
→ Serialization Deduplication
→ Final Preflight
```

Camera Runtime 本轮冻结：本文件不得创建第二套 Camera 逻辑，也不得改变现有 Action–Camera Handoff 规则。

---

## 2. Archetype Mandatory Consumption Gate

当任一关键角色满足：

```text
Cinematic Combat Archetype != none
```

必须在 Derived Choreography Direction / Stage-2 前实际读取：

`references/libraries/combat-cinematic-archetypes/library.md`

并提取该角色对应 Archetype 的 Runtime Bias。

禁止：

```text
Planning Context 里保存“李连杰型”
→ 不读 Library
→ 只在 Final Prompt 写“轻灵流畅 / 李连杰式”
```

如果 Archetype 已确认但对应执行知识没有实际读取：

> **Archetype Consumption Missing**

此时不得进入 Final PASS；必须回到 Library Read → Bias Extraction。

### 2.1 Archetype 名称不是最终动作

明星名称只是用户层创作参考。Runtime 应将其转换成中性动作偏置，例如：

```text
李连杰型
→ Footwork / Route / Axis / Level / Kick Integration / Whole-body Linkage ↑

吴京型
→ Explosive Entry / Whole-body Drive / Hard Contact / Base Disruption / Re-entry ↑

甄子丹型
→ Rapid Interception / Burst Footwork / Range Transition / Close-range Chain ↑

成龙型
→ Environment Affordance / Route / Recovery / Obstacle Traversal ↑

李小龙型
→ Stop-hit / Broken Rhythm / Explosive Entry / Exit / Range Control ↑
```

具体真源以 Archetype Library 当前内容为准，不在本文件重复建立明星动作库。

---

## 3. Archetype-to-Stage-2 Weighting Gate

Archetype 必须真实改变 Stage-2 Pattern Selection 的选择权重，而不是只改变形容词。

执行：

```text
Per-Character Combat System
+ System / Hybrid Refinement
+ Combat Expression
+ Archetype Runtime Bias
+ Current State / Range / Contact / Environment
+ 当前 Gap
→ Pattern Selection Priority
```

Archetype 只改变：

- Movement Pattern 的优先级；
- Technique 类型与连接方式的优先级；
- Transition / Re-entry 的优先级；
- Rhythm / Range / Environment / Impact 的偏置。

禁止：

- 固定 Combo；
- 每 3 招必须 1 脚；
- 固定转身次数；
- 固定换位次数；
- 固定 High / Medium / Low 比例；
- 为了“像某明星”无视 Combat System 或当前 State。

### 3.1 Archetype Realization Gate

Library Read Evidence 只是必要条件，不是 PASS 条件。

Final Preflight 必须问：

> **删除明星名称后，仅看最终动作本身，能否读出该 Archetype 对 Movement / Rhythm / Range / Transition / Impact 的真实偏置？**

如果 Library 已读取，但最后仍落成通用的：

```text
前臂偏转
→ 肩线封堵
→ 抓腕
→ 顶肩 / 压墙
```

且所选 Archetype 明显要求更强 Footwork / Range / Route / Whole-body 变化，则判：

> **Archetype Realization Failure**

回到 Stage-2 Weighting + Pattern Selection 重写，不在旧动作上补几个风格词。

---

## 4. Per-Character Signature Separation Gate

只要关键角色之间的：

```text
Combat System
+ Combat Expression
+ Cinematic Combat Archetype
```

存在已确认差异，该差异必须贯穿 Combat Spine，而不是只在开头出现一次。

持续检查：

- Entry 方式；
- Movement 偏好；
- Technique 选择；
- Range Transition；
- Rhythm；
- Initiative Theft；
- 失去主动后的 Re-entry；
- 对 Contact / Pressure 的处理方式。

测试问题：

> **删除角色姓名，只看动作逻辑，是否仍能大致判断哪一方是哪一种打法？**

如果双方后半段同质化成同一动作骨架，只是轮流执行：

> **Per-Character Signature Collapse**

必须回到 Exchange Spine / Stage-2 Selection 修复，而不是靠角色形容词区分。

---

## 5. Ending Signature Compatibility Gate

Ending / Advantage Recommendation 必须消费：

```text
Per-Character Combat System
+ Combat Expression
+ Cinematic Combat Archetype
+ Advantage Trajectory / Current Active State
```

Ending 负责定义：

- 最终谁取得什么程度优势；
- 对手是否仍能反抗；
- 末拍处于什么战术 / 空间状态。

Ending 不得为了表达“谁占优”而偷偷引入新的 dominant technique。

典型失败：

```text
上游：轻灵 Footwork / Route / Level / Kick Integration
→ Ending 推荐：默认抓腕 + 锁臂 + 压墙
→ 下游全部被腕肘 / 肩线控制吸走
```

如果 Ending 的 dominant technique 明显破坏已确认 Signature：

> **Ending Signature Compatibility Failure**

重新生成 Ending candidate 或让最后一个 Active State 自然收束。

Grappling / Wrestling / Control-oriented System 在符合自身 Signature 时仍可合法使用墙边身体控制；本 Gate 不禁止 Grappling，只禁止 Ending 偷换打法。

---

## 6. Duration-aware Choreography Budget

Duration 必须在具体 Action Phrase 展开之前参与规划，不能到 Final Assembly 才考虑。

运行输入：

```text
Duration
+ Combat Density Intent
+ Active Combat Coverage
+ Dialogue / Story Event 占用
+ Camera Complexity
+ Model Capability（如有）
→ Choreography Information Budget
```

它影响：

- Exchange Spine 能承载多少阶段变化；
- 哪些节点值得 High Granularity；
- 普通 Exchange 应保持多深；
- 给 Re-counter / Re-entry / Initiative Handoff 留多少执行空间。

它不产生：

- 固定动作数；
- 固定 Exchange 数；
- 固定腿法次数；
- 固定转身 / 换位次数。

例如 15 秒 High Coverage Combat 的意义是：

> **不能让所有普通 Exchange 都膨胀成 High-detail；需要给更多真实攻防来回留执行空间。**

而不是：

> “15 秒必须 8 招 / 6 个 Exchange”。

---

## 7. Two-pass Choreography Planning

### Pass 1 — Exchange Spine / Battle Beat Skeleton

在读取大量局部 Pattern 并展开细节之前，先形成一条轻量完整的 Combat Spine。

结构可以包含：

```text
Entry
→ Exchange
→ Re-counter
→ Initiative Shift
→ Exchange
→ Signature / Reversal
→ Ending
```

但这不是固定模板，也不要求固定节点数量。

Pass 1 只需要清楚：

```text
谁发起
→ 对方怎样回应
→ 产生什么新的 Contact / Range / Axis / Position / Support / Advantage State
→ 下一 Exchange 为什么可以从这里开始
```

Pass 1 必须先检查：

- Duration / Active Combat Coverage；
- Exchange Depth；
- Advantage / Counterplay；
- Per-Character Signature Separation；
- Route / Range / Position / Level / Support 是否有真实变化；
- 是否已经在骨架阶段就压成少数几个大动作盒。

原则：

> **先确定整段战斗需要发生什么变化，再决定调用什么 Pattern。**

禁止：

```text
先读到 M01 / T02
→ 为了“用上知识库”硬塞斜切 / 低线动作
```

### Pass 2 — Selective Stage-2 Expansion

Exchange Spine 成立后，再逐个检查真正需要专业具体化的 Gap：

```text
Gap
→ Movement / Technique / Transition Slot
→ Pattern Selection
→ Concrete Action Phrase
→ Granularity Level
```

优先：

```text
Major Reversal / Initiative Theft / Signature Moment
→ High Granularity

Ordinary Exchange / Re-counter / meaningful Range Change
→ Medium Granularity

Connector / Recovery / Re-entry Transition
→ Low Granularity
```

High 不是“越长越好”；只是承担更完整的关键因果。

---

## 8. Stage-2 Pattern Traceability Gate

Regression / Debug 时，每个被 Stage-2 实例化的关键 Exchange 必须可追踪：

```text
Planning / Choreography Gap
→ Slot
→ Main Pattern
→ optional Auxiliary Pattern
→ 实际读取的 leaf knowledge
→ Pattern 提供的关键 Detail
→ Concrete Action Phrase
```

示意：

```text
Gap:
正面对线过于静态，需要创造 Route / Axis 变化

Slot:
Movement

Main Pattern:
M01 Outside Angle Cut

Auxiliary:
T02 Low-line Base Disruption

Realized Phrase:
女方向男方外侧斜切……
```

普通最终 Prompt 不输出 Trace；Trace 是 Runtime / Regression Evidence。

Failure 分流：

```text
没有 Pattern Hit
→ Routing Failure

Pattern Hit 不符合 Archetype / System / Gap
→ Selection / Weighting Failure

Pattern 正确但 Phrase 写坏
→ Realization Failure

Choreography 正确但最终 Prompt 被压坏
→ Assembly / Serialization Failure

Prompt 正确但生成视频不执行
→ Model / Adapter Failure
```

如果只读了 `minimum-validation-set.md`，但无法指出具体 Pattern Hit 与 Realized Phrase，不得判 Stage-2 已成功执行。

---

## 9. Movement Causality Gate

不能仅检查最终 Prompt 是否出现：

- 侧切；
- 转轴；
- 沉身；
- 高低位；
- 步法；
- 支撑转换。

必须检查：

> **Movement 是否改变了战斗问题？**

PASS：

```text
Movement
→ 改变 Route / Axis / Range / Position / Support / Balance / Level
→ 对手被迫重新响应
→ 新 State 成为下一 Technique / Defense / Re-entry 原因
```

FAIL：

```text
上肢先完成主要格挡 / 抓控
→ 旁边补一句“同时移动一步”
→ 主链仍然是挡拳 → 抓腕 → 压肩
```

即使 Movement Pattern 已命中，如果 Movement 只是给上肢 Technique 配脚步，仍判：

> **Upper-body Technique Dominance / Movement Causality Failure**

必须重写因果链，而不是增加 Movement 关键词。

### 9.1 Concrete Technique Resolution Gate

Stage-2 的 Pattern / Technique 名称是**动作生成知识**，不是可直接交给视频模型的最终招式。Pattern 命中后，承担 Active Combat 的 Technique 必须继续实例化成一个当前 Exchange 中真实发生的具体身体动作。

特别禁止把下列类别词直接当作动作 Head：

```text
全身连动短击
全身连动反击
短促身体控制
低线腿法 / 低线动作
破平衡动作
近身反制
用身体改变朝向
用全身力量截入
```

这些词可以作为内部 intent / mechanic / modifier，但不能替代“人物到底做了什么”。

#### Head-action Test

对每个承担关键攻防的 Phrase，临时删除以下类型的修饰 / 结果词：

```text
快速 / 短促 / 连续 / 全身连动 / 低线 / 强力
反制 / 控制 / 破平衡 / 改变路线 / 改变朝向 / 借动量
```

然后问：

> **剩下的文字能否回答：哪个身体部位 / 接触面，对哪个可见目标或身体关系，执行了什么具体动作？**

如果不能，判：

> **Technique Category Leakage / Abstract Action Head**

必须回到当前 System + State + Range + Pattern Detail，选定一个具体动作，不得靠增加更多形容词修复。

#### 最小可执行语义

普通 Active Technique 至少应形成：

```text
一个具体动作
+ 一个明确接触面 / 身体关系（上下文已极清楚时可自然省略）
+ 一个明确目标 / 接触对象
+ 一个立即可见的对手响应或状态后果
```

例如：

```text
FAIL：女方用低线腿法扰乱男方支撑脚。
PASS：女方用前脚内侧勾扫男方承重脚外侧，迫使他跨步补位。

FAIL：女方以短促的全身连动截入改变他的路线。
PASS：女方斜切半步后用掌根推击男方上胸，男方肩线被推偏并跨步转向。

FAIL：女方用短促身体控制改变男方朝向。
PASS：女方以前臂横架男方胸口，外侧跨步带转，使他的肩线转向门框。
```

这里不要求使用专业招式名。**清楚的普通身体语言优先于含糊的武术术语。**

#### 防止反向过度展开

Concrete 不等于把每个动作都写成生物力学说明书：

- High Granularity 关键反转可以补必要 Footwork / Axis / Support / Force Chain；
- Medium 只需一个具体 Technique + 对手响应 / 状态后果；
- Low Connector 可以只保留明确动作与 Continuation Entry；
- 不为了通过本 Gate，把每个普通 Exchange 都补齐脚、髋、肩、受力、恢复全过程。

因此本 Gate 与 `Granularity Over-expansion` 同时生效：

> **先把“做什么”说具体，再按 Granularity 决定“解释多少”。**

### 9.2 Impact Aftermath / Damage Continuity Gate

当 Concrete Action 中已经发生**有效打击、抓扯、摔撞、压迫、拖拽或环境碰撞**时，Runtime 不能只描述即时运动反应，还必须判断该接触是否会留下后续镜头可见的 **Aftermath State**。

本 Gate 覆盖三类可见对象：

```text
Human / Body
+ Clothing / Wearables
+ Environment / Objects / Materials
```

核心链路：

```text
Effective Contact / Force Event
→ Immediate Physical Response
→ plausible Visible State / Appearance Change
→ Persistent Continuity in later shots
→ optional escalation only if later force justifies it
```

#### A. Human / Body Aftermath

当明确受击部位、力度与写实尺度足以产生可见痕迹时，应选择**一个与当前 Physical Presentation Domain 相匹配的最小合理后果**，例如：

- 嘴角 / 唇部受到有效拳掌擦击 → 发红、轻微破皮或少量血迹；
- 额头 / 眉骨 / 脸颊受到明确撞击 → 局部泛红、擦伤或逐渐显现的轻度紫红淤痕；
- 前臂 / 手背 / 膝部与墙面、地面发生明显摩擦或撞击 → 局部红印、擦痕或轻微磨伤。

不是每次触碰都必须留下伤痕。轻微封挡、擦碰、无明显承伤的 Contact 可以只有运动 / 受力反馈；**只有动作本身已经被描述为有效命中、重撞或持续压迫时，才检查持久可见后果。**

#### B. Clothing / Wearable Aftermath

抓袖、扯领、抱控、拖拽、墙压或摔撞如果明显作用到服装 / 穿戴物，后果应服从力度与材质：

```text
轻度
→ 褶皱 / 拉紧 / 歪斜 / 衣摆移位 / 领带松动

中度持续或强力抓扯
→ 明显拉伸 / 局部开线 / 小裂口 / 纽扣松脱或崩开（上下文合理时）
```

禁止：

```text
一次普通抓袖
→ 衣服立刻大面积撕烂
```

也禁止：

```text
衣袖已经被强力扯裂
→ 下一镜头自动恢复完整
```

#### C. Environment / Object / Material Aftermath

人物撞击、推压、甩碰环境物体时，必须按对象真实材质决定反馈，而不是统一“破坏”：

- 玻璃隔断：可先出现振动、轻响、手印 / 擦痕或轻微形变感；只有足够强且剧情 / Physical Scale 允许时才升级到裂纹 / 破裂；
- 墙面 / 门框：可出现擦痕、轻微掉灰、局部撞痕；普通人体撞击不自动形成夸张大坑；
- 办公椅 / 小型家具：可滑移、偏转、翻倒并保持新位置；不应无重量飞出；
- 文件 / 纸张 / 小物：可散落、掉地、位置改变，并在后续镜头保留；
- 衣物、玻璃、墙面、家具等的反馈必须符合当前材质和受力方向。

#### Default Aftermath Intensity

用户没有另外指定时，默认：

> **轻到中度电影化写实后果。**

目标是让观众看见“这场战斗留下了代价”，但不自动升级为：

- 大量喷血；
- 严重开放性伤口；
- 夸张面部变形；
- 大面积破衣；
- 玻璃 / 墙体 / 家具无理由大规模毁坏。

如果用户明确要求更轻、更重、更血腥或更破坏性的风格，再按用户目标调整；不得由 Runtime 自行升级。

#### Persistence / Accumulation Contract

一旦某个可见 Aftermath 已经进入画面，它必须成为后续 Continuity State：

```text
嘴角已有少量血迹
→ 后续仍保持，除非画面内明确擦除 / 清理

额角已出现红肿 / 淤痕
→ 后续保持，并可随时间 / 再次受击合理加深

领带已松、衣袖已裂
→ 后续继续保持松动 / 裂口

椅子已被撞开、纸张已散落
→ 后续保持新的环境状态
```

禁止：

> **Damage / Material / Environment Reset**

即：没有画面内原因，伤痕、衣物破损、物体位移或环境损伤在下一镜头自动消失 / 恢复初始状态。

后果只能：

```text
保持
→ 被后续动作合理加重
→ 或被明确的画面内行为改变
```

不能无因重置。

#### Aftermath Information Budget

本 Gate 不要求每个 Exchange 都追加一串伤痕说明。只把**当前已经具有可见持续价值**的后果写入最接近的 Action Phrase 或必要 Continuity 描述：

- 对当前镜头只是瞬时、低价值且后续不可见的轻微反馈，可以不展开；
- 对后续画面会持续出现、能强化真实感或影响表演 / 环境状态的后果，应简洁保留；
- 同一伤痕 / 破损 / 环境变化后续只需保持，不在每个段落重新解释来源；
- 不为了“更真实”给每次击打机械添加一种新伤痕。

本 Gate 与 `Granularity Over-expansion` / `Serialization Deduplication` 同时生效：

> **后果要真实存在，但描述只写到足以让模型保持它。**

Failure 可判：

- `Impact Aftermath Missing`：明显有效受创 / 抓扯 / 撞击却完全没有合理可见反馈；
- `Damage Continuity Reset`：已出现的伤痕 / 衣物损伤在后续无因消失；
- `Environment State Reset`：已移动 / 受损物体无因恢复；
- `Material Response Mismatch`：反馈与材质 / 力度明显不符；
- `Aftermath Overstatement`：轻度接触被自动升级成重伤 / 大破坏。

---

## 10. Exchange Density / Granularity Distribution Gate

正式识别两个相反 Failure：

### 10.1 Granularity Under-specification

```text
快速反制
连续攻击
低线动作
持续换位
全身连动短击
短促身体控制
```

如果删除抽象形容词后仍不知道人物具体做了什么，Phrase 不可执行。

### 10.2 Granularity Over-expansion

```text
动作具体化增强
→ 每个普通 Exchange 都展开脚步、髋、肩轴、受力、恢复等全部细节
→ 单个 Phrase 吃掉过多信息 / 执行预算
→ 15 秒只剩少量大 Exchange
```

判：

> **Granularity Over-expansion**

Final Preflight 检查：

- Active Exchange 是否明显过少；
- 普通 Exchange 是否被错误展开为 High；
- High / Medium / Low 是否有真实展开深度差异；
- 是否因为文字细节而牺牲 Re-counter / Re-entry / Initiative Handoff；
- 是否出现 `High → High → High → Ending` 的结构塌缩。

禁止通过固定动作数 / 固定比例解决。

---

## 11. Concrete Compression Gate

Medium / Low Phrase 可以更短，但不能重新模糊。

承担 Active Combat 的压缩 Phrase 至少保留当前必要组合：

```text
明确动作
+ 明确对手响应或可见状态后果
+ 必要 Continuation Entry
```

禁止给视频模型未决选择：

```text
掌根或前臂……
踢 / 扫 / 蹬其中一种……
某种低线动作……
```

也禁止把已经收敛的 Technique 再压回动作类别：

```text
全身连动短击……
短促身体控制……
低线腿法扰乱……
破平衡反制……
用身体改变朝向……
```

应由 Runtime 先决策成一个明确可执行动作；压缩时可以删掉次要 Mechanics，但不能删掉动作 Head、目标和关键状态后果。

原则：

> **更短的动作句，不等于更模糊的动作句。**

---

## 12. Serialization Deduplication Gate

Prompt Assembly 后执行一次语义去重。

同一个控制意图优先只保留一次最强表达：

```text
具体正向动作
>
必要全局正向规则
>
少量高价值 Negative
```

如果具体动作已经自然表达：

- 不 Reset；
- Motion Handoff；
- Position / Axis 变化；
- 接触受力；
- 已形成的 Injury / Clothing / Environment Aftermath；

不要在后面的 Continuity / Style / Avoid 段再重复解释同一件事。

目标：

```text
具体 Action Flow 承担主要语义
+ 少量真正全局 Camera / Physics / Continuity
+ 极少数模型高风险 Avoid
```

禁止：

```text
动作写一遍
+ 全局规则再解释
+ Style 再解释
+ Avoid 反向再解释
```

Dedup 的目的不是单纯缩短，而是把 Prompt Information Budget 还给真实 Exchange。

---

## 13. Camera Runtime Freeze

本轮真实 Regression 暂未出现足够证据要求重构 Camera。

因此：

- 不修改 `action-camera-handoff-playbook.md`；
- 不新增 Camera Engine；
- 保持现有 Action-triggered Camera Handoff；
- 只在最终 Regression 检查其他修复是否破坏 Camera。

未来只有在 Generated-video Regression 明确出现：

- Camera 抢动作；
- Cut 造成 Motion Reset；
- Viewer Task 丢失；
- Adapter / Assembly 丢失 Camera Handoff；

才重新开启 Camera 专项修复。

---

## 14. Combat Final Preflight Additions

在现有 Final Preflight 基础上追加检查：

1. **Archetype Consumption**：有 Archetype 的角色是否真的读取了 Library？
2. **Archetype Realization**：动作本身是否能读出其 Runtime Bias？
3. **Per-Character Signature Separation**：双方打法是否持续可辨识？
4. **Ending Signature Compatibility**：Ending 是否偷换 dominant technique？
5. **Movement Causality**：Movement 是否真的制造下一战斗状态？
6. **Stage-2 Traceability**：Regression / Debug 是否存在 Gap → Slot → Pattern → Phrase 证据？
7. **Duration-aware Planning**：是否先考虑时长与 Active Coverage，再展开细节？
8. **Exchange Spine**：是否先有完整轻量 Combat Spine，再做局部 High-detail？
9. **Concrete Technique Resolution**：关键 Technique 是否已经从 Pattern / 类别词实例化成具体动作，是否仍出现 `全身连动短击 / 短促身体控制 / 低线腿法` 等 Abstract Action Head？
10. **Impact Aftermath / Damage Continuity**：明显有效的受击、抓扯、摔撞或环境碰撞是否产生了与部位、力度、材质和 Physical Presentation 相匹配的最小合理可见后果；已出现的人体伤痕、衣物状态、环境位移 / 损伤是否在后续保持，是否存在无因 Reset 或过度升级？
11. **Exchange Density**：是否因过度展开只剩少量大动作？
12. **Concrete Compression**：Medium / Low 是否短但仍明确可执行？
13. **Serialization Deduplication**：同一控制语义是否被多段重复？
14. **Camera Preservation**：现有 Action–Camera Handoff 是否未被破坏？

如果任何关键 Gate 失败，优先回到对应 Failure Layer 修复；不要第一反应扩知识库。

---

## 15. Anti-overdesign

本文件禁止演化为：

- 新 Combat State Machine；
- Lower-body Engine；
- Body Method Engine；
- 明星独立 Combat Engine；
- 固定 Combo Library；
- 固定动作数 / Exchange 数；
- 固定腿法 / 换位次数；
- 固定受伤数量 / 固定流血次数 / 每击必留伤；
- 固定衣物破损或环境破坏配额；
- 第二套 Camera Runtime；
- 固定 Skeleton 模板。

本轮目标是修复消费顺序、选择权重、动作密度、可见后果连续性与序列化，不是增加系统层数。
