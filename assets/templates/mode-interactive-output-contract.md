# 交互模式输出合同

## 适用条件

只有用户明确希望共同讨论、逐步设计、先提问再生成、比较多个大方向或明确要求 Grill Me 时进入交互模式。否则默认 Quick Mode。

---

## 核心规则

- 每次只问一个最影响结果的问题；
- 每个问题同时给出推荐答案；
- 沿设计依赖顺序推进，上游先于下游；
- 已确认的信息不重复询问；
- 能从请求、上下文和素材高置信度推断的内容不追问；
- 只追问会实质改变视频目标、动作、镜头、节拍、连续性或模型实现路径的变量；
- **优化目标不是“问题越少越好”，而是每一个问题都必须值得问；**
- 用户要求收口，或剩余问题只影响轻微细节时，立即停止提问并完成交付；
- **Interactive 默认最多 10 轮追问。10 轮是上限保护，不是目标轮数，也不是必须问满；如果前 4–6 轮甚至更少已经足以形成完整可执行需求，应立即提前收口。**

---

## High-value Question Budget / 高价值问题预算

Interactive 使用**价值驱动的动态轮数**，而不是固定问卷。

每次准备继续追问前，先判断当前候选问题是否同时满足：

```text
用户尚未明确
+ 系统无法高置信度代替用户决定
+ 不同答案会显著改变最终视频
+ 该问题优先级高于剩余未确认项
```

只有同时满足，才值得继续问。

因此：

- 可能 2–3 轮就已经足够；
- 4–6 轮在复杂一点的动作 / 叙事任务中完全合理；
- 必要时可以继续到 7–10 轮；
- **不得为了“显得完整”或走完 Planning Graph 而强行问满；**
- 达到第 10 轮后，不再新增用户问题；剩余低风险 / 次要不确定项按当前上下文和推荐方案静默补全并收口；
- 如果第 10 轮前仍存在真正会导致方案不可执行的核心冲突，应优先在前面的高价值问题中暴露，而不是把关键冲突拖到最后。

原则：

> **High-value Questions, Not Minimum Questions.**  
> **追求高价值问题覆盖，不追求最少问题，也不追求问满上限。**

---

## Combat Interactive Mode

Action Combat 与 Quick Mode 共用同一 Combat Planning Graph、Choreography Engine、State / Continuity Engine、Final Preflight Gate 和质量上限。

Interactive 只负责 **Decision Exposure Policy / 决策暴露策略**：

```text
用户已明确
→ 直接继承

高置信度 + 低风险
→ 静默补全

多个方向都合理
+ 会显著改变成片
+ 当前置信度不足
→ 暴露当前唯一最关键分叉
```

### Combat Planning Gate

Combat 追问前先内部检查：

- 当前真正的上游高影响分叉是什么；
- 是否遗漏与场景明显相关的 Choreography Profile；
- Character Identity 是否需要用户参与决定，还是可以动态推导；
- 当前问题是否比尚未解决的 Character Identity / Rhythm / Profile 更重要；
- 是否把 Contact Solidity、Action Sufficiency、Camera Readability、Final Preflight 等基础质量机制误做成问卷；
- 当前推荐是否把职业、性别、年龄、外貌或体型直接转换成固定打法；
- **如果当前信息已经足以完整规划 Combat Sequence，是否应立即收口而不是继续沿 Planning Graph 逐节点发问。**

如果当前问题只是系统应该自己做好的质量机制，不问用户。

---

## Action Combat 推荐依赖顺序

```text
核心 Combat Intent / 观看目标
→ Combat Branch（Modern / Wuxia 等）
→ Cinematic Choreography Profile
→ Active Combat Coverage（只有存在真实方向分叉时）
→ Action Exchange Rhythm
→ Combat Character Identity 的关键差异
→ Environment / Camera Intent（只有会明显改变成片时）
→ 战斗结果 / 收尾
```

这是**依赖顺序，不是固定问卷顺序**。任一节点如果已经由用户明确、可高置信度自动补全，或不会显著改变成片，应直接跳过。

### 重要约束

- **不要过早先问“谁赢”**，除非胜负本身就是用户的核心观看目标或会彻底改变前面所有设计；
- 高手对决若“高手连续攻防型”明显相关，不能因为选项设计漏掉它；
- Camera 通常可以在动作与空间计划后自动推导，不应为了问 Camera 跳过更高价值的 Character Identity；
- Contact Solidity、Kinetic Scope、Temporal Packing、Motion Handoff、Action Sufficiency、Final Preflight 等不作为固定交互问题；
- 用户已明确“连续、高密度、电影化”时，不再逐项追问这些基础质量条件；
- **不以固定 4 轮、6 轮或其他轮数作为完成标准；完成标准是高影响需求已经足以执行。**

