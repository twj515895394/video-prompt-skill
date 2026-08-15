---
name: video-prompt-skill
description: 当用户需要根据文字、图片、视频或音频生成文生视频、图生视频、多模态参考视频、视频复刻、编辑、延长、音频驱动、故事板、多镜头视频或复杂动作格斗/电影武侠 Prompt 时，应使用此技能。
---

# Video Prompt Skill

## 使用目标

把用户的创作意图和参考素材转成可直接投喂视频模型的完整 Prompt、镜头级时间轴或 Prompt Pack。

结果必须同时解决：

- 从什么画面和状态开始；
- 谁或什么在运动；
- 动作如何按时间发展；
- 镜头为什么动、怎样动、停在哪里；
- 人物、场景、道具和运动如何保持连续；
- 表演、对白、环境音、音效和音乐怎样与画面同步；
- 最后一拍怎样自然收束；
- Generic、Seedance 2.0 或 LTX-2.3 应采用什么表达方式。

默认目标是直接交付可复制使用的最终结果，而不是只提供灵感词、术语列表或概念讲解。

## 适用范围

支持以下任务：

- 文生视频；
- 图生视频；
- 多图、多视频、多音频参考视频；
- 视频参考复刻和视频转视频；
- 视频局部编辑；
- 视频向前或向后延长；
- 音频驱动、对白驱动和音乐卡点；
- 故事板、分镜、多镜头和多片段视频；
- 复杂现代格斗、1vN 动作戏、电影武侠和常见冷兵器战斗；
- Generic、Seedance 2.0、LTX-2.3 视频 Prompt 适配；
- 视频 Prompt 失败诊断和重写。

不负责：

- 角色立绘、场景设定图和静态海报本身的生图 Prompt；
- 视频文件下载、抽帧、转码或剪辑执行；
- 未正式支持模型的专属参数和伪造语法；
- 用导演名、风格名或质量词替代可执行的视频设计。

## 核心原则

- 除非用户明确要求讨论、脑暴、逐步设计或先提问，否则默认进入快速模式。
- 快速模式零追问、零人工确认、零过程说明，直接输出可用结果。
- 交互模式遵循 `grill-me`：每次只问一个最关键的问题，并给出推荐答案。
- 先解决初始状态、主体运动、镜头任务、时间节拍和结束落点，再补风格。
- 主体运动、镜头运动、环境变化和声音事件必须分别判断。
- 多模态素材必须分配职责；每个关键维度只能有一个主真源，禁止平均融合。
- 同一知识只保留一个正文真源；索引可以多处引用，但禁止复制正文。
- Reference 可以很多，但每次只读取当前任务真正需要的一条或几条路线。
- 复杂战斗遵循“约束错误，不约束创作”：固定因果、连续性和物理底线，不固定招式、Beat 数量或镜头模板。
- 复杂战斗同时遵循 **Clarity Through Structure, Not Action Reduction**：高信息密度允许存在，但必须用 Action Phrase、状态连续性、镜头可读性和执行预算组织清楚。
- Combat Final Prompt 遵循 **State Machine Internalized, Choreography Externalized**：状态机制在内部运行，最终由可见动作、接触、受力和空间变化主导。
- Action Combat 的 `Stage-2 Pattern Hit Evidence + action-camera-handoff-playbook.md + prompt-assembly/control.md + Combat Final Preflight` 是最终交付必经路径；其中真正命中条件的 leaf execution knowledge 不能被“按需”预算跳过。
- 不向用户暴露内部目录、维护路径、资料迁移和加载过程。

## 第一步：判断输入

读取 `references/inputs/index.md`，只选择一份主输入 Reference。

### 1. 纯文字输入

读取：`references/inputs/text-input.md`

用于从文字建立初始画面、动作顺序、镜头和时间结构。

### 2. 单张图片

读取：`references/inputs/single-image-input.md`

先判断图片职责：首帧、尾帧、人物、场景、风格、构图、动作或表情终态。

### 3. 多张图片

读取：`references/inputs/multi-image-input.md`

必须为每张图片分配明确职责，并确定人物、服装、场景、首帧、尾帧、构图、光影和动作各自的主参考。

### 4. 一个或多个视频

读取：`references/inputs/video-input.md`

