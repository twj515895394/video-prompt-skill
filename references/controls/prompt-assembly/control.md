# Prompt Assembly Control

## 目标

把任务目标、素材职责、时间 / 动作、镜头、连续性、音画、风格和限制组织成一份清楚、无重复、可直接执行的导演方案。

本页负责信息优先级、组装顺序、压缩、冲突裁决和输出完整性；具体模型语法由 Model Adapter 完成。

对于 Action Combat，必须贯彻：

> **State Machine Internalized, Choreography Externalized.**  
> **状态机内化，动作编排外显。**

并追加一条强制原则：

> **Concrete Choreography In, Concrete Choreography Out.**  
> **前面已经设计具体的动作，组装阶段不能重新压缩成抽象战斗摘要。**

---

## 1. 信息优先级

```text
用户当前明确要求
→ 当前 Task / Playbook 的核心质量合同
→ 输入素材职责
→ 动作 / 时间 / 镜头关键决策
→ 风格与细节
→ 自动补全
```

### Combat 语义优先级

```text
1. 正向可见 Action Flow / Reaction / Contact / Consequence
2. Position / Range / Environment 的可见变化
3. Character Identity / Rhythm / Intensity / Signature 的可见表现
4. Camera / Audio 支持
5. 少量真正必要的 Continuity / Negative Constraints
```

> **动作语言是主体，状态解释是内部工具。**

---

## 2. 通用组装顺序

1. 任务核心与输出目标；
2. 素材职责 / 强保留边界；
3. 全局稳定项；
4. 场景、人物与初始状态；
5. 动作 / 时间流；
6. Camera Coverage / 表演 / Audio；
7. 风格与质感；
8. 少量高价值限制；
9. Model Adapter 交接。

同一信息只写一次；动态变化不要误写成全局固定项。

---

## 3. Combat Final Prompt Assembly

### 3.1 Internal State → Visible Action

内部可以是：

```text
Range: Close
Advantage: A slight advantage
Contact: Solid
Tactical: Counter-to-Counter
```

最终不要 Dump 状态表，应写成：

> A 压进短距离；B 在偏开攻击线的同时已经侧切，A 沿她的新路线立刻封入；B 不重新站稳，借刚形成的角度反击，接触让 A 肩线偏转，这个偏转又直接成为下一次进入窗口。

重点：谁移动 / 攻击、对手如何在动作过程中响应、接触如何改变身体 / 空间、下一动作怎样直接启动。

### 3.2 Executable Granularity Preservation

如果 Choreography Plan / Stage-2 Execution Knowledge 已经提供具体动作链，Assembly 必须优先保留以下信息中的必要组合：

```text
Current Body / Range State
→ Specific Physical / Weapon Action
→ Contact / Evasion / Interception
→ Opponent Immediate Response
→ Footwork / Axis / Range / Position Consequence
→ Immediate Continuation Entry
```

不能为了“简洁”把它压回：

- 连续格挡；
- 快速反制；
- 贴身缠斗；
- 持续压迫；
- 不断换位；
- 高频攻防；
- 双方持续互有来回。

这些词可以做风格摘要或次要过渡，但不能代替关键 Active Exchange。

一个简单检查：

> **如果删除“高速 / 连续 / 专业 / 高密度 / 反制 / 缠斗”等抽象词后，仍无法清楚知道人物具体做了什么，则 Assembly 过度压缩。**

Assembly 也不能走向另一极端：不要求逐拳逐脚编号、厘米级位移或关节角度。原则是：**关键因果动作具体，次要过渡压缩。**

### 3.3 Continuous Action Spine

高密度 Combat 默认使用 **Continuous Action Spine + Soft Time Anchors**。

不要默认写成：

```text
0–1.5s：动作 A
1.5–4.5s：动作 B
4.5–7.5s：动作 C
7.5–11.5s：动作 D
```

这种硬时间盒容易诱导“完成一个动作 → Reset → 下一动作”。

