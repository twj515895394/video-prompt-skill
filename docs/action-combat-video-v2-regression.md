# Action Combat Video V2 Regression & Quality Benchmark

> 状态：**Phase 11 Mandatory-path Rewire 已完成；V2-46 / V2-47 已实施；V2-48 / V2-49 Runtime 已进入 Phase 12 Prompt-level 回归。真实成片必须在 Phase 13 重新生成，不得沿用旧 PASS。**
>
> 设计依据：`docs/action-combat-video-v2-spec.md`
>
> 实施计划：`docs/action-combat-video-v2-implementation-plan.md`
>
> Traceability Audit：`docs/action-combat-video-v2-traceability-audit.md`

## 1. 验证原则

```text
Level 0｜Prompt-level Regression
→ Final Prompt 是否真的执行了当前 Spec，而不是只“读过规则”

Level 1｜Static / Structural Regression
→ 规则、路由、序列化、Gate 是否真正接线

Level 2｜Generated Video Quality Regression
→ 成片是否真正连续打起来，同时具有电影化 Camera Coverage
```

> **静态规则正确只是必要条件；Prompt 本身不合格时禁止直接进入真实视频；真实成片质量是最终验收。**

本轮特别避免四个错误：

1. 成片不好就继续增加抽象机制；
2. 为了动作可读性，把 Combat Camera 固化成全程中全景 / 中景连续跟拍；
3. 为了 Prompt 简洁，把已经具体的 Choreography 重新压缩成“连续反制 / 持续缠斗 / 不断换位”；
4. 为了少问，把真正会显著改变成片的 Camera Intent 静默替用户决定。

---

## 2. 已暴露的核心失败

原 G01 办公室高手 1v1 的真实测试暴露：

- 真实有效交战仍偏少；
- 动作主要锁在上半身；
- Camera 的“稳定”被执行成近似固定；
- 3–4 秒时间块只承载一个宏动作；
- 每 1–2 秒一个动作，动作完成后归位；
- Hard Timeline Blocks 强化动作分段；
- 双方容易轮流出招；
- Advantage / Reversal 可能只存在于文字描述；
- 连续动作若简单加速，又可能退化成全程同速、同压力。

后续办公室 Prompt 进一步暴露：

- Mandatory Prompt Assembly 已生效；
- Continuous Action Spine 与 Temporal Packing 已改善；
- V2-46 修正后 Camera Coverage 已明显改善；
- Interactive 轮数本身不是问题，但单轮推荐可能提前夹带 downstream 决策；
- Final Prompt 仍存在“连续格挡 / 快速反制 / 不断换位”等 **Abstract Action Block**；
- Initiative Handoff 虽有规则，但句法仍可能轻微回合化；
- Ending 可能通过对视 / 呼吸 / Pose 过早吞掉 Active Exchange。

当前重点 Failure Signatures：

```text
Upper-body Combat Lock / Kinetic Underfill
Temporal Combat Stretch / Action Underpacking
Action Segmentation / Excessive Neutral Reset
Timeline-induced Action Segmentation
Abstract Action Block / Non-executable Choreography Summary
Turn-taking Combat / Initiative Segmentation
Invisible Advantage / Nominal Reversal
Homogeneous Initiative Style / Identity-by-Demographic Shortcut
Camera Mobility Underfill
Combat Camera Coverage Lock / Medium-wide Overconstraint
Cut-induced Action Reset
Flat Combat Intensity
```

这些属于统一 Gate 下的 Failure Signatures，不建立同等数量独立模块。

---

## 3. Static Regression Gate

### 3.1 Mandatory Runtime Path

- [x] `SKILL.md` 明确 Action Combat 最终固定读取 `prompt-assembly/control.md`；
- [x] Combat Prompt Assembly 不再占普通 `0-3 Controls` 可选预算；
- [x] `action-combat-video/index.md` 明确 `Final Assembly → Final Preflight → FAIL rewrite → PASS template` 必经链；
- [x] Quick / Interactive 均不能跳过 Final Assembly / Preflight；
- [x] **Stage-2 Execution Knowledge 后必须进入 Concrete Action Phrase Construction。**

### 3.2 Interactive Runtime — V2-47 / V2-48

- [x] Interactive 使用 High-value Question Budget；
- [x] 默认最多 10 轮，轮数不是 PASS / FAIL 标准；
- [x] **One Question, One Primary Decision Node 已接入；**
- [x] 推荐答案可解释 downstream 影响，但不能提前锁死 Character Identity / Camera / Ending / Result；
- [x] **Camera Intent 已进入 Conditional High-value Node Pool；**
- [x] Camera 不固定必问；
- [x] Camera 问题使用导演观看策略，不直接问 Camera Complexity / Mobility / Cut Density 等内部参数。

