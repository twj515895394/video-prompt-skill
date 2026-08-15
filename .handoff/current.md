# Video Prompt Skill — Action Combat Regression Fix Handoff

> 更新时间：2026-08-15 20:45（UTC+8）  
> 仓库：`twj515895394/video-prompt-skill`  
> 分支：`main`  
> 当前阶段：**G01 第一轮真实 Regression 已完成分析；RF-01～RF-21 已确认并完成首批 Runtime 接线与静态回读。下一会话不继续扩设计，直接接收用户重新测试后的完整材料并执行第二轮 Regression Analysis。**

---

## 0. 新会话接管指令

新会话开始后优先读取：

1. `.handoff/current.md`
2. `docs/action-combat-video-regression-fix-spec.md`
3. `references/tasks/action-combat-video/interactive-combat-policy.md`
4. `references/tasks/action-combat-video/regression-fix-runtime-policy.md`
5. 如需核对 Stage-2，再读取 `references/libraries/combat-choreography-patterns/minimum-validation-set.md`

**不要重新 Grill RF-01～RF-21，不要重新讨论为什么要做 Archetype / Hybrid，不要先扩完整武术知识库。**

用户下一会话会直接带回新的测试内容。第一目标是：

> **基于新测试证据判断本批 Runtime 修复是否真正生效，并把失败定位到 Recommendation / Interactive / Archetype Consumption / Stage-2 Selection / Choreography Realization / Assembly / Model 中的具体层。**

核心原则：

> **Regression → Failure Layer → Minimal Fix → Regression Again.**
>
> **Routing First, Knowledge Second.**
>
> **Prompt PASS ≠ Generated Video PASS。**

如果新测试已经 PASS，不要为了“更完整”继续扩系统。

---

## 1. 固定 Golden Scenario / G01

继续使用同一场景，便于和上一轮横向比较：

- 15 秒；
- 普通现代中国公司办公室；
- 中国女性，22 岁，漂亮，长高马尾，正常职场服装；
- 中国男性，55 岁，矮胖、秃顶领导，正常职场服装；
- 两人分别属于敌对杀手组织，都是职业杀手；
- Close Combat / 贴身搏斗；
- 两人之间不要隔办公桌或大型障碍物；
- 无枪械、无刀具；
- Interactive Mode；
- 原始输入不要主动指定 MMA；
- 如非测试目标，不主动在第一句直接指定某个明星 Archetype，让 Runtime 自己暴露选择。

上一轮实际选择：

```text
Round 1
女方：Chinese Cinematic Kung-fu Hybrid
男方：散打

Round 2
女方 Expression：冷静诱导 / 后发反制 / 控制风险
男方 Expression：主动压迫 / 持续抢先 / 被化解后立即再进入
Archetype：李连杰型

Camera
动作可读 + 电影冲击平衡

Ending
女方阶段性明显优势
```

上一轮主要失败：

- Round 1 推荐空间偏窄；
- Round 2 Expression 只有推荐 A，没有真实可选分叉；
- 李小龙型在实际 Archetype 候选中消失；
- 用户选中李连杰型，但 Read List 没有读取 Archetype Library；
- Stage-2 最小 Pattern 有进入动作，但缺少 `Gap → Slot → Pattern → Phrase` 可追踪证据；
- Movement 有增加，但关键主动权仍大量由前臂 / 肩线 / 抓控 / 腕肘驱动；
- Ending 推荐“墙边 + 控腕”反向吸走上游李连杰型 Signature；
- 15 秒仍约 3 个大 Exchange + Ending；
- 普通 Exchange 被过度展开，产生 Granularity Over-expansion；
- Final Prompt 存在“掌根或前臂”“低线动作”等未决 / 模糊动作；
- 同一控制语义在 Action / Global Rule / Style / Avoid 中重复；
- Camera Handoff 基本正常。

---

## 2. 已确认设计真源

主 Spec：

`docs/action-combat-video-regression-fix-spec.md`

当前状态：

> **Confirmed Design + Initial Runtime Implemented / 待 G01 Regression 验证**

本批编号：

`RF-01 ～ RF-21`

### Round 1