先判断视频提供动作、表演、运镜、节奏、转场、特效、声音，还是待编辑 / 延长主体。

### 5. 音频输入

读取：`references/inputs/audio-input.md`

判断音频承担对白、音色与语气、时间节拍、BGM、环境音、拟音或关键音效。

### 6. 图片 / 视频 / 音频混合输入

读取：`references/inputs/mixed-multimodal-input.md`

混合输入只读取这一份主输入页，不同时加载多份单模态输入页。

## 第二步：判断任务

读取 `references/tasks/index.md`，只选择一份主任务路线。

### 1. 文生视频

读取：`references/tasks/text-to-video/playbook.md`

### 2. 图生视频

读取：`references/tasks/image-to-video/playbook.md`

### 3. 多模态参考视频

读取：`references/tasks/multimodal-reference-video/playbook.md`

### 4. 视频参考复刻 / 视频转视频

读取：`references/tasks/video-reference-and-video-to-video/playbook.md`

### 5. 视频局部编辑

读取：`references/tasks/video-editing/playbook.md`

### 6. 视频向前 / 向后延长

读取：`references/tasks/video-extension/playbook.md`

### 7. 音频驱动与音乐卡点

读取：`references/tasks/audio-driven-and-beat-sync/playbook.md`

### 8. 故事板 / 多镜头 / 多片段到视频

读取：`references/tasks/storyboard-and-multi-shot-video/playbook.md`

### 9. 复杂动作格斗 / 电影武侠

当核心难点是持续攻防、动作编排、Battle Beat、Range / Advantage / Condition、1vN Target Handoff、兵器连续性、接触实感或 Action / Camera / Audio 三线同步时，固定读取：

- `references/tasks/action-combat-video/index.md`
- `references/tasks/action-combat-video/core-playbook.md`
- `references/tasks/action-combat-video/choreography-playbook.md`

然后只选择一个专项分支：

- 现代格斗：`references/tasks/action-combat-video/modern-combat-playbook.md`
- 电影武侠：`references/tasks/action-combat-video/cinematic-wuxia-playbook.md`

### Action Combat Post-Planning Mandatory Path

Fighting Direction、关键 Character Identity / Technique 差异和 Camera Intent（如需要）一旦由用户确认或静默确定，**不得直接跳到 Controls / Template / Final Prompt**。必须重新进入执行阶段：

```text
Confirmed Combat Planning Context
→ Stage-2 Gap Detection
→ Stage-2 Pattern Hit Evidence Gate
→ 必要 leaf execution knowledge Read
→ Concrete Action Phrase
→ State / Continuity Validation
→ Model Execution Realizability
→ Motion / Energy Carry-over
→ action-camera-handoff-playbook.md
→ Camera / Spatial Coordination
→ prompt-assembly/control.md
→ Combat Final Preflight
→ Delivery
```

固定读取：

- `references/tasks/action-combat-video/action-camera-handoff-playbook.md`
- `references/controls/prompt-assembly/control.md`

其中 `action-camera-handoff-playbook.md` 负责 Stage-2 Evidence、Model Execution Realizability、Motion / Energy Carry-over 与 Action ↔ Camera Handoff；`prompt-assembly/control.md` 负责最终保真序列化。两者都不占普通 `0-3` Controls 配额。

#### Stage-2 leaf knowledge 条件必读

出现以下任一条件时，不得以“已经读过 Choreography / Modern / Wuxia”为由跳过 leaf execution knowledge：

- High / Expert Combat 且目标是连续高手对决；
- Fighting Direction 明确要求拳腿摔控混合、Movement / Level / Axis / Route / Support 显著变化；
- 用户确认了明确 Technique Identity，例如“拳腿组合 vs 拳肘抱摔”；
- 草拟动作仍主要由前臂 / 肩线 / 抓腕 / 顶肩等 Upper-body Contact 驱动；
- Transition 缺少 Contact / Momentum / Axis / Range / Recovery Handoff；
- Final Preflight 出现 `Static Standing Combat / Upper-body Technique Dominance`。

当前 CK 最小验证阶段，如果没有其他**已经实际读取**且足以覆盖当前 Gap 的专业 leaf knowledge，必须读取：

- `references/libraries/combat-choreography-patterns/minimum-validation-set.md`

