# Video Prompt References Index

## 路由目标

用最少量 reference 支撑当前任务，避免把视频 skill 重新变成“大而散的资料堆”。

默认加载预算：

- `1` 份模式 reference
- `1` 份输入 reference
- `1` 份任务 reference
- `timeline/timeline-assembly.md`
- `continuity/continuity-guardrails.md`
- `0-2` 份高价值控制 reference
- `0-1` 份输出结构 reference
- `0-2` 份附录

## 路由优先级

冲突时按以下优先级执行：

1. 用户当前明确要求
2. 当前任务 playbook
3. 高频控制 reference
4. 时间轴与连续性 reference
5. 输入分析 reference
6. 模式 reference
7. 附录

## 第一步：判断模式

### 快速模式

加载：

- `mode-quick/quick-mode.md`

### 交互模式

加载：

- `mode-interactive/interactive-mode.md`

## 第二步：判断输入

### 纯文字

加载：

- `input-text-only/text-expansion.md`

### 有参考图

加载：

- `input-image-ref/image-reference-analysis.md`

额外执行：

- 先判图像类型
- 再判主图与辅助图

## 第三步：判断任务

### 图生视频

加载：

- `task-image-to-video/image-to-video-playbook.md`

### 文生视频

加载：

- `task-text-to-video/playbook.md`

## 第四步：判断输出结构

### 单片段

按需加载：

- `output-single-unit/output-spec.md`

### 多片段

按需加载：

- `output-multi-unit/output-spec.md`

## 第五步：按需加载附录

## 第五步：按需加载高价值控制页

以下文件不属于附录，而是“高价值控制 reference”。当用户明确要求视频更真实、运镜别失控、片段更像真实镜头时，优先加载：

- `style-control/anti-ai-video-realism.md`
- `style-control/camera-failure-patterns-negative.md`
- `continuity/human-motion-consistency.md`
- `timeline/lifestyle-beat-and-landing.md`

推荐触发规则：

- 要“像真实镜头 / 别像动起来的 AI 图”：加载 `anti-ai-video-realism.md`
- 要“镜头别乱飘 / 别太炫 / 运镜自然一点”：加载 `camera-failure-patterns-negative.md`
- 要“别变脸 / 跨帧人物要稳 / 动作别跳”：加载 `human-motion-consistency.md`
- 要“有生活化收尾 / 有自然落点 / 别像被剪断”：加载 `lifestyle-beat-and-landing.md`

## 第六步：按需加载附录

### 运镜附录

- `appendix/camera-movement-appendix.md`

适用：

- 需要明确镜头如何动
- 需要区分推进、拉远、跟拍、环绕、手持等不同运动行为

### 风格附录

- `appendix/visual-style-appendix.md`

适用：

- 题材气质或设备质感不明确
- 用户只说“电影感、广告感、短剧感”，需要拆解

### 动作节拍附录

- `appendix/action-beat-appendix.md`

适用：

- 动作、冲击、奔跑、对抗、爆点镜头是主任务
- 需要把动作拆成起势、接触、反馈、恢复

## 禁止误用

- 不把图生视频直接套成文生视频模板
- 不只写氛围不写时间顺序
- 不把所有运镜术语一次性塞进去
- 不忽略输入资产类型差异，把首帧图、角色图、场景图混成同一种图
