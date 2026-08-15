# Video Prompt Skill — Action Combat Current Handoff

> 更新时间：2026-08-15 15:32（UTC+8）
>
> 仓库：`twj515895394/video-prompt-skill`
>
> 分支：`main`
>
> 用途：下一会话直接读取本文件。用户会带回**最新实际 Skill 对话、Runtime Read List、Final Prompt，随后可能继续提供真实生成视频结果**。不要重新讨论已经确认的设计，优先做固定 G01 证据驱动回归。

---

## 0. 当前状态一句话

Action Combat 已完成一轮关键 Runtime 重构：

- Stage-2 Pattern Hit Evidence；
- Model Execution Realizability；
- Subject Motion 条件必读；
- Persistent Combat Signature；
- Action–Camera Handoff；
- Perceptual Impact Trigger；
- Camera Base Viewing Priority / Camera Hard Constraint 拆分；
- Combat Prompt 内联关键 Camera Accent；
- Final Prompt QA / Self-Repair；
- Interactive 取消 10 轮硬上限。

**但是：这些最新修复尚未经过新的真实生成视频 PASS 验证。下一步必须先跑固定 G01 Prompt / Runtime 回归，再决定是否继续增加机制或知识。**

---

## 1. 用户 / 项目工作原则

项目使用 Grill-Me：

- 沿设计树逐分支推进；
- 每次只问一个问题；
- 每个问题给推荐答案；
- 已确认内容不重复询问；
- 如果用户确认实施，直接落仓库，不只讨论。

用户最新明确偏好：

> **不排斥多交互几次，即使超过 10 次，只追求最优结果输出。**

因此 Interactive 最新规则：

- 不设置固定硬轮数上限；
- 第 10 轮只是 `Quality Review Checkpoint`；
- 如果后续仍有真正高价值分叉，可以继续超过 10 轮；
- 即使超过 10 轮，仍坚持一次只问一个问题；
- 系统本应自动保证的质量机制，不应继续拿来问用户。

核心评价原则：

> **真实生成视频质量 > Prompt 文本看起来更专业 / 更细 / 更符合理论。**

如果 Prompt 变细、规则变多，但真实视频动作、连续性或 Camera 反而下降，仍然必须判 FAIL。

---

## 2. Golden Scenario G01 — 当前固定回归基线

### 2.1 原始请求

```text
使用交互模式，帮我做一段一个女生和男生再办公室打架的15秒电影片段，实际两个人穿着正常的职场服装但其实是2个杀手组织的职业杀手。中国男女，女的22岁长发高马尾漂亮身材完美，男性是一个秃顶又爱又胖的55岁领导,贴身搏斗，不要隔着什么办公桌
```

### 2.2 当前固定用户选择

#### Fighting Direction

**综合格斗 / MMA**

不要再使用旧 handoff 里“中国武术电影化近身格斗”的旧推荐作为当前 G01 基线。

#### Character Technique Identity → Persistent Combat Signature

```text
女方：拳腿组合
男方：拳肘 + 抱摔
```

#### Camera Base Viewing Priority

**完整动作可读优先**

#### Camera Hard Constraint

当前 G01 **没有额外 Hard Constraint**：

- 不是 One-take；
- 不是 Fixed Camera；
- 不是 No Cut；
- Runtime 可以按动作状态动态选择 Cut / Reframe / Camera Accent。

### 2.3 G01 回归目的

必须保持同一场景 + 同一选择，优先隔离以下修复是否真的生效：

1. Stage-2 leaf 是否真实被读取；
2. Subject Motion 是否真实被读取；
3. Whole-body / Footwork / Support 是否进入主因果；
4. 女方拳腿、男方拳肘抱摔是否持续兑现；
5. Camera 是否仍退化为保守中大全景；
6. Perceptual Impact 是否只在高价值节点使用；
7. Prompt QA 是否能发现并自动修复明显实现问题。

---

## 3. 旧 G01 真实生成视频失败 — 最高优先级 Ground Truth

旧版 / 修复前 G01 Final Prompt 已经实际生成过视频。

用户真实反馈：**“差很多很多”**。

主要问题：

- 动作连续性明显更差；
- Camera 灵活性明显下降；
- 动作几乎集中在上半身；
- 动作电影感明显下降。

