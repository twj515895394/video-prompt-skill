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
+ Planning Gate
+ 按缺口选择的少量 Controls
+ 按需展开的少量 Library Detail
+ 可选 Model Adapter
+ prompt-assembly/control.md（Combat 必经）
+ Combat Final Preflight（必经）
+ 当前输出模板 / Model Serialization
```

其中 `prompt-assembly/control.md` 在普通任务中仍可按需读取；**一旦进入 Action Combat，则不占普通 `0-3 Controls` 可选预算，必须在最终交付前读取并执行。**

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
- Kinetic / Temporal / Motion Continuity；
- Camera Readability / Mobility；
- Combat Audio；
- Final Preflight Criteria。

> **Core 负责“打得对、接得上”；Choreography 负责“打得够、连续、丰富、好看、有实感”；Prompt Assembly 负责“把内部设计真正序列化成模型可执行的最终 Prompt”。**

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
→ Planning Gate
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

Planning Gate 必须先检查：

- 是否遗漏明显相关的 Choreography Profile；
- 是否过早锁定结局；
- Character Identity 是否被职业、性别、年龄、外貌或体型快捷映射；
- 是否把系统应自动保证的质量条件错误变成用户问卷。

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
- State / Continuity Validation；
- Final Assembly / Final Preflight。

高置信度、低风险项自动补全；内部状态不默认展示；直接输出完整可复制 Prompt。

### Interactive Mode

只在以下条件同时成立时暴露一个决策：

- 存在多个明显不同方向；
- 方向会显著改变成片；
- 当前信息不足以高置信度选择。

不把 Contact Solidity、Kinetic Scope、Temporal Packing、Motion Handoff、Action Sufficiency、Camera Readability、Final Preflight 等基础质量机制变成固定问卷。

推荐答案不得把人口属性当打法模板。例如年龄、性别、外貌、体型可以影响能力边界，但不能单独推出“年轻女性必然速度闪避”“矮胖年长男性必然力量抓控”。

---

## 7. Combat 必经 Final Assembly / Preflight

输入仍由 `references/inputs/` 判断，不在本任务复制素材规则；输出仍挂接现有 single-shot / multi-shot / model-adapted 模板，不建立平行 Combat 模板。

但 Action Combat 的最终运行链必须是：

```text
Combat Planning Context
→ Stage-2 Execution Knowledge
→ Action Phrase / Battle Beat
→ Core State Validation
→ Camera / Audio / Spatial Coordination
→ 读取并执行 prompt-assembly/control.md
→ Combat-aware Final Prompt Assembly
→ Combat Final Preflight
→ FAIL：内部重写 Action Phrase / Character Identity / Prompt Assembly，并重新检查
→ PASS：挂接当前输出模板 / Model Adapter
→ Delivery
```

### Final Preflight 最小合并 Gate

不把所有 Failure Signature 输出成 Checklist；最终只回答这些高价值问题：

1. **动作是否够**：Coverage / Exchange Depth / Kinetic Scope 是否与观看目标匹配；
2. **动作是否连续**：是否存在明显 Action Underpacking、Neutral Reset、Turn-taking Combat；
3. **角色是否真实区分**：Character Identity 是否由动作表现，且没有人口属性快捷模板；
4. **动作是否有实感和空间后果**：Contact / Range / Position / Environment 是否真正改变下一拍；
5. **镜头是否跟着战斗空间走**：Stable ≠ Static；高 Kinetic Scope 不能配长期近固定 Camera；
6. **最终序列化是否正确**：高密度 Combat 默认 Continuous Action Spine + Soft Time Anchors，不被通用模板重新切成硬时间盒；
7. **Prompt 是否 Action-first**：Negative 少而有依据，不添加用户未要求的剧情禁止项。

任一关键项 FAIL，不允许直接交付。

---

## 8. 输出模板覆盖关系

Combat 不建立独立 single-shot / multi-shot 模板副本，但**专项 Task 规则优先于通用模板默认规则**。

特别是高密度 Combat：

- 通用模板的“时长较长 / 3+ 阶段可使用绝对时间轴”不能自动触发；
- 默认继承 Choreography / Prompt Assembly 的 `Continuous Action Spine + Soft Time Anchors`；
- 只有用户明确逐秒、外部同步、多镜头边界或 Model Adapter 有实测依据时才使用 Hard Time Blocks；
- 即使使用 Hard Time Blocks，也必须跨块保持 Motion Handoff，时间边界不得成为 Neutral Reset。

最终 Prompt 遵循：

> **State Machine Internalized, Choreography Externalized.**  
> **时间码服从动作连续性，而不是动作服从时间码。**

---

## 9. 上位原则

> **约束错误，不约束创作。**  
> **Clarity Through Structure, Not Action Reduction.**  
> **高信息密度，但低混乱度。**  
> **少建运行时概念，多做高价值质量检查。**

Battle Beat、Action Phrase、Profile、Pattern、Golden Scenario 都不是固定动作模板。

禁止为了“清晰”默认削减有效攻防；复杂度优先通过结构、Phrase 切分、Camera Readability 与模型执行预算处理。新增 Failure Signature 不自动意味着新增 Runtime 模块。