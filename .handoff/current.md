# Video Prompt Skill — Action Combat Regression Fix Handoff

> 更新时间：2026-08-15 21:52（UTC+8）  
> 仓库：`twj515895394/video-prompt-skill`  
> 分支：`main`  
> 当前阶段：**RF-22 一级 Direct READ 已能真实命中，但最新真实测试暴露 Early Direct Read：Runtime Policy 在 Camera / Physical Presentation 尚未 resolved 前被提前读取。已按确认方案 A 完成 Interactive Planning Completion Gate 最小修复；下一步重新从完全相同 G01 Run 1 开始，目标连续两次 PASS-NATIVE。**

---

## 0. 新会话接管指令

新会话优先读取：

1. `.handoff/current.md`
2. `docs/action-combat-video-regression-fix-spec.md`
3. `SKILL.md` 中 `Action Combat Post-Planning Mandatory Path`
4. `references/tasks/action-combat-video/interactive-combat-policy.md`
5. `references/tasks/action-combat-video/regression-fix-runtime-policy.md`
6. 如需核对 Stage-2，再读 `references/libraries/combat-choreography-patterns/minimum-validation-set.md`

**不要重新 Grill RF-01～RF-22。不要顺手修 Archetype UX、Compression、Dedup、Quick Mode、Camera 或扩 Combat Knowledge。**

当前唯一主任务：

> **使用完全相同的固定 G01 输入与选择，从 Run 1 重新开始，验证 RF-22 是否连续两次 PASS-NATIVE；每次有效执行再检查 RF-14～RF-20。**

核心原则：

> **Routing First, Knowledge Second.**  
> **Regression → Failure Layer → Minimal Fix → Regression Again.**  
> **Prompt PASS ≠ Generated Video PASS。**

---

## 1. 已知前史

### 1.1 第二轮真实 G01 已确认的改善

此前真实测试已经证明：

- Round 1 已出现约 7 个高价值 Pairing + 自定义，Recommendation Breadth 明显改善；
- Hybrid 选择后没有机械追加门派问卷；
- Round 2 Expression 已有真实 A/B/C + 自定义；
- 五种基础 Archetype 文本上均能出现；
- Movement Causality 明显改善：斜切 / 转轴 / 重落脚会真实改变下一战斗 State；
- Per-Character Signature 可区分；
- Ending 不再默认塌成抓腕 / 锁臂 / 压墙模板；
- Camera Handoff 基本保持正常。

### 1.2 第二轮核心失败：Runtime Policy 完全漏读

当时实际 Read List 没有：

`references/tasks/action-combat-video/regression-fix-runtime-policy.md`

尽管旧 `interactive-combat-policy.md` 写了 Mandatory Read。

因此定位为：

> **RF-22 — Post-Planning Runtime Handoff Reliability / Routing Failure**

随后已完成第一版 RF-22：把 Runtime Policy 提升到 `SKILL.md` 一级 Direct READ，并增加 Read Evidence / Recovery。

---

## 2. 最新真实测试：Early Direct Read Failure

用户在 RF-22 第一版实施后再次运行真实 Interactive G01。最新测试有一个重要进展：

> `regression-fix-runtime-policy.md` **这次确实被真实 READ 了。**

但实际时序是：

```text
Round 1
→ Round 2
→ Ending A
→ READ regression-fix-runtime-policy.md
→ Camera 问题
→ Camera 选择 B
→ Stage-2 / Camera / Assembly
→ Final Prompt
```

也就是说：

- Runtime Policy 不再“完全漏读”；
- 但它在 **Camera Base Viewing Priority 尚未 resolved** 时已经读取；
- `Physical Presentation Domain / Physical Scale` 本次也没有完成固定 G01 的选择；
- 因此 `Interactive Planning Complete` 被过早判定。

按照 RF-22 既有合同：Runtime Policy 必须在所有当前高价值 Interactive 决策完成后、任何 Post-Planning 派生之前读取。

因此本次正式定性：

> **RF-22 FAIL — Early Direct Read / Interactive Planning Completion Gate Failure**

这不是 Knowledge Failure，也不是 RF-14～RF-20 正文失败导致的 Routing 问题。

