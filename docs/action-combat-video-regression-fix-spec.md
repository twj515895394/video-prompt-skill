# Action Combat Regression Fix Spec

> 状态：Confirmed Design / Runtime Not Yet Implemented  
> 日期：2026-08-15  
> 来源：G01 办公室职业杀手 15 秒近身格斗真实 Interactive Regression 及后续 Grill Me 决策  
> 作用：记录本轮已确认的 Action Combat 回归修复设计。该文档先作为本批修复的 Spec 真源；在本批 Grill 收口前，不直接修改 Camera Runtime，不先扩武术知识库。

---

## 0. 本轮定位

本轮真实回归已经证明：

- Interactive 上游已比旧版本明显改善；
- Hybrid UX 已基本正确；
- Stage-2 最小 Movement / Technique Pattern 已开始进入最终动作；
- 但仍存在 Recommendation Breadth、Round 2 Candidate Coverage、Archetype Consumption、Archetype → Stage-2 Weighting、Upper-body Dominance、Granularity Over-expansion、Exchange Density、Serialization Duplication 等问题；
- Camera Handoff 本轮暂未出现足够证据要求重构，因此冻结 Camera Runtime，仅做回归保护。

本轮继续遵守：

> **Routing First, Knowledge Second.**
>
> **先证明 Runtime 是否消费正确，再决定是否扩 Knowledge。**

当前没有证据支持继续扩完整武术知识库。

---

## 1. Round 1 Recommendation Breadth / 第一问推荐宽度

### RF-01 — 不禁止 Chinese Cinematic Kung-fu Hybrid 出现在普通中国角色场景

确认：

- 不增加“只有明确 Chinese cinematic intent 才允许出现 Hybrid”的禁止规则；
- 中国角色、现代办公室、职业杀手等信息可以参与推荐相关性判断；
- 但 Runtime 不应因为这些身份信息过早把第一问收敛成单一路线；
- 问题的核心是 Recommendation Breadth / Diversity，而不是禁止 Hybrid。

### RF-02 — Round 1 默认提供更多高价值方向

Round 1 是整场战斗设计的第一处分叉，默认应比后续节点更宽。

```text
当前用户选题 / 场景 / Range / 人物关系 / 观看目标 / 已确认条件
→ 分析真实 Combat Design Space
→ 生成高价值且差异明显的候选
→ 常见情况下约 6～8 个方向
→ + 自定义
```

“约 6～8 个”只是常规经验目标，不是硬配额：

- 真正只有 4～5 个合理方向时，不为了凑数加入低价值候选；
- 存在 8～9 个高价值明显分叉时，也不机械砍到 6 个；
- Runtime 必须动态分析用户选题后决定候选数量。

### RF-03 — Recommendation Diversity Gate

候选质量检查重点不是数量，而是：

```text
Relevance
+ Meaningful Technique Difference
+ Range / Movement Difference
+ Grappling / Striking / Whole-body / Environment 等解决路径差异
+ User Decision Value
```

禁止表面给很多选项，实际只是相近拳种或相近现代站立打法换名字。

### RF-04 — 1v1 默认展示完整对战组合方案

对于 1v1：

```text
Interactive 展示层
→ 默认给“角色 A Combat System vs 角色 B Combat System”的完整 Pairing 方案
→ 每个方案解释两种体系碰撞后产生的战斗结构和观看体验
```

而不是让用户分别面对两个长列表各选一次。

底层数据仍保持：

```text
Character A Combat System
Character B Combat System
```

Pairing 只是 Interactive Presentation，不是新的 Combat System 类型。

---

## 2. Round 2 Double Sub-dimension / 双子维度修复

### RF-05 — Character Combat Expression 必须有真实候选分叉

当前 Round 2 虽然形式上同时展示 Expression + Archetype，但 Expression 不能只给一个推荐 A，让用户实际只能选择 Archetype。

确认：

