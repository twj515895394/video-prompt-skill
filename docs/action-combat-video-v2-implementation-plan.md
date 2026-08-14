# Action Combat Video V2 Implementation Plan

> 状态：**V2-01～34 初版实施已完成；V2-35～当前实测反馈增量已进入 Traceability Rework。上一轮 Runtime 修改视为候选实现，必须经过本计划 Phase 10～12 重新验收。**
>
> 设计真源：`docs/action-combat-video-v2-spec.md`
>
> Traceability Audit：`docs/action-combat-video-v2-traceability-audit.md`
>
> 回归真源：`docs/action-combat-video-v2-regression.md`
>
> 核心验收原则：**真实成片质量优先于静态规则覆盖；但任何 Runtime 修改必须先能从 Spec 追踪到 Implementation Plan，再追踪到具体文件与 Regression。**

## 1. 实施目标

V2 不推翻 V1 Combat State / Continuity Engine，而是在 `action-combat-video` Task 内增强 Combat Choreography，并确保新增设计真正成为运行必经路径。

目标分三层：

### Layer A｜Combat 设计质量

- Coverage 真正兑现；
- Action Phrase 足够丰富、连续、有因果；
- Character Identity 可见且不按职业 / 性别 / 年龄 / 体型模板化；
- Kinetic Scope 能体现全身与空间运动；
- Contact / Environment / Signature Moment 有真实作用；
- 高手交换不是“一招一停 / 轮流出招”。

### Layer B｜Prompt 序列化与执行质量

- Final Prompt 由正向可见动作主导；
- 高密度 Combat 默认使用 Continuous Action Spine + Soft Time Anchors；
- Hard Timeline 不能成为 Neutral Reset；
- Camera Complexity 与 Camera Mobility 分离；
- Negative Constraint 少而有依据；
- Prompt Assembly + Final Preflight 成为 Combat 必经出口，而不是可选 Reference。

### Layer C｜工程治理

- Spec → Plan → Runtime → Regression 可追踪；
- Failure Signature 不自动等于独立 Runtime 模块；
- 机制膨胀必须通过 Consolidation 控制；
- 新规则必须证明能改变实际生成行为；
- Prompt-level Gate 未通过时，不直接进入真实视频 Benchmark。

---

## 2. 总体实施顺序

```text
Phase 0  V2-01～34 设计冻结与基线
→ Phase 1  Task 运行骨架
→ Phase 2  Choreography + Specialist
→ Phase 3  Combat Libraries
→ Phase 4  Final Prompt / Output Contracts
→ Phase 5  Model Capability
→ Phase 6  Diagnostics
→ Phase 7  Static Regression + Golden Framework
→ Phase 8  Generated Video Benchmark（第一轮暴露失败）
→ Phase 9  初版文档 / 索引收口

第一次真实反馈后新增：

→ Phase 10 Spec / Traceability Re-baseline
→ Phase 11 Runtime Mandatory-path Rewire
→ Phase 12 Prompt-level G01 Regression
→ Phase 13 Generated Video Re-run + Model Calibration
```

原则：

> **先修接线，再修规则；先验证 Prompt 是否执行 Spec，再判断是否需要增加新设计。**

---

## 3. Phase 0～9｜初版 V2 实施基线

Phase 0～9 对应 V2-01～34，已建立：

- Core / Choreography / Modern / Wuxia 文件职责；
- Active Combat Coverage / Rhythm / Action Phrase / Exchange Depth；
- Character Identity / Tactical Interaction / Environment Affordance；
- Contact Solidity / Signature Moment；
- Action Execution Budget + Action Sufficiency；
- Camera Readability / Combat Audio；
- Two-stage On-demand Loading；
- Combat Choreography Profile / Signature Pattern；
- Prompt Action-first / Positive-first；
- Model Combat Capability Contract；
- Combat Underfill / Contact Solidity Diagnostics；
- 8 个 Golden Scenario Framework。

### 历史状态说明

原 Implementation Plan 将 V2-01～34 的 Static Regression 标记 PASS。第一次和第二次真实运行证明：

> **“Reference 中存在规则”不等于“运行时必经并执行规则”。**

