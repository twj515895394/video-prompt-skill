# Action Combat Stage-2 Routing + Action–Camera Handoff Spec

> 状态：V1 / 2026-08-15 G01 Regression 后新增
>
> 触发来源：固定 G01「15 秒办公室职业杀手近身对决」真实 Interactive → Final Prompt Regression。
>
> 目标：一次性解决本轮暴露的两个问题：
>
> 1. Stage-2 Gap-driven Routing 规则存在，但真实运行没有读取 `minimum-validation-set.md`；
> 2. Camera 已具备 Cut Continuity Safety，但动作与镜头仍是“先编动作，再挑位置切镜”，缺少动作电影式 Action ↔ Camera Handoff。

---

## 1. 本轮真实证据

### 1.1 Stage-2 Pattern Hit 失败

真实 Read List 已读取：

- `action-combat-video/index.md`
- `core-playbook.md`
- `choreography-playbook.md`
- `modern-combat-playbook.md`
- `prompt-assembly/control.md`
- `subject-motion/control.md`
- `camera-direction/control.md`
- `spatial-blocking/control.md`

但没有读取：

`references/libraries/combat-choreography-patterns/minimum-validation-set.md`

因此当前首先判定：

`Stage-2 Pattern Non-realization / Routing Evidence Missing`

不能把本次动作仍偏上肢控制直接归因于 Pattern Knowledge Coverage 不足。

### 1.2 Action–Camera 结果不足

Final Prompt 已做到：

- 中景关系可读；
- 关键 Contact 可短暂切近；
- Cut 后要求保持 Position / Direction / Contact / Momentum；
- 不把 Continuous Action Spine 锁成 one-take。

但镜头仍主要表现为：

```text
动作先完整描述
→ “关键接触时切近”
→ “立刻回到中景”
```

Camera 仍像 Action 之后附加的 Coverage，而不是由动作状态变化直接触发的电影剪辑。

---

## 2. 设计目标

本轮不扩完整武术知识库，不建立第二套 Camera 系统。

只增加两个轻量能力：

```text
A. Stage-2 Pattern Hit Evidence Gate
B. Action–Camera Handoff Contract
```

它们分别解决：

```text
“该读的执行知识是否真的读了”
+
“动作如何自然地把摄影交给下一镜”
```

---

## 3. 决策 AC-01｜Routing Evidence First

Stage-2 不能只存在逻辑描述；进入 Concrete Action Phrase 前必须能回答：

```text
当前有哪些 Execution Gap？
→ 命中了哪个 Slot？
→ 读取了哪个 leaf knowledge？
→ 哪个 Pattern / Detail 被实例化？
```

不要求把内部审计输出给用户，但 Runtime 必须实际完成。

### Pattern Hit Required Conditions

出现以下任一情况时，不能在“无 leaf execution knowledge”状态下直接进入最终 Combat Phrase：

- High / Expert Combat 且用户要求连续高手对决；
- Fighting Direction 明确要求明显 Movement / Level / Axis / Route / Support 变化；
- 用户选择中国武术电影化近身、身法角度争夺、腿法全身攻防、摔控反摔等会显著改变动作构造的方向；
- 当前草拟 Phrase 连续多个主要由 Upper-body Contact 主导；
- Transition 仍主要依赖“然后 / 随后 / 再次”，没有 Contact / Momentum / Axis / Range Handoff；
- Preflight 已出现 `Static Standing Combat / Upper-body Technique Dominance`。

当前 CK 最小验证阶段，命中上述条件且没有更具体、已读取的专业 leaf knowledge 能完整覆盖对应 Gap 时：

> **必须读取 `minimum-validation-set.md`。**

### 禁止错误实现

- 不允许为了形式每次固定读三类 Pattern；
- 不允许每个 Combat 都强制读完整 Library；
- 不允许只把 Pattern 名写进 Final Prompt；
- 不允许 Routing FAIL 后直接靠 Prompt Assembly 语言润色掩盖。

---

## 4. 决策 AC-02｜Pattern Evidence Gate 位于 Phrase Construction 之前

新的强制顺序：

```text
Fighting Direction
→ Draft Planning Gap
→ Stage-2 Pattern Hit Evidence Gate
→ 必要 leaf knowledge Read
→ Concrete Action Phrase
→ State / Continuity Validation
→ Action–Camera Handoff
→ Prompt Assembly
→ Final Preflight
```

如果 Phrase 已经生成后才发现 Pattern 未命中：

```text
FAIL
→ 回到 Stage-2
→ 读取必要 Pattern
→ 重写 Phrase
```

不能只在已有 Phrase 上补“侧切、转髋、重心”等装饰词。

---

## 5. 决策 AC-03｜Motion / Energy Carry-over

原 Transition 主要验证“下一动作逻辑上能否进入”。

本轮增加一个轻量质量问题：

> **下一动作是否由上一动作仍未消失的运动、压力、旋转、支撑变化或恢复负担自然带出来？**

