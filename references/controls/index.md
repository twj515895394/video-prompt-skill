# Controls Index

控制层负责“怎么判断、怎么协调、怎么限制”，不负责罗列大量术语，也不替代任务 Playbook。

每次按当前最大缺口读取 `0-3` 份控制页，不为了增加细节默认加载整个控制层。

## timeline-rhythm

读取：

- `timeline-rhythm/control.md`

处理：

- 绝对时间轴；
- 开场、推进、高潮、反馈和收束；
- 动作与情绪节拍；
- 镜头密度；
- 多镜头承接；
- 自然停顿和结尾落点。

## subject-motion

读取：

- `subject-motion/control.md`

处理：

- 主体动作目标；
- 起势、推进、接触、反馈、恢复；
- 重心、惯性、速度和受力；
- 人物、动物、物体和环境运动；
- 主体运动与镜头运动的强度协调。

## camera-direction

读取：

- `camera-direction/control.md`

处理：

- 景别和机位如何选择；
- 镜头为什么移动；
- 主运镜、速度和运动路线；
- 焦点转移；
- 轴线和运动方向；
- 镜头失控、漂移和炫技过载。

## spatial-blocking

读取：

- `spatial-blocking/control.md`

处理：

- 人物站位；
- 视线和朝向；
- 前中后景；
- 出入口和行动路线；
- 道具状态；
- 角色、道具和镜头之间的空间关系。

## continuity-consistency

读取：

- `continuity-consistency/control.md`

处理：

- 人物身份、脸部、发型、服装；
- 场景结构和道具状态；
- 动作阶段和体态重心；
- 光影和方向连续性；
- 跨镜、跨段和跨参考素材的一致性。

## performance-expression

读取：

- `performance-expression/control.md`

处理：

- 表演目标；
- 眼神、眉眼、嘴角、呼吸和小动作；
- 对白前后停顿；
- 情绪变化过程；
- 口型和面部一致性风险。

## audio-visual-sync

读取：

- `audio-visual-sync/control.md`

处理：

- 对白、旁白、环境音、拟音、BGM；
- 节拍点和视觉事件绑定；
- 声音进入、持续、退出；
- 口型同步；
- 音画同步和声音空间。

## reference-binding

读取：

- `reference-binding/control.md`

处理：

- 主参考与辅助参考；
- 素材职责分配；
- 局部参考；
- 多图、多视频、多音频冲突；
- 禁止平均融合；
- 参考强度和保留边界。

## prompt-assembly

读取：

- `prompt-assembly/control.md`

处理：

- 信息优先级；
- 通用导演方案的组织顺序；
- 时间轴与全局约束如何组合；
- 正向描述和负向限制的比例；
- Prompt 压缩、去重和冲突裁决；
- 与模型适配层的交接边界。

## realism-quality

读取：

- `realism-quality/control.md`

处理：

- 去 AI 漂浮感和动态海报感；
- 真实设备记录感；
- 物理可信；
- 自然表演和微小不完美；
- 光影、材质和环境反馈的一致性。

## 常用组合

### 文生视频基础

- `timeline-rhythm/control.md`
- `prompt-assembly/control.md`

按缺口再补主体运动、镜头或连续性。

### 图生视频基础

- `reference-binding/control.md`
- `continuity-consistency/control.md`

动作复杂时补 `subject-motion/control.md`，镜头易漂时补 `camera-direction/control.md`。

### 写实人物短片

- `performance-expression/control.md`
- `realism-quality/control.md`
- `timeline-rhythm/control.md`

### 动作与体育

- `subject-motion/control.md`
- `camera-direction/control.md`
- `spatial-blocking/control.md`

### 多模态与音频

- `reference-binding/control.md`
- `audio-visual-sync/control.md`
- `prompt-assembly/control.md`

## 选择规则

- 任务页已经能解决的问题，不额外读取控制页。
- 需要具体术语或选项时读取 `libraries/`，而不是继续扩写控制页。
- 用户明确指定风格时读取 `styles/`。
- 用户反馈生成失败且原因跨多个维度时，读取 `diagnostics/`。
- 模型能力、参数和素材引用语法统一读取 `models/`。
- 同一轮命中同一个控制页时只读取一次。
- 已经读取三份控制页仍无法解决时，优先检查任务是否过载，而不是继续堆控制页。