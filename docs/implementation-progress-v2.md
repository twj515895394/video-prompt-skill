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
| Phase 4 资料库与风格层 | 已完成 | 100% | 七类资料库、七种风格和来源治理已完成 |
| Phase 5 模型适配层 | 已完成 | 100% | Generic、Seedance、LTX 已接入统一输出转换 |
| Phase 6 输出合同与 SKILL.md 切换 | 已完成 | 100% | 六份输出合同、v2 SKILL 和正式总路由已启用 |
| Phase 7 验证与旧结构清理 | 未开始 | 0% | 下一执行阶段 |

## Phase 0-1：架构与路由

已完成：

- 创建重构分支；
- 建立架构决策、实施计划和迁移台账；
- 建立 `research/` 原始资料区；
- 导入并登记 17 份用户资料；
- 锁定 Generic + Seedance 2.0 + LTX-2.3；
- 建立 inputs、tasks、controls、libraries、styles、models、diagnostics 分类索引；
- 重写 `references/index.md` 为 v2 正式总路由。

## Phase 2：输入层与任务层

### 输入层

- `references/inputs/text-input.md`
- `references/inputs/single-image-input.md`
- `references/inputs/multi-image-input.md`
- `references/inputs/video-input.md`
- `references/inputs/audio-input.md`
- `references/inputs/mixed-multimodal-input.md`

### 任务层

- `references/tasks/text-to-video/playbook.md`
- `references/tasks/image-to-video/playbook.md`
- `references/tasks/multimodal-reference-video/playbook.md`
- `references/tasks/video-reference-and-video-to-video/playbook.md`
- `references/tasks/video-editing/playbook.md`
- `references/tasks/video-extension/playbook.md`
- `references/tasks/audio-driven-and-beat-sync/playbook.md`
- `references/tasks/storyboard-and-multi-shot-video/playbook.md`

## Phase 3：核心控制层

已完成十类控制真源：

- 时间轴与自然收尾；
- 主体运动、重心、惯性和反馈；
- 镜头任务、路线和失败约束；
- 站位、朝向、视线和空间调度；
- 人物、场景、道具和动作连续性；
- 表演、微表情、对白和口型；
- 对白、音效、音乐和音画同步；
- 多模态素材职责和主真源；
- Prompt 信息优先级、压缩和组装；
- 设备来源、物理可信和去 AI 感。

## Phase 4：资料库与风格层

### 七类资料库

- camera-shot；
- action-motion；
- performance-expression；
- transition-effects；
- lighting-color；
- audio-sound；
- genre-patterns。

### 七种风格

- cinematic-live-action；
- realistic-short-drama；
- anime-animation；
- comic-motion-drama；
- commercial-advertising；
- documentary-ugc；
- experimental-visual。

资料库回答“有哪些选项”，风格层回答“如何拍出来”，没有复制任务流程或模型语法。

## Phase 5：模型适配层

已完成：

- `references/models/generic.md`：默认模型无关输出；
- `references/models/seedance-2.md`：`@图片 / @视频 / @音频` 职责绑定、编辑、延长和卡点；
- `references/models/ltx-2-3.md`：自然语言导演段落、连续表演、对白和音画表达；
- `assets/templates/model-adapted-output-template.md`：统一三种适配的最终输出转换。

当前只支持以上三种正式输出协议，不建设其他模型占位层。

## Phase 6：输出合同与运行入口

### 新输出合同

- `assets/templates/mode-quick-output-contract.md`
- `assets/templates/mode-interactive-output-contract.md`
- `assets/templates/single-shot-video-template.md`
- `assets/templates/multi-shot-video-template.md`
- `assets/templates/multimodal-reference-template.md`
- `assets/templates/model-adapted-output-template.md`

### 关键决策

- 快速模式默认零追问并直接交付；
- 交互模式仅在用户明确共创时启用；
- 交互模式每次只问一个关键问题并给出推荐答案；
- 简单任务默认只输出一份最终 Prompt；
- 多镜头只展开必要的全局固定项和 Prompt Pack；
- 多模态只保留执行必要的素材职责；
- 不默认输出备选版本、自动补全项和内部分析；
- 未指定模型时使用 Generic；
- 指定 Seedance 或 LTX 时读取唯一对应适配页。

### 入口切换

- `SKILL.md` 已完整重写并切换到 v2；
- `references/index.md` 已移除默认兼容路由，正式指向 v2 叶子；
- `assets/README.md` 已切换到新模板索引；
- 旧模式、旧任务、旧时间轴、旧附录和旧输出模板不再参与默认运行；
- 旧文件暂时保留，等待 Phase 7 回归测试和断链检查后删除。

## 当前架构安全状态

- 新 v2 链路已经成为工作分支默认运行入口；
- 旧文件尚未删除，可用于回滚和迁移核对；
- 主分支未被修改；
- Phase 7 前不合并、不清理旧结构；
- 输出合同、模型适配和 Reference 加载预算已经统一。

## 下一执行阶段：Phase 7

Phase 7 将完成：

1. 建立并执行十类测试场景；
2. 建设诊断层叶子文件；
3. 检查所有新路径和交叉链接；
4. 验证 Generic、Seedance、LTX 输出差异；
5. 检查重复真源和旧路径残留；
6. 删除已满足条件的旧模式、旧输入、旧任务、旧时间轴、旧连续性、旧附录和旧模板；
7. 形成 `docs/validation-report.md`。