### 3.3 Choreography Runtime — V2-49

- [x] Coverage / Exchange Depth / Kinetic Scope 并列；
- [x] Temporal Packing / Motion Handoff / Continuous Action Spine 已接线；
- [x] **Executable Action Granularity Contract 已接入 Action Phrase；**
- [x] 关键 Phrase 要求具体身体 / 武器动作、Contact / Evasion、即时响应、Footwork / Axis / Range / Position 后果与下一动作入口；
- [x] **抽象动作词只能做摘要 / 次要过渡，不能替代关键 Active Exchange；**
- [x] Initiative Handoff 必须进入具体动作句法；
- [x] Ending Coverage Protection 已接入；
- [x] `Abstract Action Block` 已进入 Final Preflight；
- [x] Action Execution Budget 明确“颗粒度提升 ≠ 动作数量无限增长”。

### 3.4 Camera Runtime — V2-46

- [x] Camera Complexity 与 Camera Mobility 分离；
- [x] Action Continuity 与 Shot Continuity 分离；
- [x] Camera Coverage 可使用 Master / Medium / Close-up / Insert / Reaction / Impact / Re-establish；
- [x] Cut 后必须继承 Position / Direction / Contact / Momentum / Axis / Range；
- [x] Final Preflight 可拦截 Camera Coverage Lock。

### 3.5 Prompt Assembly / Template

- [x] High-density Combat 默认 Continuous Action Spine + Soft Time Anchors；
- [x] `single-shot-video` 不再等于 one-take；
- [x] **Concrete Choreography In → Concrete Choreography Out 已接入 Prompt Assembly；**
- [x] Assembly 不允许把具体 Phrase 压回“连续攻防 / 快速反制”等摘要；
- [x] Initiative Handoff 在序列化时保留动作重叠 / 状态继承；
- [x] Ending 文本过长时优先压缩 Ending；
- [x] Camera Mobility 与 Editorial Coverage 分开；
- [x] 不设置镜头数量 / 特写数量配额；
- [x] Negative Constraints 少而有针对性。

---

## 4. Golden Scenario Contract

```text
Fixed Input
+ Quality Contract
+ Failure Contract
+ Optional Test Anchor
```

> **Benchmark 锁质量，不锁固定动作答案，也不锁固定镜头答案。**

---

## 5. G01｜15 秒办公室高手近身对决

### Fixed Input

- 时长：约 15 秒；
- 场景：普通办公室开放区域；
- 人物：中国女性 + 中国男性，普通职场服装；
- 隐藏身份：敌对组织的专业杀手；
- 用户约束：贴身搏斗，不隔着办公桌；
- 目标：高手连续攻防，而不是两三次孤立动作；
- 模式：Interactive；
- 模型：Generic，除非用户另行指定。

### Interactive Quality Contract

- 每轮只解决一个主要 Planning Node；
- 推荐答案不提前夹带未确认 downstream 决策；
- 问题轮数按需求完整度动态决定；
- Camera Intent 若存在多个高价值观看策略且用户未明确，应有机会成为一轮问题；
- Camera 若已经明确或只有一个明显合理方向，不强行询问；
- 不把 Contact Solidity / Kinetic Scope / Granularity / Preflight 等内部质量机制变成问卷。

### Interactive Failure Contract

出现任一明显模式即 FAIL / REWRITE：

- 问 Choreography Profile 时同时替用户决定 Character Identity + Ending + Camera；
- 为了少问直接跳过一个明显会改变成片的 Camera Intent 分叉；
- 已经确认 Camera Intent 后重复询问；
- 把 Camera Complexity / Mobility / Cut Density 等内部参数直接问用户；
- 需求已经完整仍为了走完 Planning Graph 继续发问；
- 单纯因为问了 4～6 轮就判“太多”。

### Prompt-level Quality Contract

Final Prompt 必须满足：

- Setup 很短，贴身 Combat 很快开始；
- 不默认使用多个 1–3 秒 Hard Time Blocks；
- Active Exchange 主要是一条 Continuous Action Spine；
- 较长动作窗口包含连续因果动作流；
- 动作链存在 Motion Handoff；
- **关键 Active Exchange 不是抽象“连续攻防”，而是具体可执行动作链；**
- **关键 Phrase 能看出具体身体 / 武器动作、Contact / Evasion、即时响应、Footwork / Axis / Range / Position 后果与下一动作入口；**
- **删除“高速 / 连续 / 专业 / 高密度 / 反制 / 缠斗”等抽象词后，仍能理解主要动作因果；**
- Whole-body / Footwork / Hip / Torso / Position / Range / Axis 合理外显；
- Character Identity 不由人口属性快捷映射；
- **Counter / Re-counter 在对手动作尚未完全结束时通过 Contact / Footwork / Axis / Range / Recovery Window 抢 Initiative；**
- Camera 跟随真实 fight-space；
- 动作连续不等于 Camera one-take；
- 允许根据动作信息使用 Close-up / Insert / Reaction / Impact Shot；
- 局部 Shot 后在需要时 Re-establish；
- Cut 后 Position / Direction / Contact / Momentum / Axis / Range 连续；
- 不把“中全景 / 中景 + 轻微跟拍”作为唯一安全 Camera 默认；
- Negative 只保留真实高风险；
- **Ending 只做短收束，继承最后一次 Contact / Position / Momentum / Advantage，不提前吞掉 Active Exchange。**