该条件必读属于 Combat Stage-2 Execution Knowledge，**不占普通 `0-2 libraries detail` 可选预算**。必须能内部回答：`Gap → Slot → 实际 leaf Read → Pattern / Detail → Concrete Action`；没有真实 Read Evidence 不能假定 Stage-2 已完成。

再执行 Combat Final Preflight。`prompt-assembly/control.md` 在 Action Combat 中属于必经 Final Assembly，不占普通 `0-3` Controls 的可选预算。

简单挥拳、跑跳、追逐、体育动作不进入 Combat 专项，继续使用原主任务 + `action-motion`。

Combat 内部职责：

- `core-playbook.md`：State / Continuity / Battle Runtime Skeleton；
- `choreography-playbook.md`：Coverage / Rhythm / Action Phrase / Character Identity / Tactical Interaction / Contact Solidity / Signature Moment / Execution Budget / Kinetic / Temporal / Camera Mobility / Final Preflight Criteria；
- 专项 Playbook：Modern / Wuxia 的具体动作语言与物理尺度；
- `action-camera-handoff-playbook.md`：Stage-2 Evidence / Model Execution Realizability / Motion-Energy Carry-over / Action-triggered Camera Handoff；
- `prompt-assembly/control.md`：把内部动作设计转成最终连续、Action-first、可执行的 Prompt，并执行 Negative / Temporal / Kinetic / Camera Handoff 外显检查。

Combat 不新增独立 `combat-choreography` 全局 Control。

## 第三步：判断模式

### 快速模式

除非用户明确要求交互共创，否则默认使用快速模式。

读取：`assets/templates/mode-quick-output-contract.md`

快速模式：

- 不追问；
- 不要求确认；
- 不输出多个近似方案让用户选择；
- 不展示分析、方向决策或自动补全项；
- 信息不足时自动使用最小风险默认值；
- 冲突时自行裁决，只保留最符合主目标的路线；
- 直接输出一份可复制 Prompt 或必要的 Prompt Pack。

Combat Quick Mode 必须执行 **Full Planning + Silent Resolution**：内部仍推导 Combat Intent、Branch、Fighting Direction、Coverage、Rhythm、Character Identity、Environment、Contact Solidity、Signature Moment、Action / Camera Execution Budget、Battle Beat 与 State Contract；这些内部状态不默认展示。

Quick 不得因为输入简短而降低 Combat Coverage、Exchange Richness、Contact Solidity 或 Signature Moment 质量标准；也不得跳过 Stage-2 Evidence / Action–Camera Handoff / Combat Final Assembly / Final Preflight。

只有以下情况可以在快速模式中提出一个必要问题：

- 无法判断用户要求处理哪份输入素材；
- 同一关键维度存在两个互斥且同等强度的用户指定主参考；
- 用户要求的平台能力与任务本身确定不兼容，且不存在合理降级方案。

能做合理推断时仍然不追问。

### 交互模式

只有用户明确要求共同讨论、脑暴、逐步设计、比较方向、先提问或 Grill Me 时才进入。

读取：`assets/templates/mode-interactive-output-contract.md`

规则：

- 每次只问一个问题；
- 只问当前最影响结果的变量；
- 每个问题给出推荐答案；
- 沿设计依赖顺序推进；
- 已确认的信息不重复询问；
- 能从输入和上下文推断的内容不追问；
- 用户要求收口，或剩余问题只影响轻微细节时立即生成最终结果。

Combat Interactive Mode 与 Quick Mode 共用同一 Combat Planning Graph 和质量标准，只把高影响、低置信度、确实存在明显分叉的决策暴露给用户。

#### Combat Interactive Decision Purity 强制检查

每轮候选项必须只回答当前 Primary Planning Node。特别是：

- Fighting Direction / “怎么打”候选只能描述 Movement / Technique / Range / Physical Scale / 摔控比例 / 腿法比例 / 路线与节奏等打法差异；
- **`一镜到底 / 固定机位 / 贴身手持 / 完整动作可读 / 电影冲击 Coverage` 属于 Camera Intent，禁止混入 Fighting Direction 候选；**
- Character Identity 候选只能决定双方“怎么以不同方式打”，不得顺手锁死 Camera / Ending；
- Camera Intent 候选不得反向改变已经确认的 Fighting Direction / Technique Identity。