---

## 3. 本次 Regression 为什么不能计入 ×2 Close Criteria

本次测试除了 Early Read 外，还不是固定 G01 的完全相同选择：

固定 Regression 要求：

```text
Round 1 = A
Round 2 Expression = A
Archetype = none
Ending = A
Camera = A
Physical Scale = A
```

本次实际：

```text
Round 1 = A
Round 2 Expression = A
Archetype = none（由当前执行解析）
Ending = A
Camera = B
Physical Scale = 未完成
```

所以即使没有 Early Read，本次也不能作为 RF-22 Close Criteria 的 Run 1。

记录方式：

```text
Regression validity for RF-22 close count:
INVALID

Useful failure evidence:
YES

Observed failure:
Early Direct Read before all high-value Interactive decisions were resolved
```

下一轮必须从 **Run 1 重新开始计数**。

---

## 4. 最新测试中其他 RF 的观察结果

这些只是观察证据，**当前不允许据此顺手修改其他 Runtime**。

### 保持改善

- **RF-11 Per-Character Signature：PASS 倾向强**
  - 女方：斜切 / 转轴 / 角度 / 低位 / 后发反制；
  - 男方：直线压迫 / 拳击进入 / 抱控 / 体重推进 / 再进入。

- **RF-12 Ending Compatibility：PASS 倾向强**
  - Ending 没有偷换成新的 dominant grappling technique；
  - 女方依靠外侧角度 / 截击 / 退出获得阶段性优势。

- **RF-13 Movement Causality：PASS 倾向强**
  - Movement 会改变 Route / Support / Axis / Position，并迫使对手产生新的即时响应。

- **RF-21 Camera Runtime：保持 Freeze**
  - 本次 Camera Handoff 没有新失败证据，不重新打开 Camera Runtime。

### 仍暴露的问题

- **RF-14 Stage-2 Traceability：UNPROVEN**
  - 仅看到读取 `minimum-validation-set.md`，不足以证明完整 `Gap → Slot → Pattern → leaf → Detail → Concrete Phrase` Trace。

- **RF-15 Granularity Over-expansion：仍偏 FAIL**
  - 普通 Exchange 仍大量被展开为高细节大段。

- **RF-16 Exchange Density / Distribution：PARTIAL / 偏 FAIL**
  - 比旧版更丰富，但仍有少量“大动作盒”占据过多 15 秒信息预算的倾向。

- **RF-17 Concrete Compression：明确 FAIL**
  - Final Prompt 出现类似：
    - `短促掌击或前臂`
    - `低线踢或脚部干扰`
  - Runtime 把 A/B 未决选择留给视频模型，违反 RF-17。

- **RF-18 Duration-aware Planning：UNPROVEN**

- **RF-19 Two-pass Choreography：结果结构改善，但 Runtime Evidence UNPROVEN**

- **RF-20 Serialization Dedup：PARTIAL / 偏 FAIL**
  - Final Prompt 尾部仍重复若干前文已表达的支撑 / 重量 / Reset / 遮挡等控制意图。

**这些问题先记录，不改。必须先把 RF-22 Routing 重新证明稳定。**

---

## 5. RF-22 当前设计与职责

正式编号：

> **RF-22 — Post-Planning Runtime Handoff Reliability**

设计真源仍是：

`docs/action-combat-video-regression-fix-spec.md`

当前职责：

```text
SKILL.md
= 一级 Routing Truth
= Interactive Planning Completion Gate
+ Direct READ
+ Read Evidence Gate
+ Recovery

interactive-combat-policy.md
= Upstream Boundary
= 负责 Interactive 角色级决策与移交边界
= 不承担真正 Loader

regression-fix-runtime-policy.md
= RF-08～RF-20 Runtime Truth
= 不负责证明自己有没有被加载
```

### RF-22 正确时序

```text
所有当前高价值 Interactive 决策 resolved
→ Interactive Planning Completion Gate PASS
→ Interactive Planning Complete
→ READ regression-fix-runtime-policy.md
→ RF-22 Read Evidence Gate
→ Confirmed Planning Context
→ Derived Choreography
→ Duration Budget / Exchange Spine
→ Stage-2
→ Camera / Assembly / Adapter / Final Preflight
```

