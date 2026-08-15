# Action Combat Video V2 Implementation Plan

> 状态：**V2-01～34 初版实施已完成；V2-35～45 已完成 Traceability Re-baseline；Phase 11 Mandatory-path Rewire 已完成；V2-46 / V2-47 已实施；当前进入 V2-48 / V2-49 的 Phase 12 Prompt-quality Calibration 实施。**
>
> 当前设计真源：`docs/action-combat-video-v2-spec.md`
>
> Traceability Audit：`docs/action-combat-video-v2-traceability-audit.md`
>
> 回归真源：`docs/action-combat-video-v2-regression.md`
>
> 核心验收原则：**真实成片质量优先于静态规则覆盖；任何 Runtime 修改必须能从 Spec → Plan → Runtime → Regression 追踪。**
>
> 文档治理约定：当前主 Spec 已较长；本轮继续以其已确认的 V2-48 / V2-49 为设计真源。后续若再出现新一轮较大设计增量，优先新建新的 Spec 文档承载，不继续无限追加当前主 Spec。

---

## 1. 本轮实施目标

本轮不新增 Combat 一级 Engine，不扩建 Fighting Library，不修改 Model Adapter。

目标只解决最新办公室 G01 Prompt 暴露的四类真实问题：

1. **Interactive 单轮问题夹带 downstream 决策**；
2. **Camera Intent 在存在重大导演分叉时仍可能被静默替用户决定**；
3. **关键 Action Phrase 动作颗粒度偏粗，仍大量依赖“连续格挡 / 快速反制 / 不断换位”等抽象描述**；
4. **Initiative Handoff 与 Ending Coverage 虽已有机制，但 Final Prompt 仍可能出现轻微回合感或 Ending 吞掉有效交战时间。**

本轮的设计原则：

> **不靠增加固定询问轮次解决动作执行问题。**
>
> **用户决定导演方向，系统负责把方向展开成具体、连续、可执行的动作。**
>
> **关键因果动作具体，次要过渡动作可以压缩。**
>
> **Camera 创作意图可条件询问，Camera 基础质量仍由系统自动保证。**

---

## 2. 当前阶段与实施顺序

```text
Phase 0–9  V2-01～34 初版设计 / 实现 / 静态回归
→ Phase 10 Spec / Traceability Re-baseline
→ Phase 11 Runtime Mandatory-path Rewire
→ Phase 12A V2-46 Camera Coverage Correction            ✅ 已实施
→ Phase 12B V2-47 Interactive Question Budget           ✅ 已实施
→ Phase 12C V2-48 Interactive Purity + Camera Exposure   🚧 本轮实施
→ Phase 12D V2-49 Executable Action Granularity          🚧 本轮实施
→ Phase 12E Same-input G01 Prompt Regression              ⏸ 实施后测试
→ Phase 13 Generated Video Re-run + Model Calibration     ⏸ Prompt PASS 后
```

本轮固定顺序：

```text
Spec 已确认
→ Implementation Plan
→ Runtime File Mapping
→ Runtime 修改
→ Regression Contract 更新
→ Static Read / Rule Gate
→ 同一办公室 G01 Prompt 回归
→ Prompt PASS
→ 真实视频生成
```

不得跳过 Plan 直接改 Runtime。

---

## 3. 已完成基线，不在本轮重复开发

以下能力已经存在并继续作为本轮基础：

- Mandatory Combat Prompt Assembly；
- Combat Final Preflight；
- Continuous Action Spine + Soft Time Anchors；
- Temporal Action Packing；
- Motion Handoff；
- Kinetic Scope；
- Visible Advantage；
- Initiative Handoff；
- Character Identity Demographic Guard；
- Action Continuity ≠ Shot Continuity；
- Camera Readability + Mobility + Editorial Coverage；
- Interactive High-value Question Budget + 10-round Safety Cap。

本轮不是重新设计这些机制，而是让其中尚未充分兑现的部分进入更强的执行表达。

---

## 4. 本轮设计增量

### V2-48｜Interactive Decision Purity + Conditional Camera Intent Exposure

核心要求：

