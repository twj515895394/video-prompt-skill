# Action Combat Video V2 Implementation Plan

> 状态：**仓库侧 Phase 0–7、Phase 9 已完成；Phase 8 真实成片质量回归待外部视频生成端执行**
>
> 设计真源：`docs/action-combat-video-v2-spec.md`
>
> 回归真源：`docs/action-combat-video-v2-regression.md`
>
> V1 基线：`docs/action-combat-video-spec.md` / `docs/action-combat-video-implementation-plan.md`
>
> 核心验收原则：**真实成片质量优先于静态规则覆盖；静态正确只是必要条件。**

## 1. 实施目标

V2 不推翻 V1 的 Combat State / Continuity Engine，而是在同一个 `action-combat-video` Task 内正式落地 **Combat Choreography Engine / 动作编排引擎**。

目标：

- Combat Coverage 真正兑现，而不是 Timeline 写满但实际不打；
- 有效攻防足够丰富、连续、有因果；
- Combat Character Identity 能从动作看出差异；
- Environment 真正改变战术 / 空间；
- Strike / Grapple / Throw / Weapon / Environment Contact 有可信 Solidity；
- 少量 Signature Moment 真正形成视觉记忆；
- Camera / Audio 服务动作可读性、节奏和实感；
- Final Prompt 由正向可见动作语言主导；
- Quick / Interactive 共用同一 Combat Planning Graph；
- Model Combat Capability 只反馈执行路径，不偷改导演意图；
- 回归升级为 Static + Generated Video Quality 双层体系。

实施总原则：

> **Core 负责“打得对、接得上”；Choreography 负责“打得够、丰富、好看、有实感”；专项 Playbook 负责“这种战斗具体怎么表现”。**
>
> **Clarity Through Structure, Not Action Reduction.**
>
> **State Machine Internalized, Choreography Externalized.**

---

## 2. 分批顺序

```text
Phase 0 设计冻结与基线
→ Phase 1 Task 运行骨架
→ Phase 2 Choreography Engine 与专项 Playbook
→ Phase 3 Combat Libraries
→ Phase 4 Final Prompt / Output Contracts
→ Phase 5 Model Capability Contract
→ Phase 6 Diagnostics
→ Phase 7 Static Regression + Golden Benchmark Framework
→ Phase 8 Generated Video Quality Benchmark
→ Phase 9 文档 / 索引收口
```

每阶段原则：独立职责、独立 Gate、可定位回归；不为“模块化”复制正文，不重新引入固定动作数量模板或职业 → 固定打法映射。

---

## 3. Phase 0｜设计冻结与基线 — ✅ 完成

### 产物

- `docs/action-combat-video-v2-spec.md`
- `docs/action-combat-video-v2-implementation-plan.md`

### 已完成

- V2-01 ～ V2-34 一级设计全部确认；
- Combat Choreography Engine 确认属于 `action-combat-video` Task；
- 确认新增 `choreography-playbook.md`；
- 不新增 Combat Choreography 全局 Control；
- 确认 Static + Generated Video Quality 双层回归；
- Golden Scenario 采用 `Fixed Input + Quality Contract + Failure Contract + Optional Test Anchor`。

### Gate

一级设计树已冻结；实现期只允许为落地 / 回归做局部校正。

---

## 4. Phase 1｜Task 运行骨架 — ✅ 完成

### 文件

```text
references/tasks/action-combat-video/index.md
references/tasks/action-combat-video/core-playbook.md
references/tasks/action-combat-video/choreography-playbook.md
SKILL.md
```

### 已完成

- 新增 `choreography-playbook.md`；
- `core-playbook.md` 回归 State / Continuity / Battle Runtime Skeleton；
- Battle Beat 明确不是固定动作数量容器；
- 删除 V1 `2–4` 全局动作锚点的运行期职责；
- Router 改为 `core + choreography + 1 specialist`；
- Two-stage On-demand Loading 接入；
- 建立轻量 `Combat Planning Context`；
- Quick = Full Planning + Silent Resolution；
- Interactive = 同一 Planning Graph + Decision Exposure Policy；
- SKILL 入口同步。

