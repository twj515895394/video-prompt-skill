# Video Prompt Skill v2 迁移清单

## 1. 用途

本文记录旧结构到 Reference Architecture v2 的迁移关系。

状态定义：

- `keep-temporary`：迁移完成前继续保留；
- `migrate`：内容主要迁移到一个新真源；
- `split`：内容按职责拆入多个新真源；
- `merge`：与其他旧文件合并成一个新真源；
- `replace`：由新文件完整替代；
- `delete-after-validation`：验证通过后删除。

当前阶段不删除任何旧运行期文件。

---

## 2. 根文件与输出模板

| 旧路径 | 当前作用 | 目标路径 | 迁移方式 | 当前状态 |
|---|---|---|---|---|
| `SKILL.md` | 旧任务、模式与加载入口 | `SKILL.md` | Phase 6 完整改写 | keep-temporary |
| `assets/README.md` | 模板目录说明 | `assets/README.md` | 更新为新输出合同索引 | keep-temporary |
| `assets/templates/single-unit-output-template.md` | 单片段输出 | `assets/templates/single-shot-video-template.md` | 迁移并补模型适配槽位 | migrate |
| `assets/templates/multi-unit-output-template.md` | 多片段输出 | `assets/templates/multi-shot-video-template.md` | 迁移并补跨镜连续性 | migrate |
| `assets/templates/interactive-output-template.md` | 交互方向摘要 | `assets/templates/mode-interactive-output-contract.md` | 与交互模式规则合并 | merge |

---

## 3. 模式层

| 旧路径 | 有效内容 | 目标位置 | 迁移方式 | 当前状态 |
|---|---|---|---|---|
| `references/mode-quick/quick-mode.md` | 零打扰执行、自动补全、冲突裁决 | `SKILL.md` + `assets/templates/mode-quick-output-contract.md` | 拆分运行规则与输出合同 | split |
| `references/mode-interactive/interactive-mode.md` | Grill Me、单问题追问、收口条件 | `SKILL.md` + `assets/templates/mode-interactive-output-contract.md` | 拆分运行规则与输出合同 | split |

迁移后不再保留独立模式 Reference，避免每次执行额外加载一份模式正文。

---

## 4. 输入层

| 旧路径 | 有效内容 | 目标路径 | 迁移方式 | 当前状态 |
|---|---|---|---|---|
| `references/input-text-only/text-expansion.md` | 文字扩展、首帧建立、运动补全 | `references/inputs/text-input.md` | 重写并增强 | migrate |
| `references/input-image-ref/image-reference-analysis.md` | 图像类型、主辅图、参考锚点 | `references/inputs/single-image-input.md` + `multi-image-input.md` | 按单图/多图拆分 | split |

新增输入真源：

- `references/inputs/video-input.md`
- `references/inputs/audio-input.md`
- `references/inputs/mixed-multimodal-input.md`

这些内容主要来自 Seedance 多模态资料、LTX 指南和后续通用抽象，旧结构无对应文件。

---

## 5. 任务层

| 旧路径 | 有效内容 | 目标路径 | 迁移方式 | 当前状态 |
|---|---|---|---|---|
| `references/task-text-to-video/playbook.md` | 文生视频主流程 | `references/tasks/text-to-video/playbook.md` | 重写并补输入/控制/模型路由 | migrate |
| `references/task-image-to-video/image-to-video-playbook.md` | 图生视频主流程 | `references/tasks/image-to-video/playbook.md` | 重写并区分单图、多图与运动延续 | migrate |
| `references/output-single-unit/output-spec.md` | 单片段交付结构 | `assets/templates/single-shot-video-template.md` | 与模板合并 | merge |
| `references/output-multi-unit/output-spec.md` | 多片段交付结构 | `assets/templates/multi-shot-video-template.md` | 与模板合并 | merge |

新增任务真源：

- `tasks/multimodal-reference-video/playbook.md`
- `tasks/video-reference-and-video-to-video/playbook.md`
- `tasks/video-editing/playbook.md`
- `tasks/video-extension/playbook.md`
- `tasks/audio-driven-and-beat-sync/playbook.md`
- `tasks/storyboard-and-multi-shot-video/playbook.md`

---

## 6. 时间轴、连续性与质量控制

