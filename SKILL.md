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
- 复杂战斗同时遵循“通过结构获得清晰，而不是通过动作通缩获得清晰”：高信息密度允许存在，但必须用 Action Phrase、状态连续性、镜头可读性和执行预算组织清楚。
- 不向用户暴露内部目录、维护路径、资料迁移和加载过程。

## 第一步：判断输入

读取 `references/inputs/index.md`，只选择一份主输入 Reference。

### 1. 纯文字输入

读取：

- `references/inputs/text-input.md`

用于从文字建立初始画面、动作顺序、镜头和时间结构。

### 2. 单张图片

读取：

- `references/inputs/single-image-input.md`

先判断图片职责：

- 首帧；
- 尾帧；
- 人物；
- 场景；
- 风格；
- 构图；
- 动作或表情终态。

### 3. 多张图片

读取：

- `references/inputs/multi-image-input.md`

必须为每张图片分配明确职责，并确定人物、服装、场景、首帧、尾帧、构图、光影和动作各自的主参考。

### 4. 一个或多个视频

读取：

- `references/inputs/video-input.md`

先判断视频提供什么：

- 动作；
- 表演；
- 运镜；
- 节奏；
- 转场；
- 特效；
- 声音；
- 待编辑或待延长主体。

### 5. 音频输入

读取：

- `references/inputs/audio-input.md`

判断音频承担：

- 对白；
- 音色与语气；
- 时间节拍；
- BGM；
- 环境音；
- 拟音或关键音效。

### 6. 图片 / 视频 / 音频混合输入

读取：

- `references/inputs/mixed-multimodal-input.md`

混合输入只读取这一份主输入页，不同时加载多份单模态输入页。

## 第二步：判断任务

读取 `references/tasks/index.md`，只选择一份主任务 Playbook。

### 1. 文生视频

读取：

- `references/tasks/text-to-video/playbook.md`

### 2. 图生视频

读取：

- `references/tasks/image-to-video/playbook.md`

### 3. 多模态参考视频

读取：

- `references/tasks/multimodal-reference-video/playbook.md`

### 4. 视频参考复刻 / 视频转视频

读取：

- `references/tasks/video-reference-and-video-to-video/playbook.md`

### 5. 视频局部编辑

读取：

- `references/tasks/video-editing/playbook.md`

### 6. 视频向前 / 向后延长

读取：

- `references/tasks/video-extension/playbook.md`

### 7. 音频驱动与音乐卡点

读取：

- `references/tasks/audio-driven-and-beat-sync/playbook.md`

### 8. 故事板 / 多镜头 / 多片段到视频

读取：

- `references/tasks/storyboard-and-multi-shot-video/playbook.md`

### 9. 复杂动作格斗 / 电影武侠

当核心难点是持续攻防、动作编排、Battle Beat、Range / Advantage / Condition、1vN Target Handoff、兵器连续性、接触实感或 Action / Camera / Audio 三线同步时，读取：

- `references/tasks/action-combat-video/index.md`
- `references/tasks/action-combat-video/core-playbook.md`
- `references/tasks/action-combat-video/choreography-playbook.md`

然后只选择一个专项分支：

- 现代格斗：`references/tasks/action-combat-video/modern-combat-playbook.md`
- 电影武侠：`references/tasks/action-combat-video/cinematic-wuxia-playbook.md`

简单挥拳、跑跳、追逐、体育动作不进入 Combat 专项，继续使用原主任务 + `action-motion`。

题材不同通常不新增任务路线；Action Combat 只因执行流程显著不同而作为一级专项任务。

Combat 内部职责：

- `core-playbook.md` 负责 State / Continuity / Battle Runtime Skeleton；
- `choreography-playbook.md` 负责 Coverage / Rhythm / Action Phrase / Character Identity / Contact Solidity / Signature Moment / Execution Budget 等动作导演逻辑；
- 专项 Playbook 负责 Modern / Wuxia 的具体动作语言与物理尺度。

## 第三步：判断模式

### 快速模式

除非用户明确要求交互共创，否则默认使用快速模式。

读取：

- `assets/templates/mode-quick-output-contract.md`

快速模式：

