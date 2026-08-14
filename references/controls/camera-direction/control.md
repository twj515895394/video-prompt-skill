# Camera Direction Control

## 目标

决定观众从哪里看、为什么移动、怎样移动、何时切换观察距离，以及镜头何时停住，使摄影与剪辑服务主体动作和叙事，而不是成为独立炫技。

本页负责镜头决策和失控约束；具体镜头术语、焦段与机位选项由 `libraries/camera-shot/` 提供。

## 何时读取

- 用户只说“高级运镜、电影级运镜、丝滑跟拍”；
- 镜头漂浮、持续环绕、像游戏视角；
- 主体动作看不清；
- 镜头运动没有起点、路线或落点；
- 多镜头景别变化杂乱；
- 需要设计焦点转移、主观视角或长镜头调度；
- 动作片 / Combat 需要在空间可读与特写冲击之间动态切换。

## 核心公式

单个 Shot：

```text
镜头任务 + 起始景别/机位 + 主运动 + 方向/路线 + 速度变化 + 聚焦对象 + 停止状态
```

多 Shot Coverage：

```text
当前动作信息
→ 选择观察距离 / 机位
→ CUT / Movement
→ 继承 Direction / Position / Contact / Momentum
→ 必要时 Re-establish 空间
```

先回答“为什么这样看”，再决定“怎么动 / 是否切”。

## 镜头任务类型

### 建立空间

目标：交代人物位置、环境规模和行动方向。

优先：固定全景、缓慢摇移、升降建立、短距离进入、Master / Re-establish。

### 跟随行动

目标：保持主体可读，同时展示移动过程。

优先：侧向跟拍、后方跟随、稳定器短跟、低幅度手持。

### 聚焦信息

目标：让观众注意表情、道具、线索、动作细节或接触点。

优先：推近、拉焦转移、局部特写、Insert、Reaction、运动后定格。

### 强化情绪

目标：改变人与空间的心理关系。

优先：压迫式推近、疏离式后拉、低机位、俯拍、前景遮挡、人物 Reaction Close-up。

### 制造冲击

目标：配合动作爆点、转场或信息反转。

优先：短促推进、急停、甩镜、跟冲、Impact Shot；必须保持爆点前后可读。

## 决策顺序

1. 当前 Shot 唯一要让观众看到什么；
2. 该信息需要完整身体、关系空间，还是局部 / 接触 / 反应细节；
3. 是通过 Camera Movement 还是 Cut 更清楚地表达；
4. 若移动，起点、方向、路径和停止点是什么；
5. 若 Cut，上一镜留下什么 Action State，下一镜如何继承；
6. 运动速度 / 景别距离如何变化；
7. 是否需要 Re-establish 恢复空间关系；
8. 镜头结束时为下一镜留下什么条件。

固定镜头能完成任务时，不强制增加运镜；同样，连续跟拍能完成任务时也不强制切镜。

## 景别与动作匹配

- 远景/全景：空间、站位、完整动作、群像；
- 中全景/中景：人物关系、主要攻防、动作方向；
- 中近景/近景：眼神、面部反应、近距离身体交互；
- 特写/大特写：拳脚 / 武器 / 手部 / 接触点 / 关键道具 / 情绪爆点；
- Insert：脚步、支撑脚、握持、武器线路、环境触发物等关键动作信息；
- Re-establish：局部镜头之后重新确认 Position / Range / Axis。

避免在需要理解完整空间关系时长期只拍局部，也避免为了“动作可读”把整段锁成中全景。

## Action Continuity ≠ Shot Continuity

对于动作片 / Combat：

> **动作连续不等于摄影镜头必须连续。**

`Continuous Action Spine` 只要求动作因果与状态不断线，不要求一镜到底。

可以动态使用：

```text
Master / Relationship Shot
→ Close-up / Extreme Close-up
→ Footwork / Hand / Weapon Insert
→ Reaction / Impact Shot
→ Re-establish
```

跨镜必须尽量继承：

- Position / 左右关系；
- Action Direction；
- Contact State；
- Momentum；
- Body / Weapon Axis；
- Range；
- 当前动作后果。

Cut 后禁止人物无原因回到默认站位、默认距离或重新起架。

## 单镜头主运动规则

每个 Shot 通常只保留一个主运镜：

- 推；
- 拉；
- 摇；
- 移；
- 跟；
- 升降；
- 环绕；
- 固定；
- 主观移动。

最多再叠加一个次级变化，例如轻微拉焦或速度变化。不要把推、拉、摇、移、环绕和变焦同时塞入同一短 Shot。

**一镜只保留一个主运动，不代表整段视频只能有一个景别或一个 Shot。**

## 速度与惯性

镜头运动必须具有物理感：

- 开始前有可读起点；
- 起步可缓慢或迅速，但要与动作爆发匹配；
- 运动路线保持连续；
- 接近目标时减速或自然交给 Cut；
- 结束时停稳或留下明确 Handoff。

手持不是随机抖动，稳定器也不是无摩擦漂浮。

## 与主体动作协调