| 旧路径 | 有效内容 | 目标路径 | 迁移方式 | 当前状态 |
|---|---|---|---|---|
| `references/timeline/timeline-assembly.md` | 绝对时间、主体状态、镜头状态、节拍 | `references/controls/timeline-rhythm/timeline-assembly.md` | 迁移并扩展 | migrate |
| `references/timeline/lifestyle-beat-and-landing.md` | 生活化节拍与自然收尾 | `references/controls/timeline-rhythm/natural-beat-and-landing.md` | 迁移 | migrate |
| `references/continuity/continuity-guardrails.md` | 人物、场景、道具和镜头连续性 | `references/controls/continuity-consistency/continuity-guardrails.md` | 迁移并去重 | migrate |
| `references/continuity/human-motion-consistency.md` | 身份、体态、重心和动作阶段 | `references/controls/continuity-consistency/human-motion-consistency.md` | 迁移 | migrate |
| `references/style-control/anti-ai-video-realism.md` | 去漂浮感、设备感、自然动作 | `references/controls/realism-quality/anti-ai-video-realism.md` | 迁移 | migrate |
| `references/style-control/camera-failure-patterns-negative.md` | 运镜失败与负向限制 | `references/controls/camera-direction/camera-failure-guardrails.md` | 迁移并改为控制规则 | migrate |

---

## 7. 旧附录

| 旧路径 | 有效内容 | 目标路径 | 迁移方式 | 当前状态 |
|---|---|---|---|---|
| `references/appendix/camera-movement-appendix.md` | 运镜选择和基础术语 | `libraries/camera-shot/` + `controls/camera-direction/` | 方法与术语拆分 | split |
| `references/appendix/action-beat-appendix.md` | 蓄力、接触、反馈、恢复 | `libraries/action-motion/action-beat-structure.md` | 与用户动作戏资料合并 | merge |
| `references/appendix/visual-style-appendix.md` | 设备层、作者气质、光影色调 | `styles/` + `libraries/genre-patterns/` | 风格实现与题材选择拆分 | split |
| `references/appendix/index.md` | 旧附录导航 | 无 | 新索引完成后删除 | delete-after-validation |

v2 不再保留独立 `appendix/`。高价值知识必须明确归入 controls、libraries 或 styles。

---

## 8. 总索引

| 旧路径 | 当前作用 | 目标 | 迁移方式 | 当前状态 |
|---|---|---|---|---|
| `references/index.md` | 旧模式/输入/任务/附录路由 | v2 总索引 | Phase 1 重写；迁移期保留兼容说明 | replace |

---

## 9. 用户资料候选沉淀映射

| 原始资料 | 主要候选真源 |
|---|---|
| `基础Prompt结构(1).md` | `controls/prompt-assembly/` |
| `文生视频Prompt结构.md` | `tasks/text-to-video/` |
| `图生视频Prompt结构.md`、`图生视频.md` | `tasks/image-to-video/` + `inputs/*image*` |
| `故事版分镜到视频流程.md` | `tasks/storyboard-and-multi-shot-video/` |
| `导演级运镜术语选择器.md` | `libraries/camera-shot/` |
| `视角机位与景别选择器(1).md` | `libraries/camera-shot/` |
| `打击帧与动作戏结构.md` | `libraries/action-motion/` + `controls/subject-motion/` |
| `表情与微表情选择器(1).md` | `libraries/performance-expression/` + `controls/performance-expression/` |
| `电影光影与色调选择器(1).md` | `libraries/lighting-color/` |
| `电影感Prompt拆解公式(1).md` | `styles/cinematic-live-action/` + `controls/prompt-assembly/` |
| `AI视频风格选择器.md` | `libraries/genre-patterns/` + `styles/` |
| `影视风格选择器(1).md` | `libraries/genre-patterns/` |
| `写实电影短剧.md` | `styles/realistic-short-drama/` |
| `AI漫剧.md` | `styles/comic-motion-drama/` |
| `图像风格提取流程(1).md` | `inputs/single-image-input.md` + `controls/reference-binding/` |
| `角色发型选择器(1).md` | 默认不完整迁入视频 Skill；仅提炼动态一致性部分 |

---

## 10. 外部资料候选沉淀映射

| 来源 | 主要用途 | 候选真源 |
|---|---|---|
| `dexhunter/seedance2-skill` | Seedance 能力、素材引用和任务模式 | `models/seedance-2.md` + 相关任务页 |
| `awesome-seedance-2-prompts` | 高质量案例结构、音画与分时段模式 | `research/extraction-notes/`，再按主题合并 |
| LTX-2.3 官方 Prompt Guide | LTX Prompt 原则、I2V 运动描述、表演与音频 | `models/ltx-2-3.md` + 通用控制页 |

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
