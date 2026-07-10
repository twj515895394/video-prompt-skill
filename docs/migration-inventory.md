# Video Prompt Skill v2 迁移清单

## 1. 用途

记录旧结构、原始资料与 Reference Architecture v2 的迁移关系。

状态：

- `active-v2`：已经成为 v2 正式运行入口或真源；
- `migrated-await-validation`：有效内容已进入新真源，等待 Phase 7 验证；
- `split-await-validation`：旧内容按职责拆入多个新真源；
- `merge-await-validation`：多个旧文件合并成一个新真源；
- `legacy-delete-after-validation`：已经停止默认读取，Phase 7 验证后删除。

Phase 6 不删除旧文件；Phase 7 完成回归、断链和重复真源检查后再清理。

## 2. 根文件与输出模板

| 路径 | 新状态 / 目标 | 当前状态 |
|---|---|---|
| `SKILL.md` | 已完整重写并切换 v2 路由 | active-v2 |
| `assets/README.md` | 已切换到新输出合同索引 | active-v2 |
| `assets/templates/mode-quick-output-contract.md` | 快速模式正式输出合同 | active-v2 |
| `assets/templates/mode-interactive-output-contract.md` | 交互模式正式输出合同 | active-v2 |
| `assets/templates/single-shot-video-template.md` | 单镜头正式模板 | active-v2 |
| `assets/templates/multi-shot-video-template.md` | 多镜头 / 多片段正式模板 | active-v2 |
| `assets/templates/multimodal-reference-template.md` | 多模态职责正式模板 | active-v2 |
| `assets/templates/model-adapted-output-template.md` | Generic / Seedance / LTX 转换模板 | active-v2 |
| `assets/templates/single-unit-output-template.md` | 已由单镜头模板替代 | legacy-delete-after-validation |
| `assets/templates/multi-unit-output-template.md` | 已由多镜头模板替代 | legacy-delete-after-validation |
| `assets/templates/interactive-output-template.md` | 已由交互模式输出合同替代 | legacy-delete-after-validation |

## 3. 模式层

| 旧路径 | 新位置 | 当前状态 |
|---|---|---|
| `references/mode-quick/quick-mode.md` | `SKILL.md` + `mode-quick-output-contract.md` | legacy-delete-after-validation |
| `references/mode-interactive/interactive-mode.md` | `SKILL.md` + `mode-interactive-output-contract.md` | legacy-delete-after-validation |

独立模式 Reference 已停止默认读取。

## 4. 输入层

| 旧路径 | 新真源 | 当前状态 |
|---|---|---|
| `references/input-text-only/text-expansion.md` | `references/inputs/text-input.md` | legacy-delete-after-validation |
| `references/input-image-ref/image-reference-analysis.md` | `references/inputs/single-image-input.md` + `multi-image-input.md` | legacy-delete-after-validation |

新增正式真源：

- `references/inputs/video-input.md`；
- `references/inputs/audio-input.md`；
- `references/inputs/mixed-multimodal-input.md`。

## 5. 任务层

| 旧路径 | 新真源 | 当前状态 |
|---|---|---|
| `references/task-text-to-video/playbook.md` | `references/tasks/text-to-video/playbook.md` | legacy-delete-after-validation |
| `references/task-image-to-video/image-to-video-playbook.md` | `references/tasks/image-to-video/playbook.md` | legacy-delete-after-validation |
| `references/output-single-unit/output-spec.md` | `single-shot-video-template.md` + 快速模式合同 | legacy-delete-after-validation |
| `references/output-multi-unit/output-spec.md` | `multi-shot-video-template.md` + 快速模式合同 | legacy-delete-after-validation |

新增正式任务：多模态参考、视频复刻 / 转视频、视频局部编辑、视频延长、音频驱动和故事板 / 多镜头。

## 6. 控制层