### Character Identity Recommendation Guard

Character Identity 必须动态推导。推荐答案中不得出现以下快捷逻辑：

```text
职业 → 固定流派 / 固定打法
性别 → 固定速度 / 力量 / 防守偏好
年龄 → 固定迟缓 / 经验 / 力量偏好
体型 → 固定压迫 / 抓控 / 闪避偏好
外貌 → 固定动作风格
```

这些信息可以影响运动能力、Reach、惯性、支撑、恢复速度或视觉对比，但**不能单独决定打法**。

例如用户给出“22 岁女性 + 55 岁矮胖男性 + 两人都是职业杀手”，推荐不能自动写成：

- 女方 = 速度、角度、闪避；
- 男方 = 体重、力量、抓控。

除非用户已经明确这些打法，否则应先由 Combat Intent、Choreography Profile、经验、对手关系、空间、Range 与当前 State 推导；若多个打法方向都合理且差异会显著改变成片，才把“双方打法差异”作为当前一个交互问题。

推荐答案应描述**动作逻辑**而不是人口属性刻板映射，例如：

- 一方偏主动侧切、抢角度、连续截断；
- 另一方偏路线封锁、短距离打断、节奏破坏；

但这些也只是当前场景的可选设计，不是某类人的固定模板。

例如用户要求“15 秒办公室两名职业高手连续近身对决”，系统可以静默补全 High Coverage、Contact Solidity、Continuous Action Spine 等质量机制；真正值得暴露的可能是 Choreography Profile 或双方打法差异，而不是让用户回答十几个内部参数。

---

## 其他任务追问优先级

### 文生视频

```text
核心观看目标 → 开场画面 → 主体运动 / 表演 → 镜头主任务 → 节拍 / 时长 → 收尾
```

### 图生视频

```text
图片职责 → 必保锚点 → 如何开始运动 → 镜头如何跟随 → 最终落点
```

### 多模态参考

```text
素材职责 → 各维度唯一真源 → 必须保留 / 禁止继承 → 兼容性 → 最终时间轴
```

### 多镜头 / 故事板

```text
全片主线 → 段落目标 → 镜间承接 → 跨镜固定项 → 每镜动作 / 镜头
```

### 视频编辑 / 延长

```text
必须保持不变 → 必须修改 / 延长方向 → 允许变化范围 → 新落点
```

这些同样只是优先依赖关系，不是必须逐项发问的固定问卷。

---

## 单轮问题格式

```text
当前最关键的问题：...

我的推荐：...

原因：...
```

必要时可给 2–3 个明显方向，但必须明确推荐一个。

---

## 交互阶段允许输出

允许：当前唯一问题、推荐答案、与推荐直接相关的方向差异、极简已确认结论。

不得提前 Dump：完整未定 Prompt、多个问题、内部 State Table、Planning Context、Reference 加载细节。

---

## 收口条件

满足任一条件即结束追问：

- 用户说“直接出结果 / 按推荐做 / 够了”；
- 核心观看目标、动作方向、镜头原则、节拍和收尾已可执行；
- 剩余节点可高置信度自动补全；
- 再问只会影响轻微细节；
- 用户明确不希望继续深挖；
- **虽然尚未达到 10 轮，但当前需求已经达到完整可执行状态；**
- **已达到 10 轮上限：剩余非核心不确定项按推荐静默补全并交付。**

> **收口由“需求是否足够完整”驱动，不由轮数驱动；10 轮只负责防止无休止追问。**

---

## 最终交付

收口后必须交付可直接复制使用的结果。

Action Combat 收口后，系统内部继续执行：

- Choreography Planning；
- State / Continuity；
- Contact / Kinetic / Temporal Continuity；
- Camera Readability / Mobility / Coverage；
- **Combat-aware Prompt Assembly；**
- **Final Preflight Gate；**

Final Preflight FAIL 时先内部重写并重新检查，不允许因为交互已经结束就直接交付；也不把失败自动转成新的用户问题。

这些内部机制不作为大段 Meta 说明输出给用户。

---

## Quick / Interactive 边界

> **Quick = Full Planning + Silent Resolution。**

- Quick 直接完成所有低风险决策；
- Interactive 只把真正高影响、低置信度分叉交给用户；
- 两者共用同一动作引擎和质量标准；
- Interactive 不能因为问得更多就获得更高质量上限；
- Interactive 的价值是让用户控制关键创作分叉，而不是最小化问答次数；
- 用户在交互中要求直接生成时，立即收口，不继续追问。