- 不追问；
- 不要求确认；
- 不输出多个近似方案让用户选择；
- 不展示分析、方向决策或自动补全项；
- 信息不足时自动使用最小风险默认值；
- 冲突时自行裁决，只保留最符合主目标的路线；
- 直接输出一份可复制 Prompt 或必要的 Prompt Pack。

Combat Quick Mode 必须执行**完整 Combat Planning，但静默解决低风险决策**：内部仍推导 Combat Intent、Branch、Coverage、Rhythm、Character Identity、Environment、Contact Solidity、Signature Moment、Action / Camera Execution Budget、Battle Beat 与 State Contract；这些内部状态不默认展示，最终直接输出详细、完整、专业、可复制 Prompt。

只有以下情况可以在快速模式中提出一个必要问题：

- 无法判断用户要求处理哪份输入素材；
- 同一关键维度存在两个互斥且同等强度的用户指定主参考；
- 用户要求的平台能力与任务本身确定不兼容，且不存在合理降级方案。

能做合理推断时仍然不追问。

### 交互模式

只有用户明确要求共同讨论、脑暴、逐步设计、比较方向、先提问或 Grill Me 时才进入。

读取：

- `assets/templates/mode-interactive-output-contract.md`

规则：

- 每次只问一个问题；
- 只问当前最影响结果的变量；
- 每个问题给出推荐答案；
- 沿设计依赖顺序推进；
- 已确认的信息不重复询问；
- 能从输入和上下文推断的内容不追问；
- 用户要求收口，或剩余问题只影响轻微细节时立即生成最终结果。

Combat Interactive Mode 与 Quick Mode 共用同一 Combat Planning Graph 和质量标准，只把高影响、低置信度、确实存在明显分叉的决策暴露给用户；可以按需展示 Combat Blueprint / Beat Sheet，但最终仍必须再汇总成一份可直接复制给视频模型使用的完整 Prompt。

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
- `prompt-assembly/control.md`：信息优先级、去重、压缩和最终组装；
- `realism-quality/control.md`：真实设备感、物理可信和去 AI 漂浮感。

Combat 不新增 `combat-choreography` 专属 Control。Combat Choreography Engine 属于 `action-combat-video` Task；通用 Controls 继续只提供跨任务能力。任务 Playbook 已能解决的问题，不额外加载控制页。

## 第五步：按需读取资料库

读取 `references/libraries/index.md`，按需加载 `0-2` 份资料库。

可选：

- `camera-shot/library.md`：景别、机位、焦段、设备和运镜选项；
- `action-motion/library.md`：动作、打击、体育和环境反馈结构；
- `performance-expression/library.md`：表情、微表情和对白表演选项；
- `transition-effects/library.md`：剪辑、转场和视觉特效；
- `lighting-color/library.md`：光源、光影、色调和动态光；
- `audio-sound/library.md`：对白、环境音、拟音、BGM 和声音空间；
- `genre-patterns/library.md`：短剧、漫剧、广告、动作、悬疑、纪录等题材模板；
- `combat-fighting-profiles/library.md`：现代格斗动作语言；
- `combat-martial-profiles/library.md`：武术 / 武侠空手动作语言；
- `combat-weapon-profiles/library.md`：刀 / 剑 / 枪 / 棍动作语言与兵器连续性；
- `combat-environment-patterns/library.md`：战斗环境互动模式。

资料库回答“可以选什么”，控制页回答“为什么选、如何协调”。Combat Playbook 回答“怎么编排”，Combat Libraries 不复制状态机。

Combat V2 采用 Two-stage On-demand Loading：先用 Task Core / Choreography / 当前专项与轻量索引形成 `Combat Planning Context`，再只展开当前动作计划真正需要的少量 Library Detail；正常情况下仍控制在约 `0-2` 份主要 Library Detail。

## 第六步：按需读取风格

读取 `references/styles/index.md`，最多加载一份主 style Reference：

- `cinematic-live-action/style.md`；
- `realistic-short-drama/style.md`；
- `anime-animation/style.md`；
- `comic-motion-drama/style.md`；
- `commercial-advertising/style.md`；
- `documentary-ugc/style.md`；
- `experimental-visual/style.md`。

