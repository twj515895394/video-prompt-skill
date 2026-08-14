# Action Combat Video V2 Regression & Quality Benchmark

> 状态：**Phase 11 Mandatory-path Rewire 已完成静态接线；V2-46 Camera Coverage 横向修正已进入 Phase 12；真实成片必须在 Phase 13 重新生成，不得沿用旧 PASS。**
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

本轮特别避免两个错误：

1. 成片不好就继续增加抽象机制；
2. 为了动作可读性，把 Combat Camera 固化成全程中全景 / 中景连续跟拍。

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

Phase 12 新的办公室 Prompt 又暴露：

- Mandatory Prompt Assembly 已经生效；
- Continuous Action Spine 与 Temporal Packing 明显改善；
- 但 Camera 被收敛成“中全景 / 准中景为主 + 低复杂度连续跟随”；
- `Continuous Action Spine` 被隐性理解为“Camera 也应尽量连续”；
- 动作电影常见的 Contact / Footwork / Weapon / Reaction / Impact Close-up 与 Editorial Coverage 被压低。

因此当前重点观察：

```text
Upper-body Combat Lock / Kinetic Underfill
Temporal Combat Stretch / Action Underpacking
Action Segmentation / Excessive Neutral Reset
Timeline-induced Action Segmentation
Camera Mobility Underfill
Combat Camera Coverage Lock / Medium-wide Overconstraint
Cut-induced Action Reset
Turn-taking Combat / Initiative Segmentation
Invisible Advantage / Nominal Reversal
Homogeneous Initiative Style / Identity-by-Demographic Shortcut
Flat Combat Intensity
```

这些属于统一 Gate 下的 Failure Signatures，不建立同等数量独立模块。

---

## 3. 第二次 Interactive → Prompt 失败证据

### 3.1 输入

- 15 秒；
- 中国女性 + 中国男性；
- 普通职场服装；
- 两人都是敌对杀手组织的职业杀手；
- 办公室；
- 用户明确要求“贴身搏斗，不要隔着办公桌”；
- Interactive Mode。

### 3.2 当时根因

当时 Runtime 没有读取 `prompt-assembly/control.md`，因此 V2-40 / Final Assembly / Negative Discipline 可被绕过；Single-shot Template 也会把多阶段 Combat 拉回 Hard Timeline。

Phase 11 已修复该 Mandatory-path 问题。

---

## 4. Static Regression Gate

### 4.1 Mandatory Runtime Path

- [x] `SKILL.md` 明确 Action Combat 最终固定读取 `prompt-assembly/control.md`；
- [x] Combat Prompt Assembly 不再占普通 `0-3 Controls` 可选预算；
- [x] `action-combat-video/index.md` 明确 `Final Assembly → Final Preflight → FAIL rewrite → PASS template` 必经链；
- [x] Output Template 不能覆盖 Combat Task 的时间序列化规则；
- [x] Quick / Interactive 均不能跳过 Final Assembly / Preflight。

### 4.2 Choreography Runtime

- [x] Coverage / Exchange Depth / Kinetic Scope 并列；
- [x] Temporal Packing / Motion Handoff / Continuous Action Spine 已接线；
- [x] Intensity / Visible Advantage / Initiative 已收敛为动作原则；
- [x] Camera Complexity 与 Camera Mobility 分离；
- [x] **Action Continuity 与 Shot Continuity 分离；**
- [x] **Camera Coverage 可使用 Master / Medium / Close-up / Insert / Reaction / Impact / Re-establish；**
- [x] **Cut 后必须继承 Position / Direction / Contact / Momentum / Axis / Range；**
- [x] Final Preflight 可拦截 Camera Coverage Lock。

### 4.3 Prompt Assembly / Template

- [x] High-density Combat 默认 Continuous Action Spine + Soft Time Anchors；
- [x] `single-shot-video` 不再等于 one-take；
- [x] Combat 可在单一视频生成单元内部使用有目的的 Cut / Insert / Reaction / Impact；
- [x] Camera Mobility 与 Editorial Coverage 分开；
- [x] 不设置镜头数量 / 特写数量配额；
- [x] Negative Constraints 少而有针对性。

---