这不是静态猜测，而是实际生成视频反馈。

正式 Failure 概念：

- `Prompt–Video Execution Divergence`
- `Instruction Saturation / Micro-choreography Overconstraint`
- `Upper-body Semantic Dominance`
- `Effective Granularity Flattening`
- `Camera Strategy Overconstraint`
- `Subject Motion Routing Missing`

重要：

> **当前最新修复还没有新的真实视频 PASS 结果。不能把 Prompt-level 改善写成 Generated-video PASS。**

---

## 4. 旧版 G01 实际 Runtime / Prompt 暴露的问题

用户曾提供完整实际交互过程和 Final Prompt。

### 4.1 Fighting Direction Decision Purity

旧 Fighting Direction 候选中混入：

> `一镜到底沉浸式`

这是 Camera 概念，不属于 Fighting Direction。

已修。

### 4.2 Stage-2 Pattern Hit Evidence = FAIL

当时选择：

- MMA；
- 女拳腿组合；
- 男拳肘抱摔；
- 连续近身高手对决。

但 Runtime Read List **没有读取**：

`references/libraries/combat-choreography-patterns/minimum-validation-set.md`

因此当时 Stage-2 只停留在高层动作标签，没有足够 Evidence。

已修成条件必读 / Evidence Gate。

### 4.3 Subject Motion Routing Missing

旧 Runtime 没有读取：

`references/controls/subject-motion/control.md`

而当时最大失败正是：

- 上肢锁死；
- Footwork / Support 只是修饰；
- Whole-body Driver 不足。

现在短时 High Kinetic / Whole-body Combat 命中条件时，Subject Motion 已升级为**条件必读**。

### 4.4 Technique Identity Evaporation

旧 Prompt：

- 女方开头出现一记低线腿法，后面又变成抽象“连续拳腿组合”；
- 男方只“尝试 body lock”，没有真正形成摔控 / 失败摔控 / 反摔 / Position 后果；
- 中后段双方都逐渐塌回前臂、肩线、抓臂、短打。

现在已升级为 `Persistent Combat Signature`。

### 4.5 Camera Strategy Overconstraint

旧“完整动作可读型”被序列化成：

> 稳定器中大全景为主 + 少量跟拍

结果 Camera Mobility 不足。

现在已把：

- `Base Viewing Priority`
- `Camera Hard Constraint`

拆成两个正交概念。

### 4.6 Action–Camera 仍不够体验化

旧 Camera 主要解决“看清动作”，但缺少真正动作电影的：

- Threat POV / Near-lens；
- Impact Consequence Close-up；
- Near-miss / Whip-by；
- Body-mechanics Detail；
- Range Compression；
- Initiative / Reaction Experience。

现在已新增 `Perceptual Impact Trigger`。

---

## 5. 当前 Action Combat Mandatory Runtime

当前推荐理解：

```text
Confirmed Combat Planning Context
→ Stage-2 Gap Detection
→ Stage-2 Pattern Hit Evidence Gate
→ 必要 leaf execution knowledge Read
→ Persistent Combat Signature Realization（如存在角色打法差异）
→ subject-motion/control.md（短时 High Kinetic / Whole-body 条件命中时必读）
→ Movement / Technique / Transition Pattern
→ Concrete Action Phrase
→ State / Continuity Validation
→ Model Execution Realizability
→ Motion / Energy Carry-over
→ Camera Hard Constraint Check
→ Camera Base Viewing Priority
→ Action–Camera Handoff
→ Perceptual Impact Trigger（稀疏、高价值）
→ prompt-assembly/control.md
→ Combat Final Preflight
→ Final Prompt QA / Self-Repair Gate
→ Delivery
```

Quick 与 Interactive 共用相同质量上限。

---

## 6. Stage-2 / Minimum Validation Set

当前最小验证知识：

`references/libraries/combat-choreography-patterns/minimum-validation-set.md`

包含：

### Movement

- M01 Outside Angle Cut
- M02 Level Drop Reposition
- M03 Axis-turn Exit
- M04 Support-base Transfer

### Technique

- T01 Short Strike Interception
- T02 Low-line Base Disruption
- T03 Off-balance Takedown Entry
- T04 Whole-body Linked Counter

### Transition