Combat 不新增一级 Style；“怎么打”由 Combat Playbook + Profile 决定，“画面长什么样”继续由现有 Style 决定。

用户只说“电影感、广告感、短剧感”时，必须把风格拆成镜头、表演、光影、材质、节奏和声音，不直接把抽象标签当成执行方案。

## 第七步：模型适配

读取 `references/models/index.md`，最多加载一份模型适配页。

### Generic

用户未指定模型时默认读取：

- `references/models/generic.md`

使用模型无关、语义清楚的自然语言，不伪造平台语法或参数。

对于 Combat，Generic Professional Prompt 本身就是完整最终产品，不要求先指定平台。

### Seedance 2.0

用户明确使用 Seedance 2.0，或任务依赖其多模态引用、视频编辑、延长或卡点能力时读取：

- `references/models/seedance-2.md`

将已确定的素材职责转换为明确的 `@图片N / @视频N / @音频N` 绑定。

### LTX-2.3

用户明确使用 LTX-2.3 时读取：

- `references/models/ltx-2-3.md`

默认把结构化导演方案转换为具体、流动、现在时的自然语言段落。图生视频重点写接下来如何运动，表演和对白必须带动作与停顿。

不创建或加载其他模型适配页。

## 第八步：选择输出模板

所有任务固定读取一份模式输出合同，并按任务形态读取交付模板。

### 单镜头

读取：

- `assets/templates/single-shot-video-template.md`

### 多镜头 / 多片段 / 故事板

读取：

- `assets/templates/multi-shot-video-template.md`

### 多模态参考

需要向最终 Prompt 保留素材职责时补读：

- `assets/templates/multimodal-reference-template.md`

### 模型转换

需要把通用方案转换为目标模型表达时读取：

- `assets/templates/model-adapted-output-template.md`

Combat 不建立平行输出模板：先用 Combat Blueprint 判断单镜头 / 多镜头，再把动作、镜头、声音、连续性、物理约束和专项 Negative Constraints 注入现有模板。

简单任务默认只输出一份最终 Prompt。多镜头任务输出必要的全局固定项和镜头 Prompt Pack。备选版本、自动补全项和方向摘要均不默认输出。

## Reference 加载预算

固定读取：

- `1` 份 input Reference；
- `1` 份 task Playbook；
- `1` 份模式输出合同；
- `1` 份主交付模板。

按需读取：

- `0-3` 份 controls；
- `0-2` 份 libraries；
- `0-1` 份 style；
- `0-1` 份 model adapter；
- `0-1` 份多模态模板；
- 失败诊断时 `0-1` 份 diagnostic。

Combat 的 `index + core + choreography + 一个专项分支` 视为同一主 Task 路线，不同时加载现代与武侠两个分支。

索引文件只用于导航，不计入业务 Reference 数量。

规则：

- 不为了凑满预算读取资料；
- 同一文件被多个入口命中时只读取一次；
- 不一次性读取整个目录；
- 正常生成不读取 diagnostics；
- 原始研究资料不作为运行期 Reference。

## 信息优先级

发生冲突时按以下顺序处理：

```text
用户当前明确要求
→ 必须保留 / 必须修改 / 必须禁止
→ 当前任务 Playbook
→ 当前输入 Reference 和素材职责
→ 已加载 controls
→ 已加载 libraries 与 style
→ model adapter 的能力边界和表达方式
→ 自动补全
```

模型适配可以限制能力和改变表达方式，但不能擅自改变用户的剧情目标、人物关系和核心动作。

## 自动补全与冲突裁决

- 缺少时长时，按任务复杂度选择足以完成动作且不过载的最小合理时长；
- 缺少镜头时，优先使用固定机位、轻微推进或短距离跟拍；
- 缺少收尾时，为动作、视线、重心、镜头和声音补自然落点；
- 缺少声音时，只补有明确画面来源的环境音或拟音；
- 多素材冲突时，为每个关键维度选择唯一主真源；
- 主体动作强时减弱镜头幅度，镜头动作强时简化主体动作；
- 互斥风格只保留最符合核心观看目标的一种；
- Combat 缺少流派时选择最符合剧情和距离关系的低风险动作语言，不强行堆叠多流派；
- Combat 缺少音乐时按场景决定弱 BGM、无 BGM 或节奏音乐，不为了“完整”机械加音乐；
- 不擅自增加新角色、新剧情线、大世界观或强情绪反转。

