# Action–Camera Handoff Playbook

## 1. 职责

本文件是 Action Combat 的轻量桥接 Runtime。

它不替代：

- `core-playbook.md` 的 Combat State / Continuity；
- `choreography-playbook.md` 的动作编排；
- 专项 Combat Playbook 的具体动作语言；
- `camera-direction/control.md` 的通用摄影术语与镜头规则；
- `prompt-assembly/control.md` 的最终序列化。

它只负责七件事：

1. Stage-2 Execution Knowledge 是否真的命中；
2. Concrete Choreography 是否具有 Model Execution Realizability；
3. 动作之间是否存在 Motion / Energy Carry-over；
4. Base Viewing Priority 与 Camera Hard Constraint 是否被正确区分；
5. Camera 是否由正在发生的动作状态变化触发；
6. 关键动作瞬间是否存在值得改变观看方式的 Viewer Experience Opportunity；
7. Cut / Reframe 后是否继承仍然活着的运动，而不只是位置连续。

核心原则：

> **Action 决定 Camera 为什么变化；Camera 不能把连续动作切成重新开始的动作块。**

> **Base Viewing Priority 决定默认怎么看；Camera Hard Constraint 决定什么绝对不能违反。两者正交。**

> **Camera Accent 不是逐动作配镜头；普通动作继续当前 Shot，只有高价值动作信息或观看体验变化才触发 Camera 介入。**

> **Concrete Detail 必须服务模型执行；Prompt 更细但成片更差，仍然是 FAIL。**

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

## 2.5 Model Execution Realizability Gate

真实 G01 成片已经证明：**Prompt-level textual specificity 上升，不保证 Generated-video quality 上升。**

当动作描述越来越细，却同时要求模型追踪过多独立肢体、Contact、状态、Camera 和 Negative 时，模型可能发生：

- 动作碎片化；
- 上肢动作被优先保留；
- Footwork / Support / Route 丢失；
- Camera 退回保守中景；
- Motion Handoff 在成片中消失。

因此 Concrete Action Phrase 除“够具体”外，还必须通过下面的可执行性检查。

### A. Motor Driver First

对于 Whole-body / Movement-driven Fighting Direction，Phrase 应先让模型理解主要身体运动驱动：

```text
Whole-body / Support / Route Driver
→ Technique
→ Opponent Response
→ Position / Balance Consequence
→ Continuation
```

避免长期：

```text
Forearm / Wrist / Shoulder / Arm Technique
→ 最后补一句侧步 / 转髋 / 降低重心
```

具体上肢动作可以存在，但不能连续多个关键 Phrase 都成为主要因果驱动。

### B. Feet-fixed Test

内部检查：

> 如果删除脚步、支撑、Route、Level、Axis、Position 变化，这段主要攻防是否仍几乎可以原地完成？

若 yes，且当前 Fighting Direction 明确需要 Whole-body / Movement-driven Combat，则 FAIL：

`Upper-body Semantic Dominance / Static Standing Combat`

修复必须改变动作主驱动，不是机械再加一个踢腿词。

### C. Instruction Saturation

同一短动作窗口若同时要求模型精确追踪：

```text
多个独立肢体动作
+ 多个 Contact 点
+ 多个 State Consequence
+ 精细 Footwork / Axis
+ Camera Change
+ Audio Accent
+ 多条 Negative
```

应视为 `Instruction Saturation / Micro-choreography Overconstraint` 风险。

压缩时优先：

```text
删除重复身体局部细节
→ 合并同一动力链中的次要上肢动作
→ 删除重复 State 解释
→ 删除低价值 Camera / Audio 细节
→ 删除重复 Negative
```

必须保留：

```text
Motor Driver
+ 关键 Technique
+ Opponent Response
+ Balance / Position / Range 后果
+ Continuation Entry
```

**压描述复杂度，不压动作连续性。**

### D. Effective High Granularity Everywhere

High / Medium / Low 不能只看文字长短。

如果多个连续 Phrase 都要求模型追踪多个肢体、多个 Contact、多个空间状态，即使标成 Medium / Low，仍属于：