### Gate

✅ Core / Choreography 职责分离；Quick 不绕过 Choreography；Modern / Wuxia 仍只选一个专项分支。

---

## 5. Phase 2｜Choreography + 专项实现 — ✅ 完成

### 文件

```text
references/tasks/action-combat-video/choreography-playbook.md
references/tasks/action-combat-video/modern-combat-playbook.md
references/tasks/action-combat-video/cinematic-wuxia-playbook.md
```

### 已完成

Choreography 主链已覆盖：

- Choreography Profile；
- Active Combat Coverage + 时间预算；
- Rhythm；
- Action Phrase / Exchange Depth；
- Combat Character Identity；
- Tactical Interaction；
- Environment Action Affordance；
- Contact Solidity；
- Signature Moment；
- Action Execution Budget + Action Sufficiency Check；
- Camera Readability Budget；
- Combat Audio Choreography；
- Clarity Through Structure；
- Final Prompt Action Externalization；
- Model Capability 输入边界。

Modern 已明确：

- 职业不直接映射 Tactical Close Combat；
- 高手连续攻防 / Mixed Rhythm / Contact Solidity 的现代实现；
- Strike / Grapple / Takedown / Environment 不同反馈；
- Camera / Audio 只做专项表现。

Wuxia 已明确：

- 保持电影武侠物理尺度；
- Blade / Weapon Clash / 长兵器距离采用正确 Contact / Range 逻辑；
- 身法必须有起点 / 路径 / 落地；
- 不被现代“重拳反馈”污染。

### Gate

✅ Core 质量合同一致，Modern / Wuxia 表现语法不同；专项层不反向重定义 Core / Choreography。

---

## 6. Phase 3｜Combat Libraries 与按需知识 — ✅ 完成

### 新增

```text
references/libraries/combat-choreography-profiles/library.md
references/libraries/signature-moment-patterns/index.md
references/libraries/signature-moment-patterns/patterns/constrained-space-reversal.md
references/libraries/signature-moment-patterns/patterns/environment-assisted-counter.md
references/libraries/signature-moment-patterns/patterns/rapid-counter-recounter.md
references/libraries/signature-moment-patterns/patterns/weapon-distance-transition.md
references/libraries/signature-moment-patterns/patterns/false-opening-trap.md
references/libraries/signature-moment-patterns/patterns/momentum-redirection.md
references/libraries/signature-moment-patterns/patterns/dominance-reversal.md
```

### 修改

```text
references/libraries/combat-fighting-profiles/library.md
references/libraries/combat-martial-profiles/library.md
references/libraries/combat-weapon-profiles/library.md
references/libraries/combat-environment-patterns/library.md
references/libraries/index.md
```

### 已完成

- 6 个稳定 Choreography Profile Seed；
- 7 个 Signature Moment Pattern Seed；
- Signature Pattern 按动作机制组织，不按影视标题组织；
- Runtime Pattern 与 Source Case 研究职责分离；
- 当前未伪造 / 强绑未经核实的影视 Source Case；
- Fighting 明确 `职业 ≠ Character Identity ≠ Fighting Profile`；
- Martial / Weapon 增加正确 Contact Modality / Range / Initiative；
- Environment 改成 Affordance 驱动；
- 默认约 2 个主要 Library Detail Slot；
- 专业正确性优先于 Signature 创意增强；
- 不建设 Combat Character Identity / occupation portrait Library。

### Gate

✅ 能力增加但单次 Runtime Reference 仍保持小而有针对性；`source-cases/` 不进入默认运行。

---

## 7. Phase 4｜Final Prompt / Output Contracts — ✅ 完成

### 文件

```text
references/controls/prompt-assembly/control.md
assets/templates/mode-quick-output-contract.md
assets/templates/mode-interactive-output-contract.md
assets/templates/model-adapted-output-template.md
```

### 已完成

