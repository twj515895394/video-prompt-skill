# Video Prompt Skill — Action Combat Current Handoff

> 更新时间：2026-08-15 18:12（UTC+8）  
> 仓库：`twj515895394/video-prompt-skill`  
> 分支：`main`  
> 当前阶段：**Identity × Combat System 已通过真实 Interactive 验证；Advantage × Counterplay 已完成 Spec + Runtime；Action–Camera Realization × Preservation 已完成 Spec + Runtime / Assembly / Adapter 静态实施。下一步进入 G01 + 最小 Camera Priority 对照真实回归。**

---

## 0. 当前状态一句话

**不要继续扩具体拳种、流派或 Camera Grammar。下一步唯一高价值动作是重新跑办公室 G01，同时验证 Advantage × Counterplay 与 Action–Camera Realization × Preservation；随后再跑 1 个不同 Camera Base Viewing Priority 的最小对照案例。**

当前已有两条待真实回归的实施线：

```text
A. Advantage × Counterplay
→ Spec + Runtime 已实施
→ 需要验证劣势方是否真的会还手，而不是“准备 / 即将反击”

B. Action–Camera Realization × Preservation
→ Spec + Runtime / Assembly / Adapters 已实施
→ 需要验证关键 Camera Moment 是否真正绑定具体动作，并在 Adapter 后仍保真
```

---

## 1. 已完成上一批：Identity × Combat System

上一批已经完成并经过真实 Interactive 测试：

```text
Character / Narrative Identity
≠ Combat System

Round 1：Per-Character Combat System / System Refinement
Round 2：Per-Character Combat Expression

Physical Presentation Domain：条件暴露
Derived Choreography Direction：Runtime 自动派生
legacy Fighting Direction：只保留 compatibility execution slot
```

真实办公室 G01 与古代女剑客测试已经证明：

- “职业杀手 → Fighting Direction / 打法”混层明显改善；
- Round 1 / Round 2 结构真实生效；
- Physical Presentation Domain 与 Combat System 正交；
- Stage-2 / Subject Motion / Action–Camera / Prompt Assembly 路由明显改善；
- Final Prompt 的 Whole-body / Movement / Persistent Signature 比旧版本更好。

主 Spec：

`docs/combat-system-performance-identity-separation-spec.md`

本轮不要回头重新 Grill 太极、MMA、咏春、八极、散打等具体流派细节。

---

## 2. 已实施：Advantage × Counterplay

主 Spec：

`docs/combat-advantage-counterplay-spec.md`

运行期正文真源：

`references/tasks/action-combat-video/advantage-structure-contract.md`

核心 Planning 结构：

```text
Advantage Structure
├─ Outcome / Advantage
├─ Counterplay Shape
└─ Advantage Trajectory
```

核心原则：

```text
Advantage ≠ Attack Share
Outcome ≠ Advantage Trajectory
Disadvantaged ≠ Passive
```

推荐默认 Counterplay Shape：

```text
High Counterplay, Repeatedly Neutralized
```

即：

```text
优势方总体占优
→ 劣势方多次真实 Attack / Counter / Re-entry
→ 这些动作真实形成威胁或状态变化
→ 优势方不断化解 / 截断 / 借势反制
→ 总体 Advantage 仍属于优势方
```

Counterplay 只能在真实发生主动战斗行为并造成状态后果时算 Realized；“等待 / 准备 / 即将反扑”只能算 Setup。

Ending 已降级为条件节点，不能吞掉主要 Combat Budget。

当前重要 Failure Signatures：

- `Counterplay Starvation`
- `Initiative Starvation`
- `Deferred Counterplay Collapse`
- `Advantage-to-Passivity Shortcut`
- `Outcome-Trajectory Collapse`

---

## 3. 新增真实 Regression：Camera Intent 存在，但没有落到具体动作

本次真实 Interactive 中，用户选择：

```text
Camera Base Viewing Priority = 电影冲击优先
```

最终 Prompt 却出现：

```text
“第一次真实接触发生时，镜头短暂切近……”
```

但：

- 没有明确是哪一个具体 Action Moment 触发该切近；
- Camera Change 没有与某一段正在发生的动作绑定；
- 没有明确继承哪一类 live motion；
- 后文又出现“从冲击近景重新拉回中景”等 Camera State 引用，而该状态没有被可靠建立。

现有 `action-camera-handoff-playbook.md` 与 `prompt-assembly/control.md` 其实已经明确禁止“关键接触时短暂切近”这种泛化写法。

