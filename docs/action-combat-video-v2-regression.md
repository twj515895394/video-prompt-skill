# Action Combat Video V2 Regression & Quality Benchmark

> 状态：V2 运行规则已按第一次真实成片反馈重新实现；**新的静态接线需复核，真实成片 Phase 8 必须重新生成，不得沿用旧 PASS。**
>
> 设计依据：`docs/action-combat-video-v2-spec.md`
>
> 实施计划：`docs/action-combat-video-v2-implementation-plan.md`

## 1. 验证原则

```text
Level 1｜Static / Structural Regression
→ 规则、路由、序列化、Gate 是否真正接线

Level 2｜Generated Video Quality Regression
→ 成片是否真正连续打起来
```

> **静态规则正确只是必要条件；真实成片质量是最终验收。**

本轮特别避免一个错误：如果成片仍不好，不优先继续增加更多抽象概念，而先检查 Concrete Choreography、Final Prompt Externalization、Model Capability 与现有规则是否真正兑现。

---

## 2. 第一次真实成片暴露的核心失败

原 G01 办公室高手 1v1 的真实测试暴露：

- V1 / 初版 V2 的真实有效交战仍偏少；
- 动作主要锁在上半身，脚步 / 膝髋 / 躯干 / 重心和空间位移不足；
- Camera 的“稳定”被执行成近似固定；
- 3–4 秒时间块只承载一个宏动作，动作被摊薄；
- 每 1–2 秒一个动作，动作完成后归位再起手；
- Hard Timeline Blocks 强化动作分段；
- 双方容易轮流出招，而不是在动作过程中抢 Initiative；
- Advantage / Reversal 可能只存在于文字描述；
- 连续动作若简单加速，又可能退化成全程同速、同压力。

因此本轮重点观察以下 Failure Signatures：

```text
Upper-body Combat Lock / Kinetic Underfill
Temporal Combat Stretch / Action Underpacking
Action Segmentation / Excessive Neutral Reset
Timeline-induced Action Segmentation
Camera Mobility Underfill
Turn-taking Combat / Initiative Segmentation
Invisible Advantage / Nominal Reversal
Homogeneous Initiative Style
Flat Combat Intensity
```

这些属于少数统一运行合同下的观察结果，不代表必须建立九个独立运行模块。

---

## 3. Static Regression Gate（本轮）

### 3.1 Choreography Runtime

必须确认：

- [ ] Planning Gate 位于具体 Phrase 设计前；
- [ ] Coverage / Exchange Depth / Kinetic Scope 三个充分性维度并列存在；
- [ ] Temporal Action Packing 已接线；
- [ ] Motion Handoff / Neutral Reset Discipline 已接线；
- [ ] Continuous Action Spine + Soft Time Anchors 已成为高密度 Combat 默认；
- [ ] Combat Intensity Curve 已接线但不是固定三段式；
- [ ] Visible Advantage / Initiative Handoff 已转成动作原则；
- [ ] Character Identity 影响抢主动方式，但没有职业模板；
- [ ] Camera Complexity 与 Camera Mobility 正式分离；
- [ ] Final Preflight Gate 可以否决并内部重写。

### 3.2 Prompt Assembly

必须确认：

- [ ] Action Language Dominance；
- [ ] High-density Combat 默认不机械使用 1–3 秒硬时间盒；
- [ ] Hard Timeline 只有明确理由才使用；
- [ ] Kinetic Scope 被外显为全身 / 空间动作；
- [ ] Advantage / Initiative 不主要通过 Meta 说明；
- [ ] Stable Camera 不被序列化成 Static Camera；
- [ ] Negative Constraints 少而有针对性；
- [ ] Prompt Assembly 失败时先重写，而不是直接交付。

### 3.3 Interactive

必须确认：

- [ ] 不过早默认先问“谁赢”；
- [ ] 高手连续对决不会漏掉相关 Choreography Profile；
- [ ] Character Identity 的高价值分叉优先于可自动推导 Camera 问卷；
- [ ] Kinetic / Contact / Packing / Handoff / Sufficiency / Preflight 不成为固定问题；
- [ ] 用户要求收口时立即执行完整内部规划并交付。

### 3.4 Diagnostic

`combat-choreography-underfill` 应统一识别 Coverage、Kinetic、Temporal、Motion Handoff、Camera Mobility、Initiative / Advantage、Intensity 等 Under-realization，而不是新增大量重复 Diagnostic。

---

## 4. Golden Scenario Contract

每个 Golden Scenario 使用：

```text
Fixed Input
+ Quality Contract
+ Failure Contract
+ Optional Test Anchor
```

> **Benchmark 锁质量，不锁固定动作答案。**

---

## 5. G01｜15 秒办公室高手近身对决（当前主回归）

### Fixed Input

- 时长：约 15 秒；
- 场景：下班后的普通办公室；
- 人物：中国女性 + 中国男性，普通职场服装；
- 隐藏身份：敌对组织的专业杀手；
- 风格：现实基础上的电影化近身格斗；
- 目标：高手连续攻防，而不是两三次孤立动作；
- Ending：按当前测试版本锁定，不允许 Ending 提前吞掉 Active Exchange。

### Quality Contract

必须观察：