用户完成最后一个高价值 Combat 选择后，必须执行上面的 **Action Combat Post-Planning Mandatory Path**，不能从 Interactive 直接跳到 Final Assembly。

## 第四步：按缺口读取控制页

读取 `references/controls/index.md`，按需加载 `0-3` 份控制页。

可选方向：

- `timeline-rhythm/control.md`：时间轴、节拍和自然落点；
- `subject-motion/control.md`：主体动作、重心、惯性和反馈；
- `camera-direction/control.md`：景别、机位、主运镜和镜头失控约束；
- `spatial-blocking/control.md`：站位、朝向、视线、动线和空间关系；
- `continuity-consistency/control.md`：人物、服装、场景、道具和动作状态连续性；
- `performance-expression/control.md`：表演、微表情、呼吸、停顿和口型；
- `audio-visual-sync/control.md`：对白、音效、BGM、节拍和音画同步；
- `reference-binding/control.md`：多模态素材职责、主真源和冲突处理；
- `prompt-assembly/control.md`：普通任务按需用于信息优先级、去重、压缩和最终组装；**Action Combat 固定读取，不计入本节 `0-3` 可选预算**；
- `realism-quality/control.md`：真实设备感、物理可信和去 AI 漂浮感。

Combat Choreography Engine 属于 Task；通用 Controls 继续只提供跨任务能力。

## 第五步：按需读取资料库

读取 `references/libraries/index.md`，正常按需加载约 `0-2` 份主要 Detail。

### 通用 Libraries

- `camera-shot/library.md`
- `action-motion/library.md`
- `performance-expression/library.md`
- `transition-effects/library.md`
- `lighting-color/library.md`
- `audio-sound/library.md`
- `genre-patterns/library.md`

### Combat Libraries

- `combat-choreography-profiles/library.md`：少量稳定 Cinematic Choreography Profile；
- `combat-fighting-profiles/library.md`：现代格斗 Technique / Execution Knowledge；
- `combat-martial-profiles/library.md`：武术 / 武侠空手知识；
- `combat-weapon-profiles/library.md`：刀 / 剑 / 枪 / 棍 Range、Contact、Weapon State；
- `combat-environment-patterns/library.md`：Environment Affordance 专业模式；
- `signature-moment-patterns/index.md`：轻量 Pattern 路由，再只加载命中的 `patterns/<id>.md`。

Combat V2 采用 Two-stage On-demand Loading：

```text
Task Core / Choreography / 当前专项 / 轻量索引
→ Combat Planning Context
→ Stage-2 Pattern Hit Evidence Gate
→ 条件命中的 leaf execution knowledge
→ Concrete Action Phrase
```

Detail Slot 竞争优先级：专业动作 / 兵器正确性 → Character Identity 差异化 → Signature Moment / 创意增强。

Stage-2 Gate 真正命中的 leaf execution knowledge 属于 Mandatory Execution Reference，不因普通 `0-2` Detail 预算而被跳过。

不建设 Combat Character Identity / occupation portrait Library；`source-cases/` 研究档案不进入正常运行。

## 第六步：按需读取风格

读取 `references/styles/index.md`，最多加载一份主 style Reference：

- `cinematic-live-action/style.md`
- `realistic-short-drama/style.md`
- `anime-animation/style.md`
- `comic-motion-drama/style.md`
- `commercial-advertising/style.md`
- `documentary-ugc/style.md`
- `experimental-visual/style.md`

Combat 不新增一级 Style；“怎么打”由 Combat Choreography / specialist / Profile 决定，“画面长什么样”继续由现有 Style 决定。

## 第七步：模型适配

读取 `references/models/index.md`，最多加载一份模型适配页。

### Generic

用户未指定模型时读取：`references/models/generic.md`

使用模型无关、语义清楚的自然语言，不伪造平台语法或参数。

### Seedance 2.0

用户明确使用 Seedance 2.0 时读取：`references/models/seedance-2.md`

将已确定素材职责转换为明确的 `@图片N / @视频N / @音频N` 绑定。

### LTX-2.3

用户明确使用 LTX-2.3 时读取：`references/models/ltx-2-3.md`

默认把结构化导演方案转换为具体、流动、现在时的自然语言段落。

### Combat Capability Contract

Combat Model Adapter 可提供：

