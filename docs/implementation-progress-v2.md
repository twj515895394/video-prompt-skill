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
| Phase 3 核心控制层 | 已完成 | 100% | 十类核心控制真源和精确路由已完成 |
| Phase 4 资料库与风格层 | 未开始 | 0% | 下一执行阶段 |
| Phase 5 模型适配层 | 已提前完成主体 | 85% | Generic、Seedance、LTX 正文已完成，后续随验证微调 |
| Phase 6 输出合同与 SKILL.md 切换 | 未开始 | 0% | 依赖资料层和测试用例 |
| Phase 7 验证与旧结构清理 | 未开始 | 0% | 最终阶段 |

---

## Phase 0 完成项

- 创建分支 `refactor/reference-architecture-v2`。
- 建立架构决策、实施计划和迁移台账。
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

模型适配层已从骨架提升为可用正文，但不复制通用导演知识。

---

## Phase 2 完成项

### 输入层

- `references/inputs/text-input.md`
- `references/inputs/single-image-input.md`
- `references/inputs/multi-image-input.md`
- `references/inputs/video-input.md`
- `references/inputs/audio-input.md`
- `references/inputs/mixed-multimodal-input.md`

输入层已覆盖图片、视频、音频和混合多模态职责，以及主真源与冲突裁决。

### 任务层

- `references/tasks/text-to-video/playbook.md`
- `references/tasks/image-to-video/playbook.md`
- `references/tasks/multimodal-reference-video/playbook.md`
- `references/tasks/video-reference-and-video-to-video/playbook.md`
- `references/tasks/video-editing/playbook.md`
- `references/tasks/video-extension/playbook.md`
- `references/tasks/audio-driven-and-beat-sync/playbook.md`
- `references/tasks/storyboard-and-multi-shot-video/playbook.md`

任务边界已经按执行差异拆分，不按题材重复建设。

---

## Phase 3 完成项

### 核心控制真源

- `references/controls/timeline-rhythm/control.md`
- `references/controls/subject-motion/control.md`
- `references/controls/camera-direction/control.md`
- `references/controls/spatial-blocking/control.md`
- `references/controls/continuity-consistency/control.md`
- `references/controls/performance-expression/control.md`
- `references/controls/audio-visual-sync/control.md`
- `references/controls/reference-binding/control.md`
- `references/controls/prompt-assembly/control.md`
- `references/controls/realism-quality/control.md`

### 已完成的结构重组

- 将旧时间轴和生活化自然收尾合并为 `timeline-rhythm` 单一真源。
- 将基础连续性和人物运动连续性按“状态稳定”与“运动物理”拆分到连续性、主体运动两个控制页。
- 将旧运镜负向限制合入完整的正向镜头决策，不再单独维护负面词清单。
- 将旧去 AI 感规则扩展为设备来源、运动、光影、材质、表演和声音六层真实感控制。
- 新增空间调度、表演、音画同步、多模态绑定和 Prompt 组装等旧架构缺失的一等控制模块。
- 清除通用控制层中的模型专属引用语法，模型差异只留给 `references/models/`。
- 更新 `references/controls/index.md`，每个类别均可路由到唯一叶子文件。

### Phase 3 验收结果

- 每个控制页回答“如何判断与控制”，不是术语列表。
- 同一规则有明确真源，旧文件只在迁移期兼容保留。
- 通用控制页不承担模型专属参数和引用语法。
- 常用任务可在最多三份控制页内形成完整控制组合。
- 未删除任何旧运行期文件，当前 `SKILL.md` 仍可继续工作。

---

## 当前架构安全状态

- 旧 `SKILL.md` 尚未切换。
- 旧 Reference 尚未删除。
- 新 `references/index.md` 包含兼容路由。
- 新目录与旧目录并行存在。
- 新控制层已完成，但只有 Phase 6 切换入口后才成为默认运行链路。

---

## 下一执行阶段：Phase 4

Phase 4 将建设“可选详细知识”与“风格实现”，不再扩写控制方法。

建议顺序：

1. `libraries/camera-shot/`
   - 导演级运镜术语；
   - 景别、机位、焦段与镜头类型。
2. `libraries/action-motion/`
   - 打击帧；
   - 动作、追逐、体育和物理反馈方案。
3. `libraries/performance-expression/`
   - 表情、微表情、眼神、呼吸和对白表演选项。
4. `libraries/lighting-color/`
   - 光影类型、电影色调与主体分离。
5. `libraries/audio-sound/` 与 `transition-effects/`
   - 声音设计、音乐卡点、转场和视觉特效。
6. `libraries/genre-patterns/`
   - 写实短剧、AI 漫剧、动作、广告等题材级组合。
7. `styles/`
   - 电影写实、写实短剧、动画、漫剧、广告、UGC 和实验视觉的执行方式。

Phase 4 仍不改写 `SKILL.md`，不删除旧 Reference。