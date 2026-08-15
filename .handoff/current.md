# Video Prompt Skill — Action Combat Regression Fix Handoff

> 更新时间：2026-08-15 20:32（UTC+8）  
> 仓库：`twj515895394/video-prompt-skill`  
> 分支：`main`  
> 当前阶段：**G01 第一轮真实 Regression 已完成分析；RF-01～RF-21 已确认并完成首批 Runtime 接线。停止继续扩设计，下一步直接重新跑同一个 G01 Interactive Regression。**

---

## 0. 新会话接管指令

新会话开始后优先读取：

1. `.handoff/current.md`
2. `docs/action-combat-video-regression-fix-spec.md`
3. `references/tasks/action-combat-video/interactive-combat-policy.md`
4. `references/tasks/action-combat-video/regression-fix-runtime-policy.md`

不要重新 Grill 已确认的 RF-01～RF-21，不要重新讨论为什么要做 Archetype / Hybrid，也不要先扩完整拳种知识库。

**下一步不是继续设计，而是重新跑 G01，验证本批 Runtime 修复是否真正生效。**

核心原则：

> **Regression → Failure Layer → Minimal Fix → Regression Again.**
>
> **Routing First, Knowledge Second.**

---

## 1. 本轮真实 Regression 输入

固定 Golden Scenario：

- 15 秒；
- 普通现代中国公司办公室；
- 中国女性，22 岁，长高马尾，正常职场服装；
- 中国男性，55 岁，矮胖、秃顶领导，正常职场服装；
- 两人分别属于敌对杀手组织，都是职业杀手；
- Close Combat；
- 双方之间不要隔办公桌或大型障碍；
- 无枪械、无刀具；
- Interactive Mode。

上一轮用户实际选择：

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

上一轮 Final Prompt 的主要问题：

- Round 1 推荐空间偏窄；
- Round 2 Expression 只有推荐 A，没有真实分叉；
- 李小龙型在实际候选中消失；
- 用户选中李连杰型，但 Read List 没有读取 Archetype Library；
- Stage-2 最小 Pattern 有进入动作，但缺乏可追踪 Pattern Hit Evidence；
- Movement 有增加，但关键主动权仍大量由前臂 / 肩线 / 抓控 / 腕肘驱动；
- Ending 推荐“墙边 + 控腕”反向吸走上游李连杰型动作 Signature；
- 15 秒仍约 3 个大 Exchange + Ending；
- 普通 Exchange 被过度展开，产生 Granularity Over-expansion；
- Final Prompt 存在“掌根或前臂”“低线动作”等未决 / 模糊动作；
- 同一控制语义在 Action / Global Rule / Style / Avoid 中重复；
- Camera Handoff 本轮基本正常，不作为修复重点。

---

## 2. 已确认 Spec

主真源：

`docs/action-combat-video-regression-fix-spec.md`

本批确认项编号：

`RF-01 ～ RF-21`

### Round 1

- RF-01：不禁止 Hybrid 出现在普通中国角色题材；解决点是 Recommendation Breadth，而不是禁止 Hybrid。
- RF-02：Round 1 默认更宽，常见约 6～8 个高价值方向，但数量动态决定，不是硬配额。
- RF-03：Recommendation Diversity Gate 检查设计空间差异，不检查单纯数量。
- RF-04：1v1 默认展示完整双方 Combat System Pairing；底层仍 Per-Character 独立存储。

### Round 2

- RF-05：Expression 必须提供 2～3 个真实动态候选 + 自定义；不能只有推荐 A。
- RF-06：Archetype 选择默认完整展示李连杰 / 吴京 / 甄子丹 / 成龙 / 李小龙 + none/custom；可以动态排序，不得无理由静默删除。
- RF-07：Archetype 是 Character-level 属性；双方可以不同，也可共享；不新增固定轮次。

### Archetype Runtime

- RF-08：Archetype != none 时必须实际读取 `combat-cinematic-archetypes/library.md`。
- RF-09：Archetype Runtime Bias 必须真实影响 Stage-2 Pattern Selection 权重。
- RF-10：Library Read 不是 PASS；最终动作本身必须可辨识 Archetype，失败为 `Archetype Realization Failure`。

### Character / Ending / Movement

- RF-11：Per-Character Signature Separation Gate，双方不能打到后面同质化。
- RF-12：Ending Signature Compatibility Gate；Ending 只定义结束优势状态，不得偷换 dominant technique。
- RF-13：Movement Causality Gate；Movement 必须真实改变下一战斗问题，不是给上肢动作补脚步。

### Stage-2 / Granularity / Duration