- RF-01：不禁止 Hybrid 出现在普通中国角色题材；核心修复是 Recommendation Breadth，而非禁止 Hybrid。
- RF-02：Round 1 作为第一处分叉，常见约 6～8 个高价值方向，但数量必须动态分析，不是硬配额。
- RF-03：Recommendation Diversity Gate 检查真正设计空间差异，不检查单纯数量。
- RF-04：1v1 默认展示双方完整 Combat System Pairing；底层仍 Per-Character 独立保存。

### Round 2

- RF-05：Expression 必须提供 2～3 个真实动态候选 + 自定义；不能只有推荐 A。
- RF-06：Archetype Selection 默认完整展示李连杰 / 吴京 / 甄子丹 / 成龙 / 李小龙 + none/custom；可排序，不得无理由静默删除。
- RF-07：Archetype 是 Character-level 属性；双方可以不同，也可以共享；不新增固定轮次。

### Archetype Runtime

- RF-08：Archetype != none 时必须实际读取 `combat-cinematic-archetypes/library.md`。
- RF-09：Archetype Runtime Bias 必须真实影响 Stage-2 Pattern Selection 权重。
- RF-10：Library Read 不是 PASS；最终动作本身必须可辨识 Archetype，否则为 `Archetype Realization Failure`。

### Character / Ending / Movement

- RF-11：Per-Character Signature Separation Gate；双方不能打到后面同质化。
- RF-12：Ending Signature Compatibility Gate；Ending 只定义结束优势状态，不得偷换 dominant technique。
- RF-13：Movement Causality Gate；Movement 必须真实改变下一战斗问题，不是给上肢动作补脚步。

### Stage-2 / Granularity / Duration

- RF-14：Stage-2 Pattern Traceability：`Gap → Slot → Pattern → Detail → Concrete Phrase`。
- RF-15：正式识别 `Granularity Over-expansion`。
- RF-16：Exchange Density / Granularity Distribution Gate。
- RF-17：Concrete Compression Gate：更短但仍明确，不允许 “A or B / 某种低线动作”。
- RF-18：Duration-aware Choreography Budget；时长前置影响展开深度，但不产生固定动作数。
- RF-19：Two-pass Choreography：先 Exchange Spine / Battle Beat Skeleton，再选择性 Stage-2 Expansion。

### Assembly / Camera

- RF-20：Serialization Deduplication Gate；优先级：`具体正向动作 > 必要全局正向规则 > 少量高价值 Negative`。
- RF-21：Camera Runtime Freeze；本轮不顺手重构 Camera，只做 Regression Preservation。

---

## 3. 已完成 Runtime 实施

### 3.1 Interactive Combat Policy

文件：

`references/tasks/action-combat-video/interactive-combat-policy.md`

实施 Commit：

`1a314bfe64f7b3636f0c2269bf107fe738a7b80a`

已经接入：

- Round 1 Dynamic Recommendation Breadth；
- 常见约 6～8 个但非固定；
- Recommendation Diversity Gate；
- 1v1 Pairing Presentation；
- Hybrid 合法存在但不做身份硬映射；
- Round 2 Expression Candidate Coverage；
- 五种基础 Archetype 完整覆盖；
- 李小龙型不得静默消失；
- Per-Character Archetype；
- Round 2 后 Mandatory Handoff 到 Regression Runtime Policy。

### 3.2 Regression Fix Runtime Policy

新增：

`references/tasks/action-combat-video/regression-fix-runtime-policy.md`

创建 Commit：

`b99931ce0fe3602e12086fe5792c171333fa2a70`

强制运行链：

```text
Confirmed Per-Character Planning Context
→ Archetype Mandatory Consumption
→ Derived Choreography Direction
→ Duration-aware Choreography Budget
→ Pass 1: Exchange Spine / Battle Beat Skeleton
→ Per-Character Signature + Advantage / Ending Compatibility
→ Stage-2 Gap Detection
→ Archetype-weighted Pattern Selection
→ Stage-2 Pattern Trace
→ Pass 2: Selective Concrete Expansion
→ Movement Causality Check
→ Granularity / Exchange Density Check
→ Concrete Compression
→ Action–Camera Handoff（沿用原 Runtime）
→ Prompt Assembly
→ Serialization Deduplication
→ Final Preflight
```

该文件是轻量 Runtime 补强层，不是第二套 Combat Engine。

### 3.3 Stage-2 Minimum Validation Set

文件：

`references/libraries/combat-choreography-patterns/minimum-validation-set.md`

实施 Commit：

`5cf7d28a7835a04122aac2ab3cd48893e2af8993`

