# Action Combat Video V2 Implementation Plan

> 状态：**V2-01～34 初版实施已完成；V2-35～45 已完成 Traceability Re-baseline；Phase 11 Mandatory-path Rewire 已完成并通过静态接线；V2-46 Camera Coverage 横向修正已进入 Phase 12 实现与回归；V2-47 Interactive High-value Question Budget 已接入交互合同。**
>
> 设计真源：`docs/action-combat-video-v2-spec.md`
>
> Traceability Audit：`docs/action-combat-video-v2-traceability-audit.md`
>
> 回归真源：`docs/action-combat-video-v2-regression.md`
>
> 核心验收原则：**真实成片质量优先于静态规则覆盖；任何 Runtime 修改必须能从 Spec → Plan → Runtime → Regression 追踪。**

## 1. 实施目标

V2 不推翻 V1 Combat State / Continuity Engine，而是在 `action-combat-video` Task 内增强 Combat Choreography，并确保设计真正成为运行必经路径。

### Layer A｜Combat 设计质量

- Coverage 真正兑现；
- Action Phrase 足够丰富、连续、有因果；
- Character Identity 可见且不按职业 / 性别 / 年龄 / 外貌 / 体型模板化；
- Kinetic Scope 体现全身与空间运动；
- Contact / Environment / Signature Moment 有真实作用；
- 高手交换不是“一招一停 / 轮流出招”。

### Layer B｜Prompt 与 Camera 执行质量

- Final Prompt 由正向可见动作主导；
- 高密度 Combat 默认 Continuous Action Spine + Soft Time Anchors；
- Hard Timeline 不能成为 Neutral Reset；
- Camera Complexity 与 Camera Mobility 分离；
- **Action Continuity 与 Shot Continuity 分离；**
- Combat 可以动态使用 Master / Medium / Close-up / Extreme Close-up / Insert / Reaction / Impact / Re-establish；
- Cut 后必须继承 Position / Direction / Contact / Momentum / Axis / Range；
- Negative Constraint 少而有依据；
- Prompt Assembly + Final Preflight 是 Combat 必经出口。

### Layer C｜Interactive 与工程治理

- Spec → Plan → Runtime → Regression 可追踪；
- Failure Signature 不自动等于独立 Runtime 模块；
- 机制膨胀通过 Consolidation 控制；
- Prompt-level Gate 未通过时，不进入真实视频 Benchmark；
- **Interactive 追求高价值问题覆盖，而不是最少问题或固定轮数；**
- **默认最多 10 轮作为上限保护，需求一旦完整可执行即可提前收口。**

---

## 2. 总体实施顺序

```text
Phase 0–9  V2-01～34 初版设计 / 实现 / 静态回归
→ Phase 10 Spec / Traceability Re-baseline
→ Phase 11 Runtime Mandatory-path Rewire
→ Phase 12 Prompt-level G01 Regression + Camera Coverage Correction + Interactive Exposure Calibration
→ Phase 13 Generated Video Re-run + Model Calibration
```

原则：

> **先修接线，再修规则；先验证 Prompt，再判断是否需要增加知识或模型适配。**

---

## 3. Phase 0～9｜初版基线

已建立：

- Core / Choreography / Modern / Wuxia 职责；
- Coverage / Rhythm / Action Phrase / Exchange Depth；
- Character Identity / Tactical Interaction / Environment Affordance；
- Contact Solidity / Signature Moment；
- Action Execution Budget / Camera Readability；
- Two-stage Loading；
- Combat Choreography Profiles / Signature Patterns；
- Model Capability Contract；
- Diagnostics / Golden Scenarios。

第一次真实生成证明：**Static PASS 不能代替 Runtime 必经与真实成片质量。**

---

## 4. 实测反馈形成的设计增量

本轮增量从 **V2-35** 开始：

- V2-35 Combat Planning / Final Preflight Gate；
- V2-36 Combat Kinetic Scope；
- V2-37 Camera Mobility Coupling；
- V2-38 Temporal Action Packing；
- V2-39 Motion Handoff；
- V2-40 Continuous Action Spine + Soft Time Anchors；
- V2-41 Combat Intensity Curve；
- V2-42 Visible Advantage Dynamics；
- V2-43 Initiative Handoff；
- V2-44 Initiative × Character Identity；
- V2-45 Runtime Consolidation / Anti-overdesign；
- V2-46 Action Continuity ≠ Shot Continuity / Combat Camera Coverage；
- **V2-47 Interactive High-value Question Budget / 高价值问题预算。**

当前执行纪律：

- 暂停继续纵向新增 Combat 一级抽象机制；
- 动作本体一级机制暂时冻结；
- Failure Signature 主要服务 Gate / Diagnostic / Benchmark；
- V2-46 是 Camera 横向缺口修正，必须并入现有 Camera / Prompt 合同，不新建 Combat Camera Engine；
- V2-47 只调整 Interactive Decision Exposure / Stop Policy，不改变 Combat Planning Graph 和质量上限。

