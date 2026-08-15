# Action Combat Regression Fix Spec

> 状态：**Confirmed Design + Initial Runtime Implemented / 待 G01 Regression 验证**  
> 日期：2026-08-15  
> 来源：G01 办公室职业杀手 15 秒近身格斗真实 Interactive Regression 及后续 Grill Me 决策  
> 作用：定义本轮 Action Combat 回归修复的设计真源与验收口径。Runtime 首批实现已经落库；下一步必须重新跑同一个 G01，不继续无证据扩设计。

Runtime 实施入口：

- `references/tasks/action-combat-video/interactive-combat-policy.md`
- `references/tasks/action-combat-video/regression-fix-runtime-policy.md`
- `references/libraries/combat-choreography-patterns/minimum-validation-set.md`

当前原则：

> **Routing First, Knowledge Second.**  
> **Regression → Failure Layer → Minimal Fix → Regression Again.**

---

## 0. 本轮问题定位

上一轮真实 G01 已证明：

- Interactive 上游比旧版本明显改善；
- Hybrid Silent Expansion 基本正确；
- Stage-2 最小 Movement / Technique Pattern 已开始进入动作；
- Camera Handoff 基本正常；
- 但仍存在 Recommendation Breadth、Round 2 Candidate Coverage、Archetype Consumption、Archetype → Stage-2 Weighting、Upper-body Dominance、Ending Signature Drift、Granularity Over-expansion、Exchange Density、Concrete Compression、Serialization Duplication 等问题。

当前没有证据支持继续扩完整武术知识库；先修 Runtime 消费链和 Assembly。

---

# A. Interactive / Recommendation

## RF-01 — Hybrid 合法，但不能把题材身份变成单一路线

确认：

- 不禁止 Chinese Cinematic Kung-fu Hybrid 出现在普通中国角色、现代办公室、职业杀手等题材；
- 角色国籍 / 职业 / 场景可以参与推荐相关性；
- 但不能因为“中国人 / 杀手 / 办公室”把第一问过早收敛成一个默认 Combat System；
- 解决方式是 Recommendation Breadth / Diversity，而不是禁止 Hybrid。

---

## RF-02 — Round 1 动态宽候选

Round 1 是整场 Combat Design Space 的第一处分叉，应比后续节点更宽。

```text
当前用户选题
+ Scene / Range / Environment
+ Character Relation / Physical Conditions
+ Viewing Intent
+ 已确认限制
→ 分析真实 Combat Design Space
→ 动态筛选高价值候选
```

常见情况下约 **6～8 个方向 + 自定义**，但这不是硬配额：

- 只有 4～5 个真正合理方向时，不凑数；
- 有 8～9 个真实高价值分叉时，不机械砍到 6 个；
- 数量由当前选题动态决定。

---

## RF-03 — Recommendation Diversity Gate

候选质量看：

```text
Relevance
+ Meaningful Technique Difference
+ Range / Movement Difference
+ Striking / Grappling / Whole-body / Environment 等解决路径差异
+ User Decision Value
```

禁止“数量很多但其实是相近拳种换名字”。

---

## RF-04 — 1v1 默认展示完整 Pairing

1v1 的 Round 1 默认展示：

> **角色 A Combat System vs 角色 B Combat System 的完整对战方向。**

每个候选解释两套体系碰撞后会怎样改变：

- Range；
- Movement；
- Counterplay；
- Pressure / Counter；
- 整体观看体验。

底层仍分别保存：

```text
Character A Combat System
Character B Combat System
```

Pairing 只是 Interactive Presentation，不是新的 System 类型。

---

# B. Round 2 / Expression / Archetype

## RF-05 — Expression 必须有真实候选

Round 2 仍是一个 Primary Planning Node，但内部两个子维度分开展示、分开选择、同轮完成。

Character Combat Expression 不能只给一个“推荐 A”。

如果用户未明确 Expression：

```text
动态生成 2～3 个真正不同的 Expression 组合
+ 自定义
```

差异必须真实改变：

- Initiative；
- Risk；
- Counter / Pressure；
- Re-entry；
- Rhythm。

不新增固定 Round 3。

---

## RF-06 — 五种基础 Archetype 默认完整展示

当 Round 2 暴露 Archetype Selection 时，默认覆盖：