- X01 Contact → Movement Re-entry
- X02 High → Low → High
- X03 Strike → Off-balance / Takedown
- X04 Failed Control → Angle Exit → Re-entry

核心 Evidence Chain：

```text
Gap
→ Slot
→ actual leaf Read
→ Pattern / Detail
→ Concrete Action Phrase
```

如果没有真实 leaf Read，不能假定 Stage-2 已完成。

当前原则：

> **先证明 Routing / Pattern Realization 有效，再扩武术知识库。**

不要一看到生成不好就立刻增加几百个招式。

---

## 7. Model Execution Realizability

真实失败已经证明：

> **更细的 Prompt ≠ 更好的生成视频。**

### Motor Driver First

Whole-body / Movement-driven Combat 优先：

```text
Whole-body / Support / Route Driver
→ Key Technique
→ Opponent Response
→ Balance / Position / Range Consequence
→ Continuation
```

不要长期：

```text
Forearm / Wrist / Shoulder Technique
→ 最后补一句侧步 / 转髋 / 降重心
```

### Feet-fixed Test

问：

> 如果删掉脚步、支撑、Route、Level、Axis、Position，这段攻防是否仍然基本可以原地完成？

如果 yes，而当前 Fighting Direction 要求 Whole-body，则 FAIL：

`Upper-body Semantic Dominance / Static Standing Combat`

### Instruction Saturation

短窗口同时要求过多：

- 多肢体；
- 多 Contact；
- 多 State；
- 精细 Footwork；
- Camera Change；
- Audio；
- Negative；

会造成模型执行退化。

原则：

> **压描述复杂度，不压动作连续性。**

### Effective Granularity

High / Medium / Low 是模型执行负荷，不只是字数标签。

不能连续多个 Phrase 实际都变成 High Granularity。

---

## 8. Subject Motion 条件必读

关键文件：

`references/controls/subject-motion/control.md`

命中条件主要包括：

- 约 10–20s 短时 Combat；
- 持续近身 / High Kinetic；
- 目标依赖 Whole-body、Footwork、Support / Balance、Range / Position / Axis / Route；
- 或已经存在上肢锁死 / Footwork 只作为修饰语风险。

命中后：

- 必须实际读取；
- 占普通 `0-3 Controls` 中 1 个位置；
- 不能因为 Core / Choreography 已经写过 Motion 就跳过。

失败标记：

`Subject Motion Routing Missing`

当前 G01 明确命中该 Gate。

---

## 9. Persistent Combat Signature

用户确认的 Technique Identity 不能只做一次性招式标签。

最新定义：

> **角色持续通过什么动作逻辑创造下一状态、抢 Initiative、改变 Range / Support / Position。**

### G01 女方：拳腿组合

不要求固定踢 N 次。

但应持续体现类似：

```text
拳法制造高位 Reaction / Guard
→ 腿法改变 Support / Range
→ Footwork / Angle 利用后果
→ 再进入拳法
```

### G01 男方：拳肘 + 抱摔

不要求每次摔倒成功。

但 Grapple / Takedown 必须形成真实后果：

```text
短打 / 肘创造贴身窗口
→ Clinch / Body-lock Entry
→ 成功摔控
或被反摔
或被迫换位
或改变对手 Support / Position / Range
→ 继续下一次贴身进入
```

只有“尝试抱住”而没有状态变化，不算兑现。

失败：

`Technique Identity Evaporation / Persistent Signature Collapse`

禁止通过“后面补一脚 / 补一次抱摔词”打卡修复。

---

## 10. Action–Camera Runtime

核心文件：

`references/tasks/action-combat-video/action-camera-handoff-playbook.md`

核心原则：

> **Action 决定 Camera 为什么变化；Camera 必须继续仍然活着的 Motion。**

Camera 不应把动作切成一个个重新起步的小盒子。

### Action–Camera Handoff

```text
Current Action State
→ Camera Hard Constraint Check
→ Base Viewing Priority
→ Viewer Experience Opportunity（可选）
→ Camera Task
→ Shot Entry Trigger
→ Inherited Motion State
→ Observation
→ Shot Exit / Handoff
```

### 常见 Action Trigger