## Prompt 组装原则

- 先写任务和时长，再写素材职责；
- 先建立初始状态，再写运动；
- 时间轴中分别写主体状态、镜头状态、表演 / 声音和结束状态；
- 全局固定项只写一次，本段只写变化；
- 抽象情绪改写成眼神、呼吸、眉眼、嘴角、姿态和小动作；
- 光影和声音必须有场景来源；
- 每段视频只保留一个主镜头任务；
- 多镜头必须写镜间承接和跨镜稳定项；
- 图生视频减少静态画面复述，重点写从当前状态如何运动；
- Combat 先由 Core 保证 Action–Reaction、Range / Advantage / Condition / Target / Weapon / Environment 状态连续，再由 Choreography 保证 Coverage、Action Phrase、角色打法、接触实感、动作充分性与镜头可读性；
- Combat 的 Audio 与 Action / Camera 同时间线设计，场景需要时包含环境声、拟音、兵器声、呼吸和音乐策略；
- 负向限制只针对当前最危险的失败模式，通常保留 `3-8` 项；
- 最后一拍必须可自然停住。

## 输出前自查

### 输入与任务

- 是否选择了唯一主输入路线；
- 是否选择了唯一主任务 Playbook；
- 多模态素材是否分配了明确职责；
- 每个关键维度是否只有一个主真源。

### 画面与运动

- 初始画面是否清楚；
- 主体运动和镜头运动是否分开；
- 动作阶段、重心、接触和反馈是否成立；
- 镜头是否有起点、方向、速度和停止点；
- 空间、站位、朝向和道具状态是否连续。

### Combat 专项

如果当前是 Action Combat：

- Active Combat Coverage 是否与用户观看目标相符，是否存在无价值长对峙 / 站立 / 提前 Pose；
- 是否形成足够的连续 Action Phrase，而不是只有少量孤立交互；
- Rhythm / Exchange Depth 是否符合角色能力与 Choreography Profile；
- Combat Character Identity 是否能从实际动作看出差异；
- Range 变化是否有动作因果；
- 重要 Contact 是否有接触、受力 / 压力传递、Reaction 与 Consequence；
- Advantage 变化是否有 Turning Event；
- Condition 是否影响后续动作；
- 1vN Target 切换是否有 Handoff；
- Weapon State 是否连续；
- 环境参与是否真正改变战术 / 空间而非随机装饰；
- 相邻 Beat 的结束 / 起始状态是否可衔接；
- Action / Camera / Audio 是否互相服务而不是互相竞争；
- 是否避免把默认 Beat、Profile、Pattern 或回归案例当固定模板；
- 是否没有为了“清晰”无理由削减有效攻防。

### 表演与音画

- 情绪是否转成可观察表演；
- 对白是否有说话人、停顿和身体动作；
- 音效和音乐是否绑定画面节点；
- 声音是否有来源和空间关系。

### 结构与模型

- 是否有清楚的开始、推进和结束状态；
- 多镜头是否有承接与跨包交接；
- 用户未指定模型时是否使用 Generic；
- Seedance 是否正确绑定素材职责；
- LTX 是否使用连贯自然语言并强调运动；
- 是否删除了无价值备选、自动补全说明和重复内容。

## 失败诊断

只有用户明确反馈生成效果不好、多个维度同时失效或 Prompt 存在复杂冲突时，读取：

- `references/diagnostics/index.md`

Combat 中如果单个动作并非主问题，而是 Advantage / Condition / Target / Weapon / Beat State Contract 前后无法同时成立，可使用 `combat-state-continuity-failure`。

正常生成任务不提前加载诊断层。

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
- 不把研究区原始资料直接作为最终知识；
- Combat 不把招式示例、Beat 数量、回归场景或默认节奏写成死框架；
- Combat 不使用固定 `2-4` 交互节点作为 Battle Beat 全局动作数量上限；
- Combat 不为了“清晰”默认减少有效攻防；
- Combat 不建立独立 single-shot / multi-shot 模板副本；
- 不暴露内部 Reference、目录、迁移和维护说明。