可继承的 Carry-over 包括：

- linear momentum；
- angular momentum / body rotation；
- contact pressure；
- support transfer；
- recovery burden；
- forced step；
- body axis deviation；
- range compression / expansion；
- environment rebound / post；
- unfinished attack / defense motion。

优先：

```text
Evasion rotation
→ 直接成为 outside entry

Wall post / recovery
→ 直接成为 pivot / counter 支点

Low-line disruption
→ forced re-step
→ 直接给下一次 angle entry
```

避免：

```text
动作完成
→ 站稳
→ 重新起架
→ 再开始下一动作
```

Motion / Energy Carry-over 是 Transition 的质量维度，不新建独立 Pattern 类型。

---

## 6. 决策 AC-04｜Action–Camera Handoff 不是 Shot List

不建立固定：

```text
Master → Close-up → Insert → Re-establish
```

也不设置 15 秒必须多少 Shot。

Action–Camera Handoff 只回答：

> **当前动作状态为什么值得改变观看方式，以及下一 Shot 如何从正在发生的动作里进入。**

内部最小结构：

```text
Current Action State
→ Camera Task
→ Shot Entry Trigger
→ Inherited Motion State
→ Observation
→ Shot Exit / Handoff
```

这些是内部导演规划变量，不默认 Dump 成字段表给用户。

---

## 7. 决策 AC-05｜Shot Entry 必须有动作动机

Action Combat 中发生 CUT / 明显景别变化时，优先从以下 Trigger 产生：

### Cut on Motion

动作已经开始，在运动尚未完成时切换观察角度；下一镜继续同一运动。

### Contact / Consequence Trigger

Contact 真正改变 Balance / Axis / Guard / Range / Position / Initiative 时切入局部或 Impact 观察；下一镜优先看到其后果，而不是重复接触本身。

### Direction / Axis Change

人物明显改变 Route、运动方向或身体轴线时改变机位，让新空间关系成为镜头信息。

### Initiative Reversal

主动权真正翻转时，Camera 可以改变关系角度或距离，让“控制关系变化”视觉化。

### Range / Level / Support Change

高→低、站立→地面、远→近、支撑脚转换等决定下一动作入口时，可使用低位 / 局部 / Relationship Shot。

### Occlusion / Match Motion

身体、前景、墙柱、快速穿越等自然遮挡可以成为 Cut Bridge，但必须继承同一动作方向和 Momentum。

### Environment Boundary

Fight-space 从开放区压到墙、门框、楼梯等边界时，Camera 可以跟随空间约束改变，而不是机械回到同一中景。

不要求每场使用全部 Trigger。

---

## 8. 决策 AC-06｜Cut 不应等动作完成后才发生

优先：

```text
Shot A：动作启动 / 压力建立
→ CUT while motion is alive
→ Shot B：同一动作继续 / Contact / Reaction
→ 下一动作从 Reaction 直接发生
```

避免：

```text
Shot A：完整动作 + 完整反应 + 站稳
→ CUT
→ Shot B：重新起架开始下一动作
```

跨镜至少继承一类 Active Motion，并同时保持必要 Spatial State：

```text
Active Motion / Contact / Pressure / Recovery
+
Position / Direction / Axis / Range / Left-Right
```

这比单纯“Cut 后位置一致”更严格。

---

## 9. 决策 AC-07｜Camera Coverage 由信息变化驱动，不做对称景别循环

避免自动形成：

```text
Medium → Close → Medium → Close
```

镜头变化应对应：

- 新的动作信息；
- 新的空间关系；
- 新的 Control / Initiative；
- 新的 Level / Support；
- Signature Moment；
- 观众可能丢失空间关系，需要 Re-establish。

因此 Re-establish 不是“每次特写后必回中景”，而是空间可读性真的有风险时才使用。

---

## 10. 决策 AC-08｜Action–Camera 必须在 Final Prompt 中耦合外显

Combat Prompt 不应只在动作段之后追加一个泛化 Camera 段：

```text
“关键接触时切近，随后回中景”
```

优先把关键 Camera Handoff 锚定在 Action Spine 内：

```text
她开始沉身从高线下穿时，镜头随下沉短暂降低；
在脚步跨过对方支撑线、对方被迫重新踩稳的瞬间切到低位近景，
下一镜继续同一失衡反应并立刻拉回双方新的斜侧关系。
```

只外显对成片真正有价值的少量 Handoff，不把 Final Prompt 写成逐 Shot 技术表。

---

## 11. 决策 AC-09｜明确一镜到底时不强制 Editorial Handoff

如果用户明确要求 One-take / 一镜到底：

- 不强制 CUT Trigger；
- 仍使用 Action ↔ Camera Handoff 思想组织单 Shot 内的 Camera Movement；
- Camera 的 Route / Speed / Stop / Reframe 仍应由 Action State Change 触发；
- 仍禁止无摩擦漂浮式跟拍。

