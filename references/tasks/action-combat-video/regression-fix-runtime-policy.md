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

---

## 10. Exchange Density / Granularity Distribution Gate

正式识别两个相反 Failure：

### 10.1 Granularity Under-specification

```text
快速反制
连续攻击
低线动作
持续换位
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

应由 Runtime 先决策成一个明确可执行动作。

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
9. **Exchange Density**：是否因过度展开只剩少量大动作？
10. **Concrete Compression**：Medium / Low 是否短但仍明确可执行？
11. **Serialization Deduplication**：同一控制语义是否被多段重复？
12. **Camera Preservation**：现有 Action–Camera Handoff 是否未被破坏？

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
- 第二套 Camera Runtime；
- 固定 Skeleton 模板。

本轮目标是修复消费顺序、选择权重、动作密度与序列化，不是增加系统层数。
