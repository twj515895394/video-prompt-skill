# Action Combat Video Implementation Plan

> 状态：实施中
>
> 设计依据：`docs/action-combat-video-spec.md`
>
> 目标分支：`feat/action-combat-v1`

## 1. 实施目标

把 Action Combat 从设计 Spec 落地为 `video-prompt-skill` 的一级专项任务能力，第一版覆盖：

- 现代写实 / 电影化近身格斗；
- 电影武侠 / 武术动作；
- 1v1 与 1vN；
- 刀 / 剑 / 枪 / 棍；
- Action / Camera / Audio 三线同步；
- Combat Spatial Map、Range / Advantage / Condition、Target Handoff、Beat State Contract；
- Generic Professional Prompt 作为默认最终产品；
- 与现有 single-shot / multi-shot 输出合同衔接。

实施原则：

> **约束错误，不约束创作。**
>
> 固定的是因果、连续性、状态继承、物理反馈和输出完整度；动作编排、Beat 数量、镜头选择、环境利用和节奏只提供策略，不做死模板。

## 2. 架构边界

### Task / Playbook

新增一级专项任务：

```text
references/tasks/action-combat-video/
├── index.md
├── core-playbook.md
├── modern-combat-playbook.md
└── cinematic-wuxia-playbook.md
```

职责：路由、Combat 工作流、Battle Beat、状态链、三线编排和最终 Prompt 组装要求。

### Controls

第一版不新增 Combat 专属 Control。优先复用：

- `timeline-rhythm`
- `subject-motion`
- `camera-direction`
- `spatial-blocking`
- `continuity-consistency`
- `audio-visual-sync`
- `prompt-assembly`
- `realism-quality`

### Libraries

按职责聚合可选知识，避免一个流派一个文件：

- `combat-fighting-profiles`
- `combat-martial-profiles`
- `combat-weapon-profiles`
- `combat-environment-patterns`

### Styles

不新增 Combat Style。继续复用现有视觉 Styles。

### Diagnostics

优先复用现有 diagnostics；新增一个综合型：

- `combat-state-continuity-failure`

只处理现有诊断覆盖不好的 Advantage / Condition / Target / Weapon / Beat State Contract 状态断裂。

## 3. 实施阶段

### Phase 1｜Task 能力落地

- [ ] 新建 Action Combat 路由页；
- [ ] 新建 Combat Core Playbook；
- [ ] 新建 Modern Combat Playbook；
- [ ] 新建 Cinematic Wuxia Playbook；
- [ ] 接入 `references/tasks/index.md`；
- [ ] 接入 `SKILL.md` 任务路由。

完成标准：用户提出复杂动作格斗 / 武侠动作戏时可以唯一命中 Action Combat Task，Quick Mode 不增加追问。

### Phase 2｜Combat Libraries

- [ ] 现代格斗动作画像库；
- [ ] 武术 / 武侠动作画像库；
- [ ] 兵器动作画像库；
- [ ] 环境战斗交互模式库；
- [ ] 更新 `references/libraries/index.md`。

完成标准：Playbook 只保存“怎么编排”，Library 保存“有哪些动作语言 / 兵器语言 / 环境模式”，无正文重复。

### Phase 3｜Diagnostic

- [ ] 新建 `combat-state-continuity-failure`；
- [ ] 更新 diagnostics index；
- [ ] 明确与现有 motion / spatial / anatomy / physics / audio diagnostics 的路由边界。

完成标准：普通失败继续走现有诊断，只有 Combat 状态链断裂才走新增页。

### Phase 4｜运行入口与索引整合

- [ ] 更新 `references/index.md`；
- [ ] 检查 `SKILL.md` 的任务范围和路由；
- [ ] 确保模型适配仍为可选层；
- [ ] 确保 Combat 不复制 single-shot / multi-shot 模板正文；
- [ ] 检查加载预算。

完成标准：正常 Combat Quick Mode 只加载 1 个主 Task、必要 Controls、0–2 Libraries、可选 Style / Model Adapter。

### Phase 5｜静态回归与验证

建立覆盖性测试样例，但明确：**测试样例不是生成模板。**

至少覆盖：

- 现代 1v1；
- 现代 1vN；
- 站立打击到缠斗 / 控制的距离变化；
- 连续长镜头动作戏；
- 武侠空手；
- 剑类兵器；
- 长兵器与短兵器距离差；
- 武侠 1vN；
- 环境强交互；
- Condition 跨 Beat 累积；
- Advantage Turning Event；
- Action / Camera / Audio 同步。

检查项：

- Range 是否有因果变化；
- Target 是否通过 Handoff 切换；
- Beat End State 是否继承；
- Condition 是否持续影响后续动作；
- Camera Axis 是否可解释；
- Weapon State 是否连续；
- 打击是否有 Contact / Reaction / Recovery；
- 场景需要时音频是否进入 Beat；
- 最终 Prompt 是否详细、完整、专业、可直接复制；
- 是否避免把回归样例当固定动作框架。

### Phase 6｜文档收口

- [ ] 更新本实施计划状态；
- [ ] 更新 `docs/action-combat-video-spec.md` 实施状态；
- [ ] 记录回归结果；
- [ ] 记录最终文件清单与架构边界；
- [ ] 做分支差异核对。

## 4. 不实施内容

第一版暂不实施：

- 枪战 Playbook；
- 仙侠能量战斗体系；
- 每个流派一个独立文件；
- Combat 专属视觉 Style；
- 大量 Combat 专属 Controls；
- 一套与现有输出合同平行的 Combat 模板系统；
- 固定 Beat 数量、固定动作组合或固定镜头模板。

枪战后续复用 Combat Core，新增专项 Playbook / Library 扩展即可。

## 5. 交付物

预计最终新增 / 修改：

```text
docs/action-combat-video-spec.md
docs/action-combat-video-implementation-plan.md
docs/action-combat-video-regression.md

references/tasks/action-combat-video/*
references/tasks/index.md
references/libraries/combat-*/library.md
references/libraries/index.md
references/diagnostics/combat-state-continuity-failure/diagnostic.md
references/diagnostics/index.md
references/index.md
SKILL.md
```

实际实现如发现现有真源已经足够，将优先扩展 / 引用现有文件，而不是机械创建计划中的全部候选文件。