### Early Read 定义

```text
Runtime Policy READ
发生在 Completion Gate PASS 之前
→ Early Direct Read
→ RF-22 FAIL
→ 该 READ 不算有效 RF-22 Evidence
→ 本执行不得计入连续 PASS-NATIVE 关闭计数
```

---

## 6. 方案 A：Interactive Planning Completion Gate — 已确认并实施

用户已明确确认：**A**。

目标不是建立复杂状态机，也不是新增问卷，而是把原来过软的：

> `所有高价值 Interactive 决策完成`

变成一个可执行 predicate。

`SKILL.md` Direct READ 前现在至少检查：

```text
Combat System / required Refinement resolved?
Character Combat Expression resolved?
optional Cinematic Combat Archetype resolved as selected / inherited / none?
Advantage / Ending resolved?
Camera Base Viewing Priority resolved?
Camera Hard Constraint resolved when user-specified or high-value ambiguous?
Physical Presentation Domain resolved?
```

语义：

- `resolved` 不等于每项都必须增加一轮问题；
- 继续允许 Known → Refine、高置信度继承、合法默认、none 与条件暴露；
- Gate 只阻止 unresolved 高价值项被误判为 Planning Complete；
- 任一 unresolved 时：**DO NOT READ Runtime Policy**，继续 Interactive；
- 全部 resolved 后才允许 Direct READ。

### 本次实施 Commit

`SKILL.md`

Commit：

`f465e4b61f9cc9aed7de73183001969a206b13bd`

Commit message：

`fix: gate RF-22 runtime read on completed interactive planning`

该提交同时增加：

- Completion Gate；
- Early Direct Read 明确定义；
- Early Read 不算有效 Evidence；
- Regression / Debug 可观察 `Planning Completion Gate` 与 `Runtime Policy Read Timing`；
- `PASS-NATIVE` 明确要求 READ 发生在 Completion Gate PASS 之后；
- 严禁在 Completion Gate PASS 前读取 Runtime Policy。

### 明确没有修改

本次没有修改：

- `regression-fix-runtime-policy.md` RF-08～RF-20 正文；
- `action-camera-handoff-playbook.md`；
- Archetype Library；
- Stage-2 Knowledge；
- Quick Mode；
- Round 2 Archetype Selection UX；
- Concrete Compression / Dedup 规则正文；
- Camera Runtime。

这是故意的 Minimal Fix。

---

## 7. RF-22 Result States

### PASS-NATIVE

```text
Completion Gate PASS
→ 一级 Direct READ 首次正常命中
→ READ 发生在任何 Post-Planning 派生之前
→ 未触发 Recovery
```

### PASS-RECOVERED

```text
Completion Gate PASS
→ 一级 Direct READ 漏掉
→ Handoff Gate 捕获
→ 自动补读
→ 污染的 Post-Planning 派生全部作废
→ 从 Confirmed Interactive Planning Context 重启
```

### FAIL

任一成立：

- **Early Direct Read：Completion Gate PASS 前就读取 Runtime Policy；**
- 没有真实 READ；
- 漏读后未被 Gate 捕获；
- 补读但未作废旧派生结果；
- 已进入 Final Assembly 后才补救；
- Recovery 没有从正确入口重新执行。

### Close Criteria

只有：

> **完全相同 G01，连续 2 次 PASS-NATIVE**

才关闭 RF-22。

`PASS-RECOVERED` 可以继续检查同一次执行的 RF-14～RF-20，但不能用于关闭 RF-22。

---

## 8. 下一轮固定 G01

必须完全复用以下测试，不加入 Archetype Variant。

原始需求：

- 15 秒；
- 中国现代办公室；
- 22 岁中国女性，长发高马尾，漂亮，正常职场服装；
- 55 岁中国男性领导，矮胖、秃顶，正常职场服装；
- 两人分别是敌对杀手组织的职业杀手；
- 徒手贴身近战；
- 不隔办公桌 / 大型障碍物；
- Interactive Mode；
- 无枪械刀具。