`Effective Granularity Flattening / Instruction Saturation`

- High：只展开 Major Reversal / Signature 所需关键局部因果；
- Medium：优先整身运动 + 关键 Technique + 后果；
- Low：只保留 Motion Handoff 所需动作桥梁。

### E. Upper-body Semantic Dominance

不做机械词频配额，但要检查：

> 连续多个关键 Phrase 的主要因果是否仍由 Hand / Forearm / Wrist / Shoulder / Arm Control 驱动？

如果 yes，而 Movement 只作为修饰语出现，则即使 Prompt 中写了“侧切 / 转髋 / 降低重心”，也不能判 Whole-body PASS。

### F. Prompt–Video Execution Divergence

真实成片反馈优先级高于 Prompt 文本观感。

如果相同 Golden Scenario 的新版 Prompt：

- 文本更具体；
- Static Gate 更多；

但真实视频的 Action Continuity / Whole-body Contribution / Camera Mobility 明显下降，则判：

`Prompt–Video Execution Divergence / Generated Video Regression`

此时优先检查 Instruction Saturation、Upper-body Semantic Dominance、Camera Strategy Overconstraint，不继续增加更多动作术语。

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
→ Camera Hard Constraint Check
→ Base Viewing Priority
→ Viewer Experience Opportunity（可选）
→ Camera Task
→ Shot Entry Trigger
→ Inherited Motion State
→ Observation
→ Shot Exit / Handoff
```

这是导演规划结构，不默认作为字段表输出。

`Camera Hard Constraint Check` 先判断当前摄影手段是否被 One-take / Fixed Camera / No Cut 等明确边界限制；只有通过 Hard Constraint 的实现方式才进入后续 Camera Task。

`Base Viewing Priority` 不是固定 Shot Template，只决定在没有更强 Action Trigger 时默认优先看清 / 感受什么。

`Viewer Experience Opportunity` 不是每个 Action 都必须填写；它只用于判断某个动作瞬间是否值得从“看清动作”进一步升级为“让观众感受到威胁 / 冲击 / 失衡 / 距离压缩 / 主动权翻转”。

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
- 恢复新的空间关系；
- 让观众短暂体验逼近威胁、冲击、失衡或距离突然压缩。

---

## 4.5 Camera Decision Hierarchy

Camera 运行时按以下优先级处理：

```text
用户明确 Camera Hard Constraint
> Base Viewing Priority
> Action-triggered Camera Handoff
> Perceptual Impact Accent
> 装饰性 Camera Variation
```

其中：

- `Camera Hard Constraint` 只限制摄影手段，不改变 Combat 动作目标；
- `Base Viewing Priority` 是默认观看倾向，不是固定景别 / Cut Pattern；
- Action-triggered Handoff 与 Perceptual Accent 必须在 Hard Constraint 允许范围内寻找实现；
- 如果一个 Camera Accent 会违反 Hard Constraint，必须换实现方式，而不是忽略 Hard Constraint。

例如：

```text
Base Viewing Priority = 电影冲击体验优先
Hard Constraint = One-take
```

可以使用：Near-lens、快速推近 / 拉开、绕侧、Camera Height Change、关系角度变化；不能使用 Editorial Cut。

```text
Base Viewing Priority = 完整动作可读优先
Hard Constraint = Fixed Camera
```

必须保持固定机位，但仍可通过动作进入 / 离开构图、前景遮挡、景深、主体距离变化和构图内关系来强化动作；不能偷偷跟拍。

---

## 5. Action-triggered Camera Change

Action Combat 的 Camera Change 优先由动作信息变化触发，而不是为了“更电影”随机切换。

所有 Trigger 先经过 Camera Hard Constraint Check：如果当前 Hard Constraint 禁止 Cut / 禁止 Camera 位移，则将触发转换为允许的 Reframe / 机内关系变化 / 动作调度方式，而不是直接丢掉动作信息。

### 5.1 Cut on Motion

动作已经开始，在 Motion 尚未结束时 Cut；下一镜继续同一个动作。

仅在 Camera Hard Constraint 允许 Cut 时使用。

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

人物发生明显 Route / Direction / Body Axis 改变时，可改变机位或跟拍方向，让新关系变得可读；若 Hard Constraint 禁止位移，则改用构图内动作路线 / 允许的 Reframe 表达。

### 5.4 Initiative Reversal

主动权翻转时，可改变 Relationship Angle / Distance，使新的控制关系视觉化；若 Hard Constraint 限制 Camera Movement，则优先让角色关系在当前 Camera Boundary 内完成视觉翻转。

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
- Cut 后人物不能无原因换侧 / 换位；
- Camera Hard Constraint 允许 Cut；若 No-cut / One-take，则遮挡只作为连续镜头中的视觉过渡，不形成 Editorial Cut。

### 5.7 Environment Boundary

Fight-space 从开放区域进入墙、门框、走廊、楼梯等边界时，Camera 可以跟随空间约束改变。

不是为了环境丰富，而是环境已经改变动作路线。

### 5.8 Perceptual Impact Trigger / 主观体验触发

Camera 不只负责“把动作拍清楚”。少数关键动作瞬间，如果存在明显的**观看体验价值**，可以改变观察方式，让观众直接感受到正在发生的威胁、冲击或身体状态变化。

内部判断：

```text
Action State Change
+ Viewer Experience Opportunity
+ Camera Hard Constraint Check
→ 是否值得且允许 Camera Accent？
```

只有值得且允许时才介入；普通连接动作默认继续当前 Shot / 当前 Camera Path。

可用体验类型包括但不限于：

#### Threat POV / Near-lens

攻击快速逼近某一角色的视觉空间时，可短暂采用主观或近主观视角，让拳、脚、武器或身体压迫快速逼近镜头。

例如：

```text
男方右拳突然压进女方视线
→ Camera 短暂贴近她的主观观看位置
→ 拳锋逼近镜头
→ 她在命中前侧闪
→ Camera 顺拳势从她肩侧切出
→ 继续同一记挥空动作
```

要求：

- POV / Near-lens 必须短促；
- 不能把整个 Combat 变成固定第一视角；
- Cut / Reframe 后继续原来的攻击方向和 Momentum；
- 若 Hard Constraint 禁止 Cut，则以连续 Camera Movement / Near-lens pass-by 完成同样体验。

#### Impact Consequence Close-up

关键命中值得强化时，可以切近受击区域，但目标不是“展示拳碰到脸”本身，而是强化**Contact 后果**。

例如：

```text
女方一拳击中男方侧脸
→ 接触瞬间进入受击侧近景 / 特写
→ 看见头部、肩轴被冲击带偏
→ 下一镜直接继承这股偏转
→ 她从新形成的外侧角度继续进入
```

如果局部镜头只看到“打中哪里”，却丢失受力、轴线、Reaction 与下一动作入口，则价值不足。

若 Hard Constraint 不允许切近 / Camera 位移，不强行生成 Close-up；改为让 Impact Consequence 在当前允许观察边界中变得更可读。

#### Near-miss / Whip-by

攻击几乎擦过人物或镜头时，可利用快速掠过前景 / 镜头边缘形成威胁感和自然 Cut Bridge，但动作方向必须连续；No-cut 时仍可作为镜内 Whip-by。

#### Body-mechanics Detail

当低扫、支撑转移、失衡、膝髋变化、落地、抱摔入口等真正决定后续动作时，可短促观察脚步 / 支撑 / 髋部 / 重心，而不是为了“有特写”机械拍局部。

#### Range-compression Shot

双方从开放距离突然压进贴身、抱摔或身体压迫时，可以通过 Camera 靠近、改变关系角度或短促局部强化距离被压缩的体感；Fixed Camera 时改由角色向 Camera / 构图边界的距离变化完成。

#### Initiative / Reaction Experience

主动权翻转或突然反制时，可用 Reaction Shot、Relationship Angle Change 或短暂距离变化，让观众直接感到“控制权已经换人”，而不是额外文字解释；Hard Constraint 不允许 Cut 时，用连续关系变化实现。

### Perceptual Trigger 约束

- **不是每个动作都配一个 Camera Accent。**
- 不设置 POV / Close-up / Insert 数量配额；
- 同一短窗口连续触发多个体验型镜头时，应检查 Camera Complexity 与 Instruction Saturation；
- 如果当前 Shot 已经能同时看清动作并产生足够冲击，就不为变化而变化；
- Perceptual Accent 必须依附真实 Action State，不能先决定“这里要一个酷炫 POV”再反向编动作；
- 体验型镜头之后不默认立刻回中景，只有空间关系真的可能丢失时才 Re-establish；
- 任何 Accent 都必须服从 Camera Hard Constraint。

触发滥用时判：

`Perceptual Accent Overuse / Camera Accent Overmapping`

---

## 6. Live-motion Cut Contract

本节只在 Camera Hard Constraint 允许 Cut 时生效。

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

Shot Scale / Camera Position 应由当前信息需要和 Camera Hard Constraint 共同决定。

### Camera Accent Density

默认关系是：

```text
普通连接动作
→ 继承当前 Shot