- Character Combat Expression 提供 2～3 个真正不同的动态组合 + 自定义；
- 推荐项可以标注“推荐”，但不能成为唯一可选 Expression；
- Expression 与 Archetype 同轮完成；
- 不新增固定 Round 3。

典型交互可以是：

```text
Character Combat Expression
A. 推荐：女方冷静诱导 / 后发反制；男方主动压迫 / 持续再进入
B. 女方主动抢先；男方沉稳反击
C. 双方克制试探后突然爆发
D. 自定义

Cinematic Combat Archetype
1. 李连杰型
2. 吴京型
3. 甄子丹型
4. 成龙型
5. 李小龙型
6. 不指定 / 自定义
```

用户可一次回复 `A + 李连杰型` 等。

### RF-06 — 五种基础 Archetype 默认完整展示

当 Round 2 需要暴露 Cinematic Combat Archetype Selection 时：

基础候选固定覆盖：

1. 李连杰型
2. 吴京型
3. 甄子丹型
4. 成龙型
5. 李小龙型
6. 不指定 / 自定义

Runtime 可以：

- 动态排序；
- 标记推荐；
- 根据上下文解释不同适配度。

Runtime 不可以：

- 在无明确高价值原因时静默删掉某一种基础 Archetype；
- 再次出现本轮回归中“李小龙型在 Policy / Library 中存在，但实际选项消失”的情况。

Failure：

> **Archetype Candidate Coverage Failure**

---

## 3. Character-level Cinematic Combat Archetype

### RF-07 — Archetype 保持 Character-level 属性

底层 Planning Context 应按角色保存：

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

Interactive 不新增固定轮次：

- Round 2 可以动态推荐双方不同 Archetype；
- 用户一句话指定“双方统一某一型”时直接继承，不额外追问。

---

## 4. Archetype Runtime Consumption

### RF-08 — Archetype Mandatory Consumption Gate

当：

```text
Cinematic Combat Archetype != none
```

则进入 Derived Choreography Direction / Stage-2 前必须实际读取对应 Archetype Library / leaf knowledge。

链路：

```text
用户确认 Archetype
→ Archetype Library Read
→ 提取 Runtime Bias
→ 注入 Derived Choreography Direction
→ Stage-2 Gap Detection / Pattern Selection
```

如果 Archetype 已确认但对应执行知识没有实际读取：

> **Archetype Consumption Missing**

Final Preflight 不得仅凭 Planning Context 中存在明星标签判 PASS。

### RF-09 — Archetype-to-Stage-2 Weighting

Archetype 不是只读参考标签，而是 Stage-2 Pattern Selection 的真实权重输入。

例如李连杰型应提高：

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

其他 Archetype 同理根据其 Library Runtime Bias 影响 Pattern Selection。

明确禁止：

- 每 3 招必须 1 脚；
- 固定转身次数；
- 固定换位次数；
- 固定明星 Combo；
- 固定动作套餐。

Archetype 改变选择权重和偏置，不定义机械配额。

### RF-10 — Archetype Realization Gate

Library Read Evidence 只是必要条件，不是 PASS 条件。

Final Preflight 必须进一步检查：

> 删除明星名称后，仅从最终动作本身能否明显读出所选 Archetype 的 Movement / Rhythm / Range / Transition / Impact 偏置？

如果 Library 已读，但最终仍回到同质化动作骨架：

> **Archetype Realization Failure**

---

## 5. Per-Character Signature Separation

### RF-11 — Per-Character Signature Separation Gate

不同角色已经确认不同：

```text
Combat System
+ Combat Expression
+ Cinematic Combat Archetype
```

则这种差异必须贯穿整场战斗。

检查维度包括：

```text
Entry 方式
Movement 偏好
Technique 选择
Range Transition
Rhythm
Initiative Theft 方式
失去主动后的 Re-entry
```

如果后半段双方重新同质化成相同的：