- `One Question, One Primary Decision Node`；
- 当前问题可以说明 downstream 影响，但不得提前锁死未确认的 downstream 选择；
- Camera 不固定必问，但进入高价值候选节点；
- 当固定 / 克制机位、one-take、完整动作可读、电影冲击型 Coverage、贴身沉浸等多个方向都合理且显著改变成片时，应条件暴露 Camera Intent；
- Camera 问的是用户可理解的导演观看策略，不问内部 Camera 参数。

### V2-49｜Executable Action Granularity

核心要求：

承担主要战斗因果的 Action Phrase 应尽量具备：

```text
Current Body / Range State
→ Specific Physical / Weapon Action
→ Contact / Evasion / Interception
→ Opponent Immediate Response
→ Footwork / Axis / Range / Position Consequence
→ Immediate Continuation Entry
```

这不是固定六步模板；重点是模型能够理解“当前身体状态下具体发生什么，以及下一动作为什么立刻能发生”。

禁止关键数秒主要依赖：

- 连续格挡；
- 快速反制；
- 贴身缠斗；
- 持续压迫；
- 不断换位；
- 高频攻防；
- 双方互有来回。

同时禁止走向逐拳逐脚机械枚举。

---

## 5. Runtime File Mapping

### 5.1 `assets/templates/mode-interactive-output-contract.md` — Modify

对应：V2-48。

实施内容：

1. 在 V2-47 High-value Question Filter 基础上增加 **Decision Purity Check**：

```text
当前问题的 Primary Planning Node 是什么？
→ 推荐答案是否只解决该节点？
→ 是否提前锁死尚未确认的 Character Identity / Camera / Ending / Result？
```

2. 明确推荐答案允许：
   - 解释 downstream 影响；
   - 给出系统推荐；
   - 说明为什么该选择重要。

   但不允许把 downstream 选择直接写成既定事实。

3. 将 Camera Intent 正式加入 **Conditional High-value Node Pool**：
   - 用户已明确 → 继承；
   - 单一明显合理方向 → 静默推导；
   - 多个明显不同、都会显著改变成片的导演观看策略 → 暴露 Camera Intent 一问。

4. Camera 问题使用观看策略语言，例如：
   - 电影冲击型 Coverage；
   - 完整动作可读型；
   - 贴身沉浸型；
   - 固定 / 克制机位型；
   - 一镜到底型。

   这些仅为候选表达，不写成固定五选一模板。

5. 不新增固定 Camera 询问轮次，不改变 10-round Safety Cap。

### 5.2 `references/tasks/action-combat-video/choreography-playbook.md` — Modify

对应：V2-49；同时强化已有 V2-43 / V2-08。

实施内容：

1. 在 Action Phrase 构造阶段加入 **Executable Granularity Contract**。

2. 关键 Phrase 不允许只停留在战术概括；必须把关键因果外显为身体 / 武器动作事实。

3. 强化 Initiative Handoff 的实际构造：
   - Counter / Re-counter 优先发生在对方动作尚未完全结束时；
   - 使用 Contact / Footwork / Axis / Range / Recovery Window 作为下一动作入口；
   - 避免 `A 完成 → B 开始` 的回合式语义。

4. 强化 Action Execution Budget 的理解：
   - 细化关键因果动作；
   - 压缩次要过渡；
   - 不把颗粒度提升实现成动作数量无限增长。

5. Ending Coverage Protection：
   - Ending 必须继承最后一次 Contact / Position / Momentum / Advantage；
   - High Coverage 短 Combat 中，长时间 Pose / 对视不能自动占用最后数秒；
   - 用户明确要求长悬停 / 情绪 Ending 时才允许扩大 Ending Budget。

6. Planning / Preflight 增加 `Abstract Action Block` 检查入口。

### 5.3 `references/controls/prompt-assembly/control.md` — Modify

对应：V2-49 的最终外显；同时保持 V2-46。

实施内容：

1. Combat Final Assembly 不得把已经具体的 Choreography Plan 压缩回泛化动作摘要。

2. 对承担主要 Active Exchange 的文本，优先保留：
   - 具体动作部位 / 武器线路；
   - Contact / Evasion / Interception；
   - 对手即时响应；
   - Footwork / Axis / Range / Position 后果；
   - 下一动作入口。

