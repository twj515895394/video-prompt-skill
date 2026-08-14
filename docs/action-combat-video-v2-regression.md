# Action Combat Video V2 Regression & Quality Benchmark

> 状态：**Phase 11 Mandatory-path Rewire 已完成静态接线；Phase 12 Prompt-level G01 待重新生成 Prompt 验收；真实成片必须在 Phase 13 重新生成，不得沿用旧 PASS。**
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
→ 成片是否真正连续打起来
```

> **静态规则正确只是必要条件；Prompt 本身不合格时禁止直接进入真实视频；真实成片质量是最终验收。**

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
Homogeneous Initiative Style / Identity-by-Demographic Shortcut
Flat Combat Intensity
```

这些属于少数统一运行合同下的观察结果，不代表必须建立同等数量独立运行模块。

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

### 3.2 实际运行读取

实际读取了：

- `SKILL.md`；
- input / task indexes；
- action-combat `index / core / choreography / modern`；
- interactive contract；
- single-shot template；
- choreography profiles / fighting profiles；
- subject-motion / camera-direction / spatial-blocking；
- cinematic style；
- generic model。

**没有读取 `prompt-assembly/control.md`。**

因此当时的 Runtime 合法绕过了 V2-40 / Final Assembly / Negative Discipline。

### 3.3 最终 Prompt 典型结构

```text
0–1.5s：对峙 / 进入
1.5–4s：男方压迫，女方偏开反击
4–7s：男方抓控，女方脱离
7–10s：男方重新压迫，女方防守
10–13.5s：男方抱控，女方反转
13.5–15s：控制收尾
```

### 3.4 Prompt-level 判定

- **V2-35 Final Preflight：FAIL** — Hard Timeline、无依据 Negative 等没有被 Gate 否决；
- **V2-36 Kinetic Scope：PARTIAL/FAIL** — 上肢 / 抓控仍占主体；
- **V2-37 Camera Mobility：PARTIAL** — 只有“低幅度稳定侧跟”，没有真正形成 fight-space Camera Path；
- **V2-38 Temporal Packing：FAIL** — 多个 2.5–3.5 秒窗口仍只承载一个宏事件；
- **V2-39 Motion Handoff：PARTIAL/FAIL** — 宏观仍是“一方做一组，另一方解决”；
- **V2-40 Continuous Spine：FAIL** — 直接输出六个 Hard Time Blocks；
- **V2-41 Intensity Curve：PARTIAL** — 有局部压力变化，但被硬块割裂；
- **V2-42 Visible Advantage：PARTIAL/PASS** — 门框 / 墙面压迫有一定可见优势证据；
- **V2-43 Initiative Handoff：FAIL** — 主要仍是轮流式宏动作；
- **V2-44 Character Identity Guard：FAIL（反例）** — 推荐直接把年轻女性推成“速度 / 角度 / 闪避”，把年长矮胖男性推成“体重 / 力量 / 抓控”；
- **Negative Discipline：FAIL** — 用户未要求禁止武器，却自动加入“武器或枪械”等剧情限制；
- **Range Initialization：FAIL / 用户意图偏离** — 用户明确“贴身搏斗”，Prompt 却从约 2.5 米 + 1.5 秒对峙开始。

### 3.5 根因结论

此失败样本不能简单归因于 Choreography Rule 不足。主要根因按优先级是：

```text
A. Prompt Assembly / Final Preflight 不是必经路径
→ B. Single-shot 通用时间轴规则覆盖 V2-40
→ C. Character Identity 推荐存在人口属性快捷映射
→ D. Concrete Choreography 仍偏上肢 / 抓控
→ E. 最后才是模型执行能力
```

Phase 11 只修 A / B / C；D 留到 Phase 12 Prompt-level 结果之后再决定是否进入 Concrete Knowledge Audit。

---

## 4. Static Regression Gate（Phase 11）

### 4.1 Mandatory Runtime Path

- [x] `SKILL.md` 明确 Action Combat 最终固定读取 `prompt-assembly/control.md`；
- [x] Combat Prompt Assembly 不再占普通 `0-3 Controls` 可选预算；
- [x] `action-combat-video/index.md` 明确 `Final Assembly → Final Preflight → FAIL rewrite → PASS template` 必经链；
- [x] Output Template 只能承载结果，不能覆盖 Combat Task 的时间序列化规则；
- [x] Quick / Interactive 均不能跳过 Final Assembly / Preflight。

### 4.2 Choreography Runtime

- [x] Planning Gate 位于具体 Phrase 设计前；
- [x] Coverage / Exchange Depth / Kinetic Scope 三个充分性维度并列存在；
- [x] Temporal Action Packing 已接线；
- [x] Motion Handoff / Neutral Reset Discipline 已接线；
- [x] Continuous Action Spine + Soft Time Anchors 已成为高密度 Combat 默认；
- [x] Combat Intensity Curve 已接线但不是固定三段式；
- [x] Visible Advantage / Initiative Handoff 已转成动作原则；
- [x] Initiative Handoff 受 Character Identity 约束但没有新增状态机；
- [x] Camera Complexity 与 Camera Mobility 正式分离；
- [x] Final Preflight Gate 可以否决并内部重写。

### 4.3 Prompt Assembly / Template

- [x] Action Language Dominance；
- [x] High-density Combat 默认不机械使用 1–3 秒硬时间盒；
- [x] Hard Timeline 只有用户 / 同步 / Model Benchmark 等明确理由才使用；
- [x] Single-shot Template 已增加 Action Combat Override；
- [x] Kinetic Scope 被要求外显为全身 / 空间动作；
- [x] Stable Camera 不被序列化成 Static Camera；
- [x] Negative Constraints 少而有针对性；
- [x] Prompt Assembly / Preflight 失败时先内部重写，而不是直接交付。

