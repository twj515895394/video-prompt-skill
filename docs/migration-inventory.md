# Video Prompt Skill v2 迁移清单

## 1. 用途

本文记录旧结构到 Reference Architecture v2 的迁移关系。

状态定义：

- `keep-temporary`：迁移完成前继续保留；
- `planned`：已确定目标但尚未实施；
- `migrated-await-validation`：新真源已完成，等待新 `SKILL.md` 和测试验证；
- `split-await-validation`：旧内容已拆入多个新真源，等待验证；
- `merge-await-validation`：多个旧文件已合并成新真源，等待验证；
- `delete-after-validation`：验证通过后删除。

当前阶段不删除任何旧运行期文件。

---

## 2. 根文件与输出模板

| 旧路径 | 当前作用 | 目标路径 | 迁移方式 | 当前状态 |
|---|---|---|---|---|
| `SKILL.md` | 旧任务、模式与加载入口 | `SKILL.md` | Phase 6 完整改写 | keep-temporary |
| `assets/README.md` | 模板目录说明 | `assets/README.md` | 更新为新输出合同索引 | planned |
| `assets/templates/single-unit-output-template.md` | 单片段输出 | `assets/templates/single-shot-video-template.md` | 迁移并补适配层槽位 | planned |
| `assets/templates/multi-unit-output-template.md` | 多片段输出 | `assets/templates/multi-shot-video-template.md` | 迁移并补跨镜连续性 | planned |
| `assets/templates/interactive-output-template.md` | 交互方向摘要 | `assets/templates/mode-interactive-output-contract.md` | 与交互模式规则合并 | planned |

---

## 3. 模式层

| 旧路径 | 有效内容 | 目标位置 | 迁移方式 | 当前状态 |
|---|---|---|---|---|
| `references/mode-quick/quick-mode.md` | 零打扰执行、自动补全、冲突裁决 | `SKILL.md` + `assets/templates/mode-quick-output-contract.md` | 拆分运行规则与输出合同 | keep-temporary |
| `references/mode-interactive/interactive-mode.md` | Grill Me、单问题追问、收口条件 | `SKILL.md` + `assets/templates/mode-interactive-output-contract.md` | 拆分运行规则与输出合同 | keep-temporary |

迁移后不再保留独立模式 Reference，避免每次执行额外加载一份模式正文。

---

## 4. 输入层

| 旧路径 | 有效内容 | 新真源 | 迁移方式 | 当前状态 |
|---|---|---|---|---|
| `references/input-text-only/text-expansion.md` | 文字扩展、首帧建立、运动补全 | `references/inputs/text-input.md` | 重写并增强 | migrated-await-validation |
| `references/input-image-ref/image-reference-analysis.md` | 图像类型、主辅图、参考锚点 | `references/inputs/single-image-input.md` + `multi-image-input.md` | 按单图/多图拆分 | split-await-validation |

新增输入真源已经完成：

- `references/inputs/video-input.md`
- `references/inputs/audio-input.md`
- `references/inputs/mixed-multimodal-input.md`

旧输入文件在 Phase 7 前继续保留。

---

## 5. 任务层

| 旧路径 | 有效内容 | 新真源 | 迁移方式 | 当前状态 |
|---|---|---|---|---|
| `references/task-text-to-video/playbook.md` | 文生视频主流程 | `references/tasks/text-to-video/playbook.md` | 重写并补输入、控制和适配路由 | migrated-await-validation |
| `references/task-image-to-video/image-to-video-playbook.md` | 图生视频主流程 | `references/tasks/image-to-video/playbook.md` | 重写并区分单图、多图与运动延续 | migrated-await-validation |
| `references/output-single-unit/output-spec.md` | 单片段交付结构 | `assets/templates/single-shot-video-template.md` | 与模板合并 | planned |
| `references/output-multi-unit/output-spec.md` | 多片段交付结构 | `assets/templates/multi-shot-video-template.md` | 与模板合并 | planned |

新增任务真源已经完成：

- `references/tasks/multimodal-reference-video/playbook.md`
- `references/tasks/video-reference-and-video-to-video/playbook.md`
- `references/tasks/video-editing/playbook.md`
- `references/tasks/video-extension/playbook.md`
- `references/tasks/audio-driven-and-beat-sync/playbook.md`
- `references/tasks/storyboard-and-multi-shot-video/playbook.md`

---

## 6. 时间轴、运动、连续性与质量控制

旧文件没有按原目录逐份复制，而是按控制职责合并重构。

| 旧路径 | 有效内容 | 新真源 | 迁移方式 | 当前状态 |
|---|---|---|---|---|
| `references/timeline/timeline-assembly.md` | 绝对时间、主体状态、镜头状态、节拍 | `references/controls/timeline-rhythm/control.md` | 与自然收尾合并重构 | merge-await-validation |
| `references/timeline/lifestyle-beat-and-landing.md` | 生活化节拍与自然收尾 | `references/controls/timeline-rhythm/control.md` | 与时间轴合并重构 | merge-await-validation |
| `references/continuity/continuity-guardrails.md` | 人物、场景、道具和镜头连续性 | `references/controls/continuity-consistency/control.md` | 与人物运动连续性合并 | merge-await-validation |
| `references/continuity/human-motion-consistency.md` | 身份、体态、重心和动作阶段 | `references/controls/continuity-consistency/control.md` + `subject-motion/control.md` | 按状态与物理运动拆分 | split-await-validation |
| `references/style-control/anti-ai-video-realism.md` | 去漂浮感、设备感、自然动作 | `references/controls/realism-quality/control.md` | 扩展为完整真实感控制 | migrated-await-validation |
| `references/style-control/camera-failure-patterns-negative.md` | 运镜失败与负向限制 | `references/controls/camera-direction/control.md` | 合入正向镜头决策 | migrated-await-validation |