新增：

- Pattern Traceability；
- Archetype / Signature Weighting 边界；
- Movement Causality；
- G01 新验收要求；
- 明确“只读文件 ≠ Stage-2 已成功执行”。

### 3.4 Spec 状态同步

文件：

`docs/action-combat-video-regression-fix-spec.md`

最新状态 Commit：

`1ab0d9c1ddec4fbd4375be717b23fa30561c8d54`

状态已经更新为：

> **Confirmed Design + Initial Runtime Implemented / 待 G01 Regression 验证**

### 3.5 主 Wiring 静态确认

`SKILL.md` 仍固定：

```text
Interactive Action Combat
→ READ references/tasks/action-combat-video/interactive-combat-policy.md
```

新的 `interactive-combat-policy.md` 再强制：

```text
Round 1 / Round 2 完成
→ READ references/tasks/action-combat-video/regression-fix-runtime-policy.md
→ 再进入 Derived Choreography Direction / Stage-2
```

因此新 Runtime Policy 已进入 Interactive Action Combat 主链，不是孤立文档。

---

## 4. 本轮明确冻结 / 不做

### Camera Runtime Freeze

没有修改：

`references/tasks/action-combat-video/action-camera-handoff-playbook.md`

原因：上一轮真实 Regression 中 Action-triggered Camera Handoff 基本正常，没有证据要求重构。

下一轮只验证：

- Camera 是否被其他修改破坏；
- Cut / Reframe 后 Motion 是否继续；
- Viewer Task 是否保留；
- Adapter / Assembly 是否仍 Preserve Handoff。

### Knowledge Expansion Freeze

暂不扩：

- 完整中国武术百科；
- 每明星独立 Combat Engine；
- 明星固定 Combo Library；
- Lower-body Engine；
- Body Method State Machine；
- 每拳种独立 Runtime Tree。

只有当下面全部成立：

```text
Routing 正确
+ Required Read 正确
+ Pattern Hit 正确
+ Archetype Weighting 正确
+ Concrete Choreography 正确
+ Final Prompt 正确
+
真实生成结果仍明显缺能力
```

才进入 Knowledge Coverage Audit / Model Capability 分析。

---

## 5. 下一会话用户最好直接提供的测试材料

用户不需要重新解释项目背景，直接粘贴最新测试即可。

推荐一次提供：

```text
【原始需求】
...

【完整 Interactive 对话】
...

【每轮最终选择】
Round 1：...
Round 2 Expression：...
女方 Archetype：...
男方 Archetype：...
Camera：...
Advantage / Ending：...

【Read List】
...

【Pattern / Trace Evidence】
...

【Final Prompt】
...

【模型】
Generic / Seedance / LTX / 其他

【如果已生成视频】
1. 最满意：...
2. 最明显失败：...
3. 是否站桩：...
4. 是否能看出双方不同打法：...
5. 是否能看出所选 Archetype：...
6. 动作数量 / 连续性：...
7. Camera：...
```

材料不全时，先用已有证据分析；不要要求用户重复已经提供的信息。

---

## 6. 第二轮 Regression 固定检查顺序

下一会话严格优先检查 Runtime 是否执行正确，再判断 Knowledge 是否不足。

### Gate A — Round 1 Recommendation Breadth

检查：

- 是否出现更宽的动态 Pairing 候选；
- 数量是否由当前选题动态决定；
- 常见可以约 6～8 个，但不能机械凑数；
- Pairing 是否真的覆盖不同 Combat Design Space；
- Hybrid 可以被推荐，但不是唯一方向；
- 不因为“现代杀手”机械 MMA；
- 不因为“中国角色”机械只剩中国功夫。

失败优先归类：

- `Recommendation Breadth Failure`
- `Recommendation Diversity Failure`
- `Identity-to-System Shortcut`

### Gate B — Hybrid UX

如果选择 Hybrid：

- 不固定追问“具体混哪些门派”；
- 直接进入 Round 2 或其他真正高价值节点；
- 用户主动指定主 / 辅体系时才进入 Hybrid Refinement。

### Gate C — Round 2 Double Sub-dimension

检查：

- Expression 是否有多个真实候选；
- Expression 候选是否真的改变 Initiative / Risk / Pressure / Counter / Re-entry / Rhythm；
- Archetype 是否完整展示 5 种；
- 李小龙型是否出现；
- Expression 与 Archetype 是否分开展示、同轮选择；
- 是否允许女方 / 男方分别设置 Archetype；
- 是否允许双方共享同一 Archetype。