因此从 Phase 10 起，旧 Static PASS 不再覆盖新增 V2-35～当前反馈增量。

---

## 4. 第一次真实反馈形成的设计增量

本轮增量设计从 **V2-35** 开始：

- V2-35 Combat Planning / Final Preflight Gate；
- V2-36 Combat Kinetic Scope；
- V2-37 Camera Mobility Coupling；
- V2-38 Temporal Action Packing；
- V2-39 Combat Action Interlock / Motion Handoff；
- V2-40 Continuous Action Spine + Soft Time Anchors；
- V2-41 Combat Intensity Curve；
- V2-42 Visible Advantage Dynamics；
- V2-43 Initiative Handoff。

此外对话已确认：

- Initiative Handoff 的表现应受 Character Identity 约束，但不新增大型状态机；
- 暂停继续纵向细化 Combat 概念，进入横向 Design Tree Audit；
- 动作本体一级机制暂时冻结，重点转向 Concrete Choreography Knowledge；
- Runtime 实现采用 Consolidation，避免“一个失败现象 = 一个新模块”。

这些结论必须先写回 Spec，再执行 Phase 11。

---

## 5. Phase 10｜Spec / Traceability Re-baseline — 🚧 当前阶段

### 目标

重新建立：

```text
Spec Decision
→ Runtime Requirement
→ Affected Files
→ Implementation Strategy
→ Regression Evidence
```

### 输入

- `docs/action-combat-video-v2-spec.md`
- `docs/action-combat-video-v2-traceability-audit.md`
- 第一次真实视频反馈
- 第二次 Interactive → Final Prompt 失败样本

### 必做

1. 补齐 Spec 中已确认但尚未记录的后续决策；
2. 把 V2-35～当前确认点纳入正式 Implementation Mapping；
3. 逐文件标记：`Modify / Keep / No Change Required / Roll Back`；
4. 判断通用 Controls / Templates 是否会覆盖 Combat 专项规则；
5. 检查上一轮 5 个 Runtime 提交，禁止直接视为完成；
6. 明确 Prompt-level Regression Gate。

### Phase 10 Gate

只有以下条件都满足才能进入 Phase 11：

- Spec 与 Plan 没有已知遗漏；
- 每个新增设计至少有一个明确 Runtime 落点或明确 `No Runtime Change` 理由；
- 每个 Runtime 修改至少能追踪到 Spec；
- 已知模板冲突已经进入 File Mapping；
- 没有因为 Failure Signature 数量增加而计划创建同等数量独立模块。

---

## 6. Phase 11｜Runtime Mandatory-path Rewire

### 核心目标

解决当前最大根因：**Combat 可以读到 Choreography，却绕过 Final Prompt Assembly / Preflight。**

### 11.1 必经运行链

目标运行链必须明确为：

```text
Input / Task Routing
→ Combat Core
→ Combat Choreography
→ 1 Specialist
→ Planning Gate
→ Stage-2 Execution Knowledge
→ Action Phrase / State Validation
→ 必要 Camera / Spatial / Motion Coordination
→ Combat-aware Final Prompt Assembly
→ Combat Final Preflight
→ FAIL: 内部重写并重跑
→ PASS: Output Template / Model Serialization
→ Delivery
```

关键点：**Prompt Assembly / Final Preflight 是 Combat 必经出口，不再属于“可能不读的 0–3 Controls”。**

### 11.2 Affected Files

#### A. 必须修改

`SKILL.md`

- Combat 路由增加 mandatory final assembly / preflight；
- 不能让 `prompt-assembly` 继续完全依赖通用 0–3 Control 预算；
- Combat 输出前自查补 V2-35～43 的合并 Gate，而不是列几十个术语。

`references/tasks/action-combat-video/index.md`

- Runtime Structure 增加 Final Assembly / Preflight 强制出口；
- 输出模板只能承载结果，不能覆盖 Combat Choreography 的时间序列化规则。

`assets/templates/single-shot-video-template.md`

- 增加 Combat Override：高密度 Combat 不因“时长较长 + 3 个阶段”自动切绝对时间块；
- 如果 Combat Task 已提供 Continuous Action Spine，则模板必须继承；
- Hard Timeline 仅在用户 / Model / 同步需求明确时使用。

