# Action Combat Video Task Router

## 1. 何时进入本任务

当用户的主要目标是生成或设计**动作格斗 / 武术 / 武侠战斗视频 Prompt**，且成败高度依赖持续攻防、动作因果、距离变化、空间站位、受力反馈、多人目标切换、兵器连续性或动作导演质量时，读取本任务。

典型信号：

- 近身格斗、拳脚、摔投、缠斗、制服；
- 1v1 / 1vN 动作戏；
- 武术、武侠、刀剑枪棍交锋；
- 用户明确要求动作连续、高手对决、拳拳到肉、兵器轨迹、长镜头打斗；
- 普通 `text-to-video` / `image-to-video` 已不足以表达 Combat State + Choreography 双重要求。

本任务是执行差异明显的专项工作流，不只是题材标签。

---

## 2. 不进入本任务的情况

- 只有一个简单挥拳、跑动或体育动作：继续使用原主任务 + `action-motion`；
- 用户主要提供故事板并要求管理整部多镜头片段：主任务仍可为 `storyboard-and-multi-shot-video`，Combat 作为专项编排知识按需引用；
- 用户主要要求视频局部编辑 / 延长：主任务仍由对应编辑 / 延长 Playbook 决定；
- 枪战：当前没有正式 Gunfight 专项 Playbook，除非后续扩展，否则只复用可迁移的 Combat Core / Choreography 原则，不伪装成已完整支持分支。

---

## 3. Combat 运行结构

进入本任务后，运行时骨架固定为：

```text
core-playbook.md
+ choreography-playbook.md
+ 1 个当前专项 Playbook
+ 按缺口选择的少量 Controls
+ 按需展开的少量 Library Detail
+ 可选 Model Adapter
```

### `core-playbook.md`

负责 Combat State / Continuity / Battle Runtime Skeleton：

- Combat Intent；
- Spatial Map；
- Range / Advantage / Condition；
- Turning Event；
- Target Handoff；
- Beat State Contract；
- Position / Environment / Weapon State；
- Spatial / Physical / Continuity Validation。

### `choreography-playbook.md`

负责 Combat Choreography Engine：

- Choreography Profile；
- Active Combat Coverage；
- Rhythm；
- Action Phrase；
- Exchange Depth；
- Character Identity；
- Tactical Interaction；
- Environment Affordance；
- Contact Solidity；
- Signature Moment；
- Action Sufficiency / Execution Budget；
- Camera Readability；
- Combat Audio；
- Final Prompt Action Externalization。

> **Core 负责“打得对、接得上”；Choreography 负责“打得够、丰富、好看、有实感”。**

---

## 4. 专项分支路由

Core + Choreography 之后只选择一个主要专项 Playbook。

### 现代格斗

读取：`modern-combat-playbook.md`

包括写实近身格斗、电影化动作片、拳击 / 泰拳 / 散打 / MMA / 摔跤 / 缠斗等动作语言。

### 电影武侠

读取：`cinematic-wuxia-playbook.md`

包括空手武术与刀 / 剑 / 枪 / 棍，默认是电影武侠而非仙侠。

专项 Playbook 只负责具体动作语言、物理尺度、默认 Range / Rhythm / Contact 表现与专业 Profile 使用方式，不得反向重定义 Core / Choreography 的通用质量合同。

---

## 5. Two-stage On-demand Loading

Combat V2 使用：

> **Plan First, Load Detail Second / 先规划，再加载详情。**

### Stage 1：Planning

使用：

```text
Task Router
+ Core
+ Choreography
+ 当前专项 Playbook
+ 必要轻量 Index
+ 可选 Model Capability 摘要
→ Combat Planning Context
```

Planning Context 只保留当前任务需要的轻量变量，例如：

- Combat Branch；
- Choreography Profile；
- Coverage；
- Rhythm；
- Character Identity 倾向；
- Contact Modality；
- Environment Importance；
- Signature Moment Need；
- Camera / Model 风险。

不把所有 Library 正文一次性加载。

### Stage 2：Execution Knowledge

正常情况下只展开约 2 个主要 Library Detail Slot：

```text
Slot A：Technique / Execution Knowledge
→ Fighting / Martial / Weapon Profile

Slot B：Choreography Enhancement Knowledge
→ Signature Moment Pattern 或其他真正需要的增强知识
```

优先级：专业正确性 > Character Identity 差异化 > 创意增强。

> **能力很多，不等于每次加载很多。**

---

## 6. Quick / Interactive 共享规划图

Quick 与 Interactive 使用同一个 Combat Planning Graph 和同一套质量标准。

### Quick Mode

> **Quick = Full Planning + Silent Resolution.**

Quick 不因输入简短而跳过：

- Coverage；
- Rhythm；
- Character Identity；
- Contact Solidity；
- Environment；
- Signature Moment；
- Camera / Execution Budget；
- State / Continuity Validation。

高置信度、低风险项自动补全；内部状态不默认展示；直接输出完整可复制 Prompt。

### Interactive Mode

只在以下条件同时成立时暴露一个决策：

- 存在多个明显不同方向；
- 方向会显著改变成片；
- 当前信息不足以高置信度选择。

不把 Contact Solidity、连续性检查、Action Sufficiency 等基础质量机制变成固定问卷。

---

## 7. 输入与输出关系

输入仍由 `references/inputs/` 判断，不在本任务复制素材规则。

输出仍使用现有 single-shot / multi-shot / model-adapted 合同，不建立平行 Combat 模板。

内部流程：

```text
Combat Planning Context
→ Action Phrase / Battle Beat
→ Core State Validation
→ Camera / Audio Coordination
→ Final Prompt Action Externalization
→ 挂接现有输出合同
→ 输出完整可复制 Prompt
```

最终 Prompt 遵循：

> **State Machine Internalized, Choreography Externalized.**

状态机制保留在内部，外部主要写人物实际怎么动、怎么接触、怎么受力、怎么换位、怎么继续打。

---

## 8. 上位原则

> **约束错误，不约束创作。**  
> **Clarity Through Structure, Not Action Reduction.**  
> **高信息密度，但低混乱度。**

Battle Beat、Action Phrase、Profile、Pattern、Golden Scenario 都不是固定动作模板。

禁止为了“清晰”默认削减有效攻防；复杂度优先通过结构、Phrase 切分、Camera Readability 与模型执行预算处理。