```text
格挡 → 侧切 → 低扫 → 抓控 → 转轴
```

只是轮流使用，则判：

> **Per-Character Signature Collapse**

这是已有 Persistent Combat Signature 的双角色差异化落实。

---

## 6. Ending / Advantage Compatibility

### RF-12 — Ending Signature Compatibility Gate

Ending / Advantage Recommendation 必须消费：

```text
Combat System
+ Combat Expression
+ Cinematic Combat Archetype
+ 当前 Advantage Trajectory
```

Ending 负责定义：

- 谁取得什么程度的优势；
- 对手当前是否仍能反抗；
- 结束画面处于什么战术状态。

Ending 不得为了表达“谁占优”而偷偷引入新的 dominant technique。

例如：

- 李连杰型不应默认被 Ending 拉回“抓腕 + 锁臂 + 压墙”模板；
- Grappling / Wrestling 主导角色采用墙边身体控制则可以合理。

如果 Ending 引入的主导技术明显破坏已确认 Signature：

> **Ending Signature Compatibility Failure**

重新生成 Ending candidate。

---

## 7. Movement Causality / Upper-body Dominance

### RF-13 — Movement Causality Gate

不能只检查 Prompt 是否出现：

- 侧切；
- 转轴；
- 沉身；
- 高低位；
- 步法；
- 支撑转换。

必须检查 Movement 是否真实创造新的战斗问题或下一动作入口。

PASS 语义：

```text
Movement
→ 改变 Route / Axis / Range / Position / Support / Balance / Level
→ 对手被迫重新响应
→ 新状态直接成为下一 Technique / Defense / Re-entry 原因
```

FAIL 语义：

```text
先由上肢完成主要格挡 / 抓控
→ 再附带“同时侧移一步”
→ 主链仍然是挡拳 → 抓腕 → 压肩
```

即使使用了 Movement Pattern，如果 Movement 只是给上肢 Technique 配脚步，仍判 Upper-body Dominance。

核心问题：

> **Movement 是否改变了战斗问题？**

---

## 8. Stage-2 Traceability

### RF-14 — Stage-2 Pattern Traceability Gate

Regression / Debug 模式必须可追踪：

```text
Planning / Choreography Gap
→ Slot
→ Main Pattern
→ optional Auxiliary Pattern
→ Pattern 提供的关键 Detail
→ Concrete Action Phrase
```

示例：

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

普通最终 Prompt 不展示这些内部调试信息。

通过 Traceability 可以区分：

```text
Pattern 未选
→ Routing Failure

Pattern 选错
→ Selection / Weighting Failure

Pattern 选对但 Phrase 写坏
→ Realization Failure

Choreography 正确但 Final Prompt 被压坏
→ Assembly / Serialization Failure

Prompt 正确但视频不执行
→ Model / Adapter Failure
```

---

## 9. Granularity / Exchange Density

### RF-15 — Granularity Over-expansion 是正式 Failure

本轮再次复现此前已出现的问题：

```text
动作具体化增强
→ 每个 Phrase 被写得越来越细
→ 普通 Exchange 也获得 High Granularity
→ 单个动作占用过多信息 / 执行预算
→ 15 秒最终只剩少量大 Exchange
```

正式 Failure：

> **Granularity Over-expansion**

它与 Granularity Under-specification 是两个相反失败端：

```text
过度压缩
→ 快速反制 / 连续攻击 / 低线动作
→ 不可执行

过度展开
→ 普通动作也解释脚步、髋、肩轴、受力、恢复等全部细节
→ 单个动作很好，但整场动作数量不足
```

### RF-16 — Exchange Density / Granularity Distribution Gate

Final Preflight 检查：

```text
Active Exchange 是否过少？
是否大量普通 Exchange 被错误展开成 High？
是否因为描述过细导致真实战斗事件不足？
High / Medium / Low 是否有实际展开差异？
```