- Action-first Semantic Priority；
- `State Machine Internalized, Choreography Externalized`；
- Final Prompt 由 Action Phrase / Reaction / Contact / Spatial Change 主导；
- Positive-first Constraint Strategy；
- Negative 只用于正向表达不足以解决的真实高风险；
- 禁止无根据的 `no visible weapons` 等任意限制；
- 压缩时优先删 Meta / 重复 Constraint，不优先删有效攻防；
- Quick / Interactive 最终质量标准一致；
- Model Adapter 只能改变序列化和执行路径。

### Gate

✅ Final Prompt 不再由 State Table / Negative Boilerplate 主导。

---

## 8. Phase 5｜Model Combat Capability Contract — ✅ 完成（待 Phase 8 校准等级）

### 文件

```text
references/models/index.md
references/models/generic.md
references/models/seedance-2.md
references/models/ltx-2-3.md
```

### 统一维度

- Motion Complexity Capacity；
- Multi-character Stability；
- Contact / Interaction Fidelity；
- Spatial Continuity；
- Camera Complexity Capacity；
- Temporal / Prompt Following。

### 已完成

- 统一 Capability Contract；
- 只有可靠证据才允许 High / Medium / Low；
- 无实测时明确 `Unverified`；
- Generic / Seedance 2.0 / LTX-2.3 当前 Combat 专项能力均不伪造等级；
- Known Risks 与正式 Capability Rating 分开；
- 降载顺序：Camera → 同窗口复杂度 → Phrase 拆分 → 次要分支；
- 禁止因模型能力弱直接把 High Coverage 变成低动作量。

### Gate

✅ Contract 架构完成；⚠️ 真实能力等级必须在 Phase 8 基于 Golden Benchmark 再校准。

---

## 9. Phase 6｜Combat Diagnostics — ✅ 完成

### 新增

```text
references/diagnostics/combat-choreography-underfill/diagnostic.md
references/diagnostics/combat-contact-solidity-failure/diagnostic.md
```

### 三类主诊断

```text
打得不对 / 接不上
→ combat-state-continuity-failure

打得太少 / 不够丰富
→ combat-choreography-underfill

打到了但打不实
→ combat-contact-solidity-failure
```

### 已完成

- Underfill 检查 Coverage / Active Exchange / Phrase / Exchange Depth / Downtime；
- Solidity Failure 检查 Contact Modality 与 Commitment → Transfer → Reaction → Consequence；
- Anatomy / Physics / Camera / Audio 等基础问题继续走原有 Diagnostic；
- `diagnostics/index.md`、`references/index.md`、`SKILL.md` 已接线。

### Gate

✅ Diagnostic 主因分工明确，不用一个“大而全 Combat Diagnostic”重复所有问题。

---

## 10. Phase 7｜Static Regression + Golden Framework — ✅ 完成

### 文件

`docs/action-combat-video-v2-regression.md`

### 已完成

- Task / Runtime 静态回归；
- Choreography 机制检查；
- 废弃规则检查；
- Knowledge / Loading 检查；
- Final Prompt Action-first 检查；
- Model Contract 检查；
- Diagnostic 路由检查；
- 首批 8 个 Golden Scenario；
- Quality / Failure / Optional Test Anchor；
- Generated Video 10 项质量指标；
- Prompt Intent → Generated Result Gap；
- V1 / V2 对照方法；
- Benchmark Run Record Schema。

### 本阶段发现并修复

静态 Gate 首次发现：

- `references/tasks/index.md` 未登记 Choreography；
- `references/index.md` / `SKILL.md` 对新 Library / Diagnostic 接线不完整。

均已修复并重新检查。

### Gate

✅ **Static / Structural Regression PASS。**

Static PASS 不等于成片质量 PASS。

---

## 11. Phase 8｜Generated Video Quality Benchmark — ⏳ 待真实生成端执行

### 目标

用真实生成视频验证 V2 是否真正优于 V1。

### Golden Scenarios

1. 15 秒办公室高手近身对决；
2. 力量型 vs 灵活型；
3. 狭窄走廊 / 受限空间；
4. 硬派拳脚 Contact Solidity；
5. 短兵器刀战；
6. 长兵器距离切换；
7. Grapple / Takedown；
8. 1vN Target Handoff。

### 必记字段