- RF-14：Stage-2 Pattern Traceability：`Gap → Slot → Pattern → Detail → Concrete Phrase`。
- RF-15：正式识别 `Granularity Over-expansion`。
- RF-16：Exchange Density / Granularity Distribution Gate。
- RF-17：Concrete Compression Gate：更短但仍明确，不允许“A or B / 某种低线动作”。
- RF-18：Duration-aware Choreography Budget；时长前置影响展开深度，但不产生固定动作数。
- RF-19：Two-pass Choreography：先 Exchange Spine / Battle Beat Skeleton，再选择性 Stage-2 Expansion。

### Assembly / Camera

- RF-20：Serialization Deduplication Gate；具体正向动作 > 必要全局正向规则 > 少量高价值 Negative。
- RF-21：本轮 Camera Runtime Freeze；不顺手重构 Camera，只做 Regression Preservation。

---

## 3. 已完成 Runtime 实施

### 3.1 Interactive Combat Policy

文件：

`references/tasks/action-combat-video/interactive-combat-policy.md`

Commit：

`1a314bfe64f7b3636f0c2269bf107fe738a7b80a`

已实施：

- Round 1 Dynamic Recommendation Breadth；
- 常见约 6～8 个、非固定数量；
- Recommendation Diversity Gate；
- 1v1 Pairing Presentation；
- Chinese Cinematic intent 与 Hybrid 边界；
- Round 2 Expression Candidate Coverage；
- 五种基础 Archetype 完整覆盖，李小龙型不得静默消失；
- Per-Character Archetype；
- Round 2 完成后 Mandatory Handoff 到新的 Regression Runtime Policy。

### 3.2 Regression Fix Runtime Policy

新增：

`references/tasks/action-combat-video/regression-fix-runtime-policy.md`

Commit：

`b99931ce0fe3602e12086fe5792c171333fa2a70`

负责：

```text
Archetype Mandatory Consumption
→ Archetype-to-Stage-2 Weighting
→ Per-Character Signature Separation
→ Ending Signature Compatibility
→ Duration-aware Choreography Budget
→ Pass 1 Exchange Spine
→ Stage-2 Gap / Pattern Selection
→ Pattern Traceability
→ Pass 2 Selective Expansion
→ Movement Causality
→ Exchange Density / Granularity
→ Concrete Compression
→ Action-Camera（沿用旧 Runtime）
→ Prompt Assembly
→ Serialization Deduplication
→ Final Preflight additions
```

该文件是轻量运行期补强，不是第二套 Combat Engine。

### 3.3 Minimum Validation Set

文件：

`references/libraries/combat-choreography-patterns/minimum-validation-set.md`

Commit：

`5cf7d28a7835a04122aac2ab3cd48893e2af8993`

已增加：

- Pattern Traceability；
- Archetype / Signature Weighting 边界；
- Movement Causality Gate；
- G01 新验收要求；
- 明确“只读文件 ≠ Stage-2 已成功执行”。

### 3.4 主 Wiring 静态确认

`SKILL.md` 仍固定：

```text
Interactive Action Combat
→ READ references/tasks/action-combat-video/interactive-combat-policy.md
```

而新的 `interactive-combat-policy.md` 已强制：

```text
Round 1 / Round 2 完成
→ READ references/tasks/action-combat-video/regression-fix-runtime-policy.md
→ 再进入 Derived Choreography Direction / Stage-2
```

因此新 Runtime Policy 已经进入 Interactive Action Combat 主链，不是孤立文档。

---

## 4. 本轮明确没有修改

### Camera Runtime

没有修改：

`references/tasks/action-combat-video/action-camera-handoff-playbook.md`

原因：上一轮真实 Regression 的 Action-triggered Camera Handoff 基本正常，没有足够证据要求重构。

后续只验证：

- Camera 是否被其他修改破坏；
- Cut / Reframe 后 Motion 是否继续；
- Viewer Task 是否保留；
- Adapter / Assembly 是否仍 Preserve Handoff。

### Knowledge Expansion

暂不扩：

- 完整中国武术百科；
- 每明星独立 Combat Engine；
- 明星固定 Combo Library；
- Lower-body Engine；
- Body Method State Machine；
- 每拳种独立 Runtime Tree。

只有当：

```text
Routing / Read / Pattern Hit / Archetype Weighting / Prompt 都正确
+
真实输出仍明显缺动作能力
```

才进入 Knowledge Coverage Audit。

---

## 5. 下一步固定：重新跑 G01

不要继续设计新规则，直接用同一个 Golden Scenario 测试 Interactive。

建议原始输入保持接近上一轮，不主动在输入里指定 MMA 或具体明星，以便观察推荐链是否改变。

### Gate A — Round 1 Recommendation

检查：

- 是否出现更宽的动态 Pairing 候选；
- 常见是否约 6～8 个，但不是机械数量；
- 候选是否真的覆盖不同 Combat Design Space；
- Hybrid 可以被推荐，但不是唯一方向；
- 不因为“现代杀手”机械 MMA；
- 不因为“中国角色”机械只剩中国功夫。