1. 李连杰型；
2. 吴京型；
3. 甄子丹型；
4. 成龙型；
5. 李小龙型；
6. 不指定 / 自定义。

Runtime 可以动态排序和标记推荐，但不能无理由静默删除某一种。

上一轮“李小龙型在 Policy / Library 中存在但实际候选消失”定义为：

> **Archetype Candidate Coverage Failure**

---

## RF-07 — Archetype 是 Character-level 属性

底层按角色保存：

```text
Character A
- Combat System
- Combat Expression
- Cinematic Combat Archetype

Character B
- Combat System
- Combat Expression
- Cinematic Combat Archetype
```

允许：

```text
女方：Hybrid + 冷静后发 + 李连杰型
男方：散打 + 主动压迫 + 吴京型
```

也允许：

```text
双方统一李连杰型
```

不新增固定轮次；Round 2 内完成。

---

# C. Archetype Runtime Consumption

## RF-08 — Archetype Mandatory Consumption Gate

当任一关键角色：

```text
Cinematic Combat Archetype != none
```

进入 Derived Choreography Direction / Stage-2 前必须实际读取：

`references/libraries/combat-cinematic-archetypes/library.md`

链路：

```text
Archetype confirmed
→ Library Read
→ Runtime Bias Extraction
→ Derived Choreography Direction
→ Stage-2
```

如果 Archetype 已确认但对应 Library 没有实际读取：

> **Archetype Consumption Missing**

Final Preflight 不得 PASS。

---

## RF-09 — Archetype-to-Stage-2 Weighting

Archetype 不是只读标签，必须真实改变 Stage-2 Pattern Selection 权重。

例如李连杰型提高：

```text
Footwork
Route Change
Axis Change
Level Change
Kick Integration
Whole-body Linkage
```

并降低长期：

```text
Wrist Control
Forearm / Shoulder-line Dominance
Static Clinch
Static Trading
```

其他 Archetype 按其 Library Runtime Bias 执行。

明确禁止：

- 固定 Combo；
- 固定腿法次数；
- 固定转身 / 换位次数；
- 固定 High / Medium / Low 比例。

Archetype 只改变选择权重，不建立动作配额。

---

## RF-10 — Archetype Realization Gate

Library Read 只是必要条件，不是 PASS。

Final Preflight 必须问：

> **删除明星名称后，只看动作本身，能否读出对应 Archetype 的 Movement / Rhythm / Range / Transition / Impact 偏置？**

如果 Library 已读，但动作仍退化成通用同质骨架：

> **Archetype Realization Failure**

回到 Stage-2 Weighting / Pattern Selection 重写。

---

# D. Character Signature / Ending / Movement

## RF-11 — Per-Character Signature Separation Gate

不同角色已经确认不同：

```text
Combat System
+ Combat Expression
+ Cinematic Combat Archetype
```

则这种差异必须贯穿整场 Combat Spine。

持续检查：

- Entry；
- Movement；
- Technique；
- Range Transition；
- Rhythm；
- Initiative Theft；
- Re-entry。

测试：

> 删除角色姓名，只看动作逻辑，是否仍能大致判断谁是哪种打法？

如果双方后半段同质化，只是轮流使用同一动作骨架：

> **Per-Character Signature Collapse**

---

## RF-12 — Ending Signature Compatibility Gate

Ending / Advantage Recommendation 必须消费：

```text
Combat System
+ Combat Expression
+ Cinematic Combat Archetype
+ Advantage Trajectory / Last Active State
```

Ending 负责定义：

- 谁占优；
- 对方是否仍能反抗；
- 末拍的战术 / 空间状态。

Ending 不得偷偷引入新的 dominant technique。

典型失败：

```text
上游：李连杰型 Footwork / Route / Level / Kick Integration
→ Ending 默认抓腕 + 锁臂 + 压墙
→ 下游全部被腕肘 / 肩线控制吸走
```

失败：

> **Ending Signature Compatibility Failure**

Grappling / Wrestling 角色在符合自身 Signature 时仍可合法使用墙边控制。本 Gate 不禁止 Grappling，只禁止 Ending 偷换打法。

---

## RF-13 — Movement Causality Gate