### Prompt-level Failure Contract

出现任一明显持续模式即 FAIL / REWRITE：

- 多个默认硬时间盒；
- 每段只有一个宏动作；
- **关键数秒主要写“连续格挡 / 快速反制 / 贴身缠斗 / 不断换位 / 双方互有来回”；**
- **Character Identity 只有打法标签，没有具体动作证据；**
- **Initiative / Advantage 只有 Meta 说明，没有身体、Contact、Footwork、Axis、Range 后果；**
- 长时间上肢架手 / 抓腕；
- A 做完一段才轮到 B；
- Camera 因“稳定”几乎不移动；
- 全程几乎只有中全景 / 中景；
- Continuous Action Spine 被解释成不能 Cut；
- 特写 / Insert 后人物空间关系无故重置；
- **Camera / Audio 比主要身体动作写得更具体；**
- Character Identity 被人口属性模板化；
- 长 Negative 清单；
- **最后数秒主要是对视 / 呼吸 / Pose，实际有效交战被提前终止。**

### Generated-video Quality Contract

必须观察：

- High Active Combat Coverage；
- 多个连续且可读的 Action Phrase；
- **Concrete Choreography Realization：Prompt 中具体动作是否在成片中被执行，而不是重新退化成模糊手臂交互；**
- Temporal Packing / Motion Handoff；
- Whole-body / Position / Range / Angle / Axis；
- Environment Integration；
- Character Distinction；
- Initiative / Advantage 可见；
- Contact Solidity；
- Intensity Variation；
- Camera Mobility；
- Shot Scale / Editorial Coverage；
- Action Continuity Across Cuts；
- 局部特写与 Master / Re-establish 的空间可读平衡；
- Signature Moment；
- Ending 短收束。

---

## 6. 其余 Golden Scenarios

- **G02｜力量型 vs 灵活反制型**；
- **G03｜狭窄走廊**；
- **G04｜硬派拳脚**；
- **G05｜短兵器刀战**；
- **G06｜长兵器 vs 短兵器**；
- **G07｜Grapple / Takedown**；
- **G08｜1vN**。

不得为了优化 G01 把所有场景模板化成同一种动作链或 Shot Coverage。

---

## 7. Generated Video Quality Metrics

### M01｜Active Combat Coverage Realization
真正有效交战时间。

### M02｜Exchange / Choreography Richness
有效 Phrase / Counter / Continuation 丰富度。

### M03｜Executable Granularity Realization
关键动作是否具体执行；是否从抽象“连续攻防”落实成可辨识身体 / 武器动作、即时响应和后续入口。

### M04｜Kinetic Scope Realization
Whole-body / Position / Range / Axis / Contact-driven displacement。

### M05｜Motion Continuity / Temporal Packing
是否一招一停、Neutral Reset、时间轴切碎。

### M06｜Character Distinction
双方动作与抢主动方式是否不同。

### M07｜Visible Advantage / Initiative
控制权与主动权变化是否可见，Counter 是否发生在动作链内。

### M08｜Combat Contact Solidity
Commitment / Transfer / Reaction / Consequence。

### M09｜Environment Integration
是否真正改变线路 / Position / Range / Advantage。

### M10｜Camera Readability + Mobility
动作是否看清，Camera 是否跟随空间变化。

### M11｜Shot Scale / Editorial Coverage
是否根据动作信息动态切换 Master / Medium / Close-up / Insert / Reaction / Impact / Re-establish，而不是全程中景或无意义乱切。

### M12｜Action Continuity Across Cuts
Cut 前后 Position / Direction / Contact / Momentum / Axis / Range 是否连续。

### M13｜Intensity / Signature
连续战斗是否有层次；Signature 是否形成真实峰值。

### M14｜Ending Coverage Discipline
Ending 是否在不吞掉主要 Active Exchange 的前提下完成收束。

### M15｜Spatial / Physical Continuity
Position / Range / Condition / Weapon / Environment State 连续性。

---

## 8. Prompt Intent → Generated Result Gap

每次必须记录计划与成片差距，例如：