- 主体动作强：降低无必要 Camera Chaos，**不等于禁止 Cut、特写或景别变化**；
- 主体动作弱：镜头可承担情绪推进；
- 爆点瞬间：可通过 Impact Shot / Push / Cut 短暂强化，随后恢复可读关系；
- 主体改变方向：镜头 / 下一 Shot 必须继承动作方向与空间轴；
- 多人互动：镜头围绕关系轴组织，不随意跨轴；
- 局部特写之后若空间关系可能丢失，优先 Re-establish，而不是取消特写。

## Combat / High-action Coverage 建议

动作电影可以在以下观察策略之间动态切换：

- Master / Establishing：先交代双方位置、Range、空间限制；
- Relationship Medium：看清主要连续攻防；
- Contact Close-up / Impact：强化真正改变状态的接触；
- Footwork / Weapon / Hand Insert：展示决定下一动作的信息；
- Reaction Close-up：强调威胁、受击、优势变化；
- Re-establish：局部镜头后重新确认空间。

不规定数量，不要求每场都使用全部类型。

正确目标不是“特写越多越电影”，而是：

> **每个镜头都承担动作信息，同时整段仍看得懂谁在哪里、动作从哪里来、下一步为什么发生。**

## 镜头轴线与方向

跨镜头需要保持：

- 人物左右位置的基本关系；
- 行进 / 攻击方向；
- 视线方向；
- Contact 与 Momentum 延续；
- 光源和空间入口；
- 180 度轴线或明确的跨轴过渡。

若必须跨轴，应使用中性正面镜头、明显环绕过程或空间建立镜头作为过渡。

## 焦点控制

拉焦或焦点转移必须对应信息转移：

- 前景人物 → 后景线索；
- 武器 / 手部 → 人物反应；
- 接触点 → 受力后果；
- 眼睛 → 手中物体。

不要让焦点无理由呼吸、反复漂移或同时要求全画面浅景深与全部清晰。

## 高频失败模式

### 镜头漂浮

现象：像脱离设备在空中无惯性滑动。

修复：写清起点、短路线、设备感、减速和停止点。

### 运镜过度

现象：镜头持续绕、冲、摇，主体任务不清。

修复：单 Shot 保留一个主任务；用更清楚的 Cut / Re-establish 替代无意义复杂运动。

### 主体与镜头竞争

现象：人物高速运动，镜头又反向快速移动，动作关系丢失。

修复：降低单 Shot Camera Complexity；可选择更宽 Relationship Shot，或用短促局部镜头后重新建立空间。

### Combat Camera Coverage Lock

现象：为了“可读”整段几乎只有中全景 / 中景 + 轻微跟拍，缺少动作电影必要的局部观察与冲击变化。

修复：保留空间锚点，同时允许有价值的 Contact / Footwork / Weapon / Reaction / Impact Shot；必要时使用 Re-establish 恢复关系。

限制：禁止把 `Continuous Action Spine` 理解成“不能 Cut”。

### Cut-induced Action Reset

现象：每次 Cut 后人物回到默认姿态 / 默认距离，像重新开始一个动作。

修复：在 Cut 前后明确继承 Direction、Contact、Momentum、Position / Range / Axis，使下一 Shot 从上一 Shot 正在发生的动作状态直接继续。

### 假手持

现象：抖动周期机械、幅度恒定。

修复：使用轻微、不规则但低幅度的呼吸式手持，并保持构图可读。

### 游戏稳定器感

现象：镜头无摩擦穿行、永不减速。

修复：缩短运动距离，增加起步和停稳，保留真实设备限制。

### 无结束状态

现象：镜头到最后仍在高速运动。

修复：在最后节拍减速、锁定对象、完成 Cut Handoff 或自然停止。

## 负向限制使用规则

- 先完成正向镜头设计，再补负向限制；
- 每条 Prompt 只选最危险的 2-4 项；
- 负向限制不能替代起点、路线、Cut Handoff 和落点；
- 不无差别堆叠所有镜头失败词。

## 输出模板

单 Shot：

```text
镜头任务：
起始景别与机位：
主体动作：
主运镜：
运动方向与路线：
速度变化：
焦点对象：
结束景别与停止状态：
```

多 Shot / Action Coverage：

```text
空间锚点 / Master：
关键 Shot 1：动作信息 + 景别 / 机位 + Handoff State
关键 Shot 2：继承上一动作 + 局部信息 / Impact / Reaction
Re-establish：恢复 Position / Range / Axis
最终落点：
```

不要为了套格式固定 Shot 数量。

## 输出前检查

- 当前每个 Shot 的任务是否清楚；
- 是否真的需要移动 / Cut；
- 单 Shot 主运镜是否过载；
- 起点、方向、路线和终点是否清楚；
- 主体动作是否仍可读；
- 动作片是否误把“可读”实现成全程中全景；
- Cut 后 Direction / Position / Contact / Momentum / Axis 是否连续；
- 局部特写后是否需要 Re-establish；
- 负向限制是否只针对真实风险。

## 边界

- 时间节拍读取 `timeline-rhythm/control.md`；
- 人物站位和空间轴线规划读取 `spatial-blocking/control.md`；
- 具体运镜术语、机位和焦段读取 `libraries/camera-shot/`；
- Combat 的 Action Continuity / Motion Handoff 真源读取 `references/tasks/action-combat-video/choreography-playbook.md`；
- 真实设备感读取 `realism-quality/control.md`。