---

## 5. Phase 10｜Spec / Traceability Re-baseline — ✅ 完成

已完成：

```text
Spec Decision
→ Runtime Requirement
→ Affected Files
→ Implementation Strategy
→ Regression Evidence
```

并确认上一轮“先改 Runtime、后补 Plan”的流程错误已纠正。

---

## 6. Phase 11｜Runtime Mandatory-path Rewire — ✅ Static PASS

### 必经运行链

```text
Input / Task Routing
→ Combat Core
→ Combat Choreography
→ Specialist
→ Planning Gate
→ Stage-2 Execution Knowledge
→ Action Phrase / State Validation
→ Camera / Spatial / Motion Coordination
→ prompt-assembly/control.md
→ Combat-aware Final Prompt Assembly
→ Combat Final Preflight
→ FAIL: internal rewrite + recheck
→ PASS: Output Template / Model Serialization
→ Delivery
```

### 已完成

`SKILL.md`
- Prompt Assembly / Preflight 成为 Combat 必经；
- 不占普通 `0–3 Controls` Slot。

`references/tasks/action-combat-video/index.md`
- 明确 Final Assembly / Preflight 必经链。

`assets/templates/single-shot-video-template.md`
- Combat 不再因“15 秒 + 多阶段”自动切 Hard Timeline。

`assets/templates/mode-interactive-output-contract.md`
- 不提前问结局；
- Character Identity Recommendation Guard 禁止人口属性快捷映射。

`docs/action-combat-video-v2-regression.md`
- 增加 Prompt-level Regression。

---

## 7. Phase 12｜Prompt-level G01 Regression + Camera Coverage Correction + Interactive Exposure Calibration — 🚧 当前阶段

### Fixed Input

15 秒办公室，普通职场服装，中国男女，两人实际为敌对组织职业杀手，贴身搏斗，不隔办公桌。

### 已确认的第二轮结果

Mandatory Path 已生效：

- `prompt-assembly/control.md` 已实际读取；
- Hard Timeline 明显改善；
- Continuous Action Spine / Motion Handoff 明显改善。

新的 Prompt 同时暴露两个校准点：

1. Camera 横向问题：Action Continuity 被隐性实现成 Shot Continuity，Camera Coverage 收敛成“中全景 / 中景 + 低复杂度连续跟随”；
2. Interactive 轮数本身不是问题，关键是每一轮是否真的能减少高影响需求不确定性。

因此 Phase 12 同时验证 V2-46 与 V2-47。

### 7.1 V2-46 Runtime Mapping

#### A. `references/tasks/action-combat-video/choreography-playbook.md` — Modify

目标：

- 将 Camera 合同扩展为 `Readability + Mobility + Coverage`；
- 明确 `Action Continuity ≠ Shot Continuity`；
- Cut 后 Action State 必须连续；
- Preflight 拦截 `Combat Camera Coverage Lock` / `Cut-induced Action Reset`。

#### B. `references/controls/camera-direction/control.md` — Modify

目标：

- 动作可读性不等于全程完整身体可见；
- 支持 Master / Relationship / Close-up / Insert / Reaction / Impact / Re-establish；
- “主体动作强 → 镜头弱化”只表示降低 Camera Chaos，不表示禁止 Cut / Close-up；
- Cut 继承 Action Direction / Position / Contact / Momentum。

#### C. `references/controls/prompt-assembly/control.md` — Modify

目标：

- Action Spine 连续，但 Camera Coverage 可以通过 Cut 变化；
- Final Prompt 描述“为什么切、切到什么动作信息、如何继承状态”；
- 不默认一条 continuous tracking path；
- 不设置镜头数量配额。

#### D. `assets/templates/single-shot-video-template.md` — Modify

目标：

- 明确 `single-shot-video` = 单一视频生成单元 / 观看任务，不等于 one-take；
- Combat 未明确要求一镜到底时，可以内部 Cut；
- Cut 不得成为 Action Reset。

#### E. `docs/action-combat-video-v2-regression.md` — Modify

目标：

- G01 增加 Shot Scale / Editorial Coverage；
- 增加 Action Continuity Across Cuts；
- 增加 `Combat Camera Coverage Lock` / `Cut-induced Action Reset` Failure。

### 7.2 V2-47 Runtime Mapping

#### `assets/templates/mode-interactive-output-contract.md` — Modify

目标：

- Interactive 优化目标改为 `High-value Questions, Not Minimum Questions`；
- 不设置固定 4 / 6 轮完成标准；
- 默认最多 10 轮作为追问上限保护；
- 每轮继续前必须确认问题仍属于“用户未明确 + 系统无法高置信度代替 + 会显著改变成片”的真实分叉；
- 如果前 4–6 轮甚至更少已确认完整可执行需求，立即收口；
- 达到 10 轮后停止新增问题，剩余低风险 / 次要不确定项按推荐静默补全；
- 不允许为了走完整个 Planning Graph 而机械发问。