期望：

```text
Major Reversal / Signature / Initiative Theft
→ High

Ordinary Exchange / Re-counter / meaningful Range Change
→ Medium

Connector / Recovery / Re-entry Transition
→ Low
```

禁止：

- 固定动作数；
- 固定 Phrase 数；
- 固定 High / Medium / Low 比例；
- 固定踢腿 / 换位次数。

目标是给更多真实 Exchange 留执行空间，而不是追求机械数量。

### RF-17 — Concrete Compression Gate

压缩 Medium / Low Phrase 时不能重新退化成模糊摘要。

每个承担 Active Combat 的压缩 Phrase 至少保留足够的：

```text
明确动作
+ 明确对手响应或状态后果
+ 必要 Continuation
```

禁止：

```text
掌根或前臂……
低线动作……
快速反制……
连续换位……
```

即：

> **更短的动作句，不等于更模糊的动作句。**

---

## 10. Duration-aware Choreography Budget

### RF-18 — Duration 在 Choreography Planning 前置参与

视频时长不能到 Final Assembly 才考虑。

Runtime 应在具体动作展开之前综合：

```text
Duration
+ Combat Density Intent
+ Active Combat Coverage
+ Camera Complexity
+ Dialogue / Story Event 占用
→ Choreography Information Budget
→ 影响 High / Medium / Low 展开策略
```

例如 15 秒 High Coverage Combat：

- 不代表固定必须多少招 / 多少 Exchange；
- 但意味着不能把所有普通 Exchange 都展开为 High；
- 必须给 Re-counter / Re-entry / Initiative Handoff 留出足够执行空间。

明确禁止：

> “15 秒必须 6 个 Exchange / 8 招 / 2 次腿法”等机械规则。

---

## 11. Two-pass Choreography Planning

### RF-19 — 先完整 Exchange Spine，再选择性 Stage-2 Expansion

为解决“想到一个动作就立刻写得很细，后面没空间”的问题，确认采用轻量两阶段执行顺序。

### Pass 1 — Exchange Spine / Battle Beat Skeleton

先规划整段轻量战斗骨架：

```text
Entry
→ Exchange
→ Re-counter
→ Initiative Shift
→ Exchange
→ Signature / Reversal
→ Ending
```

此阶段重点确定：

```text
谁发起
→ 对方如何回应
→ 产生什么新 State
→ 下一 Exchange 从哪个状态进入
```

先检查：

- Duration / Active Coverage；
- Exchange Depth；
- Advantage / Counterplay；
- Per-character Signature；
- Movement / Range / Position 变化；
- 是否过早压缩成少数几个大动作块。

### Pass 2 — Selective Stage-2 Expansion

再逐个检查 Exchange：

```text
Gap
→ Movement / Technique / Transition Slot
→ Pattern Selection
→ Concrete Action Phrase
→ High / Medium / Low Granularity
```

只有真正的：

- Major Reversal；
- Initiative Theft；
- Signature Moment；

才优先 High Granularity。

普通 Exchange 维持 Medium；连接动作 Low。

边界：

- 不把 Exchange Spine 做成新的复杂 Runtime Engine；
- 不做固定动作模板；
- 不要求固定 Skeleton 节点数量；
- Skeleton 只是先确定完整战斗结构，再进行专业动作具体化的执行顺序。

原则：

> **先知道这里需要发生什么战斗变化，再选择 Pattern；不能先看到 Pattern，再为了使用它硬塞动作。**

---

## 12. Prompt Serialization

### RF-20 — Serialization Deduplication Gate

Final Prompt 中同一个创作 / 控制意图只保留一次最强表达。

优先级：

```text
具体正向动作
>
必要全局正向规则
>
少量高价值 Negative
```

如果具体动作已经自然表达：

- 不 Reset；
- 连续 Motion Handoff；
- 位置变化；
- 受力；

