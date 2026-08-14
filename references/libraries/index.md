# Libraries Index

资料库负责提供“有哪些具体选项、术语、结构和题材模板”，不决定任务流程，也不代替控制规则。

每次按当前任务缺口读取 `0-2` 份主要资料库叶子文件。分类索引只负责导航，不计入业务 Reference 数量。

Combat V2 额外遵循：

> **Indexes are cheap routing knowledge; leaf files are expensive execution knowledge.**  
> **索引用于选择，正文用于执行。**

---

## camera-shot

读取：

- `camera-shot/library.md`

包含：

- 景别、视角、机位、观看位置；
- 焦段、景深、镜头类型和设备来源；
- 推、拉、摇、移、跟、环绕、升降、穿越等运镜；
- 叙事、情绪、动作和空间镜头组合。

## action-motion

读取：

- `action-motion/library.md`

包含：

- 准备、执行、接触、反馈和恢复；
- 日常人物动作、跑步、追逐、打斗和打击帧；
- 篮球、足球、滑板、舞蹈等运动；
- 动物、车辆、机械、液体、布料和环境反馈。

## performance-expression

读取：

- `performance-expression/library.md`

包含：

- 表情和微表情可见信号；
- 眼神、眉眼、嘴角、呼吸、停顿和小动作；
- 对白、关系、权力、告别和动画表演；
- 表演与镜头的常用搭配。

## transition-effects

读取：

- `transition-effects/library.md`

包含：

- 直接切、动作/形状/视线匹配和声音桥；
- 遮挡、甩镜、穿越、拉焦和反射转场；
- 时间、空间、材质和形态变化；
- 粒子、液体、破碎、重组、机械展开和音乐卡点。

## lighting-color

读取：

- `lighting-color/library.md`

包含：

- 九类基础光影和真实光源；
- 阴影色、高光色和主体分离；
- 十八种电影级色调方向；
- 时间、天气、动态光影、肤色和产品颜色。

## audio-sound

读取：

- `audio-sound/library.md`

包含：

- 对白、旁白、耳语和设备声音；
- 环境音、拟音和动作音效；
- BGM 功能、节拍、卡点和静默；
- 声音距离、方向、空间和口型注意。

## genre-patterns

读取：

- `genre-patterns/library.md`

包含：

- 写实关系短剧、AI 漫剧和动态漫画；
- 动作体育、悬疑、情绪、广告、纪录和 UGC；
- 科普、美食、旅行、奇幻、恐怖、喜剧和实验影像；
- 题材级节拍、镜头、表演、声音和收尾组合。

---

## Combat 专业 Libraries

Combat Libraries 只提供专业知识，不定义 Combat Planning Graph、Battle Beat、Coverage、Exchange Depth、Action Execution Budget 或 State Contract。

### combat-choreography-profiles

读取：

- `combat-choreography-profiles/library.md`

包含少量稳定电影动作编排原型，例如：

- 写实战术型；
- 凌厉电影动作型；
- 高手连续攻防型；
- 重型硬派型；
- 环境技巧型；
- 武侠流动拆招型。

它回答“整场动作戏通常怎么组织”，不等于视觉 Style、职业、Character Identity 或 Fighting Profile。

### combat-fighting-profiles

读取：

- `combat-fighting-profiles/library.md`

包含现代格斗 Technique / Execution Knowledge：Boxing、Muay Thai、Sanda、MMA、Wrestling / Grappling、Tactical Close Combat，以及主 / 辅 Profile 混合边界。

明确：**职业 ≠ Character Identity ≠ Fighting Profile**。

### combat-martial-profiles

读取：

- `combat-martial-profiles/library.md`

包含武术 / 武侠空手动作语言：咏春、八极、太极借力、长拳、南拳，以及电影武侠身法选项。

### combat-weapon-profiles

读取：

- `combat-weapon-profiles/library.md`