失败优先归类：

- `Expression Candidate Coverage Failure`
- `Archetype Candidate Coverage Failure`

### Gate D — Archetype Mandatory Consumption

如果选中任何 Archetype：

Read List 必须出现：

`references/libraries/combat-cinematic-archetypes/library.md`

如果没有：

> `Archetype Consumption Missing`

不要继续讨论知识覆盖，先修 Runtime Read / Handoff。

### Gate E — Archetype-to-Stage-2 Weighting

例如李连杰型，应能从 Pattern Selection / Choreography 看到：

- Footwork；
- Route；
- Axis；
- Level；
- Kick Integration；
- Whole-body Linkage；

真实提高。

不能只出现“轻灵流畅 / 李连杰型”等标签。

Library Read 正确但动作不体现时：

> `Archetype Realization Failure`

### Gate F — Stage-2 Pattern Traceability

Regression / Debug Evidence 应能回答：

```text
当前 Gap 是什么
→ Slot 是什么
→ Main Pattern 是什么
→ optional Auxiliary Pattern 是什么
→ 实际读取了哪个 leaf knowledge
→ 哪个 Detail 被实例化
→ 对应 Final / Concrete Phrase 是哪一句
```

只出现 `minimum-validation-set.md` 在 Read List，不算 Stage-2 PASS。

### Gate G — Two-pass / Duration-aware Choreography

检查是否先形成整段轻量 Exchange Spine，再局部展开。

重点看：

- 15 秒是否仍只有约 3 个大 Exchange；
- 是否恢复更多真实 Re-counter / Re-entry / Initiative Handoff；
- 是否没有出现所有 Exchange 都 High-detail；
- 是否没有固定“15 秒必须 N 招”的机械配额。

失败：

- `Granularity Over-expansion`
- `Exchange Density Collapse`

### Gate H — Movement Causality

不是检查有没有“斜切 / 转轴 / 沉身”等词，而是检查：

```text
Movement
→ 是否改变 Route / Axis / Range / Position / Support / Balance / Level
→ 是否迫使对手重新响应
→ 是否真实创造下一 Technique / Defense / Re-entry
```

如果主链仍是：

```text
挡拳
→ 抓腕
→ 压肩
```

旁边只是补脚步，则仍 FAIL。

### Gate I — Per-Character Signature Separation

删除角色姓名后，仅看动作逻辑：

- 双方是否仍能大致区分；
- System / Expression / Archetype 是否持续影响进入、Range、节奏、Technique、Re-entry；
- 是否后半段又塌成同一套动作骨架。

失败：

> `Per-Character Signature Collapse`

### Gate J — Ending Signature Compatibility

检查 Ending 是否：

- 只表达最终优势状态；
- 与当前 Combat System / Expression / Archetype / Trajectory 相容；
- 没有重新引入不匹配的 dominant technique；
- 没有因为“谁占优”自动变成抓腕 / 锁臂 / 压墙模板。

失败：

> `Ending Signature Compatibility Failure`

### Gate K — Concrete Compression

Medium / Low Phrase 应更短，但仍明确。

禁止：

- “掌根或前臂”；
- “低线动作”；
- “踢 / 扫 / 蹬其中一种”；
- “快速反制”；
- “连续换位”代替真实动作。

目标：

> **更短，但不是更模糊。**

### Gate L — Serialization Deduplication

Final Prompt 检查：

- 同一控制意图是否只保留一次最强表达；
- 具体动作已经表达连续性时，是否还在 Global / Style / Avoid 重复解释；
- Negative 是否只留下真正高价值、模型易犯的错误；
- Prompt 空间是否更多留给真实 Exchange。

### Gate M — Camera Preservation

Camera Runtime 本轮冻结，只做回归：

- Action Anchor 是否仍然明确；
- Camera Change 是否有 Viewer Task；
- Cut / Reframe 后 live motion 是否继续；
- 是否没有被其他修复误伤。

Camera PASS 时不要顺手重构。

---

## 7. 第二轮 Failure 分流

### A. Interactive 仍有问题

```text
Round 1 / Round 2 Candidate Failure
→ 修 Interactive Policy / Exposure
→ 不动 Stage-2 Knowledge
```