所以 Action–Camera Handoff 高于“是否 Cut”，它描述的是摄影如何响应动作。

---

## 12. 决策 AC-10｜Runtime 放置方式

新增轻量 Runtime：

`references/tasks/action-combat-video/action-camera-handoff-playbook.md`

职责：

- Stage-2 Pattern Hit Evidence Gate；
- Motion / Energy Carry-over；
- Action–Camera Handoff；
- Action-triggered Cut / Reframe；
- Handoff Preflight。

`action-combat-video/index.md` 负责强制接线，不把所有细节重复进去。

不新增：

- 第二套 Camera Control；
- 第二套 Choreography Engine；
- 固定 Shot Template；
- 新 Pattern 类型；
- 固定 Cut 数量。

---

## 13. Runtime Mandatory Path

更新后的 Combat 主链：

```text
Core + Choreography + 专项 Playbook
→ Fighting Direction
→ Stage-2 Gap Detection
→ Pattern Hit Evidence Gate
→ 必要 Pattern / Leaf Knowledge
→ Concrete Action Phrase
→ State Validation
→ Motion / Energy Carry-over Check
→ Action–Camera Handoff Planning
→ Camera / Spatial Coordination
→ Prompt Assembly
→ Combat Final Preflight
→ FAIL rewrite
→ Delivery
```

当 Combat Camera 明确为 one-take 时，Action–Camera Runtime 仍负责 movement/reframe handoff，但不要求 editorial cut。

---

## 14. 新 Failure Signatures

只增加少量可用于统一 Gate 的签名，不为每个签名建模块：

```text
Stage-2 Routing Evidence Missing
Action–Camera Decoupling
Dead-motion Cut / Post-action Cut
Kinetic Handoff Loss
Coverage Patterning / Symmetric Shot Cycling
```

解释：

- `Stage-2 Routing Evidence Missing`：该命中执行知识但没有实际读取；
- `Action–Camera Decoupling`：Camera 只是动作完成后的附加 Coverage；
- `Dead-motion Cut / Post-action Cut`：总在动作结束、人物站稳后切镜；
- `Kinetic Handoff Loss`：跨动作 / 跨镜只继承位置，不继承运动或压力；
- `Coverage Patterning`：机械 Medium / Close 循环，没有信息动机。

---

## 15. G01 Regression Gate

继续使用同一个办公室案例，不换 Golden Scenario。

### Gate A｜Pattern Hit Evidence

必须能看到：

- `minimum-validation-set.md` 被实际读取，或存在更具体且足以覆盖当前 Gap 的 leaf knowledge；
- 最终动作能指出至少一个 Movement / Technique / Transition Detail 的真实实例化；
- 不允许只写“中国武术电影化”标签。

### Gate B｜Upper-body Dominance

Movement 必须主动改变至少一类：

- Level；
- Route / Angle；
- Axis；
- Range；
- Position；
- Support / Balance。

不能只是“转髋 / 脚步”服务前臂控制。

### Gate C｜Motion / Energy Carry-over

关键 Transition 中至少应能观察到：

- 前一动作残余 Momentum / Contact / Support / Recovery；
- 下一动作直接利用该状态；
- 不是 Neutral Reset 后重新开始。

不使用固定次数配额。

### Gate D｜Action–Camera Handoff

如果 Final Prompt 使用 Cut / 景别变化：

- 关键 Cut 有明确动作 Trigger；
- 至少一个 Cut 发生在 Motion alive 状态，而不是动作全部完成之后；
- Shot B 继续 Shot A 的 Motion / Contact / Reaction / Pressure；
- Camera Change 与 Movement / Contact / Initiative / Range / Level / Environment 的信息变化对应；
- 不出现机械 `中景 → 特写 → 中景` 循环。

### Gate E｜Prompt Coupling

最终 Prompt 的 Camera 关键语句应锚定具体 Action Moment，而不只是末尾泛化说明。

---

## 16. 实施顺序

```text
AC-Step 1
新建本 Spec

AC-Step 2
新建 action-camera-handoff-playbook.md

AC-Step 3
修改 action-combat-video/index.md
→ Pattern Hit Evidence Gate
→ Action–Camera mandatory/conditional routing
→ Final Preflight 新 Gate

AC-Step 4
固定 G01 再跑一次 Interactive → Final Prompt

AC-Step 5
检查真实 Read List + Final Prompt
→ Pattern Hit
→ Upper-body
→ Carry-over
→ Action–Camera Handoff

AC-Step 6
只有仍持续失败时，再决定是否扩 Pattern Knowledge 或继续增强 Camera grammar
```

---

## 17. 当前边界

本 Spec 不宣称：

- 已完成 Generated Video PASS；
- 已证明最小 Pattern 知识量足够；
- 已证明 Action–Camera Handoff 对所有模型稳定；
- 已开放完整武术知识库扩建。

当前目标只是：

> **让真实 Runtime 先正确命中已经存在的执行知识，并让动作与摄影共享同一个运动状态与连续性链。**