- High Active Combat Coverage 真正兑现；
- 多个连续 Action Phrase，但 Phrase 间不中断；
- Temporal Packing 足够，不是 3–4 秒一个宏动作；
- Motion Handoff 明显，Neutral Reset 稀缺；
- Whole-body Engagement 明显，不长期锁在手臂 / 上半身；
- Position / Range / Angle / Axis 至少在当前场景合理范围内持续变化；
- 环境推动路线 / Range / Position，而不是只把人按在桌边；
- Character Identity 可从具体动作选择看出；
- Counter / Re-counter 的 Initiative 可在动作过程中转移；
- Major Advantage Reversal 如果存在，观众能从动作压力看见；
- Camera 使用简单连续 Mobility 跟随 fight-space，Stable ≠ Static；
- Contact 有 Solidity；
- 连续 Combat 内存在强度层次；
- 约 1 个主要 Signature Moment；
- Ending 只做短收束。

### Failure Contract

出现任一明显持续模式都应标记：

- 只打两三次；
- 主要为前臂 / 抓腕 / 肩部原地交互；
- 一两秒一个动作，动作之间回到中性站位；
- 时间块边界明显停顿 / Reset；
- A 打一段、B 打一段的轮流表演；
- Prompt 说“逆转”但控制关系不变；
- 两人抢主动方式完全同质；
- Camera 长期近似固定；
- 全程同速同压力；
- 长时间静态 Control；
- Camera Shake / Audio 代替真实 Contact；
- 最后数秒提前 Pose。

---

## 6. 其余 Golden Scenarios

保留原 V2 八类覆盖面，具体动作答案不锁死：

- **G02｜力量型 vs 灵活反制型**：体型 / Character Identity / momentum / angle；
- **G03｜狭窄走廊**：空间约束、Route / Axis / constrained-space reversal；
- **G04｜硬派拳脚**：Contact Solidity 与重量层次；
- **G05｜短兵器刀战**：Threat Line / Range / Parry / Initiative；
- **G06｜长兵器 vs 短兵器**：Weapon Distance Transition；
- **G07｜Grapple / Takedown**：Balance / Leverage / Position Consequence；
- **G08｜1vN**：Target Handoff / Multi-character / Spatial Readability。

本轮实现不得为了优化 G01 而把所有场景都模板化成同一种高速办公室式连续打斗。

---

## 7. Generated Video Quality Metrics

### M01｜Active Combat Coverage Realization
真正有效交战时间。

### M02｜Exchange / Choreography Richness
有效 Phrase / Counter / Continuation 丰富度。

### M03｜Kinetic Scope Realization
Whole-body / Position / Range / Axis / Contact-driven displacement 是否兑现。

### M04｜Motion Continuity / Temporal Packing
是否一招一停；是否有过多 Neutral Reset；是否被时间轴切碎。

### M05｜Character Distinction
双方动作选择与抢主动方式是否不同。

### M06｜Visible Advantage / Initiative
控制权与主动权变化是否从动作看得见。

### M07｜Combat Contact Solidity
Commitment / Transfer / Reaction / Consequence。

### M08｜Environment Integration
是否真正改变线路 / Position / Range / Advantage。

### M09｜Camera Readability + Mobility
动作是否看清，同时 Camera 是否跟随真实空间变化。

### M10｜Intensity / Signature
连续战斗是否有层次；Signature 是否形成真实峰值。

### M11｜Spatial / Physical Continuity
Position / Range / Condition / Weapon / Environment State 连续性。

---

## 8. Prompt Intent → Generated Result Gap

每次必须记录“计划”和“成片实际”之间的差距，例如：

```text
Planned Coverage: High
Observed Coverage: Low / Medium

Planned Motion: whole-body + route change
Observed Motion: upper-body locked

Planned Flow: continuous counter / re-counter
Observed Flow: one action every 1–2 seconds with reset

Planned Camera: stable mobile tracking
Observed Camera: near-static
```

Prompt 写了某条规则不等于成片兑现。

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

Planned Quality Contract:
Observed Result:
Metric Notes:
Prompt Intent → Generated Result Gap:
Failure Signature:
Pass / Partial / Fail:
Next Adjustment:
```

不同模型 / 版本 / 参数下，不能把所有变化直接归因给 Skill。

---

## 10. Phase 8 当前验收口径

本轮实现完成后必须重新生成 G01；旧视频只能作为 Failure Evidence，不能作为新版本 PASS 证据。

G01 至少需要看到相对旧结果的明确改善：

- 真实交战时间增加；
- 不再主要锁在上半身；
- 动作不再每 1–2 秒归零；
- Camera 有稳定但真实的跟随；
- 优势 / 主动权变化看得见；
- Contact 与 Intensity 不因动作增加而崩坏。

如果新成片仍失败，优先回溯：

1. Concrete Choreography / Fighting Knowledge；
2. Final Prompt Externalization；
3. Model Combat Capability / Temporal Following；
4. Action / Camera Execution Budget；
5. 现有 Choreography Rule 是否实际执行。

> **优先修实现与具体动作知识，不优先继续增加抽象机制。**

---

## 11. 当前状态

- V2-35～V2-43 相关真实成片反馈：✅ 已映射进运行规则；
- Choreography Playbook：✅ 已收敛实现；
- Prompt Assembly：✅ 已更新连续动作序列化；
- Interactive Contract：✅ 已修正规划 / 追问顺序；
- Underfill Diagnostic：✅ 已扩展综合 Failure Signatures；
- 新版 Static Regression：⏳ 需要基于当前 commit 再检查；
- 新版 G01 Actual Generated Video：⏳ **未执行，不得宣称质量 PASS。**