### 4.4 Interactive

- [x] 不过早默认先问“谁赢”；
- [x] 高手连续对决不会漏掉相关 Choreography Profile；
- [x] Character Identity 的高价值分叉优先于可自动推导 Camera 问卷；
- [x] Character Identity Recommendation Guard 明确禁止职业 / 性别 / 年龄 / 外貌 / 体型直接映射打法；
- [x] Kinetic / Contact / Packing / Handoff / Sufficiency / Preflight 不成为固定问题；
- [x] 用户要求收口时立即执行完整内部规划、Assembly 与 Preflight。

### 4.5 Diagnostic

`combat-choreography-underfill` 继续统一识别 Coverage、Kinetic、Temporal、Motion Handoff、Camera Mobility、Initiative / Advantage、Intensity 等 Under-realization，不新增大量重复 Diagnostic。

### Phase 11 Static Gate

> **PASS — Mandatory-path / Template Override / Interactive Identity Guard 已完成静态接线。**

注意：该 PASS 只证明“现在必须走这条路”，**不证明下一次 Final Prompt 一定已经达到质量要求。Phase 12 必须用同一 G01 输入重新跑 Prompt。**

---

## 5. Golden Scenario Contract

每个 Golden Scenario 使用：

```text
Fixed Input
+ Quality Contract
+ Failure Contract
+ Optional Test Anchor
```

> **Benchmark 锁质量，不锁固定动作答案。**

---

## 6. G01｜15 秒办公室高手近身对决（当前主回归）

### Fixed Input

- 时长：约 15 秒；
- 场景：下班后的普通办公室开放区域；
- 人物：中国女性 + 中国男性，普通职场服装；
- 隐藏身份：敌对组织的专业杀手；
- 风格：现实基础上的电影化近身格斗；
- 用户额外约束：贴身搏斗，不隔着办公桌；
- 目标：高手连续攻防，而不是两三次孤立动作；
- Ending：不允许 Ending 提前吞掉 Active Exchange。

### Prompt-level Quality Contract

在进入真实视频前，Final Prompt 本身必须先满足：

- 不把“贴身搏斗”初始化成明显远距离 + 长 Setup；
- 不默认使用多个 1–3 秒 Hard Time Blocks；
- Active Exchange 主要是一条 Continuous Action Spine；
- 一个较长动作窗口不能只有一个宏动作；
- 动作链存在可见 Motion Handoff，不能主要靠“然后 / 随后”；
- Whole-body / Footwork / Hip / Torso / Center-of-mass / Position / Range / Axis 至少按当前动作形式合理外显；
- Character Identity 不由人口属性快捷映射；
- Counter / Re-counter 不是双方轮流完成完整攻击段；
- Camera 有简单连续 Mobility，跟随实际 fight-space；
- Negative 只保留当前真实高风险，不自行禁止用户未提及的剧情元素；
- Ending 只占短收束。

### Generated-video Quality Contract

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
- Character Identity 被职业 / 性别 / 年龄 / 体型快捷模板化；
- Camera 长期近似固定；
- 全程同速同压力；
- 长时间静态 Control；
- Camera Shake / Audio 代替真实 Contact；
- 最后数秒提前 Pose；
- 用户未要求的剧情禁止项被写进 Negative。

---

## 7. 其余 Golden Scenarios

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

## 8. Generated Video Quality Metrics

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

## 9. Prompt Intent → Generated Result Gap

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

不同模型 / 版本 / 参数下，不能把所有变化直接归因给 Skill。

---

## 11. Phase 12 Prompt-level G01 Gate

使用与第二次失败样本相同或等价的办公室输入，重新跑 Interactive → Final Prompt。

### 必须记录

- 实际 Read 列表；
- 是否读取 `prompt-assembly/control.md`；
- Interactive 问题与推荐；
- Final Prompt；
- Prompt-level Quality Contract 每项 PASS / PARTIAL / FAIL；
- 与第二次失败 Prompt 的结构差异。

### Phase 12 Pass 条件

至少满足：

- `prompt-assembly` 确实进入 Read / Runtime；
- 不再自动输出六个类似 Hard Time Blocks；
- 不再从人口属性直接推打法；
- 不再从 2.5m + 1.5s 对峙开始违反“贴身搏斗”；
- Action Spine 内明显比旧 Prompt 有更高 Temporal Packing / Motion Handoff；
- Whole-body / Spatial Movement 比旧 Prompt 更明显；
- Camera Mobility 与 fight-space 对应；
- Negative 没有无依据剧情限制。

如果 Phase 12 FAIL：先修 Runtime / Template / Concrete Knowledge，**不进入真实视频生成，也不继续新增一级抽象机制。**

---

## 12. Phase 13 Generated Video 验收口径

Phase 12 Prompt-level PASS 后才重新生成 G01；旧视频只能作为 Failure Evidence，不能作为新版本 PASS 证据。

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

## 13. 当前状态

- V2-35～V2-45 Spec / Traceability：✅ 已重新对齐；
- Phase 11 Mandatory Final Assembly / Preflight：✅ Static PASS；
- Single-shot Combat Override：✅ Static PASS；
- Interactive Character Identity Guard：✅ Static PASS；
- Choreography Playbook Consolidation：✅ 保留，待 Prompt-level 验证；
- Prompt Assembly：✅ 已成为 Combat 必经出口；
- Underfill Diagnostic：✅ 集中式保留；
- Phase 12 Prompt-level G01：⏳ **待执行**；
- Phase 13 G01 Actual Generated Video：⏳ **未执行，不得宣称质量 PASS。**