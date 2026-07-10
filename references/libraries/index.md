# Libraries Index

资料库负责提供“有哪些具体选项、术语、结构和题材模板”，不决定任务流程，也不代替控制规则。

每次按当前任务缺口读取 `0-2` 份资料库叶子文件。分类索引只负责导航，不计入业务 Reference 数量。

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

## 常用组合

### 写实短剧

- `genre-patterns/library.md`
- `performance-expression/library.md`

### 动作或体育

- `action-motion/library.md`
- `camera-shot/library.md`

### 产品广告

- `lighting-color/library.md`
- `transition-effects/library.md`

### 音频驱动

- `audio-sound/library.md`
- 按需再选表演或动作库

### 漫剧/动画

- `performance-expression/library.md`
- `action-motion/library.md` 或 `camera-shot/library.md`

## 使用边界

- 资料库回答“可以选什么”，控制层回答“为什么选、如何协调”。
- 一次不要读取整个资料库；当前任务有明确选项时不额外读取。
- 同一术语和详细资料只在一个 library 正文真源出现。
- 社区长 Prompt 不作为资料库正文，只保留结构、变量、适用条件和失败边界。
- 风格完整实现读取 `references/styles/`。
- 模型专属语法和能力读取 `references/models/`。