动作信息 / 观看体验出现高价值变化
→ Camera Accent / Reframe / Cut 候选
```

因此：

- 一段连续 Combination 可以由同一个移动镜头覆盖多个动作；
- 一个重要动作也可能在内部包含一次高价值 Cut；
- Camera Accent 数量与 Action 数量没有一一对应关系；
- **禁止把 Action–Camera Coupling 实现成“每个动作后面附一个镜头说明”。**

### Re-establish 条件

只有在局部镜头后观众可能丢失：

- 双方位置；
- Range；
- Axis；
- Fight-space 边界；

才需要 Re-establish。

因此“特写后立刻回中景”不是默认规则。

### Camera Strategy Interpretation

Base Viewing Priority 只能解释为**观看偏好**，不能序列化成固定 Shot Pattern。

例如选择“完整动作可读优先”时，仍允许在真正改变动作理解或观看体验、且 Hard Constraint 允许时：

- Route / Direction 变化 → 侧跟 / 改关系角度；
- Level Drop → Camera 随身体降位；
- Support Change → 必要低位局部；
- Initiative Reversal → 改 Relationship Angle / Distance；
- Fight-space Boundary → 重新组织机位；
- Threat Approach → 短暂 POV / Near-lens；
- Impact Consequence → 受击侧近景 / Reaction；
- Range Compression → Camera 靠近或改关系角度。

如果 Base Viewing Priority 被执行成长期稳定中景、只有 Contact 才短暂切近，判：

`Camera Strategy Overconstraint / Camera Mobility Underfill`

如果 Camera 实现违反用户明确 Hard Constraint，判：

`Camera Hard Constraint Violation`

---

## 8. Action Spine 与 Camera Handoff 的耦合外显

Final Prompt 的关键 Camera Handoff / Perceptual Accent 应锚在具体 Action Moment 上。

### 8.1 Global Camera Baseline 要短

Camera 独立段可以保留，但只承担全局观看基线和必要 Hard Constraint，例如：

- Base Viewing Priority；
- One-take / Fixed / No Cut 等真正硬约束；
- Camera 随真实 Route / Range / Level 改变（在 Hard Constraint 允许范围内）；
- 不无意义碎切。

禁止用一大段总体 Camera 说明替代真正的 Action-triggered Camera Moment。

### 8.2 Key Camera Moment Inline

普通连接动作不需要嵌镜头；真正高价值、且符合 Hard Constraint 的 Camera Accent 直接写进对应 Action Phrase。

避免：

> 关键接触时短暂切近，然后立刻回到中景。

优先：

> 她开始沉身从高线下穿时，镜头随身体短暂降低；脚步跨过对方支撑线、迫使他重新踩稳的一瞬切到低位近景，下一镜继续同一失衡反应，并从新的斜侧关系接住她的再进入。

体验型示例：

> 男方突然压近挥拳，拳锋快速逼近她的视线，镜头短暂贴近她的主观观看位置；她在拳头几乎占满画面前侧头闪开，镜头顺着拳势从她肩侧切出，继续同一记挥空动作。

> 她趁他回收不及一拳击中侧脸，接触瞬间切到受击侧近景，看到他的头部和肩轴被冲击带偏；下一镜不重演出拳，而是直接从这股偏转继续她的外侧切入。

如果当前 Hard Constraint 为 No-cut / One-take，上述示例中的 Cut 必须改写为连续摄影内的 Reframe / Near-lens / Height / Distance / Relationship Change，不能原样保留 Cut。

不要求所有镜头都这样展开；只外显真正改变动作理解或观看体验的 Handoff / Accent。

---

## 9. Camera Hard Constraint

Camera Hard Constraint 是**不可违反的摄影实现边界**，不是观看风格。

### 9.1 One-take / Long-take

如果用户明确要求 One-take / 一镜到底：

- 禁止 Editorial Cut；
- 仍要求 Camera Movement / Reframe 由 Action State Change 触发；
- Perceptual Impact 可以通过 Near-lens、距离压缩、短促绕位、Camera Height / Relationship Angle 改变实现，不强制 Cut；
- Movement 起点、路线、速度变化和停止点继续服从 `camera-direction/control.md`；
- Fight-space 改变时 Camera 需要重新组织关系，而不是无摩擦漂浮跟随。

### 9.2 No Cut

如果用户明确要求 No Cut：

- 禁止 Editorial Cut；
- 如果 Camera 仍允许移动，则可使用连续 Tracking / Orbit / Push / Pull / Height Change / Reframe；
- Action-triggered Camera Moment 必须转换为同一 Shot 内的连续观察变化。

### 9.3 Fixed Camera

如果用户明确要求 Fixed Camera：

- Camera Position 不做空间位移；
- 不偷偷通过 Tracking / Orbit / Dolly 破坏 Fixed；
- 是否允许 Pan / Tilt / Zoom 取决于用户具体描述；未明确时采用最小风险、克制的机内 Reframe；
- 动作路线、前景遮挡、角色距离、构图内 Level / Position 变化承担主要动态表达。

### 9.4 Hard Constraint 冲突处理

如果多个用户明确 Hard Constraint 互相冲突，例如“固定机位”同时要求“围绕人物高速环绕”，不能静默平均；应优先按用户当前最新明确要求处理，仍无法消解时才进入交互决策。

Hard Constraint 不能反向削弱 Fighting Direction / Combat Coverage；Runtime 应在边界内重新设计 Camera，而不是把动作戏改简单。

Action–Camera Handoff 高于“是否剪辑”，它描述的是摄影怎样响应动作；Hard Constraint 决定这种响应可以使用哪些手段。

---

## 10. Action–Camera Preflight

Final Prompt 输出前检查：

### A. Stage-2 Evidence

- 当前是否存在必须读取 leaf execution knowledge 的 Gap？
- 如果存在，是否真的 Read？
- Pattern / Detail 是否进入可见 Concrete Action？

失败：`Stage-2 Routing Evidence Missing`。

### B. Model Execution Realizability

- Whole-body / Movement-driven Combat 是否有清楚的 Motor Driver？
- 是否通过 Feet-fixed Test？
- 连续多个关键 Phrase 是否仍由上肢语义主导？
- 是否存在 Effective High Granularity Everywhere？
- 同一短窗口是否塞入过多独立肢体 / Contact / State / Camera / Negative？

失败：

`Upper-body Semantic Dominance`  
`Instruction Saturation / Micro-choreography Overconstraint`  
`Effective Granularity Flattening`

### C. Kinetic Handoff

- 下一动作是否利用前一动作仍未消失的 Momentum / Contact / Support / Recovery / Axis？
- 是否出现大量完整收势 + Neutral Reset？

失败：`Kinetic Handoff Loss`。

### D. Camera Motivation

- 每个关键 Cut / Reframe 是否有 Action Trigger？
- 是否只是“为了电影感”随机改变景别？

失败：`Action–Camera Decoupling`。

### E. Live Motion Across Cut

仅当 Hard Constraint 允许 Cut 时检查：

- 至少关键 Cut 是否在 Motion alive 时发生？
- Shot B 是否继续 Shot A 的动作 / Contact / Reaction / Pressure？

失败：`Dead-motion Cut / Post-action Cut`。

### F. Coverage Patterning / Strategy Overconstraint

- 是否机械 Medium → Close → Medium 循环？
- Re-establish 是否只在真的需要空间恢复时使用？
- Base Viewing Priority 是否被错误固化成保守 Shot Pattern？

失败：

`Coverage Patterning / Symmetric Shot Cycling`  
`Camera Strategy Overconstraint / Camera Mobility Underfill`

### G. Perceptual Impact / Camera Accent Density

- 当前是否存在真正值得强化的 Threat / Impact / Near-miss / Support / Range Compression / Initiative Moment？
- 如果存在，Camera 是否选择了与该体验相匹配的观察方式，而不是只写“关键接触切近”？
- 是否反过来给每个动作都加 Camera Accent？
- POV / Close-up / Insert 是否已经挤压动作连续性或造成 Instruction Saturation？
- 体验型镜头后是否继续当前 Motion / Reaction / Position，而不是 Reset？

失败：

`Perceptual Impact Underuse`（存在明显高价值体验节点但全部被保守 Coverage 吞掉）  
`Perceptual Accent Overuse / Camera Accent Overmapping`

### H. Camera Hard Constraint

- 用户是否明确 One-take / No Cut / Fixed Camera 等不可违反边界？
- 当前 Cut / Camera Movement / Reframe 是否全部在这些边界内？
- 是否为了实现 Base Viewing Priority / Perceptual Impact 偷偷违反 Hard Constraint？
- Hard Constraint 是否只限制 Camera，而没有反向把 Combat 动作缩水？

失败：

`Camera Hard Constraint Violation`

---

## 11. Failure Rewrite Priority

发生失败时：

```text
Stage-2 Evidence FAIL
→ 先补 Read / Pattern Realization