不能只检查有没有：

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
→ 对手被迫产生新的即时响应
→ 新 State 成为下一 Technique / Defense / Re-entry 原因
```

FAIL：

```text
上肢先完成格挡 / 抓控
→ 同时移动一步
→ 再抓腕
```

如果 Movement 只是给上肢动作配脚步，仍判：

> **Movement Causality Failure / Upper-body Technique Dominance**

---

# E. Stage-2 Traceability

## RF-14 — Stage-2 Pattern Traceability Gate

Regression / Debug 必须能追踪：

```text
Planning / Choreography Gap
→ Slot
→ Main Pattern
→ optional Auxiliary Pattern
→ 实际读取的 leaf knowledge
→ Pattern Detail
→ Concrete Action Phrase
```

普通 Final Prompt 不展示 Trace。

Failure 分流：

```text
无 Pattern Hit
→ Routing Failure

Pattern 不符合 Gap / System / Archetype
→ Selection / Weighting Failure

Pattern 正确但 Phrase 写坏
→ Realization Failure

Choreography 正确但 Prompt 被压坏
→ Assembly / Serialization Failure

Prompt 正确但视频不执行
→ Model / Adapter Failure
```

只出现 `Read: minimum-validation-set.md` 不能证明 Stage-2 成功。

---

# F. Granularity / Exchange Density / Duration

## RF-15 — Granularity Over-expansion

正式识别此前反复出现的问题：

```text
动作具体化增强
→ 普通 Exchange 也被展开成 High-detail
→ 单个 Phrase 吃掉过多信息 / 时间预算
→ 15 秒只剩少量大 Exchange
```

Failure：

> **Granularity Over-expansion**

它与 Granularity Under-specification 是两个相反失败端。

---

## RF-16 — Exchange Density / Granularity Distribution Gate

Final Preflight 检查：

- Active Exchange 是否明显过少；
- 是否大量普通 Exchange 被错误展开成 High；
- High / Medium / Low 是否有真实展开深度差异；
- 是否因为文字细节牺牲 Re-counter / Re-entry / Initiative Handoff；
- 是否再次出现 `High → High → High → Ending`。

语义：

```text
Major Reversal / Initiative Theft / Signature
→ High

Ordinary Exchange / Re-counter / meaningful Range Change
→ Medium

