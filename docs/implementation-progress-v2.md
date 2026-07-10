# Video Prompt Skill v2 实施进度

最后更新：`2026-07-10`

实施基线：`docs/implementation-plan-v2.md`

工作分支：`refactor/reference-architecture-v2`

---

## 总体状态

| 阶段 | 状态 | 完成度 | 说明 |
|---|---|---:|---|
| Phase 0 范围冻结与迁移盘点 | 已完成 | 100% | 范围、模型、研究区和迁移台账已落地 |
| Phase 1 新架构骨架与总路由 | 已完成 | 100% | 八类索引、总索引和三份模型适配页已完成 |
| Phase 2 输入层与任务层 | 已完成 | 100% | 六类输入 Reference、八类任务 Playbook 已完成 |
| Phase 3 核心控制层 | 未开始 | 0% | 下一执行阶段 |
| Phase 4 资料库与风格层 | 未开始 | 0% | 依赖资料提炼和 Phase 3 边界 |
| Phase 5 模型适配层 | 已提前完成主体 | 85% | Generic、Seedance、LTX 正文已完成，后续随任务验证微调 |
| Phase 6 输出合同与 SKILL.md 切换 | 未开始 | 0% | 依赖控制层和资料层 |
| Phase 7 验证与旧结构清理 | 未开始 | 0% | 最终阶段 |

---

## Phase 0 完成项

- 创建分支 `refactor/reference-architecture-v2`。
- 建立 `docs/reference-architecture-v2.md`。
- 建立 `docs/implementation-plan-v2.md`。
- 建立 `docs/migration-inventory.md`。
- 建立 `research/` 原始资料区。
- 导入用户提供的 17 份 Markdown 原始资料。
- 建立来源清单和候选沉淀映射。
- 锁定正式模型范围：Generic + Seedance 2.0 + LTX-2.3。
- 明确不建设其他模型空适配器。

---

## Phase 1 完成项

### 总路由

- 重写 `references/index.md` 为 v2 总索引。
- 保留迁移期旧路径兼容区，当前 `SKILL.md` 不会提前断链。

### 分类索引

- `references/inputs/index.md`
- `references/tasks/index.md`
- `references/controls/index.md`
- `references/libraries/index.md`
- `references/styles/index.md`
- `references/models/index.md`
- `references/diagnostics/index.md`

### 模型适配

- `references/models/generic.md`
- `references/models/seedance-2.md`
- `references/models/ltx-2-3.md`

模型适配层已从“骨架”提升为可用正文：

- Generic：模型无关导演输出协议；
- Seedance：多模态职责绑定、视频参考、编辑、延长、音频与卡点；
- LTX：详细自然语言、表演节拍、I2V 运动描述、对白和音频。

---

## Phase 2 完成项

### 输入层

- `references/inputs/text-input.md`
- `references/inputs/single-image-input.md`
- `references/inputs/multi-image-input.md`
- `references/inputs/video-input.md`
- `references/inputs/audio-input.md`
- `references/inputs/mixed-multimodal-input.md`

输入层已覆盖：

- 首帧、尾帧、角色、场景和关键帧；
- 主图、辅助图和禁止平均融合；
- 视频动作、运镜、节奏、特效和声音职责；
- 音频对白、口型、BGM、节拍和环境音；
- 混合多模态主真源与冲突裁决。

### 任务层

- `references/tasks/text-to-video/playbook.md`
- `references/tasks/image-to-video/playbook.md`
- `references/tasks/multimodal-reference-video/playbook.md`
- `references/tasks/video-reference-and-video-to-video/playbook.md`
- `references/tasks/video-editing/playbook.md`
- `references/tasks/video-extension/playbook.md`
- `references/tasks/audio-driven-and-beat-sync/playbook.md`
- `references/tasks/storyboard-and-multi-shot-video/playbook.md`

任务边界已明确：

- 从零生成与从图片起动分离；
- 多模态参考独立管理素材职责；
- 视频参考复刻与局部编辑分离；
- 视频延长独立管理接点连续性；
- 音频驱动独立管理声音时间骨架；
- 故事板任务管理镜间和跨包承接。

---

## 当前架构安全状态

- 旧 `SKILL.md` 尚未切换。
- 旧 Reference 尚未删除。
- 新 `references/index.md` 包含兼容路由。
- 新目录与旧目录并行存在。
- 当前改造不会要求主分支立即使用未验证的新链路。

---

## 下一执行阶段：Phase 3

建议按以下顺序实施核心控制页：

1. `controls/timeline-rhythm/`
   - 时间轴组装
   - 自然节拍和落点
2. `controls/subject-motion/`
   - 主体运动与镜头运动分离
   - 动作阶段、重心、惯性和反馈
3. `controls/camera-direction/`
   - 镜头主任务
   - 运镜强度和失败约束
4. `controls/continuity-consistency/`
   - 人物、动作、场景和道具连续性
5. `controls/reference-binding/`
   - 多模态主真源和冲突处理
6. `controls/prompt-assembly/`
   - 信息优先级、压缩和最终组装
7. 继续补齐：
   - spatial-blocking
   - performance-expression
   - audio-visual-sync
   - realism-quality

Phase 3 完成前不改写 `SKILL.md`，不删除旧 Reference。