| 旧路径 | 新真源 | 当前状态 |
|---|---|---|
| `references/timeline/timeline-assembly.md` | `controls/timeline-rhythm/control.md` | legacy-delete-after-validation |
| `references/timeline/lifestyle-beat-and-landing.md` | `controls/timeline-rhythm/control.md` | legacy-delete-after-validation |
| `references/continuity/continuity-guardrails.md` | `controls/continuity-consistency/control.md` | legacy-delete-after-validation |
| `references/continuity/human-motion-consistency.md` | continuity + subject-motion | legacy-delete-after-validation |
| `references/style-control/anti-ai-video-realism.md` | `controls/realism-quality/control.md` | legacy-delete-after-validation |
| `references/style-control/camera-failure-patterns-negative.md` | `controls/camera-direction/control.md` | legacy-delete-after-validation |

新增正式控制：空间调度、表演、音画同步、参考绑定和 Prompt 组装。

## 7. 旧附录

| 旧路径 | 新真源 | 当前状态 |
|---|---|---|
| `references/appendix/camera-movement-appendix.md` | camera-shot library + camera-direction control | legacy-delete-after-validation |
| `references/appendix/action-beat-appendix.md` | action-motion library + subject-motion control | legacy-delete-after-validation |
| `references/appendix/visual-style-appendix.md` | genre-patterns + styles + lighting-color | legacy-delete-after-validation |
| `references/appendix/index.md` | 无正式替代分类 | legacy-delete-after-validation |

v2 不保留 `appendix/` 正式分类。

## 8. 资料库与风格真源

### 资料库

- `references/libraries/camera-shot/library.md`；
- `references/libraries/action-motion/library.md`；
- `references/libraries/performance-expression/library.md`；
- `references/libraries/transition-effects/library.md`；
- `references/libraries/lighting-color/library.md`；
- `references/libraries/audio-sound/library.md`；
- `references/libraries/genre-patterns/library.md`。

状态：`active-v2`。

### 风格

- `references/styles/cinematic-live-action/style.md`；
- `references/styles/realistic-short-drama/style.md`；
- `references/styles/anime-animation/style.md`；
- `references/styles/comic-motion-drama/style.md`；
- `references/styles/commercial-advertising/style.md`；
- `references/styles/documentary-ugc/style.md`；
- `references/styles/experimental-visual/style.md`。

状态：`active-v2`。

## 9. 用户资料处理结果

17 份用户上传资料已完成审计和正式沉淀：

- Prompt 结构进入 tasks 与 prompt-assembly；
- 运镜、动作、表演、光影进入 libraries 与 controls；
- 视频 / 影视风格拆成 genre patterns 和 styles；
- 写实短剧与 AI 漫剧进入专属 style；
- 发型资料只提炼视频动态和一致性，不复制完整生图选择器。

详情：`research/extraction-notes/phase4-library-style-extraction.md`。

## 10. 模型层

| 真源 | 当前状态 |
|---|---|
| `references/models/generic.md` | active-v2 |
| `references/models/seedance-2.md` | active-v2 |
| `references/models/ltx-2-3.md` | active-v2 |
| `assets/templates/model-adapted-output-template.md` | active-v2 |

不建设其他模型平台。

## 11. 总路由状态

- `SKILL.md` 已不再引用旧模式、旧输入、旧任务、旧时间轴、旧连续性、旧附录和旧输出结构；
- `references/index.md` 已正式路由到 v2 叶子；
- `assets/README.md` 已正式路由到六份新输出合同；
- 旧文件只保留用于 Phase 7 回归、断链检查和回滚。

## 12. Phase 7 删除前检查

- [x] 新真源存在且内容完整；
- [x] 新索引已引用唯一真源；
- [x] `SKILL.md` 已切换并不再引用旧运行路径；
- [ ] 十类核心测试场景通过；
- [ ] Generic、Seedance、LTX 输出对照验证通过；
- [ ] 仓库搜索不存在旧路径的运行期引用；
- [ ] 删除不会造成交叉链接失效；
- [ ] 删除后不存在重复真源和空占位目录；
- [x] 原始资料仍可在 `research/incoming/` 追溯。