- Cut on Motion
- Contact / Consequence
- Direction / Axis Change
- Initiative Reversal
- Range / Level / Support Change
- Occlusion / Match Motion
- Environment Boundary

---

## 11. Perceptual Impact Trigger

用户明确提出：

> **不是每个动作都嵌镜头；特写 / POV 应该迎合动作本身，灵活一点。**

因此增加：

`Perceptual Impact Trigger / 主观体验触发`

逻辑：

```text
Action State Change
+ Viewer Experience Opportunity
+ Camera Hard Constraint Check
→ 是否值得且允许 Camera Accent？
```

可使用：

### Threat POV / Near-lens

例如拳头快速迎面而来，可短暂接近被攻击者 POV / Near-lens，让拳头逼近 Camera。

### Impact Consequence Close-up

拳真正打中脸时，可以切受击侧近景 / 特写，但重点是：

- 头 / 肩轴如何被冲击带偏；
- Reaction；
- 下一动作如何继承这个偏转。

不是只展示“拳碰到了脸”。

### Near-miss / Whip-by

攻击擦过人物 / 镜头，可形成威胁体验或自然 Cut Bridge。

### Body-mechanics Detail

低扫、支撑变化、抱摔入口、落地、失衡真正决定下一动作时，可短促观察脚步 / 髋 / Support。

### Range Compression

双方突然贴身 / clinch 时，Camera 可压近或改变关系角度表达距离压缩。

### Initiative / Reaction

主动权翻转时，用 Reaction / Relationship Angle Change 让观众直接感到控制权变化。

重要约束：

> **Camera Coupling ≠ Camera-per-Action。**

普通连接动作默认继续当前 Shot。

失败：

- `Perceptual Impact Underuse`
- `Perceptual Accent Overuse / Camera Accent Overmapping`

---

## 12. Camera Intent 已拆成两层

### 12.1 Base Viewing Priority

回答：

> 默认优先让观众看清 / 感受什么？

候选包括：

- 完整动作可读优先；
- 电影冲击体验优先；
- 贴身沉浸优先；
- 空间关系优先；
- 技巧细节优先。

它不是固定 Shot Template。

G01 当前选择：

**完整动作可读优先**

正确解释：

```text
默认优先 Whole-body / Footwork / Spatial Relationship 可读
+
高价值 Threat / Impact / Support / Range / Initiative 节点
仍允许 POV / Near-lens / Close-up / Low Detail / Reaction / Reframe / Cut
```

禁止解释为：

```text
全程中大全景
+ 少量 Tracking
+ 尽量不切
```

### 12.2 Camera Hard Constraint

回答：

> 摄影实现中什么绝对不能违反？

例如：

- One-take；
- Fixed Camera；
- No Cut。

优先级：

```text
用户明确 Camera Hard Constraint
> Base Viewing Priority
> Action-triggered Handoff
> Perceptual Impact Accent
> 装饰性 Camera Variation
```

注意：

- Hard Constraint 不默认单独问；
- 用户没提、又没有真实高价值分叉时，默认为空；
- Hard Constraint 只限制 Camera 实现，不能反向缩水 Fighting Direction / Technique Identity / Combat Coverage。

---

## 13. Prompt Serialization — Camera 不再独立堆成大段

关键文件：

`references/controls/prompt-assembly/control.md`

最新原则：

### Global Camera Baseline

独立 Camera 段可以存在，但只保留非常短的总体基线：

- 动作可读；
- 空间清楚；
- Camera 随 Route / Range / Level 改变；
- 不无意义碎切。

### Key Camera Moment Inline

高价值 Camera Accent 应直接锚在对应 Action Phrase 中。

例如：

```text
男方挥拳快速逼近她的视线
→ 短暂 Near-POV / Near-lens
→ 她侧闪
→ Camera 顺同一拳势从肩侧切出
→ 继续这记挥空动作
```

或：

```text
女方一拳击中男方侧脸
→ 接触瞬间受击侧近景
→ 看到头部和肩轴被冲击带偏
→ 下一镜直接继承这股偏转
→ 她从新的外侧角度继续进入
```

不要求每个动作内嵌 Camera。

---

## 14. Final Prompt QA / Self-Repair Gate

用户最新明确认为最终应该有一次检查核对环节。

现在 Quick / Interactive 最终 Prompt 都必须经过：