```text
Golden Scenario ID
Skill / Commit
Prompt Version
Model / Model Version
Generation Parameters
Seed（if supported）
Final Prompt
Output Video
Metric Scores / Notes
Prompt Intent → Generated Result Gap
Failure Signature
Pass / Partial / Fail
```

### 成片指标

- Active Combat Coverage Realization；
- Exchange / Choreography Richness；
- Character Distinction；
- Tactical Interaction；
- Combat Contact Solidity；
- Environment Integration；
- Signature Moment；
- Camera Readability；
- Spatial / Physical Continuity；
- Rhythm Variation。

### 当前边界

当前 ChatGPT 工具环境没有可直接调用的目标视频生成器，因此**不能诚实地产生 Phase 8 成片和评分**。

不得：

- 用静态 Prompt 代替成片结论；
- 伪造 Seedance / LTX 生成结果；
- 给 Model Capability 编造 High / Medium / Low。

Phase 8 应在真实 Seedance / LTX / 目标平台上执行，再把结果回写：

- `docs/action-combat-video-v2-regression.md`；
- 对应 `references/models/<adapter>.md` Capability Contract。

### Gate

至少核心 Golden Scenarios 证明 V2 在 Coverage / Exchange / Solidity 等主要问题上优于 V1，且没有明显牺牲 Continuity / Camera Readability。

---

## 12. Phase 9｜文档与索引收口 — ✅ 仓库侧完成

### 已更新

```text
SKILL.md
references/index.md
references/tasks/index.md
references/tasks/action-combat-video/index.md
references/libraries/index.md
references/diagnostics/index.md
references/models/index.md
docs/action-combat-video-v2-regression.md
```

### 收口状态

- ✅ 运行期职责边界一致；
- ✅ Index 与真实目录一致；
- ✅ V2 静态回归 PASS；
- ✅ Golden Benchmark Framework 可重复；
- ✅ 没有新增 Combat Choreography Control；
- ✅ 没有建立职业 / Character Identity 画像库；
- ✅ Pattern / Profile / Golden Scenario 未固化为动作答案；
- ⚠️ 唯一剩余总 Gate：Phase 8 真实成片验证。

---

## 13. 关键新增文件

```text
references/tasks/action-combat-video/choreography-playbook.md
references/libraries/combat-choreography-profiles/library.md
references/libraries/signature-moment-patterns/index.md
references/libraries/signature-moment-patterns/patterns/*.md
references/diagnostics/combat-choreography-underfill/diagnostic.md
references/diagnostics/combat-contact-solidity-failure/diagnostic.md
docs/action-combat-video-v2-implementation-plan.md
docs/action-combat-video-v2-regression.md
```

当前不为了目录完整而创建空 `source-cases/` 文件；只有核实可靠影视来源后再补研究档案。

---

## 14. 当前实施状态

| Phase | 状态 | 说明 |
|---|---|---|
| Phase 0 | ✅ 完成 | V2 设计冻结、实施计划建立 |
| Phase 1 | ✅ 完成 | Task 运行骨架 / Core-Choreography 解耦 |
| Phase 2 | ✅ 完成 | Choreography 与 Modern / Wuxia 专项实现 |
| Phase 3 | ✅ 完成 | Combat Libraries / Signature Patterns / Two-stage Loading |
| Phase 4 | ✅ 完成 | Final Prompt / Output Action-first |
| Phase 5 | ✅ 架构完成 | Capability Contract 已接入；等级待 Phase 8 实测校准 |
| Phase 6 | ✅ 完成 | Combat Underfill / Solidity Diagnostics |
| Phase 7 | ✅ PASS | Static Regression + 8 个 Golden Scenario Framework |
| Phase 8 | ⏳ 待执行 | 真实视频生成 + V1/V2 成片质量对照 |
| Phase 9 | ✅ 仓库侧完成 | Index / SKILL / Docs 已收口；最终完成依赖 Phase 8 |

## 15. 当前下一步

**唯一剩余工作是 Phase 8：在真实视频模型上跑 Golden Combat Benchmark。**

Phase 8 完成前，V2 状态应称为：

> **Implementation Complete + Static Regression PASS + Generated Video Validation Pending**

而不是“最终质量验证完成”。
