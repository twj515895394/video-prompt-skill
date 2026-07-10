# Video Prompt References Index v2

## 1. 路由目标

用最少量 Reference 支撑当前任务，避免把视频 Skill 变成大而散的资料堆。

当前正式运行链路：

```text
输入理解
→ 任务 Playbook
→ 按需控制
→ 按需资料库与风格
→ 模型适配
→ 输出合同
→ 失败时诊断
```

索引只负责导航，不复制叶子正文。

## 2. 默认加载预算

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
- `0-1` 份多模态参考模板；
- 失败诊断时 `0-1` 份 diagnostic。

分类索引只用于导航，不计入业务 Reference 数量。

## 3. 信息优先级

冲突时按以下顺序执行：

```text
用户当前明确要求
→ 必须保留 / 必须修改 / 必须禁止
→ 当前任务 Playbook
→ 当前输入 Reference 与素材职责
→ 已加载 controls
→ 已加载 libraries 与 style
→ model adapter 的能力边界和表达方式
→ 自动补全
```

模型适配页可以限制表达方式和能力边界，但不能擅自改变用户剧情、人物关系和核心动作。

## 4. 输入路由

读取：`inputs/index.md`

继续路由到唯一主输入路线：

- 纯文字：`inputs/text-input.md`；
- 单张图片：`inputs/single-image-input.md`；
- 多张图片：`inputs/multi-image-input.md`；
- 一个或多个视频：`inputs/video-input.md`；
- 音频：`inputs/audio-input.md`；
- 图片 / 视频 / 音频混合输入：`inputs/mixed-multimodal-input.md`。

混合输入只读取 `mixed-multimodal-input.md`，不同时加载多份单模态输入页。

## 5. 任务路由

读取：`tasks/index.md`

继续路由到唯一主任务 Playbook：

- 文生视频：`tasks/text-to-video/playbook.md`；
- 图生视频：`tasks/image-to-video/playbook.md`；
- 多模态参考视频：`tasks/multimodal-reference-video/playbook.md`；
- 视频参考复刻 / 视频转视频：`tasks/video-reference-and-video-to-video/playbook.md`；
- 视频局部编辑：`tasks/video-editing/playbook.md`；
- 视频向前 / 向后延长：`tasks/video-extension/playbook.md`；
- 音频驱动与音乐卡点：`tasks/audio-driven-and-beat-sync/playbook.md`；
- 故事板 / 多镜头 / 多片段到视频：`tasks/storyboard-and-multi-shot-video/playbook.md`。

题材差异不新增任务 Playbook，进入 `styles/` 或 `libraries/genre-patterns/`。

## 6. 控制路由

读取：`controls/index.md`

按当前最大缺口加载 `0-3` 份：

- `controls/timeline-rhythm/control.md`；
- `controls/subject-motion/control.md`；
- `controls/camera-direction/control.md`；
- `controls/spatial-blocking/control.md`；
- `controls/continuity-consistency/control.md`；
- `controls/performance-expression/control.md`；
- `controls/audio-visual-sync/control.md`；
- `controls/reference-binding/control.md`；
- `controls/prompt-assembly/control.md`；
- `controls/realism-quality/control.md`。

任务 Playbook 已经能解决的问题，不重复读取控制页。

## 7. 资料库路由

读取：`libraries/index.md`

按需加载 `0-2` 份：

- `libraries/camera-shot/library.md`；
- `libraries/action-motion/library.md`；
- `libraries/performance-expression/library.md`；
- `libraries/transition-effects/library.md`；
- `libraries/lighting-color/library.md`；
- `libraries/audio-sound/library.md`；
- `libraries/genre-patterns/library.md`。

资料库回答“有哪些选择”，不代替控制规则。

## 8. 风格路由

读取：`styles/index.md`

最多加载一份主 style Reference：

- `styles/cinematic-live-action/style.md`；
- `styles/realistic-short-drama/style.md`；
- `styles/anime-animation/style.md`；
- `styles/comic-motion-drama/style.md`；
- `styles/commercial-advertising/style.md`；
- `styles/documentary-ugc/style.md`；
- `styles/experimental-visual/style.md`。

风格必须转成镜头、表演、光影、材质、节奏和声音，不用风格名替代执行内容。

## 9. 模型适配路由

读取：`models/index.md`

正式模型范围：

- 用户未指定模型：`models/generic.md`；
- 用户明确使用 Seedance 2.0：`models/seedance-2.md`；
- 用户明确使用 LTX-2.3：`models/ltx-2-3.md`。

不创建或加载其他模型适配页。

模型页只转换通用导演方案，不重新设计任务内容。

## 10. 输出合同路由

模式合同二选一：

- 默认快速模式：`../assets/templates/mode-quick-output-contract.md`；
- 用户明确共创：`../assets/templates/mode-interactive-output-contract.md`。

主交付模板：

- 单镜头：`../assets/templates/single-shot-video-template.md`；
- 多镜头 / 多片段 / 故事板：`../assets/templates/multi-shot-video-template.md`。

按需补读：

- 多模态职责：`../assets/templates/multimodal-reference-template.md`；
- 模型转换：`../assets/templates/model-adapted-output-template.md`。

默认输出规则：

- 简单任务只输出一份可直接复制 Prompt；
- 多镜头输出必要的全局固定项和 Prompt Pack；
- 多模态只保留执行必要的职责说明；
- 不默认输出备选版本、自动补全项和方向摘要。

## 11. 失败诊断

读取：`diagnostics/index.md`

只有以下情况进入：

- 用户反馈生成效果不好；
- 多个维度同时失效；
- 参考素材职责冲突；
- Prompt 过载或要求互相矛盾；
- 无法从单一任务页或控制页定位根因。

正常生成不提前加载诊断层。

## 12. 运行规则

- 同一轮只读取一份主 input 和一份主 task；
- 同一叶子文件被多个入口命中时只读取一次；
- 主体运动、镜头运动、环境变化和声音事件分别判断；
- 多模态素材必须分配职责，禁止平均融合；
- 一段视频必须有开始、推进和落点；
- 全局固定项只写一次，时间轴只写变化；
- 负向限制只针对当前最危险的失败模式；
- 不一次性读取整个目录；
- 不把研究区原始资料作为运行期 Reference。

## 13. 旧结构状态

Phase 6 已将 `SKILL.md` 切换到 v2。旧模式、旧输入、旧任务、旧时间轴、旧连续性、旧附录和旧输出模板不再参与默认运行。

这些文件在 Phase 7 测试和断链检查完成前暂时保留，只用于回滚和迁移核对。

迁移状态见：`../docs/migration-inventory.md`。