```text
Final Draft
→ Prompt QA
→ PASS：Delivery
→ FAIL：定位主失败项
```

### 14.1 实现质量问题

```text
Implementation / Quality Issue
→ Silent Self-Repair
→ Re-run QA
```

### 14.2 必须改变已确认创作决策才能修

```text
需要改变用户已确认 Creative Decision
→ 禁止静默修改
→ Interactive 重新问当前唯一必要问题
```

### 14.3 可以静默修

- Phrase / 语序 / 信息层级；
- 已确认内容在 Final Prompt 中丢失 / 弱化；
- Instruction Saturation；
- 重复描述；
- 低价值 Camera / Audio / Negative；
- 动作 / Camera / Continuity / Ending 的实现质量；
- 不改变高层创作决策的局部动作组织。

### 14.4 不能静默改

- Fighting Direction；
- Persistent Combat Signature / Technique Identity；
- Camera Base Viewing Priority；
- Camera Hard Constraint；
- 人物身份 / 剧情关系；
- 胜负 / Ending；
- 用户明确 Must Keep / Must Avoid；
- 多模态主真源。

### 14.5 Repair Pass

- 默认至少 QA 1 次；
- 发现实现问题：静默修复 1 次后重新 QA；
- 如果复杂任务仍存在明显新依赖问题，可再修 1 次；
- 不进行无限修复循环。

原则：

> **Quality Issue → Repair Implementation.**
>
> **Confirmed Creative Decision → Preserve.**

---

## 15. 最新 Interactive 深度规则

关键文件：

`assets/templates/mode-interactive-output-contract.md`

最新：

- 不设置固定 10 轮硬上限；
- 10 轮只是质量复核点；
- 用户明确质量优先时，可超过 10 轮；
- 后续问题仍需满足高价值条件；
- 系统本应自动保证的 Stage-2 / Contact / QA / Camera Readability 等不能机械继续问用户。

收口依据：

> **需求是否足够完整 + 后续是否还有高价值真实分叉。**

不是轮数。

---

## 16. 关键已落地文件

### Runtime / Entry

- `SKILL.md`
- `references/tasks/action-combat-video/index.md`
- `references/tasks/action-combat-video/choreography-playbook.md`
- `references/tasks/action-combat-video/core-playbook.md`
- `references/tasks/action-combat-video/modern-combat-playbook.md`
- `references/tasks/action-combat-video/action-camera-handoff-playbook.md`

### Controls

- `references/controls/index.md`
- `references/controls/subject-motion/control.md`
- `references/controls/prompt-assembly/control.md`
- `references/controls/camera-direction/control.md`
- `references/controls/spatial-blocking/control.md`

### Interactive / Quick

- `assets/templates/mode-interactive-output-contract.md`
- `assets/templates/mode-quick-output-contract.md`

### Stage-2 Knowledge

- `references/libraries/combat-choreography-patterns/minimum-validation-set.md`

### Regression / Specs

- `docs/action-combat-video-v2-regression.md`
- `docs/action-combat-video-generated-video-execution-regression-spec.md`
- `docs/action-combat-video-action-camera-handoff-spec.md`
- `docs/action-combat-video-concrete-choreography-knowledge-spec.md`
- `docs/action-combat-video-concrete-choreography-implementation-plan.md`

---

## 17. 本阶段关键 Commits

按逻辑顺序：

### Concrete Choreography / Stage-2

- `e949349b508a75895d5b966d999708902f22c6c3` — Implement Fighting Direction and gap-driven choreography routing
- `c000ffc1d47b238a87e94442beb9a12d2e0ad87e` — Preserve Fighting Direction and granularity distribution in prompt assembly
- `87a5c5629d11afd37d554636d0301c9e00c3a67e` — Fix combat post-interactive mandatory execution path

### Generated-video Realizability / Regression

- `c510f376cb6d46265eed08762289ac633e249dab` — Add generated-video execution regression spec
- `3c7850ef7af45dac70870b50af4a5ce36f687358` — Add generated-video realizability gates
- `a7f9c0e8874cac27e6f73fffc6cd4c375cedbfe3` — Record G01 generated-video quality regression

### Subject Motion