3. 抽象词可以承担：
   - 风格摘要；
   - 次要过渡；
   - 全局节奏说明。

   但不能替代关键动作链。

4. Initiative Handoff 序列化优先使用动作重叠 / 状态继承语言，例如语义上体现：
   - 尚未收势；
   - 接触后立即；
   - 脚步尚未落稳；
   - 顺前一偏转 / 抓控 / 轴线变化直接进入。

   不要求固定关键词。

5. Ending 描述必须与 Ending Budget 匹配；若 Ending 文本明显比有效交战更长、更细，应内部压缩。

6. 保持 V2-46：颗粒度提升不能导致 Camera 再退化成全程中景，也不能因为 Close-up / Cut 把动作重新分段。

### 5.4 `references/tasks/action-combat-video/index.md` — Review-first，必要时轻量 Modify

目的：确认 Mandatory Path 已明确包含：

```text
Planning
→ Stage-2 Execution Knowledge
→ Concrete Action Phrase
→ Prompt Assembly
→ Final Preflight
```

只有当前 index 对 Stage-2 → Concrete Phrase 的职责表达仍不够强时，才做最小文字强化。

不新增新 Runtime 节点。

### 5.5 `references/libraries/combat-fighting-profiles/library.md` — 本轮默认不改

本轮先不扩 Library。

只有实施 V2-49 后，相同 G01 仍持续出现：

- 连续格挡；
- 快速反制；
- 不断换位；
- 抽象打法标签；

而 Choreography / Assembly 已正确要求具体动作时，才进入 **Concrete Choreography Knowledge Audit**。

届时再判断现有 Fighting / Martial / Weapon 知识是否缺乏可组合动作链，而不是现在预先扩库。

### 5.6 `references/controls/camera-direction/control.md` — 本轮不主动改

V2-46 已经实现 Camera Coverage。

本轮 Camera 变化主要是 **Interactive 是否把 Camera Intent 暴露给用户**，不是 Camera Control 再增加新能力。

只有回归证明 Camera Intent 选择无法被当前 Control 实现时才继续修改。

### 5.7 `assets/templates/single-shot-video-template.md` — 本轮不主动改

V2-46 已解决 `single-shot-video ≠ one-take`。

本轮仅回归确认该规则没有被 V2-49 的动作细化破坏。

---

## 6. Final Preflight 增量

本轮不新建新的 Gate 系统，只扩展现有 Combat Final Preflight。

新增 / 强化检查：

### A. Executable Action Granularity

FAIL 条件：

- 关键数秒主要靠抽象动作词承担；
- Character Identity 有打法标签但没有具体动作证据；
- Initiative / Advantage 只有 Meta 说明；
- Camera / Audio 比身体动作描述更具体。

Failure Signature：

> `Abstract Action Block / Non-executable Choreography Summary`

### B. Initiative Handoff Externalization

FAIL 条件：

- `A 完成攻击 → B 开始反击` 反复出现；
- Counter 没有继承 Contact / Axis / Footwork / Range / Recovery；
- 双方各自拥有完整独立回合。

继续复用：

> `Turn-taking Combat / Initiative Segmentation`

不新建新 Failure。

### C. Ending Coverage Protection

FAIL 条件：

- High Coverage 15s Combat 过早进入长时间对视 / Pose；
- Ending 的文字与事件预算明显吞掉 Active Exchange；
- Ending 未继承最后一次战斗状态，而是重新摆姿势。

继续归入：

- Action Sufficiency；
- Coverage Budget；
- Motion Handoff / Neutral Reset；

不新建 Ending Engine。

### D. Interactive Decision Purity

Interactive Regression FAIL 条件：

- 当前问 Profile，却在推荐里提前决定 Character Identity + Ending + Camera；
- Camera 已存在明显高价值导演分叉，却因“Camera 通常自动推导”完全不允许用户选择；
- Camera 已明确仍重复询问。

---

## 7. Regression Plan

### 7.1 Fixed G01 Input

继续使用完全相同办公室输入，不换场景：

