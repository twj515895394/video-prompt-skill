# Video Prompt Skill v2 迁移清单

## 1. 用途

记录旧结构、原始资料与 Reference Architecture v2 的迁移关系。

状态：

- `keep-temporary`：验证前继续保留；
- `migrated-await-validation`：有效内容已进入新真源，等待 Phase 7 验证；
- `split-await-validation`：旧内容按职责拆入多个新真源；
- `merge-await-validation`：多个旧文件合并成一个新真源；
- `delete-after-validation`：Phase 7 验证后删除。

当前不删除旧运行期文件。

## 2. 根文件与输出模板

| 旧路径 | 目标 | 当前状态 |
|---|---|---|
| `SKILL.md` | Phase 6 完整改写并切换 v2 路由 | keep-temporary |
| `assets/README.md` | 新输出合同索引 | keep-temporary |
| `assets/templates/single-unit-output-template.md` | 新单镜头输出模板 | keep-temporary |
| `assets/templates/multi-unit-output-template.md` | 新多镜头输出模板 | keep-temporary |
| `assets/templates/interactive-output-template.md` | 交互模式输出合同 | keep-temporary |

## 3. 模式层

| 旧路径 | 新位置 | 当前状态 |
|---|---|---|
| `references/mode-quick/quick-mode.md` | `SKILL.md` + 快速模式输出合同 | keep-temporary |
| `references/mode-interactive/interactive-mode.md` | `SKILL.md` + 交互模式输出合同 | keep-temporary |

Phase 6 后不再默认读取独立模式 Reference。

## 4. 输入层

| 旧路径 | 新真源 | 当前状态 |
|---|---|---|
| `input-text-only/text-expansion.md` | `inputs/text-input.md` | migrated-await-validation |
| `input-image-ref/image-reference-analysis.md` | `inputs/single-image-input.md` + `multi-image-input.md` | split-await-validation |

新增真源：`video-input.md`、`audio-input.md`、`mixed-multimodal-input.md`。

## 5. 任务层

| 旧路径 | 新真源 | 当前状态 |
|---|---|---|
| `task-text-to-video/playbook.md` | `tasks/text-to-video/playbook.md` | migrated-await-validation |
| `task-image-to-video/image-to-video-playbook.md` | `tasks/image-to-video/playbook.md` | migrated-await-validation |
| `output-single-unit/output-spec.md` | Phase 6 输出合同 | keep-temporary |
| `output-multi-unit/output-spec.md` | Phase 6 输出合同 | keep-temporary |

新增任务：多模态参考、视频复刻/转视频、局部编辑、延长、音频驱动、故事板/多镜头。

## 6. 控制层

| 旧路径 | 新真源 | 当前状态 |
|---|---|---|
| `timeline/timeline-assembly.md` | `controls/timeline-rhythm/control.md` | merge-await-validation |
| `timeline/lifestyle-beat-and-landing.md` | `controls/timeline-rhythm/control.md` | merge-await-validation |
| `continuity/continuity-guardrails.md` | `controls/continuity-consistency/control.md` | merge-await-validation |
| `continuity/human-motion-consistency.md` | continuity + subject-motion | split-await-validation |
| `style-control/anti-ai-video-realism.md` | `controls/realism-quality/control.md` | migrated-await-validation |
| `style-control/camera-failure-patterns-negative.md` | `controls/camera-direction/control.md` | merge-await-validation |

新增控制：空间调度、表演、音画同步、参考绑定和 Prompt 组装。

## 7. 旧附录

| 旧路径 | 新真源 | 当前状态 |
|---|---|---|
| `appendix/camera-movement-appendix.md` | camera-shot library + camera-direction control | split-await-validation |
| `appendix/action-beat-appendix.md` | action-motion library + subject-motion control | merge-await-validation |
| `appendix/visual-style-appendix.md` | genre-patterns + styles + lighting-color | split-await-validation |
| `appendix/index.md` | 无 | delete-after-validation |

v2 不保留 `appendix/` 正式分类。

## 8. Phase 4 资料库真源

| 新真源 | 主要来源 | 状态 |
|---|---|---|
| `libraries/camera-shot/library.md` | 运镜术语、机位景别、旧镜头附录 | merged-await-validation |
| `libraries/action-motion/library.md` | 打击帧、动作戏、旧动作附录 | merged-await-validation |
| `libraries/performance-expression/library.md` | 表情与微表情资料 | migrated-await-validation |
| `libraries/transition-effects/library.md` | 多模态任务、社区案例结构和通用影视抽象 | migrated-await-validation |
| `libraries/lighting-color/library.md` | 电影光影与色调资料 | migrated-await-validation |
| `libraries/audio-sound/library.md` | 音频任务、模型资料和通用声音抽象 | migrated-await-validation |
| `libraries/genre-patterns/library.md` | 视频风格、影视风格、短剧和漫剧资料 | merged-await-validation |

## 9. Phase 4 风格真源

| 新真源 | 主要来源 | 状态 |
|---|---|---|
| `styles/cinematic-live-action/style.md` | 电影感公式、视频风格、光影资料 | merged-await-validation |
| `styles/realistic-short-drama/style.md` | 写实电影短剧 | migrated-await-validation |
| `styles/anime-animation/style.md` | AI 漫剧、发型动态锚点和动画抽象 | migrated-await-validation |
| `styles/comic-motion-drama/style.md` | AI 漫剧 | migrated-await-validation |
| `styles/commercial-advertising/style.md` | 多模态案例结构和广告抽象 | migrated-await-validation |
| `styles/documentary-ugc/style.md` | 设备风格、真实感控制和纪录抽象 | migrated-await-validation |
| `styles/experimental-visual/style.md` | 转场特效与视觉规则抽象 | migrated-await-validation |

## 10. 用户资料处理结果

17 份用户上传资料已完成审计和正式沉淀：

- Prompt 结构进入 tasks 与 prompt-assembly；
- 运镜、动作、表演、光影进入 libraries 与 controls；
- 视频/影视风格拆成 genre patterns 和 styles；
- 写实短剧与 AI 漫剧进入专属 style；
- 发型资料只提炼视频动态和一致性，不复制完整生图选择器。

详情：`research/extraction-notes/phase4-library-style-extraction.md`。

## 11. 模型层

| 新真源 | 当前状态 |
|---|---|
| `models/generic.md` | 主体完成，待全链路验证 |
| `models/seedance-2.md` | 主体完成，待全链路验证 |
| `models/ltx-2-3.md` | 主体完成，待全链路验证 |

不建设其他模型平台。

## 12. Phase 6 待迁移

- 快速模式和交互模式规则回收进 `SKILL.md`；
- 统一快速、交互、单镜头、多镜头、多模态和模型适配输出合同；
- 新 `SKILL.md` 默认路由到 inputs/tasks/controls/libraries/styles/models；
- 旧路径只保留兼容说明，不再默认读取。

## 13. Phase 7 删除前检查

- [ ] 新真源存在且内容完整；
- [ ] 新索引已引用唯一真源；
- [ ] `SKILL.md` 不再引用旧路径；
- [ ] 核心测试场景通过；
- [ ] 仓库搜索不存在旧路径运行引用；
- [ ] 删除不会造成交叉链接失效；
- [ ] 原始资料仍可在 `research/incoming/` 追溯。