#### Regression 观察项

下一轮 G01 记录：

- 实际问题轮数；
- 每一轮对应的 Planning Node / 用户不确定性；
- 是否存在重复问题或低价值问卷；
- 最后一轮后是否已经具备完整可执行需求；
- 是否出现“需求已经清楚但仍继续发问”或“为了少问而跳过关键分叉”。

**轮数本身不作为 PASS / FAIL；问题价值与收口时机才是验收对象。**

### 7.3 本轮明确不改

- `combat-fighting-profiles/library.md`；
- `modern-combat-playbook.md`；
- `core-playbook.md`；
- Model Adapters；
- 新 Combat 动作一级机制。

原因：当前只验证 Camera 横向修正与 Interactive 暴露策略，保持控制变量。

### 7.4 Prompt-level Quality Contract

下一次 G01 必须至少满足：

- Setup 短，贴身 Combat 快速开始；
- Continuous Action Spine；
- 无默认 Hard Time Blocks；
- Motion Handoff；
- 不按人口属性推打法；
- Whole-body / Position / Range / Axis 可见；
- Camera 跟随 fight-space；
- Action Continuity 不被误解成 one-take；
- 允许有价值的 Contact / Footwork / Reaction / Impact / Weapon Close-up / Insert；
- 局部 Shot 后在需要时 Re-establish；
- Cut 后 Position / Direction / Contact / Momentum / Axis / Range 连续；
- 不把全程中全景 / 中景作为唯一安全默认；
- Negative 少而有依据；
- Ending 不提前吞掉 Active Exchange；
- **Interactive 每轮都必须对应真实高影响分叉，需求完整后及时收口。**

### 7.5 Phase 12 Gate

下一次相同办公室输入的 Interactive + Final Prompt 通过上述 Gate 后，才进入 Phase 13。

---

## 8. Phase 13｜Generated Video Re-run + Model Calibration

观察：

- Active Combat Coverage；
- Choreography Richness；
- Kinetic Scope；
- Temporal Packing / Motion Continuity；
- Camera Mobility；
- Shot Scale / Editorial Coverage；
- Action Continuity Across Cuts；
- Character Distinction；
- Visible Advantage / Initiative；
- Contact Solidity；
- Intensity / Signature；
- Spatial / Physical Continuity。

如果 Prompt-level 已正确但成片仍退化，优先：

```text
Concrete Choreography Knowledge
→ Model Temporal / Motion Capability
→ Model-specific Serialization
→ Camera / Action simultaneous capacity
```

而不是新增抽象机制。

---

## 9. Anti-overdesign / Consolidation

```text
Temporal / Continuity Flow Contract
→ Temporal Packing + Motion Handoff + Continuous Action Spine

Pressure / Control Choreography Check
→ Intensity + Visible Advantage + Initiative

Action Sufficiency
→ Coverage + Exchange Depth + Kinetic Scope

Camera Contract
→ Readability + Mobility + Editorial Coverage

Interactive Exposure Contract
→ High-value Question Filter + Dynamic Stop + 10-round Safety Cap
```

V2-46 不建设新 Camera Engine；V2-47 不建设新 Planning Graph，只修现有 Decision Exposure Policy。

---

## 10. Concrete Choreography Knowledge 审计（后续按证据进入）

只有 Phase 12 / 13 证明“接线 + Camera 已正确，但动作仍贫乏”时，才审计 Fighting / Martial / Weapon 是否缺乏可组合动作知识。

---

## 11. 当前实施状态

| Phase | 状态 | 说明 |
|---|---|---|
| 0–9 | ✅ 基线完成 | V2-01～34 |
| 10 | ✅ 完成 | Spec / Plan / Mapping 重新对齐 |
| 11 | ✅ Static PASS | Mandatory Assembly / Preflight / Template Override |
| 12 | 🚧 当前阶段 | V2-46 / V2-47 已实施，等待同一 G01 Interactive + Prompt 再测试 |
| 13 | ⏸ 待 Phase 12 | 真实视频重跑 / Model Calibration |

当前准确状态：

> **Mandatory-path Rewire Complete；V2-46 Camera Coverage + V2-47 Interactive Exposure Calibration Implemented；Prompt-level G01 Re-test Pending。**

## 12. 当前下一步

1. 使用完全相同办公室 G01 输入重新跑 Interactive；
2. 记录 Read 列表、实际问题轮数、每轮问题与推荐、Final Prompt；
3. 检查每一轮是否真的是高影响分叉，需求完整后是否及时收口；
4. 检查 Camera 是否不再固化成全程中全景；
5. 检查 Cut / Close-up / Insert 是否有动作信息价值且不破坏 Action Continuity；
6. Prompt-level PASS 后再生成真实视频。