Execution Realizability FAIL
→ 先重写 Motor Driver / 压缩局部描述 / 恢复 Granularity 层级

Upper-body Semantic Dominance FAIL
→ 改变 Whole-body / Support / Route 主驱动，不机械补腿法

Kinetic Handoff FAIL
→ 重写 Transition / Phrase

Camera Hard Constraint Violation
→ 先移除违规摄影手段，在同一 Constraint 内重选 Camera Task 实现

Action–Camera FAIL
→ 重新选择 Action Trigger + Inherited Motion State

Perceptual Impact Underuse
→ 从已有动作中寻找真正的 Threat / Impact / Support / Range / Initiative 高价值节点，再决定观察方式

Perceptual Accent Overuse
→ 删除低价值 Camera Accent，让普通连接动作回到当前 Shot

Coverage Patterning / Camera Strategy Overconstraint FAIL
→ 重新按动作信息与 Viewer Experience Value 分配 Shot Task
```

不要通过增加更多 Pattern、更多动作术语、更多 Shot、更多特写或更多 Camera 术语修复。

---

## 12. 边界

- Fighting Direction / Coverage / Granularity：`choreography-playbook.md`；
- Range / Advantage / Position：`core-playbook.md`；
- 具体动作知识：当前专项 Playbook + Stage-2 leaf knowledge；
- Camera Base Viewing Priority / Hard Constraint 的交互暴露：`assets/templates/mode-interactive-output-contract.md`；
- Generated-video Execution Regression 设计真源：`docs/action-combat-video-generated-video-execution-regression-spec.md`；
- 通用 Camera 术语与轴线：`references/controls/camera-direction/control.md`；
- 最终序列化：`references/controls/prompt-assembly/control.md`。

本文件只做 Stage-2 Evidence、Model Execution Realizability 与 Action ↔ Camera 的轻量桥接，不扩成新的大系统。