### B. Archetype 选中了但没 Read Library

```text
→ Archetype Consumption / Mandatory Handoff Failure
→ 修 Routing / Runtime
```

### C. Library Read 正确但 Pattern 没被加权

```text
→ Archetype-to-Stage-2 Weighting Failure
→ 修 Selection Logic / Derived Direction
```

### D. Pattern Selection 正确但动作仍上肢主导

先看：

```text
Movement Causality
+ Pattern Realization
+ Per-Character Signature
```

如果 Pattern 已正确消费但表现仍不足，再考虑 Knowledge Coverage。

### E. Choreography 正确但 Final Prompt 变差

```text
→ Assembly / Concrete Compression / Serialization Dedup Failure
```

### F. Prompt-level 全部 PASS，但生成视频仍差

```text
→ Generated-video Regression
→ Model Capability / Prompt Saturation / Adapter
```

此时才考虑模型限制或进一步 Knowledge Coverage Audit。

---

## 8. 当前禁止继续做的事情

除非第二轮真实 Regression 明确证明必要，不要：

- 扩完整中国武术百科；
- 给每位明星建独立 Engine；
- 给每位明星建固定 Combo Library；
- 强制 Hybrid 选择几个门派；
- 把 MMA 全局降级；
- 把 Archetype 当 Combat System；
- 建 Lower-body Engine；
- 建 Body Method State Machine；
- 建每拳种独立 Runtime Tree；
- 建第二套 Camera Runtime；
- 用固定动作数 / 踢腿次数 / 换位次数解决 Density / Standing；
- 把“常见 6～8 个 Round 1 候选”实现成硬配额；
- 把 Exchange Spine 实现成固定 Beat 模板；
- 在没有真实第二轮 Regression 证据前继续增加复杂机制。

Anti-overdesign：

> **Simple Interactive Choice Upstream; Professional Execution Downstream.**
>
> **Duration constrains expansion depth, not fixed action count.**
>
> **Concrete but compressed; rich in exchanges, not rich in redundant explanation.**

---

## 9. 当前关键文件

### Spec

- `docs/action-combat-video-regression-fix-spec.md`
- `docs/combat-cinematic-archetype-spec.md`

### Interactive

- `references/tasks/action-combat-video/interactive-combat-policy.md`
- `assets/templates/mode-interactive-output-contract.md`

### Regression Runtime

- `references/tasks/action-combat-video/regression-fix-runtime-policy.md`

### Choreography / Stage-2

- `references/tasks/action-combat-video/choreography-playbook.md`
- `references/libraries/combat-choreography-patterns/minimum-validation-set.md`
- `references/libraries/combat-cinematic-archetypes/library.md`

### Advantage / Ending

- `references/tasks/action-combat-video/advantage-structure-contract.md`

### Assembly

- `references/controls/prompt-assembly/control.md`

### Camera — Frozen

- `references/tasks/action-combat-video/action-camera-handoff-playbook.md`

### Main Wiring

- `SKILL.md`

---

## 10. 当前关键提交

本批核心提交：

- Regression Fix Spec 初始：`2ea173ccfd48f30eb6f23719e5c318be00f96e43`
- Interactive Runtime：`1a314bfe64f7b3636f0c2269bf107fe738a7b80a`
- Regression Runtime Policy：`b99931ce0fe3602e12086fe5792c171333fa2a70`
- Stage-2 Minimum Validation Set：`5cf7d28a7835a04122aac2ab3cd48893e2af8993`
- Handoff 第一版实施态：`a1686204d1f877f02389162293a7c754ae1419eb`
- Spec 状态同步：`1ab0d9c1ddec4fbd4375be717b23fa30561c8d54`

---

## 11. 下一会话完成条件

下一会话不要以“新增了多少规则”为完成标准。

完成标准：

```text
新的真实 G01 测试
→ 对照 RF-01～RF-21 Gate
→ 定位 PASS / FAIL
→ 失败映射到具体 Failure Layer
→ 只修那个 Layer
→ 再 Regression
```

如果新的 Interactive / Read / Trace / Prompt 已经明显 PASS：

> **停止扩设计，进入生成视频验证。**

如果 Prompt-level PASS，但视频仍明显不符合：

> **进入 Generated-video Regression，而不是继续改 Prompt 架构。**

最终判断口令：

> **先看真实结果，再决定修哪里。**