Phase 3 新增并完成的控制真源：

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

---

## 7. 旧附录

| 旧路径 | 有效内容 | 目标路径 | 迁移方式 | 当前状态 |
|---|---|---|---|---|
| `references/appendix/camera-movement-appendix.md` | 运镜选择和基础术语 | `libraries/camera-shot/` + `controls/camera-direction/control.md` | 方法已迁移，术语待 Phase 4 | split-await-validation |
| `references/appendix/action-beat-appendix.md` | 蓄力、接触、反馈、恢复 | `controls/subject-motion/control.md` + `libraries/action-motion/` | 控制方法已迁移，详细库待 Phase 4 | split-await-validation |
| `references/appendix/visual-style-appendix.md` | 设备层、作者气质、光影色调 | `styles/` + `libraries/genre-patterns/` | Phase 4 拆分 | planned |
| `references/appendix/index.md` | 旧附录导航 | 无 | 新索引验证后删除 | delete-after-validation |

v2 不再保留独立 `appendix/`。高价值知识必须明确归入 controls、libraries 或 styles。

---

## 8. 总索引

| 旧路径 | 当前作用 | 新状态 | 当前状态 |
|---|---|---|---|
| `references/index.md` | 总路由 | 已重写为 v2 总索引，并保留迁移期兼容区 | migrated-await-validation |
| `references/controls/index.md` | 新控制分类路由 | 已路由到十份 Phase 3 叶子真源 | migrated-await-validation |

---

## 9. 用户资料候选沉淀映射

| 原始资料 | 主要候选真源 | 当前状态 |
|---|---|---|
| `基础Prompt结构.md` | `controls/prompt-assembly/control.md` | 已提炼通用组装规则 |
| `文生视频Prompt结构.md` | `tasks/text-to-video/` | 已提炼 |
| `图生视频Prompt结构.md`、`图生视频.md` | `tasks/image-to-video/` + `inputs/*image*` | 已提炼 |
| `故事版分镜到视频流程.md` | `tasks/storyboard-and-multi-shot-video/` | 已提炼 |
| `导演级运镜术语选择器.md` | `libraries/camera-shot/` | Phase 4 |
| `视角机位与景别选择器.md` | `libraries/camera-shot/` | Phase 4 |
| `打击帧与动作戏结构.md` | `controls/subject-motion/` + `libraries/action-motion/` | 控制规则已提炼，资料库待建 |
| `表情与微表情选择器.md` | `controls/performance-expression/` + `libraries/performance-expression/` | 控制规则已提炼，资料库待建 |
| `电影光影与色调选择器.md` | `libraries/lighting-color/` | Phase 4 |
| `电影感Prompt拆解公式.md` | `styles/cinematic-live-action/` + `controls/prompt-assembly/` | 组装规则已提炼，风格页待建 |
| `AI视频风格选择器.md` | `libraries/genre-patterns/` + `styles/` | Phase 4 |
| `影视风格选择器.md` | `libraries/genre-patterns/` | Phase 4 |
| `写实电影短剧.md` | `styles/realistic-short-drama/` | Phase 4 |
| `AI漫剧.md` | `styles/comic-motion-drama/` | Phase 4 |
| `图像风格提取流程.md` | `inputs/single-image-input.md` + `controls/reference-binding/` | 已提炼 |
| `角色发型选择器.md` | 只提炼动态一致性部分 | 已进入连续性控制，不完整复制资料 |

---

## 10. 外部资料候选沉淀映射

| 来源 | 主要用途 | 候选真源 |
|---|---|---|
| `dexhunter/seedance2-skill` | 模型能力、素材引用和任务模式 | `models/seedance-2.md` + 相关任务页 |
| `awesome-seedance-2-prompts` | 高质量案例结构、音画与分时段模式 | `research/extraction-notes/`，再按主题合并 |
| LTX-2.3 官方 Prompt Guide | Prompt 原则、I2V 运动描述、表演与音频 | `models/ltx-2-3.md` + 通用控制页 |

社区 Prompt 不原样进入运行期 Reference，只抽象结构、节拍、变量和失败边界。

---

## 11. 清理检查

旧结构删除前必须逐项检查：

- [ ] 新真源存在且内容完整；
- [ ] 新索引已引用新真源；
- [ ] `SKILL.md` 不再引用旧路径；
- [ ] 测试场景通过；
- [ ] 仓库搜索不存在旧路径残留；
- [ ] 删除不会造成交叉链接失效。

Phase 3 当前只满足前两项的控制层部分，仍不得删除旧文件。