因此本次问题正式定性为：

> **Camera Handoff Realization / Preservation Regression，而不是缺 Camera 知识，也不是缺一个新的 Interactive 问题。**

---

## 4. Action–Camera V2 Spec

沿用既有 Spec，不建立第二份 Camera 设计真源：

`docs/action-combat-video-action-camera-handoff-spec.md`

已升级为 V2：

`Camera Handoff Realization × Preservation`

V2 核心新增：

```text
Realization Gate
+
Preservation Gate
```

Spec Commit：

`ed454d5f145faf411c4435b89d5ba7ce8bfe71dc`

---

## 5. 实施计划

新增实施计划：

`docs/action-combat-video-camera-realization-preservation-implementation-plan.md`

Commit：

`40124a6ce1aa161de104a381c4d2b697a6fec7a1`

实施原则：

- 只正式作用于 Action Combat；
- 不建立平行 Camera Runtime；
- 不增加固定字段 / 固定 Shot 数量；
- 不把 Camera Gate 做成关键词计数；
- 不因为 Model Capability = Unverified 就自动降级；
- 不扩完整 Camera Benchmark；
- 不扩具体武术 / 拳种知识。

---

## 6. 双层 Gate 已确认并实施

正式结构：

```text
Action–Camera Runtime
→ Camera Handoff Realization Gate

Prompt Assembly / Model Adapter
→ Camera Handoff Preservation Gate
```

职责：

```text
Realization Gate
= 有没有真正设计并落到具体 Action Moment

Preservation Gate
= Assembly / Adapter 改写后，核心 Action–Camera 语义还在不在
```

两层都是：

> **语义合同，不是模板合同。**

不要求固定字段、固定句式、固定顺序、固定 Camera Accent 数量。

---

## 7. Realization Gate 最小语义合同

对**已经被选中的高价值 Camera Moment**，语义上至少要求：

```text
Concrete Action Anchor
+
Camera Response / Viewer Task
+
Live Motion / State Continuation
+
Camera Hard Constraint Compliance
```

解释：

### Concrete Action Anchor

Camera Change 必须依附正在发生的具体动作 / 状态变化。

以下不能单独判 PASS：

```text
第一次接触时
关键时刻
高潮处
```

### Camera Response / Viewer Task

要能理解 Camera 为什么此刻介入，以及主要要看见 / 感受到什么。

### Live Motion / State Continuation

Camera Change 后必须继续至少一类活着的：

- Momentum；
- Contact；
- Pressure；
- Rotation；
- Support Transfer；
- Forced Step；
- Recovery；
- unfinished motion。

### Hard Constraint Compliance

必须服从 One-take / No-cut / Fixed Camera 等用户明确边界。

注意：以上是语义合同，不要求输出为四字段。

---

## 8. Preservation Gate

Prompt Assembly / Model Adapter 可以自由：

- 改写句式；
- 合并句子；
- 把结构化描述压成自然段；
- 使用目标模型更适合的 Camera 语言；
- 在有可靠证据时降低实现复杂度。

但核心语义必须存活：

```text
具体 Action Anchor
+
Action ↔ Camera 因果绑定
+
主要 Camera Task / Viewer Experience Intent
+
必要 Live Motion Continuation
```

这叫：

```text
Semantic Preservation
```

而不是：

```text
Textual Copy
```

---

## 9. 新增唯一正式 Failure Signature

本批不扩大量 Failure Taxonomy。

Realization 失败继续复用：

- `Action–Camera Decoupling`
- `Perceptual Impact Underuse`
- `Camera Strategy Overconstraint / Camera Mobility Underfill`
- `Dead-motion Cut / Post-action Cut`
- `Kinetic Handoff Loss`
- `Camera Hard Constraint Violation`

只新增：

```text
Camera Handoff Serialization Loss
```

定义：

> 上游已经形成有效 Action–Camera Handoff，但经过 Prompt Assembly / Model Adapter 后，Action Anchor、Camera Intent、Viewer Experience 或 Live Motion Continuation 的关键语义被泛化、拆散或删除。

Rewrite 路径：

```text
Action–Camera Decoupling / Realization FAIL
→ 回 Action–Camera Runtime

Camera Handoff Serialization Loss
→ 只回 Prompt Assembly / 当前 Model Adapter
→ 不重新设计 Choreography
```