### Gate B — Hybrid UX

选择 Hybrid 后：

- 不固定追问“具体混哪些门派”；
- 直接进入 Round 2 或其他真正高价值节点。

### Gate C — Round 2

检查：

- Expression 是否有多个真实候选；
- Archetype 是否完整展示 5 种；
- 李小龙型是否出现；
- Expression 与 Archetype 是否分开展示、同轮选择；
- 是否可以女方 / 男方分别设置 Archetype，也可以双方共享。

### Gate D — Archetype Consumption

如果选李连杰型：

Read List 必须出现：

`references/libraries/combat-cinematic-archetypes/library.md`

并且 Trace / Choreography 应能看出：

- Footwork；
- Route；
- Axis；
- Level；
- Kick Integration；
- Whole-body Linkage；

真实提高，而不是只写“轻灵流畅”。

### Gate E — Stage-2 Trace

必须能提供类似：

```text
Gap
→ Slot
→ Main Pattern
→ optional Auxiliary Pattern
→ Detail
→ Realized Phrase
```

不能只给 Read List。

### Gate F — Two-pass / Density

检查：

- 是否先有完整 Exchange Spine；
- 15 秒是否恢复更多真实 Active Exchange；
- 是否不再只有约 3 个大 Phrase；
- Signature / Reversal High-detail；
- 普通 Exchange Medium；
- Connector Low；
- 没有固定动作数配额。

### Gate G — Movement Causality

检查 Movement 是否真实改变：

- Route；
- Axis；
- Range；
- Position；
- Support / Balance；
- Level；

并迫使对手产生新的响应。

如果只是：

```text
挡拳 + 同时移一步 + 抓腕
```

仍 FAIL。

### Gate H — Signature / Ending

检查：

- 双方打法能否持续区分；
- Ending 是否与 System / Expression / Archetype 相容；
- 李连杰型不能再次被默认“抓腕 + 压墙”吸走；
- Grappling 角色如果符合自身 Signature，则控制型 Ending 仍合法。

### Gate I — Final Prompt Assembly

检查：

- 是否没有“掌根或前臂”这类未决动作；
- 是否没有“低线动作”这种模糊类别替代 Technique；
- Medium / Low 是否更短但仍具体；
- 是否减少 Action / Global Rule / Style / Avoid 重复；
- Prompt 变短时，真实 Exchange 反而更多。

### Gate J — Camera Preservation

只做回归：

- Action Anchor；
- Viewer Task；
- Live Motion Continuation；
- Spatial Re-establish；

是否仍保持。

Camera 不作为本轮主动优化目标。

---

## 6. 下一次最好带回的材料

```text
【原始需求】
...

【完整 Interactive 对话】
...

【每轮最终选择】
Round 1：...
Round 2：...
Camera：...
Advantage / Ending：...

【Read List】
...

【Stage-2 Pattern Trace】
Exchange 1: Gap → Slot → Pattern → Phrase
Exchange 2: ...

【Final Prompt】
...

【模型】
Generic / Seedance / LTX / 其他

【如果生成了视频】
最满意：...
最明显失败：...
是否站桩：...
Archetype 是否可辨识：...
动作数量 / 连续性：...
Camera：...
```

材料不全时基于已有证据分析，不让用户重复已经提供的信息。

---

## 7. 故障分流

### Round 1 仍然候选很少 / 同质

```text
→ Interactive Recommendation Breadth / Diversity Failure
→ 修 interactive-combat-policy / presentation
```

### 李小龙再次消失

```text
→ Archetype Candidate Coverage Failure
```

### 选了 Archetype 但 Library 没读

```text
→ Archetype Consumption Missing
→ 修 Mandatory Handoff / Runtime Read
```

### Library 读了但动作仍无 Archetype 特征

```text
→ Archetype-to-Stage-2 Weighting / Realization Failure
```

### Pattern 文件读了但无法给 Trace

```text
→ Stage-2 Routing Evidence Missing
```

### Movement 有词但不改变战斗状态

```text
→ Movement Causality Failure / Upper-body Dominance
```

### 动作具体但数量再次变少

```text
→ Granularity Over-expansion
→ 检查 Duration Budget / Two-pass / Density / Compression
```

### Prompt 正确但视频仍站桩 / 动作不足

```text
→ Generated-video Regression
→ 再检查 Model Capability / Adapter / Prompt Saturation
→ 不自动扩 Knowledge
```

---

## 8. 当前结束条件

下一轮不要以“增加多少规则”为完成标准。

完成标准：

```text
同场景重新 Regression
→ RF-01～RF-21 是否真实生效
→ 定位仍失败的具体 Layer
→ 只修该 Layer
```

如果 G01 已 PASS：

> **停止继续为“更完整”扩设计。进入真实视频生成 Regression。**