- Motion Complexity Capacity；
- Multi-character Stability；
- Contact / Interaction Fidelity；
- Spatial Continuity；
- Camera Complexity Capacity；
- Temporal / Prompt Following。

没有可靠资料 / Benchmark 时标记 `Unverified`，不得伪造 High / Medium / Low。

Model Capability 只改变实现路径，不偷改 Combat Intent / Coverage / 观看目标。模型若需要降载，优先降低 Camera Complexity / 单窗口并行复杂度，不默认降低 Camera Mobility、Kinetic Scope 或把连续战斗稀释成少量动作。

## 第八步：选择输出模板

所有任务固定读取一份模式输出合同，并按任务形态读取交付模板。

### 单镜头

读取：`assets/templates/single-shot-video-template.md`

### 多镜头 / 多片段 / 故事板

读取：`assets/templates/multi-shot-video-template.md`

### 多模态参考

按需补读：`assets/templates/multimodal-reference-template.md`

### 模型转换

按需读取：`assets/templates/model-adapted-output-template.md`

Combat 不建立平行输出模板：先用 Combat Blueprint 判断单镜头 / 多镜头，再执行 Combat-aware Prompt Assembly + Final Preflight，**通过后**才把动作、镜头、声音、连续性和少量高风险约束注入现有模板。

输出模板只负责承载，不得覆盖 Combat Task 已确定的时间序列化和动作连续性规则。高密度 Combat 默认 `Continuous Action Spine + Soft Time Anchors`；通用模板不能仅因为“15 秒 / 3+ 阶段”自动改回 Hard Timeline。

## Reference 加载预算

固定读取：

- `1` 份 input Reference；
- `1` 条 task 主路线；
- `1` 份模式输出合同；
- `1` 份主交付模板。

按需读取：

- `0-3` 份 controls；
- `0-2` 份主要 libraries detail；
- `0-1` 份 style；
- `0-1` 份 model adapter；
- `0-1` 份多模态模板；
- 失败诊断时 `0-1` 份 diagnostic。

Action Combat 额外固定读取：

- `action-camera-handoff-playbook.md`，作为 Stage-2 Evidence / Realizability / Action–Camera Bridge；
- `prompt-assembly/control.md`，作为 Final Assembly / Preflight 必经 Reference；
- 条件命中的 Stage-2 leaf execution knowledge（当前最小验证阶段通常为 `minimum-validation-set.md`）。

前两项不占 `0-3 controls` 配额；真正由 Stage-2 Gate 命中的 leaf execution knowledge 不占普通 `0-2 libraries detail` 可选预算。

Combat 的 `index + core + choreography + 一个专项分支` 视为同一主 Task 路线，不同时加载现代与武侠两个分支。

规则：

- 不为了凑满预算读取资料；
- 同一文件被多个入口命中时只读取一次；
- 不一次性读取整个目录；
- 正常生成不读取 diagnostics；
- 原始研究资料 / `source-cases/` 不作为默认运行期 Reference。

## 信息优先级

发生冲突时按以下顺序处理：

```text
用户当前明确要求
→ 必须保留 / 必须修改 / 必须禁止
→ 当前任务 Playbook
→ 当前输入 Reference 和素材职责
→ Combat Stage-2 Evidence / Realizability / Action–Camera / Final Assembly（当前为 Combat 时）
→ 已加载 controls
→ 已加载 libraries 与 style
→ model adapter 的能力边界和表达方式
→ 自动补全
```

模型适配可以限制能力和改变表达方式，但不能擅自改变用户的剧情目标、人物关系、Combat Intent、Coverage 和核心动作。

## 自动补全与冲突裁决