Camera State 未建立却被后文引用，当前作为 Preservation / Continuity 检查维度，不新增独立 Failure Signature。

---

## 10. 默认 Full-fidelity，不因 Unverified 自动降级

正式默认：

```text
Full-fidelity Action–Camera Realization
```

禁止：

```text
Camera Complexity Capacity = Unverified
→ 自动减少高价值 Camera Moment
→ 自动回退保守中景
```

只有存在以下证据时才允许：

```text
Intent-preserving Degradation
```

证据：

- Verified Model Limitation；
- 可靠专项 Benchmark；
- 相同 Golden Scenario 的真实 Generated-video Regression Evidence。

降级时：

```text
降低 Camera 实现复杂度
≠
删除 Camera Intent
```

低价值 / 装饰性 Accent 可以删除；高价值 Moment 优先保留 Anchor、Viewer Intent 与 Motion Continuation。

---

## 11. Common Preservation Contract + Adapter-specific Expression

共同真源：

`references/controls/prompt-assembly/control.md`

负责：

```text
What must survive
```

各 Model Adapter 负责：

```text
How it is expressed
```

Generic / Seedance 2.0 / LTX-2.3 都继承同一 Preservation Contract，不复制一套新的 Camera Runtime。

---

## 12. 最终执行顺序已修正

真正的 Action Combat Final Path 现在是：

```text
Confirmed Per-Character Combat Context
→ Derived Choreography Direction
→ Stage-2 Gap Detection
→ Stage-2 Pattern Hit Evidence Gate
→ 必要 leaf knowledge Read
→ Concrete Action Phrase
→ State / Continuity Validation
→ Model Execution Realizability
→ Motion / Energy Carry-over
→ Action–Camera Handoff Planning
→ Camera Handoff Realization Gate
→ Camera / Spatial Coordination
→ Prompt Assembly
→ 当前 Model Adapter
→ Camera Handoff Preservation Gate
→ Combat Final Preflight（检查 Adapter 后实际 Final Prompt）
→ Output Template / Delivery
```

核心变化：

> **Adapter 之前的检查不再冒充真正 Final Preflight。真正 Final Preflight 必须检查最终实际交付 Prompt。**

---

## 13. 本批已实际修改的 Runtime / Adapter

### 13.1 Action–Camera Runtime

`references/tasks/action-combat-video/action-camera-handoff-playbook.md`

新增 / 强化：

- Camera Handoff Realization Gate；
- 4 类最小语义合同；
- Full-fidelity default；
- Unverified 不自动降级；
- Runtime-stage Preflight 与 Final Preflight 分离；
- Realization FAIL 回路。

Commit：

`599a3f5b4435b2d1bd91b978d23904f68a3f5df5`

### 13.2 Prompt Assembly

`references/controls/prompt-assembly/control.md`

新增 / 强化：

- Common Camera Handoff Preservation Contract；
- Semantic Preservation；
- `Camera Handoff Serialization Loss`；
- Camera State Establishment / Reference Check；
- Assembly-stage validation 与 Adapter 后 Final Preflight 分离；
- Serialization Loss 只回 Assembly / Adapter。

Commit：

`339a0e5d40a57af4109882900afcba2917a35acf`

### 13.3 SKILL 主路由

`SKILL.md`

新增 / 强化：

- Realization Gate；
- Model Adapter 后 Preservation Gate；
- Final Preflight 后移；
- Model Adapter Common Preservation Invariant；
- Combat 自查增加 Realization / Preservation / Camera State；
- `Unverified ≠ auto downgrade`。

Commit：

`cde212958534161de4480b25de7a997598b32abb`

### 13.4 Generic Adapter

`references/models/generic.md`

Commit：

`506aa32c8d4d573c0eff1f300eaec0f34626c8c2`

### 13.5 Seedance 2.0 Adapter

`references/models/seedance-2.md`

Commit：

`d4880e87ef28746192abd7bcb9e6a397439843ae`

### 13.6 LTX-2.3 Adapter

`references/models/ltx-2-3.md`

Commit：

`64463f607e8224409489c7bbe30d4e18243ce937`

三个 Adapter 都已经明确：

- 继承 Common Preservation Contract；
- Adapter 可以灵活改写；
- 不重新决定上游高价值 Camera Moment 是否值得存在；
- `Unverified` 不自动触发 Camera 降级；
- 发生 `Camera Handoff Serialization Loss` 时只回 Assembly / Adapter。

---

## 14. 本批静态实施状态

当前已完成：