包含刀、剑、枪、棍的 Range、轨迹、持握、Blade / Weapon Clash / Blunt Contact Modality、不同兵器换距和 Weapon State 连续性。

### combat-environment-patterns

读取：

- `combat-environment-patterns/library.md`

包含走廊、墙面 / 门框、桌椅、柱体、楼梯、栏杆、车辆、竹林、屋顶和高低差空间等 Affordance 知识。

它回答“环境可以怎样改变线路 / Range / Advantage / Position”，不是物体 → 固定动作字典。

### signature-moment-patterns

先读取轻量索引：

- `signature-moment-patterns/index.md`

然后只读取命中的 `patterns/<pattern-id>.md`。

第一批 Pattern 包括：

- constrained-space-reversal；
- environment-assisted-counter；
- rapid-counter-recounter；
- weapon-distance-transition；
- false-opening-trap；
- momentum-redirection；
- dominance-reversal。

`patterns/` 是运行时生产知识；`source-cases/` 只在维护 / 核实 / 用户明确指定作品时使用，正常生成不读取。

---

## Combat Two-stage Library Loading

### Stage 1：Planning

先使用 Task Core / Choreography / 当前专项与必要轻量 Index 形成 `Combat Planning Context`。

### Stage 2：Detail

正常情况下只展开约 2 个主要 Library Detail Slot：

```text
Slot A：Technique / Execution Knowledge
→ combat-fighting-profiles
  / combat-martial-profiles
  / combat-weapon-profiles

Slot B：Choreography Enhancement Knowledge
→ signature-moment-patterns
  / 其他确有必要的增强知识
```

`combat-choreography-profiles` 若只是通过少量稳定 Profile 做路由，可按轻量知识使用；不为了“完整”把所有 Profile 正文和所有 Signature Pattern 同时加载。

Slot 竞争优先级：

```text
用户明确指定的专业动作 / 武器知识
→ 保证专业正确性所需知识
→ Character Identity 差异化
→ Signature Moment / 创意增强
```

复杂环境只有常识不足时才让 `combat-environment-patterns` 占主要 Detail Slot。

---

## 常用组合

### 写实短剧

- `genre-patterns/library.md`
- `performance-expression/library.md`

### 普通动作或体育

- `action-motion/library.md`
- `camera-shot/library.md`

### 复杂现代格斗

先由 Choreography 选 Profile / Identity，再按需：

- Technique：`combat-fighting-profiles/library.md`；
- 创意增强：命中的 `signature-moment-patterns/patterns/<id>.md`；
- 强环境专业知识确实必要时，用 `combat-environment-patterns/library.md` 替换次要增强 Slot。

### 电影武侠

空手 Technique：

- `combat-martial-profiles/library.md`

兵器 Technique：

- `combat-weapon-profiles/library.md`

Signature / Environment 只按当前 Planning Context 选择，不因“武侠”自动全部加载。

### 产品广告

- `lighting-color/library.md`
- `transition-effects/library.md`

### 音频驱动

- `audio-sound/library.md`
- 按需再选表演或动作库

### 漫剧 / 动画

- `performance-expression/library.md`
- `action-motion/library.md` 或 `camera-shot/library.md`

---

## 使用边界

- 资料库回答“可以选什么”，控制层回答“为什么选、如何协调”，Task Playbook 回答“怎么运行和编排”。
- Combat Libraries 不定义 Battle Beat、状态机、Coverage、Action Sufficiency 或任务流程。
- 一次不要读取整个资料库；当前任务有明确选项时不额外读取。
- 同一术语和详细资料只在一个 library 正文真源出现。
- 不建设 Combat Character Identity / 职业画像 Library。
- 不把 Pattern 或 Profile 当固定动作模板。
- `source-cases/` 属于研究证据，不是默认运行时 Reference。
- 社区长 Prompt 不作为资料库正文，只保留结构、变量、适用条件和失败边界。
- 风格完整实现读取 `references/styles/`。
- 模型专属语法和能力读取 `references/models/`。