- 缺少时长时，按任务复杂度选择足以完成动作且不过载的最小合理时长；
- 缺少镜头时，普通任务优先使用固定机位、轻微推进或短距离跟拍；**Action Combat 则先看 Kinetic Scope：人物发生明显 Position / Range / Axis / Route 变化时，优先简单连续跟随，不把“稳定”自动解释为固定镜头**；
- 缺少收尾时，为动作、视线、重心、镜头和声音补自然落点；
- 缺少声音时，只补有明确画面来源的环境音或拟音；
- 多素材冲突时，为每个关键维度选择唯一主真源；
- 主体动作强时通常降低无必要 Camera Complexity；**Action Combat 不因此自动降低 Camera Mobility**；
- 用户选择“完整动作可读型”时，优先更宽、更少无意义 Cut，但**不得序列化成全程固定中大全景**；Camera 仍应随 Route / Level / Support / Initiative / Fight-space 的真实变化做有动机的跟随、降位、Reframe 或必要 Cut；
- 互斥风格只保留最符合核心观看目标的一种；
- Combat 缺少流派时选择最符合 Character Identity、剧情和距离关系的低风险动作语言，不按职业强行套 Profile；
- Combat Character Identity 不根据性别、年龄、外貌、体型直接套打法；这些只能作为能力 / 物理约束输入之一；
- Combat 缺少音乐时按场景决定弱 BGM、无 BGM 或节奏音乐，不为了“完整”机械加音乐；
- 不擅自增加新角色、新剧情线、大世界观或强情绪反转。

## Prompt 组装原则

- 先写任务和时长，再写素材职责；
- 先建立初始状态，再写运动；
- 普通任务需要时间轴时分别写主体状态、镜头状态、表演 / 声音和结束状态；
- 全局固定项只写一次，本段只写变化；
- 抽象情绪改写成眼神、呼吸、眉眼、嘴角、姿态和小动作；
- 光影和声音必须有场景来源；
- 每段视频只保留一个主镜头任务；
- 多镜头必须写镜间承接和跨镜稳定项；
- 图生视频减少静态画面复述，重点写从当前状态如何运动；
- Combat 先由 Core 保证 Action–Reaction、Range / Advantage / Condition / Target / Weapon / Environment 状态连续，再由 Choreography 保证 Coverage、Action Phrase、角色打法、Contact Solidity、Kinetic Scope、Temporal / Motion Continuity 与 Camera Mobility；
- Combat Stage-2 Gate 命中的 Movement / Technique / Transition Detail 必须真正进入 Concrete Action Phrase；没有 leaf Read Evidence 时不得在 Prompt Assembly 阶段用语言润色伪装 Pattern Realization；
- 用户明确确认的 Technique Identity 必须通过**改变动作状态的可见行为**兑现：例如“拳腿组合 vs 拳肘抱摔”不能只写一次低踢和一次“尝试抱住”，随后全部塌回同一套前臂 / 肩线 / 抓臂骨架；
- 高密度 Combat 默认使用 `Continuous Action Spine + Soft Time Anchors`，不把 Active Exchange 机械拆成每 1–3 秒一个独立动作盒；
- Combat Final Prompt 由正向动作语言主导，状态术语尽量转译为可见动作、受力和空间后果；
- Combat 的具体化必须通过 Model Execution Realizability：优先 `Whole-body Motor Driver → 关键 Technique → Opponent Response → Balance / Position Consequence → Continuation`，压描述复杂度而不是压动作连续性；
- Combat Audio 与 Action / Camera 同一连续事件流设计，但 Audio Accent Density 不等于 Action Density；
- Negative 只针对当前最危险失败模式，不默认追加通用禁止清单，也不添加用户未要求的剧情限制；
- 最后一拍必须可自然停住。

## 输出前自查

### 输入与任务

- 是否选择唯一主输入路线；
- 是否选择唯一主任务路线；
- 多模态素材是否分配明确职责；
- 每个关键维度是否只有一个主真源。

### 画面与运动

- 初始画面是否清楚；
- 主体运动和镜头运动是否分开；
- 动作阶段、重心、接触和反馈是否成立；
- 镜头是否有起点、方向、速度和停止点；
- 空间、站位、朝向和道具状态是否连续。

### Combat 专项

如果当前是 Action Combat，最终交付前必须完成一个**合并 Gate**，而不是只确认文件“读过”：