- `310eb0cd35e6c45e1e3607e5227d83da5b6b2063` — Make subject-motion conditionally mandatory
- `e60529993b8c5ab7d1b9cc23aaf469c3a063ed79` — Require subject-motion for high-kinetic short combat

### Action–Camera

- `d8f9096d04869f5a373e60b9b61f3615f40babf2` — Action-camera handoff and stage-2 routing spec
- `fa12c5db4c6a92132120f920934170a536ec8846` — Add action-camera handoff runtime playbook
- `80dfb339946572c0fb687b582a7183c43bf0955d` — Wire stage-2 evidence and action-camera into runtime
- `c7360b42288e40c06be4acf62bb133a66e062913` — Preserve action-camera handoff during prompt assembly

### Perceptual Camera

- `5a738c0473ff37e74e956060cf6d41cc829f5cb0` — Add perceptual impact camera triggers
- `9c91c3cc4149ef845f025b5d06851b75490f4881` — Serialize selective perceptual camera accents inline

### Camera Decision Split

- `c9006859d2c005e4a3d6face787655e50bac571b` — Camera Intent as Base Viewing Priority
- `0f4220e2cd475016c036254a08bc5f2c6caf2ff2` — Split viewing priority and hard constraints in interactive contract
- `4e1718989053ecff203477222ab8ef30fc41ac47` — Add runtime camera hard-constraint hierarchy
- `f9609baf9f23ca00a198c9d050d264b2ecfb0ed0` — Align top-level SKILL camera decision semantics

### Final QA + Persistent Signature + Quality-first Interactive

- `ff226e0415e9922873554f7cf43c4f9ff3845250` — Add Final Prompt QA / Silent Self-Repair to Quick
- `64206abbaf766c2077c402ad71ba9df83b9b15b7` — Interactive quality-first, remove hard 10-turn cap, add QA self-repair
- `20d597528c649b69861bd9184dc7611f6c4f3025` — Persistent Combat Signature + Combat QA repair gate

---

## 18. 下一会话应该怎么开始

用户会粘贴**最新一次实际 Skill 运行对话**。

第一步不要继续设计新机制。

先审计 Runtime Read List。

### G01 最新版本预期 Read Evidence

必须重点确认：

- `references/tasks/action-combat-video/index.md`
- `core-playbook.md`
- `choreography-playbook.md`
- `modern-combat-playbook.md`
- `minimum-validation-set.md` **必须出现**
- `subject-motion/control.md` **必须出现**
- `action-camera-handoff-playbook.md` **必须出现**
- `prompt-assembly/control.md` **必须出现**

其余 Controls 按缺口竞争：

优先可能为：

- `camera-direction/control.md`
- `spatial-blocking/control.md`

`continuity-consistency/control.md` 不应该因为“身份 / 服装保持一致”就自动挤掉 Subject Motion；只有真实多参考、多镜头、身份 / 道具 / 场景漂移风险时再进入。

如果 G01 命中 Subject Motion 条件却 Read List 没有它：

`Subject Motion Routing Missing`

如果 MMA + 明确拳腿 vs 拳肘抱摔，且 Stage-2 leaf 没有实际读：

`Stage-2 Routing Evidence Missing`

---

## 19. 下一会话 Final Prompt 审计顺序

拿到最新 Final Prompt 后，按此顺序检查：

### 19.1 Planning / Routing

- Fighting Direction 是否仍是 MMA；
- 有没有 Camera 概念再次混入 Fighting Direction；
- Read List 是否真实命中 Stage-2 + Subject Motion。

### 19.2 Persistent Combat Signature

女方是否持续表现拳腿逻辑，而不是只开头踢一次？

男方抱摔 / Grappling 是否形成真实状态变化，而不是只“attempt body lock”？

### 19.3 Whole-body / Feet-fixed Test

- Footwork / Support / Hip / Route / Range 是否创造下一攻击状态；
- 如果删掉这些，动作是否仍可以原地完成？

如果 yes：继续判 `Upper-body Semantic Dominance`。

### 19.4 Motion / Energy Carry-over

上一动作留下的：

- Momentum；
- Rotation；
- Contact Pressure；
- Support Transfer；
- Forced Step；
- Recovery Burden；
- Range Compression；

是否直接成为下一动作入口？

### 19.5 Action–Camera