## 5. Golden Scenario Contract

```text
Fixed Input
+ Quality Contract
+ Failure Contract
+ Optional Test Anchor
```

> **Benchmark 锁质量，不锁固定动作答案，也不锁固定镜头答案。**

---

## 6. G01｜15 秒办公室高手近身对决

### Fixed Input

- 时长：约 15 秒；
- 场景：普通办公室开放区域；
- 人物：中国女性 + 中国男性，普通职场服装；
- 隐藏身份：敌对组织的专业杀手；
- 风格：现实基础上的电影化近身格斗；
- 用户额外约束：贴身搏斗，不隔着办公桌；
- 目标：高手连续攻防，而不是两三次孤立动作。

### Prompt-level Quality Contract

Final Prompt 必须先满足：

- Setup 很短，贴身 Combat 很快开始；
- 不默认使用多个 1–3 秒 Hard Time Blocks；
- Active Exchange 主要是一条 Continuous Action Spine；
- 较长动作窗口包含连续因果动作流；
- 动作链存在 Motion Handoff；
- Whole-body / Footwork / Hip / Torso / Position / Range / Axis 合理外显；
- Character Identity 不由人口属性快捷映射；
- Counter / Re-counter 不是双方轮流完成完整攻击段；
- Camera 跟随真实 fight-space；
- **动作连续不等于 Camera one-take；**
- **允许根据动作信息使用 Close-up / Insert / Reaction / Impact Shot；**
- **局部 Shot 后在需要时 Re-establish；**
- **Cut 后 Position / Direction / Contact / Momentum / Axis / Range 连续；**
- **不把“中全景 / 中景 + 轻微跟拍”作为唯一安全 Camera 默认；**
- Negative 只保留真实高风险；
- Ending 只占短收束。

### Prompt-level Failure Contract

出现任一明显持续模式即 FAIL / REWRITE：

- 多个默认硬时间盒；
- 每段只有一个宏动作；
- 长时间上肢架手 / 抓腕；
- A 做完一段才轮到 B；
- Camera 因“稳定”几乎不移动；
- **全程几乎只有中全景 / 中景；**
- **Continuous Action Spine 被解释成不能 Cut；**
- **特写 / Insert 后人物空间关系无故重置；**
- Character Identity 被人口属性模板化；
- 长 Negative 清单；
- Ending 提前吞掉交战时间。

### Generated-video Quality Contract

必须观察：

- High Active Combat Coverage；
- 多个连续 Action Phrase；
- Temporal Packing / Motion Handoff；
- Whole-body / Position / Range / Angle / Axis；
- Environment Integration；
- Character Distinction；
- Initiative / Advantage 可见；
- Contact Solidity；
- Intensity Variation；
- **Camera Mobility；**
- **Shot Scale / Editorial Coverage；**
- **Action Continuity Across Cuts；**
- **局部特写与 Master / Re-establish 的空间可读平衡；**
- Signature Moment；
- Ending 短收束。

---

## 7. 其余 Golden Scenarios

- **G02｜力量型 vs 灵活反制型**；
- **G03｜狭窄走廊**；
- **G04｜硬派拳脚**；
- **G05｜短兵器刀战**；
- **G06｜长兵器 vs 短兵器**；
- **G07｜Grapple / Takedown**；
- **G08｜1vN**。

不得为了优化 G01 把所有场景模板化成同一种 Shot Coverage。

---

## 8. Generated Video Quality Metrics

### M01｜Active Combat Coverage Realization
真正有效交战时间。

### M02｜Exchange / Choreography Richness
有效 Phrase / Counter / Continuation 丰富度。

### M03｜Kinetic Scope Realization
Whole-body / Position / Range / Axis / Contact-driven displacement。

### M04｜Motion Continuity / Temporal Packing
是否一招一停、Neutral Reset、时间轴切碎。

### M05｜Character Distinction
双方动作与抢主动方式是否不同。

### M06｜Visible Advantage / Initiative
控制权与主动权变化是否可见。

### M07｜Combat Contact Solidity
Commitment / Transfer / Reaction / Consequence。

### M08｜Environment Integration
是否真正改变线路 / Position / Range / Advantage。