> 使用交互模式，帮我做一段一个女生和男生在办公室打架的15秒电影片段，实际两个人穿着正常的职场服装但其实是2个杀手组织的职业杀手。中国男女，女的22岁长发高马尾漂亮身材完美，男性是一个秃顶又矮又胖的55岁领导，贴身搏斗，不要隔着什么办公桌。

保持：

- Interactive；
- 15s；
- Generic 模型；
- 同一人物与场景输入。

### 7.2 Interactive Gate

记录：

- 实际问题轮数；
- 每轮 Primary Decision Node；
- 推荐答案是否夹带 downstream 决策；
- Camera 是否满足条件暴露逻辑；
- 需求完整后是否及时收口。

轮数多少不是 PASS / FAIL。

### 7.3 Prompt Gate

最终 Prompt 至少满足：

- Setup 短；
- Active Combat 快速开始；
- Continuous Action Spine；
- 无默认 Hard Timeline Blocks；
- 关键 Action Phrase 有具体身体动作；
- Contact / Evasion / Immediate Response 可见；
- Footwork / Axis / Range / Position 后果可见；
- 下一动作从前一状态直接进入；
- Counter / Re-counter 不呈现回合制；
- Whole-body / Spatial / Kinetic Scope 可见；
- Character Identity 通过具体动作体现；
- Camera Coverage 不固化中全景；
- Camera Intent 若被用户明确选择，最终 Prompt 必须兑现；
- Cut 后 Action State 连续；
- Ending 不提前吞掉 Active Exchange；
- Negative Constraints 少而有依据；
- 不出现明显脏文本 / 中英文残片。

### 7.4 Abstract Action Block 专项检查

对 Final Prompt 中每个承担主要有效交战的段落做快速判断：

```text
删掉“连续 / 快速 / 专业 / 高密度 / 反制 / 缠斗”等形容或概括词后，
是否仍然能看清人物具体在做什么、对方怎么立即响应、双方位置 / 轴线 / 距离如何变化？
```

如果答案是否定的，该段不通过 V2-49。

### 7.5 Prompt PASS 后才进入视频

只有 Prompt-level Gate 通过，才进入 Phase 13。

真实视频继续观察：

- Active Combat Coverage Realization；
- 动作是否仍被模型合并 / 丢失；
- Action Granularity → Generated Motion 的兑现度；
- Turn-taking 是否消失；
- Ending 是否吞时；
- Camera Impact / Readability 平衡；
- Contact / Kinetic / Spatial Continuity。

---

## 8. 开发执行顺序

为降低变量数量，按以下顺序开发：

### Step 1｜Interactive Contract

修改：

`assets/templates/mode-interactive-output-contract.md`

只实现 V2-48：

- Decision Purity；
- Conditional Camera Intent Exposure。

完成后静态检查，不立即重新测试 G01。

### Step 2｜Choreography Playbook

修改：

`references/tasks/action-combat-video/choreography-playbook.md`

实现：

- Executable Granularity Contract；
- Initiative Handoff 具体化；
- Ending Coverage Protection；
- Abstract Action Block Preflight。

### Step 3｜Prompt Assembly

修改：

`references/controls/prompt-assembly/control.md`

实现：

- 不把 Concrete Phrase 重新压缩成概括；
- 动作因果细节保留策略；
- Initiative Handoff 序列化；
- Ending 文本 / Budget 控制。

### Step 4｜Combat Router / Index Review

检查：

`references/tasks/action-combat-video/index.md`

仅在需要时做轻量强化，保证：

`Stage-2 Knowledge → Concrete Action Phrase → Assembly → Preflight` 真正明确。

### Step 5｜Regression Contract

修改：

`docs/action-combat-video-v2-regression.md`

新增：

- Interactive Decision Purity；
- Conditional Camera Intent Exposure；
- Executable Action Granularity；
- Abstract Action Block；
- Ending Coverage Protection；
- Initiative Handoff Action-language realization。

### Step 6｜Static Review

确认没有：

- 新建不必要 Engine；
- 新增固定 Interactive 问题；
- Camera 特写数量配额；
- Action 数量配额；
- Fighting Library 无证据扩建；
- Generic Model Adapter 变化。