`docs/action-combat-video-v2-regression.md`

- 加入 Prompt-level G01 Gate；
- 第二次失败 Prompt 作为 Regression Evidence。

#### B. 保留但重新验收

`references/tasks/action-combat-video/choreography-playbook.md`

- 保留把 V2-35～43 收敛成少数 Runtime Contract 的方向；
- 检查是否存在重复概念 / Checklist 膨胀；
- 确保 Character Identity 不按体型直接模板化。

`references/controls/prompt-assembly/control.md`

- 当前 Continuous Action Spine / Soft Time Anchors / Kinetic Scope Externalization / Negative Discipline 方向保留；
- 重点解决“是否必读”，不是继续增加规则。

`assets/templates/mode-interactive-output-contract.md`

- 保留“不优先问谁赢”等修复；
- 增加 Decision Recommendation 不能偷偷把性别 / 年龄 / 体型转换成固定打法。

`references/diagnostics/combat-choreography-underfill/diagnostic.md`

- 保留集中式 Failure Signature；
- 不拆成多个新 Diagnostic。

#### C. 必须评估是否修改

`references/tasks/action-combat-video/modern-combat-playbook.md`

- Kinetic Scope / Camera Mobility / Continuous Phrase 的现代动作实现是否足够具体。

`references/libraries/combat-fighting-profiles/library.md`

- 当前更多是 Profile 概述；需要审计是否缺乏可组合 Concrete Choreography Knowledge。

`references/controls/camera-direction/control.md`

- 判断 `Stable ≠ Static` 是否需要通用化；若只服务 Combat，则不复制 Combat 正文。

`references/controls/timeline-rhythm/control.md`

- 判断是否存在 Hard Timeline 默认规则与 V2-40 冲突。

`references/controls/subject-motion/control.md`
`references/controls/spatial-blocking/control.md`

- 判断是否需要提供 Kinetic Scope 所依赖的通用全身 / 空间表达能力。

`references/models/generic.md`
`references/models/seedance-2.md`
`references/models/ltx-2-3.md`

- 模型序列化不得擅自把 Continuous Spine 重切成 Hard Timeline；
- Camera 降载优先降低 Complexity，不默认降低 Mobility。

#### D. 当前无证据修改

`core-playbook.md`

- 本次主要失败不是 Range / Advantage / Condition 真源本身；只有后续 Traceability 发现状态合同缺口才修改。

`cinematic-wuxia-playbook.md`

- 本次失败样本为 Modern Combat，不以单个现代样本修改 Wuxia。

### 11.3 Phase 11 Gate

Static Traceability 必须证明：

- 高密度 Combat 无法绕过 Prompt Assembly；
- single-shot template 无法覆盖 V2-40；
- Final Preflight 具有失败→重写→再检查路径；
- Runtime 没有新增不必要的独立概念系统。

---

## 7. Phase 12｜Prompt-level G01 Regression

真实视频生成前先执行 Prompt-level Gate。

### Fixed Input

15 秒办公室，普通职场服装，中国男女，两人实际为敌对组织职业杀手，贴身搏斗，不隔办公桌。

### Prompt-level Quality Contract

必须至少满足：

- Setup 很短，贴身 Combat 很快开始；
- 不默认从 2.5m 距离 + 1.5s 对峙起步；
- 高密度主体采用 Continuous Action Spine；
- 没有 5～6 个默认 Hard Time Blocks；
- Action Phrase 内有 Motion Handoff；
- 不以“男胖年长 = 力量抓控 / 女年轻漂亮 = 速度闪避”直接推导打法；
- Kinetic Scope 不被肩 / 前臂 / 手腕 / 抓控长期占领；
- Camera 跟随真实 Route / Range / Axis；
- Major Reversal 有可见 Advantage / Initiative 变化；
- Negative 不加入无依据的 no weapon / no gun 等限制；
- Ending 不提前停止主要交战。

### Prompt-level Failure Contract

出现任一高风险模式即 FAIL / REWRITE：