```text
Planned Coverage: High
Observed Coverage: Low / Medium

Planned Granularity: specific contact-footwork-axis chain
Observed Granularity: generic arm exchange / vague struggle

Planned Flow: continuous counter / re-counter
Observed Flow: one action every 1–2 seconds with reset

Planned Initiative: stolen during opponent motion
Observed Initiative: turn-taking attacks

Planned Camera: mobile + varied coverage
Observed Camera: medium-wide locked / near-static

Planned Ending: short inherited finish
Observed Ending: long stare / pose consuming final seconds
```

---

## 9. Benchmark Run Record

```text
Benchmark Run ID:
Date:
Golden Scenario ID:
Skill / Commit:
Prompt Version:
Model / Version:
Generation Parameters:
Seed (if supported):
Input Assets:
Final Prompt:
Output Video:

Interactive Questions / Answers:
Planned Quality Contract:
Observed Result:
Metric Notes:
Prompt Intent → Generated Result Gap:
Failure Signature:
Pass / Partial / Fail:
Next Adjustment:
```

---

## 10. Phase 12 Prompt-level G01 Gate

使用同一办公室输入重新跑 Interactive → Final Prompt。

### 必须记录

- Read 列表；
- Interactive 问题与推荐；
- 每一轮 Primary Planning Node；
- 是否出现 Camera Intent 条件询问，以及为什么问 / 为什么没问；
- Final Prompt；
- Prompt-level Quality Contract PASS / PARTIAL / FAIL；
- Camera Coverage 类型；
- Executable Granularity 证据；
- 与上一版 Prompt 的结构差异。

### Phase 12 Pass 条件

至少满足：

- `prompt-assembly` 确实进入 Runtime；
- `Stage-2 → Concrete Action Phrase` 路径实际执行；
- Interactive 问题保持 Decision Purity；
- Camera Intent 在高价值分叉存在时可被条件暴露；
- 不再自动输出多个 Hard Time Blocks；
- 不再人口属性直接推打法；
- 不再违背“贴身搏斗”初始化；
- **主要 Active Exchange 具体到可执行动作链，不再由抽象动作块承担；**
- **Initiative Handoff 通过动作重叠 / 状态继承外显；**
- Action Spine 有 Temporal Packing / Motion Handoff；
- Whole-body / Spatial Movement 明显；
- Camera Mobility 与 fight-space 对应；
- Camera Coverage 不再被锁成全程中全景 / 中景；
- 允许有价值的 Contact / Footwork / Reaction / Impact Shot；
- Cut 后动作状态连续；
- **Ending 不提前吞掉 Active Exchange；**
- Negative 没有无依据剧情限制。

如果 Phase 12 FAIL：先修现有 Runtime / Prompt Assembly / Stage-2 接线，不新增一级抽象机制。

只有满足以下全部条件后，才允许进入 Concrete Choreography Knowledge Audit：

```text
Mandatory Path 正确
+ Stage-2 实际读取
+ Choreography Granularity Contract 生效
+ Prompt Assembly 保留具体动作
+ Final Preflight 能拦 Abstract Action Block
+ 同一 G01 仍持续输出泛化动作
```

---

## 11. Phase 13 Generated Video 验收口径

Phase 12 Prompt-level PASS 后才重新生成 G01。

至少需要看到：

- 真实交战时间增加；
- 不再主要锁在上半身；
- 具体 Action Phrase 真正在画面中被执行；
- 动作不再每 1–2 秒归零；
- Initiative 不再明显回合制；
- Camera 既能稳定跟随空间，也有电影化局部 Coverage；
- Cut 不破坏 Action Continuity；
- 优势 / 主动权变化可见；
- Contact 与 Intensity 不因动作增加而崩坏；
- Ending 不吞掉前面的有效动作时间。

如果仍失败，优先回溯：

1. Concrete Choreography / Fighting Knowledge；
2. Model Temporal / Motion Capability；
3. Model-specific Serialization；
4. Camera / Action simultaneous capacity。

不回到“继续增加抽象机制”的路径。

---

## 12. 当前状态

- V2-35～V2-49 Spec：✅ 已记录；
- Phase 11 Mandatory Final Assembly / Preflight：✅ Static PASS；
- V2-46 Camera Coverage：✅ 已实施；
- V2-47 High-value Question Budget：✅ 已实施；
- V2-48 Decision Purity + Conditional Camera Intent：✅ Runtime 已实施；
- V2-49 Executable Action Granularity：✅ Runtime 已实施；
- `Stage-2 → Concrete Action Phrase`：✅ Router 已强化；
- Prompt Assembly Concrete Preservation：✅ 已实施；
- Phase 12 Prompt-level G01：⏳ **等待新一轮同输入测试**；
- Phase 13 G01 Actual Generated Video：⏳ **未执行，不得宣称质量 PASS。**