优先写成：

```text
First Contact（软时间锚点）
→ 一条不中断的连续攻防主链
→ Major Advantage Reversal（软时间锚点）
→ 连续推进 / Signature Moment
→ Ending（软时间锚点）
```

时间锚点只定位重要阶段，不要求锚点前完整收势，也不要求锚点后重新起架。

严格时间戳只在以下情况使用：

- 用户明确要求逐秒；
- 需要精确 Shot 边界；
- Audio / Dialogue / 外部事件精确同步；
- Model Adapter 有实测证据表明严格时间轴更稳定。

即使使用 Hard Time Blocks，也必须写清跨块 Motion Handoff。

### 3.4 Action Continuity ≠ Shot Continuity

> **Continuous Action Spine 约束战斗动作与状态，不约束摄影必须一镜到底。**

Combat Final Prompt 可以动态使用：

- Master / Relationship Shot；
- Medium / Medium-wide；
- Contact / Weapon / Footwork Close-up；
- Extreme Close-up / Insert；
- Reaction / Impact Shot；
- Re-establish。

关键不是 Cut 数量，而是 Cut 的信息价值和动作继承。

跨镜必须尽量继承：

```text
Position / Left-Right
+ Action Direction
+ Contact
+ Momentum
+ Body / Weapon Axis
+ Range
+ 当前动作后果
```

局部特写之后，如果观众可能丢失双方位置 / Range，应安排 Re-establish；禁止 Cut 后人物回到默认站位、默认距离或重新起架。

不要把“动作可读”组装成全程中全景 / 中景 + 轻微 tracking，也不要反向规定固定数量的特写。

### 3.5 Temporal Packing + Motion Handoff

不要用“高速”代替动作密度。

较长 Active Exchange 窗口应包含连续因果动作流；动作之间优先表达：

- 同时；
- 顺势；
- 接触后立即；
- 尚未站稳时；
- 在对方收势之前；
- 沿前一动作形成的新角度 / 动量 / Range；

而不是主要依赖“然后 / 随后 / 再次”。

压缩时必须保留至少一类 Motion Handoff：Contact、Reaction、Momentum、Footwork、Body Axis、Range / Position。

### 3.6 Initiative Handoff Externalization

不要只写：

- “双方不断反制”；
- “主动权来回切换”；
- “女方迅速抢回主动”。

关键 Initiative Handoff 应在具体动作中表现：

```text
A 的攻击尚未完成
→ B 利用仍存在的 Contact / Footwork / Axis / Range / Recovery Window 改变 A 的动作
→ A 被迫立即响应
→ B 从同一运动链里接管下一次动作入口
```

可用语义包括：尚未收势、接触后立即、脚步尚未落稳、肩轴未回正、顺被偏开的线路、借仍未断开的抓控点等；这些不是固定关键词。

避免反复出现：

```text
A 完成一组攻击
→ B 开始反击
```

### 3.7 Kinetic Scope Externalization

如果内部规划存在明显 Whole-body / Position / Range / Axis 变化，Final Prompt 必须把它们写出来。

禁止把完整战斗压缩成大量：

- 抬臂格挡；
- 抓手腕；
- 压上臂；
- 原地短打；

却遗漏脚步、膝髋、躯干、重心、绕位、逼退、侧切、Range / Axis 改变。

不要求固定动作配额；只要求最终动作语言真实兑现当前 Kinetic Scope。

### 3.8 Visible Advantage

不要写“男方占优 / 女方逆转”作为主要表达。

把优势转成可见控制：

- 谁迫使对手持续 Defense；
- 谁控制 Range / Angle / Route；
- 谁逼对手退位或恢复；
- 谁通过具体动作改变对方 Axis / Position；
- 谁在 Counter 尚未结束时抢走 Initiative。

角色抢主动方式应符合 Character Identity，不把双方都写成同一种 Counter 模板。

### 3.9 Combat Intensity

