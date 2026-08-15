# Video Prompt Skill — Action Combat Regression Fix Handoff

> 更新时间：2026-08-15 21:29（UTC+8）  
> 仓库：`twj515895394/video-prompt-skill`  
> 分支：`main`  
> 当前阶段：**第二轮真实 G01 Regression 已完成分析；RF-22 Post-Planning Runtime Handoff Reliability 已确认并完成 Runtime 实施，下一步只做同一 G01 的双次 Routing Regression。**

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

> **用完全相同的第二轮 G01 输入与选择，验证 RF-22 是否连续两次 PASS-NATIVE；然后在同一执行结果中检查 RF-14～RF-20。**

核心原则：

> **Routing First, Knowledge Second.**  
> **Regression → Failure Layer → Minimal Fix → Regression Again.**  
> **Prompt PASS ≠ Generated Video PASS。**

---

## 1. 第二轮真实 G01 新证据

用户提供的第二轮测试已经证明：

### 明显改善

- Round 1 已出现 7 个 Pairing + 自定义，Recommendation Breadth 比上一轮明显改善；
- Hybrid 选择后没有机械追加门派问卷；
- Round 2 Expression 已有 A/B/C + 自定义；
- 五种基础 Archetype 文本上均出现；
- Movement Causality 明显改善：斜切 / 转轴 / 重落脚等真实改变下一战斗 State；
- Per-Character Signature 可区分；
- Ending 没有再次塌成抓腕 / 锁臂 / 压墙模板；
- Camera Handoff 基本保持正常。

### 核心新失败

实际 Read List **没有**：

`references/tasks/action-combat-video/regression-fix-runtime-policy.md`

尽管旧 `interactive-combat-policy.md` 已经写了 Mandatory Read。

因此第二轮主 Failure Layer 定位为：

> **Post-Planning Runtime Handoff Reliability / Routing Failure**

这会导致 RF-14～RF-20 的 Runtime 修复无法证明真正执行：

- Stage-2 Traceability 仍 FAIL；
- 15 秒仍约 3 个大 Exchange + Ending；
- Granularity Over-expansion 仍明显；
- Concrete Compression 仍出现“低线腿法”“A 或 B”式未决表达；
- Serialization Dedup 仍有重复。

当前证据不支持扩知识库。

---

## 2. RF-22 — 已确认设计

正式编号：

> **RF-22 — Post-Planning Runtime Handoff Reliability**

完整合同以：

`docs/action-combat-video-regression-fix-spec.md`

为设计真源。

17 项 Grill 决策已全部记录进 Spec。核心结论：

### Routing Truth

```text
SKILL.md
= 一级 Routing Truth
= Direct READ + Read Evidence Gate + Recovery

interactive-combat-policy.md
= Upstream Boundary
= 只负责 Interactive 决策和移交边界

regression-fix-runtime-policy.md
= RF-08～RF-20 Runtime Truth
= 不负责证明自己是否被加载
```

### Direct Read Timing

所有高价值 Interactive Combat 决策完成后，在任何 Post-Planning 派生之前：

```text
Interactive Planning Complete
→ READ regression-fix-runtime-policy.md
→ RF-22 Read Evidence Gate
→ Confirmed Planning Context
→ Derived Choreography / Duration / Exchange Spine / Stage-2...
```

### Read Evidence

唯一有效 Evidence：

> **当前这一次任务执行中真实发生的文件 READ。**

以下不算：

- 上游文本引用；
- Policy 写了 MUST READ；
- 模型声称遵循；
- Final Prompt 看起来符合；
- 历史执行读过。

### Recovery

如果 Gate 发现漏读：

```text
Missing Read
→ 立即 READ Runtime Policy
→ invalidate 全部 Post-Planning 派生结果
→ 只保留 Confirmed Interactive Planning Context
→ 从 Post-Planning 入口重新执行
```

禁止在旧 Runtime 产生的 Exchange Spine / Stage-2 / Action Phrase 上打补丁。

### Visibility

```text
Production
= Silent Recovery

Regression / Debug
= 可观察 PASS-NATIVE / PASS-RECOVERED / FAIL
```

### Result

```text
PASS-NATIVE
= 一级 Direct READ 首次正常命中，未触发 Recovery

PASS-RECOVERED
= 一级漏读，但 Gate 捕获并完整作废 / 重启

FAIL
= 未读 / 未捕获 / 未作废 / 太晚补救 / 重启点错误
```

### Close Criteria

RF-22 只有：

> **完全相同 G01 连续 2 次 PASS-NATIVE**

才关闭。

`PASS-RECOVERED` 可以继续检查下游 RF-14～RF-20，但 RF-22 保持 OPEN。

---

## 3. RF-22 已实施内容

### 3.1 Spec

文件：

`docs/action-combat-video-regression-fix-spec.md`

Commit：

`d2a503a127064ba6ee2433f316c5a1ff726a9a26`

已增加：

- RF-22 Failure Evidence；
- Scope；
- Routing / Runtime Truth；
- Direct Read Timing；
- Read Evidence Gate；
- Missing Read Recovery；
- Production / Debug Visibility；
- PASS-NATIVE / PASS-RECOVERED / FAIL；
- 连续 2 次 Native Close Criteria；
- 17 项已确认 Grill 决策；
- 后续固定 Regression 顺序。

### 3.2 SKILL.md

Commit：

