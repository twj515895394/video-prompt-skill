# Action–Camera Handoff Playbook

## 1. 职责

本文件是 Action Combat 的轻量桥接 Runtime。

它不替代：

- `core-playbook.md` 的 Combat State / Continuity；
- `choreography-playbook.md` 的动作编排；
- 专项 Combat Playbook 的具体动作语言；
- `camera-direction/control.md` 的通用摄影术语与镜头规则；
- `prompt-assembly/control.md` 的最终序列化。

它只负责四件事：

1. Stage-2 Execution Knowledge 是否真的命中；
2. 动作之间是否存在 Motion / Energy Carry-over；
3. Camera 是否由正在发生的动作状态变化触发；
4. Cut / Reframe 后是否继承仍然活着的运动，而不只是位置连续。

核心原则：

> **Action 决定 Camera 为什么变化；Camera 不能把连续动作切成重新开始的动作块。**

---

## 2. Stage-2 Pattern Hit Evidence Gate

在 Concrete Action Phrase 进入最终编排前，先检查当前 Planning / Draft Phrase 是否存在 Execution Gap。

### 必须优先检查的 Gap

- Movement：Route / Angle / Level / Axis / Range / Position / Support / Balance；
- Technique：具体攻击、防守、腿法、摔控、兵器动作；
- Transition：Contact / Momentum / Axis / Range / Recovery 如何进入下一动作。

### Pattern Hit Required Conditions

出现以下任一情况，不能无 leaf execution knowledge 直接交付：

- High / Expert Combat 且目标是连续高手对决；
- Fighting Direction 本身要求明显 Movement / Level / Axis / Route / Support 差异；
- 当前多个关键 Phrase 主要由前臂 / 肩线 / 抓腕 / 顶肩等 Upper-body Contact 驱动；
- Movement 只是给上肢动作补一句“侧步 / 转髋 / 降低重心”；
- Transition 主要依赖“然后 / 随后 / 再次”，没有可见 Handoff State；
- Preflight 已触发 `Static Standing Combat / Upper-body Technique Dominance`。

当前 CK 最小验证阶段，如果没有更具体且已经读取的专业 leaf knowledge 能完整覆盖对应 Gap：

> **必须读取 `references/libraries/combat-choreography-patterns/minimum-validation-set.md`。**

### Runtime Evidence

内部至少要能回答：

```text
Gap 是什么
→ 命中哪个 Slot
→ 实际读取哪个 leaf knowledge
→ 哪个 Pattern / Detail 被转成 Concrete Action
```

不要求把这些字段输出给用户，但没有真实 Read / Hit Evidence 时不得假定 Stage-2 已执行。

### FAIL 回路

如果 Phrase 已经写完才发现该读 Pattern 却没有读：

```text
FAIL
→ 回 Stage-2
→ Read leaf knowledge
→ 重写 Concrete Action Phrase
```

禁止只在旧 Phrase 上追加“侧切 / 转髋 / 高低位”等词来伪装 Pattern Realization。

---

## 3. Motion / Energy Carry-over

Action Transition 不只检查“逻辑上接得上”，还要检查上一动作留下的动力是否真正进入下一动作。

可继承的 Carry-over：

- linear momentum；
- angular momentum / torso rotation；
- contact pressure；
- support transfer；
- forced step；
- recovery burden；
- body axis deviation；
- range compression / expansion；
- wall / floor / environment post；
- unfinished attack / defense motion。

优先：

```text
闪避产生的旋转
→ 直接成为下一次侧切 / 反击入口

低线破支撑
→ 对手被迫重新踩稳
→ 直接成为换角 / 摔控入口

撑墙止住前冲
→ 支点直接变成 pivot / counter 轴
```

避免：

```text
动作完成
→ 站稳
→ 回默认姿态
→ 下一动作重新启动
```

Motion / Energy Carry-over 是 Transition 质量检查，不增加新的 Pattern 类型。

---

## 4. Action–Camera Handoff 最小结构

当 Camera 需要移动、Reframe、改变景别或 Cut 时，内部使用：

```text
Current Action State
→ Camera Task
→ Shot Entry Trigger
→ Inherited Motion State
→ Observation
→ Shot Exit / Handoff
```

这是导演规划结构，不默认作为字段表输出。

### Current Action State

至少理解当前：

- 谁在主动移动 / 攻击；
- Contact 是否仍存在；
- Momentum / Pressure 是否仍存在；
- Position / Direction / Axis / Range；
- 是否存在 Level / Support / Advantage 变化。

### Camera Task

每次明显 Camera Change 只解决一个主要问题，例如：

- 看清 Route / Angle；
- 看清 Contact Consequence；
- 看清 Support / Footwork；
- 看清 Initiative Reversal；
- 恢复新的空间关系。

---

## 5. Action-triggered Camera Change

Action Combat 的 Camera Change 优先由动作信息变化触发，而不是为了“更电影”随机切换。

### 5.1 Cut on Motion

动作已经开始，在 Motion 尚未结束时 Cut；下一镜继续同一个动作。

正确：

```text
人物开始沉身侧穿
→ CUT
→ 下一镜继续下沉和跨步，不重新站起
```

### 5.2 Contact / Consequence Trigger

只有 Contact 真正改变状态时才值得强化：

- Balance；
- Guard；
- Axis；
- Range；
- Position；
- Initiative。

Camera 应尽量看到 Contact 的**后果**，而不是只重复“打到了哪里”。

### 5.3 Direction / Axis Change

人物发生明显 Route / Direction / Body Axis 改变时，可改变机位或跟拍方向，让新关系变得可读。