Continuous 不等于全程同速。

通过 Exchange Frequency、Contact Weight / Pressure、Advantage Pressure、Kinetic Scope、Environment、Camera / Audio Accent 形成有层次的强度变化。

局部降速可以仍然很强，只要 Combat Pressure 没有消失。

### 3.10 Camera Mobility + Editorial Coverage

> **Stable ≠ Static；Mobile ≠ One-take。**

Camera Mobility 描述单个 Shot 内如何跟随 Position / Range / Axis / Route；Shot Scale / Editorial Coverage 描述整段 Combat 如何选择观察距离和 Cut。

高动作复杂度可以降低无必要 Camera Complexity，但不能自动变成：

- 全程一个机位；
- 全程中全景；
- 只允许 tracking / dolly；
- 禁止 Close-up / Insert / Impact / Reaction。

根据当前动作信息动态组织：

```text
空间关系清楚时用 Master / Relationship
→ 关键 Contact / Weapon / Footwork 用局部 Shot 强化
→ Advantage / Reaction 需要时短促靠近
→ 空间关系可能丢失时 Re-establish
```

不设置 Shot 数量或景别配额。

### 3.11 Ending Coverage Protection

Ending 的结果可以来自用户已确认的导演意图，但 Assembly 必须保护 Active Exchange Budget。

High Coverage 短 Combat 中：

- Ending 应继承最后一次 Contact / Position / Momentum / Advantage；
- 不把人物重新摆成静态 Pose 后再长时间对视；
- 不让呼吸、眼神、慢推镜等自动占用最后数秒；
- 如果 Ending 文本比主要 Active Exchange 更细、更长，应优先压缩 Ending；
- 用户明确要求长悬停 / 情绪收尾时除外。

Assembly 不新增“最后停几秒”的用户问题；这是内部 Coverage / Serialization 责任。

---

## 4. Action Language Dominance

Combat Prompt 不设置机械字数比例，但语义上必须满足：

- 具体 Action / Reaction / Contact / Consequence 是主体；
- State / Continuity / Negative 只做支撑；
- Camera / Audio 不抢走动作主体；
- Meta 解释不能比真正动作更长；
- **Camera / Audio 的细节不能明显高于主要身体动作的具体程度。**

如果一段 Prompt 大部分在写“保持连续、不要瞬移、状态正确、符合物理”，或者 Camera / Audio 写得非常具体而真正攻防只剩几句概括，应判组装失败。

---

## 5. Preserve Causality During Compression

压缩优先删除：

1. 重复状态解释；
2. 重复连续性提醒；
3. 装饰性形容词；
4. 重复 Negative；
5. 不改变战斗关系的次要动作；
6. Ending 中不必要的静态描述。

最后才缩减有效攻防。

必须优先保留：

- Specific Action → Immediate Response → Counter / Continuation；
- Contact → Reaction → Consequence；
- Motion / Initiative Handoff；
- 关键 Footwork / Range / Position / Axis 变化；
- Major Reversal / Signature 前后的因果；
- 跨 Shot 的 Action Direction / Contact / Momentum 继承；
- Ending 的真实收束状态。

> **Clarity Through Structure, Not Action Reduction。**

---

## 6. Positive-first Constraint Strategy

优先写正向可执行事实，而不是通用 Avoid List。

例如：

> “撞到桌边后身体轴线被迫偏转，下一动作直接借桌沿恢复并侧切。”

优于：

> “不要无视物理、不要瞬移、不要动作不连贯。”

Negative 只保留当前明确高风险项。

禁止自行加入用户没有要求、剧情没有依据的限制，例如无来源的 `no visible weapons`。

---

## 7. Combat Final Preflight Serialization Check

Prompt Assembly 交付前至少检查：