Connector / Recovery / Re-entry
→ Low
```

禁止固定动作数、Phrase 数或比例。

---

## RF-17 — Concrete Compression Gate

Medium / Low 可以更短，但必须仍然具体。

承担 Active Combat 的压缩 Phrase 至少保留足够的：

```text
明确动作
+ 明确对手响应或可见状态后果
+ 必要 Continuation
```

禁止：

```text
掌根或前臂……
某种低线动作……
快速反制……
持续换位……
```

Runtime 必须先决策一个明确动作，不能把 A/B 选择留给视频模型。

原则：

> **更短的动作句，不等于更模糊的动作句。**

---

## RF-18 — Duration-aware Choreography Budget

Duration 在具体 Phrase 展开之前参与 Planning。

```text
Duration
+ Combat Density Intent
+ Active Combat Coverage
+ Dialogue / Story Event 占用
+ Camera Complexity
+ Model Capability（如有）
→ Choreography Information Budget
```

它影响展开深度，但不产生固定动作数量。

对于 15 秒 High Coverage Combat：

> 不能把所有普通 Exchange 都展开为 High；必须给更多真实攻防来回留执行空间。

不是：

> “15 秒必须 8 招 / 6 个 Exchange”。

---

## RF-19 — Two-pass Choreography Planning

### Pass 1 — Exchange Spine / Battle Beat Skeleton

先形成整段轻量 Combat Spine。

只要求清楚：

```text
谁发起
→ 对方如何回应
→ 产生什么新 Contact / Range / Axis / Position / Support / Advantage State
→ 下一 Exchange 为什么可以开始
```

先检查：

- Duration / Coverage；
- Exchange Depth；
- Advantage / Counterplay；
- Per-Character Signature；
- Movement / Range / Position；
- 是否已经只剩少量大动作盒。

### Pass 2 — Selective Stage-2 Expansion

Exchange Spine 成立后，再：

```text
Gap
→ Movement / Technique / Transition Slot
→ Pattern Selection
→ Concrete Action Phrase
→ High / Medium / Low
```

核心原则：

> **先知道这里需要发生什么战斗变化，再选择 Pattern；不能先看到 Pattern，再为了使用它硬塞动作。**

Skeleton 不是新的复杂 Engine，也不是固定模板。

---

# G. Prompt Assembly / Camera

## RF-20 — Serialization Deduplication Gate

Final Prompt 同一个控制意图只保留一次最强表达。

优先级：

```text
具体正向动作
>
必要全局正向规则
>
少量高价值 Negative
```

如果具体动作已经表达：

- 不 Reset；
- Motion Handoff；
- Position / Axis；
- Contact / Weight；

不要在 Continuity / Style / Avoid 中重复解释。

目标：

```text
具体 Action Flow 承担主要语义
+ 少量真正全局 Camera / Physics / Continuity
+ 极少数模型高风险 Avoid
```

目的不是单纯缩短，而是把 Prompt Information Budget 还给真实 Exchange。

---

## RF-21 — Camera Runtime Freeze

本轮 Camera Handoff 没有足够 Failure Evidence，因此：

- 不修改 `action-camera-handoff-playbook.md`；
- 不新增第二套 Camera Runtime；
- Camera 只作为 Regression Preservation 对照层；
- 只有未来视频明确出现 Camera 抢动作、Cut Reset、Viewer Task 丢失或 Adapter / Assembly 丢失 Handoff，才重新开启 Camera 专项修复。

---

# H. Runtime 实施状态

当前首批 Runtime 已完成：

### Interactive Policy

`references/tasks/action-combat-video/interactive-combat-policy.md`

负责：

- RF-01～RF-07；
- Round 2 后 Mandatory Handoff 到 Regression Runtime Policy。

### Regression Runtime Policy

`references/tasks/action-combat-video/regression-fix-runtime-policy.md`

负责：

- RF-08～RF-21 的运行顺序、消费门禁和 Final Preflight additions；
- Camera 只沿用原 Runtime，不重建。

### Stage-2 Minimum Validation Set

`references/libraries/combat-choreography-patterns/minimum-validation-set.md`

已补：

- Pattern Traceability；
- Archetype / Signature Weighting 边界；
- Movement Causality；
- G01 新验收。

### Main Wiring

`SKILL.md` 仍固定读取：

`references/tasks/action-combat-video/interactive-combat-policy.md`

而该 Policy 已强制在 Round 1 / Round 2 后读取：

`references/tasks/action-combat-video/regression-fix-runtime-policy.md`

因此本批 Runtime 已进入 Interactive Action Combat 主链。

---

# I. 下一次 G01 Regression 验收

继续使用同一个 15 秒办公室职业杀手 Golden Scenario。

至少检查：

1. Round 1 是否出现动态、高差异 Pairing 候选；常见约 6～8 但不机械；
2. Hybrid 可以推荐，但不是唯一方向；
3. Round 2 Expression 是否有真实多候选；
4. 李连杰 / 吴京 / 甄子丹 / 成龙 / 李小龙五种是否完整；
5. 角色 Archetype 是否可独立或共享；
6. 选中 Archetype 后 Read List 是否实际出现 Archetype Library；
7. Archetype Bias 是否真实改变 Stage-2 Pattern Selection；
8. Debug 是否能给 `Gap → Slot → Pattern → Detail → Phrase` Trace；
9. Movement 是否真实改变 Route / Axis / Range / Position / Support / Level；
10. 双方 Signature 是否持续可辨识；
11. Ending 是否不再偷换成不兼容的控制模板；
12. 是否先形成 Exchange Spine，再选择性展开；
13. 15 秒是否恢复更多 Active Exchange，而非约 3 个大 Phrase；
14. Medium / Low 是否更短但仍具体；
15. Final Prompt 是否减少 Action / Global Rule / Style / Avoid 重复；
16. Camera Handoff 是否保持当前质量。

---

# J. 当前禁止继续做的事情

在新的 G01 证据出现前，不要：

- 扩完整中国武术百科；
- 建明星独立 Combat Engine；
- 建明星固定 Combo；
- 建 Lower-body Engine；
- 建 Body Method State Machine；
- 建每拳种独立 Runtime Tree；
- 建第二套 Camera Runtime；
- 使用固定腿法 / 换位 / 动作次数；
- 把“常见 6～8 个候选”实现成硬配额；
- 把 Exchange Spine 做成固定模板。

下一步固定为：

> **重新跑 G01 → 看 RF-01～RF-21 是否真实生效 → 只修仍失败的 Layer。**