### Step 7｜Same-input G01 Regression

用户本地运行同一办公室 G01。

收集：

- Read 列表；
- Interactive 全过程；
- Final Prompt。

逐项判定 V2-48 / V2-49。

---

## 9. 本轮明确不改

本轮冻结：

- `references/tasks/action-combat-video/core-playbook.md`；
- `references/tasks/action-combat-video/modern-combat-playbook.md`；
- `references/tasks/action-combat-video/cinematic-wuxia-playbook.md`；
- `references/libraries/combat-fighting-profiles/library.md`；
- Fighting / Martial / Weapon 大规模 Library；
- `references/controls/camera-direction/control.md`，除非实施中发现 V2-48 无法被当前能力承载；
- `assets/templates/single-shot-video-template.md`；
- Model Adapters；
- 新 Combat State Machine；
- 新 Combat Camera Engine；
- 固定动作数量 / 特写数量 / Interactive 轮数配额。

---

## 10. Concrete Choreography Knowledge Audit 进入条件

只有同时满足以下条件才进入下一阶段：

1. Mandatory Path 正确；
2. Stage-2 Knowledge 实际读取 / 可用；
3. Choreography 已要求 Executable Granularity；
4. Prompt Assembly 没有重新压缩动作；
5. Final Preflight 已能拦 Abstract Action Block；
6. 相同 G01 Final Prompt 仍持续缺乏具体动作构造。

满足后才审计：

- Fighting Profile 是否只有风格标签，缺少可组合 Action Chain；
- 是否缺少 Strike / Grapple / Weapon 的具体 Transition；
- 是否缺少 Whole-body / Range / Axis / Footwork 组合知识；
- 是否需要新增少量高价值 Technique Pattern，而不是扩建大全式动作库。

---

## 11. Anti-overdesign / Consolidation

本轮最终 Runtime 合并保持：

```text
Interactive Exposure Contract
→ High-value Question Filter
+ Decision Purity
+ Conditional Camera Intent Exposure
+ Dynamic Stop
+ 10-round Safety Cap

Action Construction Contract
→ Action Phrase
+ Executable Granularity
+ Motion Handoff
+ Initiative Handoff
+ Action Execution Budget

Coverage / Ending Protection
→ Active Combat Coverage
+ Ending Budget
+ Motion Handoff

Camera Contract
→ Readability
+ Mobility
+ Editorial Coverage
```

V2-48 / V2-49 在 Spec 中可以独立追踪，但 Runtime 不分别建设新 Engine。

---

## 12. 当前实施状态

| Phase | 状态 | 说明 |
|---|---|---|
| 0–9 | ✅ 基线完成 | V2-01～34 |
| 10 | ✅ 完成 | Spec / Plan / Mapping 对齐 |
| 11 | ✅ Static PASS | Mandatory Assembly / Preflight |
| 12A | ✅ 已实施 | V2-46 Camera Coverage |
| 12B | ✅ 已实施 | V2-47 Interactive Question Budget |
| 12C | 🚧 待开发 | V2-48 Decision Purity + Conditional Camera Intent |
| 12D | 🚧 待开发 | V2-49 Executable Action Granularity |
| 12E | ⏸ 待 12C/12D | Same-input G01 Prompt Regression |
| 13 | ⏸ 待 Prompt PASS | Generated Video Re-run / Model Calibration |

当前准确状态：

> **Spec V2-48 / V2-49 Confirmed；Implementation Plan Ready；Runtime Development Pending。**

---

## 13. 开发完成后的下一步

完成 Step 1～6 后，不直接扩 Library，也不换测试场景。

继续使用同一办公室 G01 输入，检查：

1. Interactive 问题是否更纯；
2. Camera 在存在真实导演分叉时是否会被条件询问；
3. Final Prompt 是否从“动作概括”提升成“可执行连续动作链”；
4. Initiative 是否真正发生在动作过程中；
5. Ending 是否仍保持短促、不吞掉有效交战；
6. Camera Coverage 是否维持 V2-46 的改善而不回退。

只有这一轮 Prompt PASS，才进入真实视频生成。