`b06f57061394f59b36ffdae49b1e94c448db2bac`

已把 `regression-fix-runtime-policy.md` 提升为 Interactive Post-Planning 一级 Direct READ。

主链变为：

```text
Interactive Planning Complete
→ READ regression-fix-runtime-policy.md
→ RF-22 Runtime Handoff Read Evidence Gate
→ Confirmed Per-Character Combat Context
→ Derived Choreography Direction
→ Duration-aware Budget / Exchange Spine
→ Stage-2
→ Camera / Assembly / Adapter / Final Preflight
```

并已加入：

- 当前执行真实 Read Evidence 要求；
- Missing Read 自动补读；
- 全部 Post-Planning 派生结果 invalidation；
- 从 Confirmed Interactive Planning Context 重启；
- Production Silent Recovery；
- Regression Debug Result；
- RF-22 仅 Interactive Scope；
- Quick Mode 不修改。

### 3.3 Interactive Policy

文件：

`references/tasks/action-combat-video/interactive-combat-policy.md`

Commit：

`9bf31595e0fb53bce4b0b19374729ca176c9d705`

已取消它承担真正 transitive Loader 的职责。

现在只声明：

```text
Interactive Planning Context complete
→ hand off to SKILL.md Post-Planning Mandatory Path
→ SKILL.md Direct READ Runtime Policy
→ RF-22 Gate
```

没有在 Interactive Policy 中建立第二套 Recovery Runtime。

### 3.4 明确未修改

本批没有修改：

- `references/tasks/action-combat-video/regression-fix-runtime-policy.md` 的 RF-08～RF-20 正文；
- `references/tasks/action-combat-video/action-camera-handoff-playbook.md`；
- Archetype Library；
- Stage-2 Knowledge；
- Quick Mode；
- Round 2 Archetype Selection UX；
- Concrete Compression / Dedup 规则正文。

这是故意的 Minimal Fix。

---

## 4. 下一轮固定 G01

下一轮必须**完全复用这次第二轮测试**，不要加入 Archetype Variant。

原始需求仍为：

- 15 秒；
- 中国现代办公室；
- 22 岁中国女性，长发高马尾，漂亮，正常职场服装；
- 55 岁中国男性领导，矮胖、秃顶，正常职场服装；
- 两人分别是敌对杀手组织的职业杀手；
- 徒手贴身近战；
- 不隔办公桌 / 大型障碍物；
- Interactive Mode；
- 无枪械刀具。

第二轮实际选择固定复用：

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

目标不是重新测试 Archetype，而是隔离 RF-22 Routing 变量。

---

## 5. 下一轮检查顺序

### Phase 1 — RF-22

Run 1：

- Runtime Policy 是否在任何 Post-Planning 派生前真实 READ；
- 是否 `PASS-NATIVE / PASS-RECOVERED / FAIL`。

Run 2：

- 完全相同输入与选择；
- 再判 RF-22。

关闭要求：

```text
PASS-NATIVE
+
PASS-NATIVE
→ RF-22 CLOSED
```

### Phase 2 — 同一 G01 检查 RF-14～RF-20

只要该执行为 `PASS-NATIVE` 或完整 `PASS-RECOVERED`，继续检查：

1. RF-14 Stage-2 Traceability；
2. RF-15 Granularity Over-expansion；
3. RF-16 Exchange Density / Granularity Distribution；
4. RF-17 Concrete Compression；
5. RF-18 Duration-aware Planning；
6. RF-19 Two-pass Choreography；
7. RF-20 Serialization Deduplication。

同时观察 RF-11 / RF-12 / RF-13 / RF-21 是否保持上一轮改善。

### Phase 3 — G01-Archetype Variant

只有普通 G01 Prompt-level Runtime 通过后，再单独增加 Archetype Variant，验证：

- RF-08 Archetype Mandatory Consumption；
- RF-09 Archetype-to-Stage-2 Weighting；
- RF-10 Archetype Realization。

### Phase 4 — Generated-video Regression

只有 Prompt-level 全部 PASS 后才生成真实视频。

如果 Prompt PASS 但成片 FAIL：

> 进入 Model Capability / Prompt Saturation / Adapter / Generated-video Regression，不继续扩 Prompt 架构。

---

## 6. 当前禁止做的事情

在新的同一 G01 ×2 结果出来前，不要：

- 再 Grill RF-22；
- 顺手修 Archetype Selection Affordance；
- 顺手修改 Compression / Dedup 规则正文；
- 把 RF-22 迁移到 Quick；
- 扩完整中国武术百科；
- 建明星独立 Engine / 固定 Combo；
- 建 Lower-body / Body Method Engine；
- 修改 Camera Runtime；
- 使用固定动作数 / Exchange 数 / 腿法次数 / 换位次数；
- 把 Exchange Spine 固化成模板。

---

## 7. 下一会话完成条件

下一会话的完成标准不是继续加规则，而是拿到真实结果：

```text
完全相同 G01 Run 1
→ RF-22 Result
→ RF-14～RF-20 Result

完全相同 G01 Run 2
→ RF-22 Result
→ 是否达到连续 2 次 PASS-NATIVE
```

理想结果：

> **RF-22 PASS-NATIVE ×2 → 关闭 RF-22 → 保留同一结果继续检查 RF-14～RF-20。**

最终口令：

> **先证明 Runtime 真正被加载，再评价 Runtime 里面的规则。**