### 5.4 Initiative Reversal

主动权翻转时，可改变 Relationship Angle / Distance，使新的控制关系视觉化。

### 5.5 Range / Level / Support Change

以下变化可触发有效 Camera Change：

- high → low；
- standing → ground；
- mid → close；
- 支撑脚转换；
- forced step / stumble；
- takedown entry。

### 5.6 Occlusion / Match Motion

人物、前景、墙柱、快速掠过镜头等自然遮挡可以成为 Cut Bridge。

要求：

- Action Direction 连续；
- Momentum 连续；
- Cut 后人物不能无原因换侧 / 换位。

### 5.7 Environment Boundary

Fight-space 从开放区域进入墙、门框、走廊、楼梯等边界时，Camera 可以跟随空间约束改变。

不是为了环境丰富，而是环境已经改变动作路线。

---

## 6. Live-motion Cut Contract

优先：

```text
Shot A：动作启动 / 压力建立
→ CUT while motion is alive
→ Shot B：同一动作继续 / Contact / Reaction
→ 下一动作直接继承 Reaction
```

避免：

```text
Shot A：动作完整结束 + 对手完整反应 + 双方站稳
→ CUT
→ Shot B：下一动作重新开始
```

跨镜至少继承：

```text
一类 Active Motion State
+
必要 Spatial State
```

Active Motion State 可为：

- Momentum；
- Contact；
- Pressure；
- Recovery；
- Rotation；
- Support transfer；
- Forced step。

Spatial State 包括：

- Position / Left-Right；
- Direction；
- Axis；
- Range。

只有位置连续而运动死掉，仍判 `Kinetic Handoff Loss`。

---

## 7. Camera Coverage 不是对称景别循环

禁止为了“有变化”机械形成：

```text
Medium
→ Close-up
→ Medium
→ Close-up
```

Shot Scale / Camera Position 应由当前信息需要决定。

### Re-establish 条件

只有在局部镜头后观众可能丢失：

- 双方位置；
- Range；
- Axis；
- Fight-space 边界；

才需要 Re-establish。

因此“特写后立刻回中景”不是默认规则。

---

## 8. Action Spine 与 Camera Handoff 的耦合外显

Final Prompt 的关键 Camera Handoff 应锚在具体 Action Moment 上。

避免：

> 关键接触时短暂切近，然后立刻回到中景。

优先：

> 她开始沉身从高线下穿时，镜头随身体短暂降低；脚步跨过对方支撑线、迫使他重新踩稳的一瞬切到低位近景，下一镜继续同一失衡反应，并从新的斜侧关系接住她的再进入。

不要求所有镜头都这样展开；只外显真正改变动作理解的 Handoff。

Camera 段仍可保留总体策略，但不能用总体策略替代动作中的关键 Handoff。

---

## 9. One-take 例外

如果用户明确要求 One-take / 一镜到底：

- 不要求 CUT Trigger；
- 仍要求 Camera Movement / Reframe 由 Action State Change 触发；
- Movement 起点、路线、速度变化和停止点继续服从 `camera-direction/control.md`；
- Fight-space 改变时 Camera 需要重新组织关系，而不是无摩擦漂浮跟随。

Action–Camera Handoff 高于“是否剪辑”，它描述的是摄影怎样响应动作。

---

## 10. Action–Camera Preflight

Final Prompt 输出前检查：

### A. Stage-2 Evidence

- 当前是否存在必须读取 leaf execution knowledge 的 Gap？
- 如果存在，是否真的 Read？
- Pattern / Detail 是否进入可见 Concrete Action？

失败：`Stage-2 Routing Evidence Missing`。

### B. Kinetic Handoff

- 下一动作是否利用前一动作仍未消失的 Momentum / Contact / Support / Recovery / Axis？
- 是否出现大量完整收势 + Neutral Reset？

失败：`Kinetic Handoff Loss`。

### C. Camera Motivation

- 每个关键 Cut / Reframe 是否有 Action Trigger？
- 是否只是“为了电影感”随机改变景别？

失败：`Action–Camera Decoupling`。

### D. Live Motion Across Cut

- 至少关键 Cut 是否在 Motion alive 时发生？
- Shot B 是否继续 Shot A 的动作 / Contact / Reaction / Pressure？

失败：`Dead-motion Cut / Post-action Cut`。

### E. Coverage Patterning

- 是否机械 Medium → Close → Medium 循环？
- Re-establish 是否只在真的需要空间恢复时使用？

失败：`Coverage Patterning / Symmetric Shot Cycling`。

---

## 11. Failure Rewrite Priority

发生失败时：

```text
Stage-2 Evidence FAIL
→ 先补 Read / Pattern Realization

Kinetic Handoff FAIL
→ 重写 Transition / Phrase

Action–Camera FAIL
→ 重新选择 Action Trigger + Inherited Motion State

Coverage Patterning FAIL
→ 重新按动作信息分配 Shot Task
```

不要通过增加更多 Shot、更多特写或更多 Camera 术语修复。

---

## 12. 边界

- Fighting Direction / Coverage / Granularity：`choreography-playbook.md`；
- Range / Advantage / Position：`core-playbook.md`；
- 具体动作知识：当前专项 Playbook + Stage-2 leaf knowledge；
- 通用 Camera 术语与轴线：`references/controls/camera-direction/control.md`；
- 最终序列化：`references/controls/prompt-assembly/control.md`。

本文件只做 Action ↔ Camera 与 Stage-2 Evidence 的桥接，不扩成新的大系统。