- Base Viewing Priority 是否被误写成固定中大全景；
- Route / Level / Support / Range / Initiative 是否能触发有意义 Camera Change；
- Camera Change 是否继承 live motion。

### 19.6 Perceptual Impact

检查是否存在少量真正高价值：

- Threat POV / Near-lens；
- Impact Consequence；
- Near-miss；
- Support / Body Mechanics；
- Range Compression；
- Initiative Reaction。

同时检查是否发生 `Camera-per-Action` 过度映射。

### 19.7 Instruction Saturation

新版规则很多，但 Final Prompt 不能把每个内部规则全部显式写出来。

优先保留：

```text
Motor Driver
+ Key Technique
+ Opponent Response
+ Position / Balance / Range Consequence
+ Continuation
+ 少量高价值 Camera Accent
```

不要把每个动作都写成完整技术 + 状态 + Camera + Audio + Negative 微规格。

### 19.8 Final QA

确认 Prompt QA / Self-Repair 是否实际发现并修复：

- Technique Identity 弱化；
- Upper-body lock；
- Camera static；
- Perceptual Underuse / Overuse；
- Instruction Saturation；
- Ending 过早吞动作；
- Negative / Continuity 过重。

---

## 20. 如果最新 Prompt 看起来仍不好，诊断顺序

不要马上扩知识库。

优先：

1. Stage-2 leaf 是否真的 Read / Hit；
2. Subject Motion 是否真的 Read；
3. Persistent Signature 是否在中后段蒸发；
4. Upper-body Semantic Dominance；
5. Effective High Granularity Everywhere；
6. Instruction Saturation；
7. Motion / Energy Carry-over；
8. Camera Strategy Overconstraint；
9. Action–Camera / Perceptual Impact 是否失配；
10. Negative / Continuity 是否过载；
11. Prompt QA 是否真的执行了修复。

只有 Routing 正确、Prompt 也合理，但真实视频仍明显失败时，再考虑：

- 模型能力边界；
- Model-specific serialization；
- 是否需要扩 Knowledge Coverage。

---

## 21. 当前还没有证明的事情

以下**都还不能宣称 PASS**：

- 新 Stage-2 Gate 能提升真实生成视频；
- Subject Motion 条件必读能解决上肢锁死；
- Persistent Combat Signature 能在真实视频中保持打法差异；
- Perceptual Impact 能提升 Camera 电影感而不导致碎切；
- Base Viewing Priority + Hard Constraint 拆分能让 Camera 更灵活；
- Final QA / Self-Repair 能稳定提高最终视频质量。

这些必须通过新的 G01 Prompt / Runtime / Generated-video Regression 验证。

---

## 22. 当前推荐下一步

> **不要继续加新抽象机制。**

下一会话收到用户最新 Skill 运行对话后：

```text
固定 G01
→ 检查实际 Interactive Decisions
→ 检查 Runtime Read List
→ 检查 Final Prompt
→ 对比旧失败 Prompt
→ Prompt-level QA
→ 用户实际生成视频
→ Generated-video Regression
```

如果 Prompt-level 已明显改善，再让用户实际生成。

如果真实视频仍失败，再按第 20 节证据驱动定位根因。

---

## 23. 不要在新会话做的事情

- 不重新问已经确认的 MMA / 拳腿 vs 拳肘抱摔 / 完整动作可读优先；
- 不把旧 handoff 的“中国武术电影化”当当前 G01 选择；
- 不把 10 轮当硬上限；
- 不把“完整动作可读”翻译成固定中大全景；
- 不为每个动作强制 Camera Accent；
- 不因为“动作还不够好”立即建设巨大武术动作数据库；
- 不因为 Prompt 文本更复杂就宣称质量更高；
- 不在没有真实生成视频反馈时宣称当前版本已经解决问题。

---

## 24. 接力提示

下一会话可以直接从用户贴出的最新运行内容开始，优先回答：

> **这次最新 Runtime 是否真正执行了我们刚刚修的 Stage-2、Subject Motion、Persistent Signature、Action–Camera / Perceptual Impact、Camera Priority / Constraint、Final QA？最终 Prompt 相比旧失败版到底改善了什么、还剩什么问题？**

在完成这一轮证据审计之前，不进入新的大设计分支。