固定选择：

```text
Round 1
A｜女：中国功夫电影混合体系
   男：摔跤 / 擒抱体系

Round 2 Expression
A｜女冷静诱导 / 后发反制
   男主动压迫 / 持续再进入

Archetype
不额外指定 / none

Ending
A｜女方完成反制并取得脱身主动

Camera
A｜完整动作可读 + 电影冲击平衡

Physical Scale
A｜写实电影尺度、无威亚无超自然
```

目标是隔离 RF-22 Routing 变量，不重新测试 Archetype UX。

---

## 9. 下一轮固定检查顺序

### Phase 1 — RF-22 Run 1

必须检查：

```text
Planning Completion Gate
→ 是否在 Camera / Physical Presentation 等当前高价值项 resolved 后才 PASS？

Runtime Policy Read Timing
→ 是否发生在 Completion Gate PASS 后？

Post-Planning
→ 是否在 Runtime Read / Evidence Gate 之后才开始？
```

判：

`PASS-NATIVE / PASS-RECOVERED / FAIL`

如果 Run 1 不是 PASS-NATIVE，则连续 Native 计数仍为 0。

### Phase 2 — 同一 Run 1 检查 RF-14～RF-20

仅当 Run 1 是 PASS-NATIVE 或完整 PASS-RECOVERED，继续：

1. RF-14 Stage-2 Traceability；
2. RF-15 Granularity Over-expansion；
3. RF-16 Exchange Density / Granularity Distribution；
4. RF-17 Concrete Compression；
5. RF-18 Duration-aware Planning；
6. RF-19 Two-pass Choreography；
7. RF-20 Serialization Deduplication。

同时观察 RF-11 / RF-12 / RF-13 / RF-21 是否保持改善。

### Phase 3 — RF-22 Run 2

完全相同输入与选择再次运行。

```text
Run 1 PASS-NATIVE
+
Run 2 PASS-NATIVE
→ RF-22 CLOSED
```

任一 Run 为 PASS-RECOVERED / FAIL：

```text
RF-22 保持 OPEN
连续 PASS-NATIVE 计数重新开始
```

### Phase 4 — G01-Archetype Variant

只有普通 G01 Prompt-level Runtime 通过后，再单独增加 Archetype Variant，验证：

- RF-08 Archetype Mandatory Consumption；
- RF-09 Archetype-to-Stage-2 Weighting；
- RF-10 Archetype Realization。

### Phase 5 — Generated-video Regression

只有 Prompt-level 全部 PASS 后才生成真实视频。

如果 Prompt PASS 但成片 FAIL：

> 进入 Model Capability / Prompt Saturation / Adapter / Generated-video Regression，不继续扩 Prompt 架构。

---

## 10. 当前禁止做的事情

在新的同一 G01 ×2 结果出来前，不要：

- 再 Grill RF-22；
- 顺手修 Round 2 Archetype Selection / 单轮多问题 UX；
- 顺手修改 Concrete Compression / Dedup 规则正文；
- 把 RF-22 迁移到 Quick；
- 扩完整中国武术百科；
- 建明星独立 Engine / 固定 Combo；
- 建 Lower-body / Body Method Engine；
- 修改 Camera Runtime；
- 使用固定动作数 / Exchange 数 / 腿法次数 / 换位次数；
- 把 Exchange Spine 固化成模板。

---

## 11. 下一会话完成条件

下一会话不再继续加规则，目标是拿到新的真实 Regression：

```text
完全相同 G01 Run 1
→ Completion Gate Evidence
→ Runtime Read Timing Evidence
→ RF-22 Result
→ 若有效，再检查 RF-14～RF-20

完全相同 G01 Run 2
→ RF-22 Result
→ 是否达到连续 2 次 PASS-NATIVE
```

理想结果：

> **Completion Gate 正确阻止 Early Read → RF-22 PASS-NATIVE ×2 → 关闭 RF-22 → 保留同一结果继续评价 RF-14～RF-20。**

最终口令：

> **先证明 Interactive 真正完成，再读取 Runtime；先证明 Runtime 真正被正确加载，再评价 Runtime 里面的规则。**