- Action Language 是否占主体；
- High / Medium Coverage 是否真的被 Action Flow 写满；
- **关键 Active Exchange 是否仍主要由“连续格挡 / 快速反制 / 贴身缠斗 / 不断换位”等摘要承担；**
- **删除抽象动作形容词后，是否仍能清楚理解关键身体动作因果；**
- 是否出现 3–4 秒只有一个宏动作的 Temporal Underpacking；
- 是否出现每 1–2 秒归位再起手的 Action Segmentation；
- Counter / Re-counter 是否在对方动作尚未完成时具体抢走 Initiative；
- 是否把高密度战斗切成多个硬时间盒；
- Kinetic Scope 是否在最终文字中可见；
- Character Identity / Advantage / Initiative 是否通过动作外显；
- Ending 是否过早进入静止 Pose / 对视并吞掉 Active Exchange；
- Camera 是否 Stable 但不是 Static；
- 是否把 Continuous Action Spine 错写成 one-take / 单一 Camera Path；
- 是否长期只有中全景 / 中景，缺少有信息价值的 Shot Scale Variation；
- Cut 后 Position / Direction / Contact / Momentum / Axis / Range 是否连续；
- Contact → Reaction → Consequence 是否可见；
- Camera / Audio 是否比身体动作更具体；
- Negative 是否少而有针对性。

触发 `Abstract Action Block / Non-executable Choreography Summary` 时，优先重写具体 Action Phrase，而不是追加“高速、连续、专业、电影化”等形容词。

不通过时先内部重写 Action Spine / Concrete Phrase / Camera Coverage / 压缩结构，再交付。

---

## 8. 单视频单元组装骨架

```text
视频目标：
参考与稳定锚点：
场景 / 人物初始关系：
连续且具体的动作主链（Combat 时为主体）：
关键软时间锚点 / Turning Point：
Camera Coverage / Audio：
必要连续性与高风险限制：
```

Combat 不要求机械拆成每 1–2 秒一个独立小段，也不要求整段摄影一镜到底。

---

## 9. 多镜头 / 多片段骨架

```text
全片目标与统一锚点：
素材职责：

Segment 1：
- 目标
- Action / Camera Flow
- 结尾 Handoff State

Segment 2：
- 继承上一段状态
- Action / Camera Flow
- 结尾 Handoff State

全片 Audio / Style / Continuity：
Model Adapter 入口：
```

多镜头 Shot 边界可以精确，但 Combat Action State 必须跨镜继承。

---

## 10. 冲突与适配边界

重点识别：

- fixed camera 与大幅空间追打冲突；
- High Coverage 与大段站立 / Ending Pose 冲突；
- 高 Exchange Depth + 高 Camera Complexity 超出模型承载；
- “稳定镜头”被误实现为“静态镜头”；
- “动作连续”被误实现为“不能 Cut”；
- 高密度 Combat 被锁成全程中全景 / 中景；
- 用户要求连续高手战，但时间结构是多个独立动作槽；
- Choreography 已经具体，但 Assembly 为了缩短 Prompt 又退回抽象动作块。

Model Adapter 允许改变素材引用、语言组织、同窗口复杂度、Camera Complexity、Shot Coverage 和 Phrase 序列化；不得改写剧情、人物身份、Combat Intent、Coverage 目标、核心动作因果、战斗结果。

模型能力较弱时优先：删除次要分支 → 保留关键具体动作因果 → 降低无必要 Camera Complexity → 保留高价值局部 Coverage → 拆成无缝 Phrase；不能直接把高手持续对决改成两三次简单交换，也不能把具体动作重新压成“连续攻防”。

---

## 11. 边界

- 素材职责：`reference-binding/control.md`；
- 时间 / 节奏：`timeline-rhythm/control.md`；
- Camera：`camera-direction/control.md`；
- Motion：`subject-motion/control.md`；
- Spatial：`spatial-blocking/control.md`；
- Combat Choreography：`references/tasks/action-combat-video/choreography-playbook.md`；
- 输出模板：`assets/templates/`；
- Model 语法 / 能力：`references/models/`。