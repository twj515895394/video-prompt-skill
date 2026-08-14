# Action Combat Video Task Router

## 1. 何时进入本任务

当用户的主要目标是生成或设计**动作格斗 / 武术 / 武侠战斗视频 Prompt**，且成败高度依赖攻防因果、距离变化、空间站位、受力反馈、多人目标切换或兵器连续性时，读取本任务。

典型信号：

- 近身格斗、拳脚、摔投、缠斗、制服；
- 1v1 / 1vN 动作戏；
- 武术、武侠、刀剑枪棍交锋；
- 用户明确要求动作连续、镜头跟随动作、拳拳到肉、兵器轨迹、长镜头打斗；
- 普通 `text-to-video` / `image-to-video` 已不足以表达战斗状态链。

本任务是执行差异明显的专项工作流，不只是题材标签。

## 2. 不进入本任务的情况

- 只有一个简单挥拳、跑动或体育动作：继续使用原主任务 + `action-motion`；
- 用户主要提供故事板并要求管理整部多镜头片段：主任务仍可为 `storyboard-and-multi-shot-video`，Combat 作为专项编排知识按需引用；
- 用户主要要求视频局部编辑 / 延长：主任务仍由对应编辑 / 延长 Playbook 决定；
- 枪战：第一版不作为正式 Combat 分支，使用 Generic 动作设计或后续扩展。

## 3. 分支路由

先读取：

- `core-playbook.md`

然后只选择一个专项 Playbook：

### 现代格斗

读取：`modern-combat-playbook.md`

包括写实近身格斗、电影化动作片、拳击 / 泰拳 / 散打 / MMA / 摔跤 / 缠斗等动作语言。

### 电影武侠

读取：`cinematic-wuxia-playbook.md`

包括空手武术与刀 / 剑 / 枪 / 棍，默认是电影武侠而非仙侠。

## 4. 输入与输出关系

输入仍由 `references/inputs/` 判断，不在本任务重复素材规则。

最终输出仍使用现有输出合同：

```text
Combat Blueprint
→ 判断 single-shot / multi-shot
→ 挂接现有输出合同
→ 注入 Combat 专项动作 / 镜头 / 声音 / 连续性 / Negative Constraints
→ 输出可直接复制的完整 Prompt
```

Combat 不建立平行模板。

## 5. Quick Mode

Quick Mode 不追问：

- 自动推断 Combat Intent；
- 自动选择现代 / 武侠分支；
- 自动选择合理强度；
- 自动建立 Battle Beat 与必要状态；
- 自动完成 Action / Camera / Audio 三线编排；
- 内部状态不默认展示；
- 直接输出详细、完整、专业、可复制 Prompt。

## 6. 上位原则

> **约束错误，不约束创作。**

Battle Beat、默认节奏、镜头模式、动作画像和回归案例都不是固定模板。用户已有明确动作创意时优先保留，只修正不可执行、无因果、空间断裂或物理冲突部分。
