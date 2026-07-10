# Video Prompt Skill v2 实施进度

最后更新：`2026-07-10`

实施基线：`docs/implementation-plan-v2.md`

工作分支：`refactor/reference-architecture-v2`

## 总体状态

| 阶段 | 状态 | 完成度 | 说明 |
|---|---|---:|---|
| Phase 0 范围冻结与迁移盘点 | 已完成 | 100% | 范围、模型、研究区和迁移台账已落地 |
| Phase 1 新架构骨架与总路由 | 已完成 | 100% | 八类索引、总索引和三份模型适配页已完成 |
| Phase 2 输入层与任务层 | 已完成 | 100% | 六类输入 Reference、八类任务 Playbook 已完成 |
| Phase 3 核心控制层 | 已完成 | 100% | 十类核心控制真源和精确路由已完成 |
| Phase 4 资料库与风格层 | 已完成 | 100% | 七类详细资料库、七种风格实现和来源提炼记录已完成 |
| Phase 5 模型适配层 | 主体完成 | 85% | Generic、Seedance、LTX 正文已完成，等待全链路验证微调 |
| Phase 6 输出合同与 SKILL.md 切换 | 未开始 | 0% | 下一执行阶段 |
| Phase 7 验证与旧结构清理 | 未开始 | 0% | 最终阶段 |

## Phase 0 完成项

- 创建重构分支。
- 建立架构决策、实施计划和迁移台账。
- 建立 `research/` 原始资料区。
- 导入 17 份用户 Markdown 原始资料。
- 锁定 Generic + Seedance 2.0 + LTX-2.3。
- 明确不建设其他模型空适配器。

## Phase 1 完成项

- 重写 `references/index.md` 为 v2 总索引。
- 建立 inputs、tasks、controls、libraries、styles、models、diagnostics 分类索引。
- 完成 `generic.md`、`seedance-2.md`、`ltx-2-3.md`。
- 保留迁移期旧路径兼容区。

## Phase 2 完成项

### 输入层

- `references/inputs/text-input.md`
- `references/inputs/single-image-input.md`
- `references/inputs/multi-image-input.md`
- `references/inputs/video-input.md`
- `references/inputs/audio-input.md`
- `references/inputs/mixed-multimodal-input.md`

### 任务层

- `tasks/text-to-video/playbook.md`
- `tasks/image-to-video/playbook.md`
- `tasks/multimodal-reference-video/playbook.md`
- `tasks/video-reference-and-video-to-video/playbook.md`
- `tasks/video-editing/playbook.md`
- `tasks/video-extension/playbook.md`
- `tasks/audio-driven-and-beat-sync/playbook.md`
- `tasks/storyboard-and-multi-shot-video/playbook.md`

## Phase 3 完成项

### 核心控制真源

- `controls/timeline-rhythm/control.md`
- `controls/subject-motion/control.md`
- `controls/camera-direction/control.md`
- `controls/spatial-blocking/control.md`
- `controls/continuity-consistency/control.md`
- `controls/performance-expression/control.md`
- `controls/audio-visual-sync/control.md`
- `controls/reference-binding/control.md`
- `controls/prompt-assembly/control.md`
- `controls/realism-quality/control.md`

### 结构结果

- 时间轴与自然收尾合并为单一节拍真源。
- 状态连续性与运动物理边界明确。
- 运镜负向限制合入正向镜头决策。
- 去 AI 感升级为设备、运动、光影、材质、表演和声音控制。
- 通用控制层不包含模型专属语法。

## Phase 4 完成项

### 资料库真源

- `references/libraries/camera-shot/library.md`
- `references/libraries/action-motion/library.md`
- `references/libraries/performance-expression/library.md`
- `references/libraries/transition-effects/library.md`
- `references/libraries/lighting-color/library.md`
- `references/libraries/audio-sound/library.md`
- `references/libraries/genre-patterns/library.md`

覆盖内容：

- 景别、机位、焦段、设备和运镜组合；
- 日常、打斗、体育、动物、物体和环境运动；
- 表情、微表情、对白和关系表演；
- 剪辑、遮挡、穿越、材质变化和视觉特效；
- 九类光影、十八种色调、时间天气和动态光；
- 对白、环境音、拟音、BGM、节拍和声音空间；
- 短剧、漫剧、动作、悬疑、广告、纪录、科普和实验题材模板。

### 风格真源

- `styles/cinematic-live-action/style.md`
- `styles/realistic-short-drama/style.md`
- `styles/anime-animation/style.md`
- `styles/comic-motion-drama/style.md`
- `styles/commercial-advertising/style.md`
- `styles/documentary-ugc/style.md`
- `styles/experimental-visual/style.md`

风格边界：

- 电影化真人：摄影、空间、自然表演与声音共同成立；
- 写实短剧：信息与人物关系快速可读；
- 动画：角色渲染、关键姿态和分层运动；
- 漫剧：画格、有限动画、表情和镜间承接；
- 广告：产品外观、卖点证据、材质和品牌落点；
- 纪录/UGC：真实设备来源和自然不完美；
- 实验影像：单一视觉规则和分阶段升级。

### 资料治理

- 建立 `research/extraction-notes/phase4-library-style-extraction.md`。
- 17 份用户资料均已审计并映射到正式真源。
- 完整发型选择器未重复迁入，只保留视频动态和一致性部分。
- 社区长 Prompt 未原样进入运行期 Reference。
- `libraries/index.md` 和 `styles/index.md` 已路由到唯一叶子文件。

## 当前架构安全状态

- 旧 `SKILL.md` 尚未切换。
- 旧 Reference 尚未删除。
- 新目录与旧目录仍并行存在。
- 新输入、任务、控制、资料库、风格和模型层已经形成完整 v2 运行知识链。
- Phase 6 切换前，现有 Skill 仍走兼容链路。

## 下一执行阶段：Phase 6

Phase 5 主体已提前完成，因此下一步直接进入 Phase 6：

1. 设计快速模式和交互模式输出合同；
2. 设计单镜头、多镜头、多模态和模型适配模板；
3. 重写 `SKILL.md`，切换到 v2 路由；
4. 保留旧结构兼容但停止默认读取；
5. 建立 Phase 7 使用的测试场景与验证清单。

Phase 6 完成前不删除旧文件。