### M09｜Camera Readability + Mobility
动作是否看清，Camera 是否跟随空间变化。

### M10｜Shot Scale / Editorial Coverage
是否根据动作信息动态切换 Master / Medium / Close-up / Insert / Reaction / Impact / Re-establish，而不是全程中景或无意义乱切。

### M11｜Action Continuity Across Cuts
Cut 前后 Position / Direction / Contact / Momentum / Axis / Range 是否连续。

### M12｜Intensity / Signature
连续战斗是否有层次；Signature 是否形成真实峰值。

### M13｜Spatial / Physical Continuity
Position / Range / Condition / Weapon / Environment State 连续性。

---

## 9. Prompt Intent → Generated Result Gap

每次必须记录计划与成片差距，例如：

```text
Planned Coverage: High
Observed Coverage: Low / Medium

Planned Motion: whole-body + route change
Observed Motion: upper-body locked

Planned Flow: continuous counter / re-counter
Observed Flow: one action every 1–2 seconds with reset

Planned Camera: mobile + varied coverage
Observed Camera: medium-wide locked / near-static

Planned Cut Continuity: action state inherited
Observed Cut Continuity: reset after every cut
```

---

## 10. Benchmark Run Record

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

Planned Quality Contract:
Observed Result:
Metric Notes:
Prompt Intent → Generated Result Gap:
Failure Signature:
Pass / Partial / Fail:
Next Adjustment:
```

---

## 11. Phase 12 Prompt-level G01 Gate

使用同一办公室输入重新跑 Interactive → Final Prompt。

### 必须记录

- Read 列表；
- Interactive 问题与推荐；
- Final Prompt；
- Prompt-level Quality Contract PASS / PARTIAL / FAIL；
- Camera Coverage 类型；
- 与上一版 Prompt 的结构差异。

### Phase 12 Pass 条件

至少满足：

- `prompt-assembly` 确实进入 Runtime；
- 不再自动输出多个 Hard Time Blocks；
- 不再人口属性直接推打法；
- 不再违背“贴身搏斗”初始化；
- Action Spine 有更高 Temporal Packing / Motion Handoff；
- Whole-body / Spatial Movement 明显；
- Camera Mobility 与 fight-space 对应；
- **Camera Coverage 不再被锁成全程中全景 / 中景；**
- **允许有价值的 Contact / Footwork / Reaction / Impact Shot；**
- **Cut 后动作状态连续；**
- Negative 没有无依据剧情限制。

如果 Phase 12 FAIL：先修 Runtime / Template / Concrete Knowledge，不进入真实视频生成，也不新增一级抽象机制。

---

## 12. Phase 13 Generated Video 验收口径

Phase 12 Prompt-level PASS 后才重新生成 G01。

至少需要看到：

- 真实交战时间增加；
- 不再主要锁在上半身；
- 动作不再每 1–2 秒归零；
- Camera 既能稳定跟随空间，也有电影化局部 Coverage；
- Cut 不破坏 Action Continuity；
- 优势 / 主动权变化可见；
- Contact 与 Intensity 不因动作增加而崩坏。

如果仍失败，优先回溯：

1. Concrete Choreography / Fighting Knowledge；
2. Final Prompt Externalization；
3. Model Combat Capability / Temporal Following；
4. Camera Coverage / Action simultaneous capacity；
5. 现有 Choreography Rule 是否实际执行。

> **优先修实现与具体动作知识，不优先继续增加抽象机制。**

---

## 13. 当前状态

- V2-35～V2-46 Spec：✅ 已记录；
- Phase 11 Mandatory Final Assembly / Preflight：✅ Static PASS；
- Single-shot Combat Override：✅ 已升级，明确不等于 one-take；
- Camera Direction：✅ 已支持 Cinematic Combat Coverage；
- Choreography Camera Gate：✅ 已加入 Action Continuity ≠ Shot Continuity；
- Prompt Assembly：✅ 已支持 Camera Mobility + Editorial Coverage；
- Phase 12 Prompt-level G01：⏳ **等待新一轮同输入测试**；
- Phase 13 G01 Actual Generated Video：⏳ **未执行，不得宣称质量 PASS。**