1. **Stage-2 是否真的命中**：当前 Fighting Direction / Technique Identity / Movement Gap 是否需要 leaf execution knowledge；若需要，是否有真实 `Gap → Slot → leaf Read → Pattern/Detail → Concrete Action` Evidence；
2. **动作是否够**：Coverage / Exchange Depth / Kinetic Scope 是否与观看目标相符，是否仍有长对峙、上半身锁死、动作被时间摊薄；
3. **动作是否连续**：Action Phrase 是否通过 Contact / Momentum / Footwork / Axis / Range / Position 等继承，是否仍是一招一停、轮流出招；
4. **角色是否合理且真实区分**：Combat Character Identity 是否能从改变状态的 Movement / Technique / Initiative 看出差异；用户已确认的“拳腿 / 拳肘抱摔”等差异是否真实兑现，而不是标签化或只出现一次未形成后果的尝试；
5. **Model Execution Realizability 是否通过**：是否出现 Effective High Granularity Everywhere、Instruction Saturation、Upper-body Semantic Dominance；Feet-fixed Test 是否失败；
6. **接触与状态是否成立**：Contact 是否有 Commitment、受力 / 压力、Reaction 与 Persistent Consequence；Range / Position / Advantage / Environment 是否影响下一拍；
7. **镜头是否跟得上且由动作触发**：Camera Complexity 与 Camera Mobility 是否分离；完整动作可读型是否仍保留有动机的 Route / Level / Support / Initiative Reframe；关键 Cut / Reframe 是否继承 Active Motion；
8. **最终序列化是否正确**：高密度 Combat 是否保持 Continuous Action Spine + Soft Time Anchors；Hard Timeline 若存在是否有明确理由且跨块无 Reset；Action–Camera Handoff 是否没有被压成泛化 Camera 段；
9. **Prompt 是否 Action-first**：是否由可见动作主导，Negative 是否少而有依据。

任一关键项 FAIL：内部回到 Stage-2 Read / Pattern Selection / Action Phrase / Character Identity / Action–Camera Handoff / Prompt Assembly 对应层重写，重新执行 Gate，通过后才允许交付。

### 表演与音画

- 情绪是否转成可观察表演；
- 对白是否有说话人、停顿和身体动作；
- 音效和音乐是否绑定画面节点；
- 声音是否有来源和空间关系。

### 结构与模型

- 是否有清楚开始、推进和结束状态；
- 多镜头是否有承接与跨包交接；
- 用户未指定模型时是否使用 Generic；
- Seedance 是否正确绑定素材职责；
- LTX 是否使用连贯自然语言并强调运动；
- Model Combat Capability 未验证时是否诚实标记 Unverified；
- 是否删除无价值备选、自动补全说明和重复内容。

## 失败诊断

只有用户明确反馈生成效果不好、多个维度同时失效或 Prompt 存在复杂冲突时，读取：`references/diagnostics/index.md`

Combat 主诊断：

- Advantage / Condition / Target / Weapon / Beat State 前后无法同时成立 → `combat-state-continuity-failure`；
- Active Combat Coverage / Exchange Richness / Kinetic / Temporal / Motion Continuity 明显不足 → `combat-choreography-underfill`；
- Contact 已发生但受力 / 压力 / 兵器 / 材质后果不可信 → `combat-contact-solidity-failure`。

手 / 肢体穿模、整体失重、Camera Chaos、音画错位继续使用对应通用 Diagnostic。

正常生成任务不提前加载诊断层；每次只选一个主 Diagnostic。

## 严禁事项

- 不只写风格，不写时间和运动；
- 不把主体运动和镜头运动混成一句空话；
- 不让多张图片、多个视频或音频平均融合；
- 不用大量导演名、品牌名或质量词代替执行变量；
- 不同时堆叠多个主运镜；
- 不让动作、镜头、光影、特效和音乐同时满强度；
- 不默认输出主版本、备选 A、备选 B；
- 不默认展示“已自动补全项”；
- 不伪造未支持模型的参数和语法；
- 不把研究区原始资料 / source-cases 直接作为默认最终知识；
- Combat 不把招式示例、Beat 数量、回归场景、Profile、Pattern 或默认节奏写成死框架；
- Combat 不使用固定 `2-4` / `2–4` 交互节点作为 Battle Beat 全局动作数量上限；
- Combat 不为了“清晰”默认减少有效攻防；
- Combat 不把职业、性别、年龄、外貌或体型直接映射固定打法；
- Combat Fighting Direction 候选不混入 Camera Intent；
- Combat 不用 Camera Shake / 大音效代替真实 Contact；
- Combat 不因“完整动作可读”自动锁成全程固定中大全景；
- Combat 不因通用单镜头模板自动把高密度连续战斗切成多个 Hard Time Blocks；
- Combat 不建立独立 single-shot / multi-shot 模板副本；
- 不暴露内部 Reference、目录、迁移和维护说明。