```text
Spec V2
✓
Implementation Plan
✓
Action–Camera Realization Runtime
✓
Prompt Assembly Preservation Contract
✓
SKILL Mandatory Path
✓
Generic Adapter
✓
Seedance Adapter
✓
LTX Adapter
✓
```

这只代表：

> **Static Implementation PASS / Routing Contract 已接通。**

不代表：

- 真实 Interactive 已 PASS；
- Final Prompt Runtime 已 PASS；
- Generated Video 已 PASS。

---

## 15. 下一轮固定 G01 Regression

继续使用办公室职业杀手 15 秒场景。

本次回归应同时验证两条实施线：

### Advantage × Counterplay

检查：

- Advantage Structure 是否按条件暴露；
- 劣势方 Counter / Re-entry 是否真实发生；
- Counterplay 是否迫使优势方真实响应；
- Ending 是否不再吞掉主要 Counterplay；
- Outcome / Trajectory 是否没有 Collapse。

### Action–Camera Realization × Preservation

Camera Base Viewing Priority 继续使用：

```text
电影冲击优先
```

检查：

- 高价值 Camera Moment 是否真正绑定具体 Action Moment；
- 不再用“第一次真实接触时短暂切近”冒充 Handoff；
- Camera Response 是否有明确 Viewer Task；
- Camera Change 后是否继续 live motion；
- Adapter 后 Action Anchor / Camera Intent / live-motion continuation 是否仍存在；
- 是否出现 `Camera Handoff Serialization Loss`；
- Camera State 是否先建立后引用；
- Camera 增强没有挤压有效 Combat Coverage。

---

## 16. 最小 Camera Priority 对照 Regression

G01 之后，再选 1 个已有 Action Combat 场景。

Camera Base Viewing Priority 改成：

- `完整动作可读`；或
- `贴身沉浸`。

目标不是验证“有没有更多镜头”，而是验证双层 Gate 没有机械化。

必须确认：

- 不机械复用 G01 的 Near-lens / Close-up / Cut Pattern；
- 普通连接动作继续当前 Shot；
- Camera Accent 仍由 Action Information / Viewer Experience Value 决定；
- 不设 Cut / Close-up 数量配额。

---

## 17. 本批不要做的事

在真实回归之前，不继续：

- 扩 MMA / 散打 / 拳击 / 摔跤 / 太极 / 咏春 / 八极等具体知识；
- 扩 Camera Grammar；
- 新建第二套 Camera Runtime；
- 为 Camera Moment 增加固定字段表；
- 设置固定 Cut / POV / Close-up 数量；
- 因 `Unverified` 主动降级所有 Adapter；
- 把双层 Gate 扩散到所有普通视频任务；
- 建完整 Model Camera Benchmark；
- 新增更多 Camera Failure Signature。

原则仍然是：

> **先跑真实回归，再决定下一刀。**

---

## 18. 下一会话行动顺序

严格按以下顺序：

```text
1. 重新跑办公室 G01 Interactive
2. 收集完整实际 Read List
3. 检查 Advantage Structure Runtime
4. 检查 Counterplay 是否真实发生
5. 检查 Camera Handoff Realization Gate 是否真实生效
6. 检查 Prompt Assembly / Model Adapter 后是否仍 Semantic Preservation
7. 对最终实际 Prompt 执行 Combat Final Preflight
8. Prompt-level PASS / FAIL
9. PASS 后生成真实视频
10. Generated-video PASS / FAIL
11. 再跑 1 个不同 Camera Priority 的最小对照案例
12. 再决定是否需要下一批修改
```

如果 Camera FAIL：

```text
Action–Camera Decoupling / Realization FAIL
→ 回 Action–Camera Runtime

Camera Handoff Serialization Loss
→ 回 Prompt Assembly / 当前 Model Adapter

Perceptual Accent Overuse
→ 删除低价值 Accent

Camera Strategy Overconstraint
→ 重新按 Action Information / Viewer Experience 分配 Camera Task
```

不要直接扩 Camera 知识。

---

## 19. 当前最终目标

本轮真正要验证的不是：

> “Prompt 里有没有写近景 / 特写 / POV”。

而是：

> **当某个 Action Moment 真正值得改变观看方式时，Camera 是否因为这个具体动作而变化；变化后是否继续同一条活着的运动链；并且这个导演意图是否能一路穿过 Prompt Assembly 与 Model Adapter，直到最终交付 Prompt。**