就不应在 Global Rule / Style / Avoid 中重复解释同一件事。

目标结构：

```text
具体动作承担主要语义
+ 少量真正全局 Camera / Physics / Continuity
+ 极少数高价值 Avoid
```

而不是：

```text
动作
+ 动作解释
+ 连续性再解释
+ Camera 再解释
+ Style 再解释
+ Avoid 反向再解释
```

这不是为了单纯缩短 Prompt，而是把信息预算还给真实 Exchange。

---

## 13. Camera Runtime Freeze

### RF-21 — 本轮冻结 Camera Runtime

本次真实 Regression 暂未出现足够证据证明 Action–Camera Runtime 需要重构。

因此本批修复：

- 不顺手优化 Camera Runtime；
- 不新增第二套 Camera Runtime；
- 不改变现有 Action–Camera Handoff 设计；
- Camera 作为 Regression 对照层；
- 后续只验证其他修改是否破坏已有 Camera Handoff。

只有未来 Generated-video Regression 明确出现：

- Camera 抢动作；
- Cut 造成 Motion Reset；
- Viewer Task 丢失；
- Camera Handoff 被 Adapter / Assembly 破坏；

再单独开启 Camera 修复。

---

## 14. 本轮 Runtime 修复范围

当前已确认、本批后续实施需要覆盖：

```text
Round 1 Recommendation Breadth / Diversity
Round 1 Dynamic Candidate Count
1v1 Pairing Presentation
Round 2 Expression Candidate Coverage
Archetype Candidate Coverage
Character-level Archetype
Archetype Mandatory Consumption
Archetype → Stage-2 Weighting
Archetype Realization
Ending Signature Compatibility
Per-character Signature Separation
Movement Causality
Stage-2 Pattern Traceability
Duration-aware Choreography Budget
Two-pass Choreography Planning
Exchange Density / Granularity Distribution
Concrete Compression
Serialization Deduplication
```

明确暂不做：

```text
Camera Runtime 重构
完整中国武术百科扩库
每位明星独立 Combat Engine
明星固定 Combo Library
固定动作数 / 腿法数 / 换位数
固定 6～8 候选硬配额
固定 15 秒 Exchange 数量
新的复杂 Skeleton Engine
```

---

## 15. Regression 验收口径

下一次 G01 回归至少验证：

1. Round 1 是否根据当前选题动态生成足够宽的高价值 Pairing 候选；
2. 候选数量是否常见约 6～8，但没有机械凑数；
3. Round 2 Expression 是否存在真实可选分叉；
4. 五种 Archetype 是否完整展示，李小龙型不再静默消失；
5. 角色 Archetype 是否可独立设置或统一设置；
6. 选中 Archetype 后是否实际读取 Library；
7. Archetype Bias 是否真实影响 Stage-2 Pattern Selection；
8. Pattern Trace 是否可证明 Gap → Slot → Pattern → Phrase；
9. Movement 是否真实改变战斗状态，而非只给上肢动作配脚步；
10. 不同角色 Signature 是否持续可辨识；
11. Ending 是否保持上游 Signature，而非默认收缩成抓腕 / 压墙；
12. Choreography 是否先形成完整 Exchange Spine；
13. 15 秒内是否恢复更丰富的 Active Exchange，而非只有约 3 个大块；
14. Medium / Low 是否更短但仍具体；
15. Final Prompt 是否明显减少重复控制语义；
16. Camera Handoff 是否保持当前质量，没有被其他改动破坏。

---

## 16. 当前实施原则

> **先记录确认设计，再统一改 Runtime。**
>
> **不要每确认一个问题就立刻改一处代码，避免 Runtime 在 Grill 未收口前反复震荡。**
>
> **Simple Interactive Choice Upstream; Professional Execution Downstream.**
>
> **Duration constrains expansion depth, not fixed action count.**
>
> **Concrete but compressed; rich in exchanges, not rich in redundant explanation.**