- `0–1.5 / 1.5–4 / 4–7 / 7–10 ...` 默认硬时间盒；
- 每一段只有一个宏动作；
- 长时间上肢架手 / 抓腕；
- 一方完成一段后另一方再开始；
- Camera 因“稳定”几乎不移动；
- 角色打法主要由性别 / 年龄 / 体型直接映射；
- 长 Negative 清单；
- Final Prompt 明显违反已经加载的 Choreography Contract。

### Gate

Prompt-level PASS 后才值得投入真实视频生成成本。

---

## 8. Phase 13｜Generated Video Re-run + Model Calibration

使用通过 Phase 12 的 G01 Prompt 重新生成真实视频。

观察：

- Active Combat Coverage Realization；
- Exchange / Choreography Richness；
- Kinetic Scope Realization；
- Temporal Packing Realization；
- Action Interlock / Motion Continuity；
- Camera Mobility Realization；
- Character Distinction；
- Visible Advantage / Initiative；
- Contact Solidity；
- Rhythm / Intensity Variation；
- Spatial / Physical Continuity。

如果 Prompt-level 已满足但视频仍退化，优先检查：

```text
Concrete Choreography Knowledge
→ Model Temporal / Motion Capability
→ Model-specific Serialization
→ Camera / Action simultaneous capacity
```

而不是继续新增 Combat 一级抽象机制。

---

## 9. Anti-overdesign / Consolidation 实施原则

从 Phase 10 起正式采用：

> **Mechanisms may be many in Spec; Runtime concepts must stay few.**

执行规则：

- V2-38 Temporal Packing、V2-39 Motion Handoff、V2-40 Continuous Spine 可共同归入 `Temporal / Continuity Flow Contract`；
- V2-41 Intensity、V2-42 Visible Advantage、V2-43 Initiative 可作为 Choreography 的压力 / 控制子检查，不建设三套新引擎；
- Failure Signature 主要服务 Preflight / Diagnostic / Benchmark；
- 新术语只有在它改变规划或输出行为时才值得留在 Runtime；
- 角色打法差异最终要落到 Concrete Action Selection，而不是越来越多 Meta 状态。

---

## 10. Concrete Choreography Knowledge 审计（Phase 13 后优先）

动作本体一级机制暂时冻结。

重点审计：

```text
Fighting / Martial / Weapon Profile
→ 是否只描述风格倾向
→ 是否能提供可组合动作构造知识
→ 是否覆盖 Whole-body / Footwork / Range / Transition / Defense / Counter / Grapple / Environment
→ 是否能生成多种 Action Phrase，而不是反复抓腕 / 前臂格挡 / 推墙
```

该工作只有在 Phase 12 / 13 证明“接线已正确但具体动作仍差”时进入，避免把架构接线问题误诊为知识库不足。

---

## 11. 当前实施状态

| Phase | 状态 | 说明 |
|---|---|---|
| 0–7 | ✅ 初版完成 | 对应 V2-01～34 |
| 8 | ⚠️ 已产生真实失败反馈 | 证明旧 Static PASS 不足 |
| 9 | ✅ 初版收口 | 仅代表当时仓库状态 |
| 10 | 🚧 进行中 | Spec / Plan / File Mapping / Regression 重新对齐 |
| 11 | ⏸ 待 Phase 10 | Runtime Mandatory-path Rewire |
| 12 | ⏸ 待 Phase 11 | Prompt-level G01 Regression |
| 13 | ⏸ 待 Phase 12 | 真实视频重跑 / Model Calibration |

当前不能再使用：

> `Implementation Complete + Static Regression PASS + Generated Video Validation Pending`

作为完整状态描述。

当前准确状态是：

> **Post-feedback Traceability Rework In Progress；上一轮 Runtime 实现尚未完成正式一致性验收。**

## 12. 当前下一步

1. 完成 Spec 已确认遗漏项收口；
2. 按 `action-combat-video-v2-traceability-audit.md` 完成 Phase 10 File Mapping；
3. 进入 Phase 11 修强制运行链；
4. Phase 12 用同一办公室输入重新跑 Prompt；
5. Prompt-level PASS 后再生成真实视频。
