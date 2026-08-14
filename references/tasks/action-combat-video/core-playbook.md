# Action Combat Core Playbook

## 1. 核心目标

把战斗设计成可读、连续、可执行的状态变化，而不是招式名词堆叠。

内部主链：

```text
Combat Intent
→ Combat Spatial Map
→ Beat Start State
→ Action / Camera / Audio Choreography
→ Turning / Handoff
→ Beat End State
→ Beat State Contract
→ Next Beat
```

最终交付始终是视频模型可直接执行的自然语言 Prompt，不把内部状态表直接 Dump 给用户或模型。

## 2. Battle Beat

Combat 的主要组织单位是 Battle Beat。Beat 数量不固定，根据总时长、人数、复杂度和叙事目标自动决定。

一个 Beat 默认只承担一个主要攻防目标，并包含若干连续交互节点和一个清楚的结束状态。

通用阶段可参考：

```text
观察 / 起势
→ 接触 / 试探
→ 攻防交换
→ 转折 / 爆发
→ 缠斗 / 脱离 / 重组
→ 终结 / 制服 / 收势
```

这些是可选节奏，不是强制模板。

## 3. Combat Intent

优先识别战斗目的，例如：

- 制服；
- 脱身；
- 压制；
- 保护；
- 拖延；
- 试探；
- 击败 / 终结；
- 展示实力。

Intent 影响动作选择、Beat 顺序、主导权、镜头重点和结尾落点。Quick Mode 未指定时从剧情自动推断。

## 4. Combat Spatial Map

战斗开始前内部建立轻量空间真源，只维护真正影响动作与镜头的变量：

- 人物初始位置与朝向；
- 主要环境锚点；
- 障碍、出口、死角、高低差；
- 可移动区域与通道；
- 当前 Camera Axis；
- 初始 Combat Range State。

每个 Beat 只能增量更新：

> **Position State → Movement / Interaction → New Position State**

禁止人物、道具、环境和镜头关系无因果漂移。

## 5. Combat Range State

内部可使用：远距离、长兵器距离、中距离、近距离、缠斗距离、脱离 / 重置距离。

距离变化必须由动作产生：

> **Current Range → Range Transition Action → New Range**

例如逼近、格挡后压入、推开、侧移、脱离、兵器偏转后贴身等。

不要为了状态标签而机械写标签；最终 Prompt 直接描述双方如何改变距离。

## 6. Combat Advantage State 与 Turning Event

内部维护均势 / 轻度占优 / 明显压制 / 脱离重置等主导关系，并记录优势来源：距离、速度、力量、技术、兵器长度、地形、人数、失衡、受伤或死角。

明显主导权改变必须有 Turning Event：

> **旧优势 → 转折事件 → 优势来源变化 → 新优势**

转折可以来自落空、成功格挡 / 拆招、失衡、换距、缴械、环境换位、受伤、第三人介入等。

避免机械“你一下我一下”的轮流反转。

## 7. Combat Condition State

受伤、体力、呼吸和局部功能跨 Beat 累积，但不做 RPG 数值化。

只维护对后续动作真正有影响的状态，并让它改变：

- 速度；
- 连招长度；
- 站姿 / 重心；
- 防守方式；
- 动作选择；
- Range 与 Advantage；
- 表演与呼吸。

状态不应无理由在下一 Beat 重置。

## 8. Action–Reaction Pair

关键交互使用：

> **Initiator Action → Defender Response → Contact / Outcome → State Change**

动作链必须表现双方互相影响，而不是各自完成独立招式列表。

关键命中或接触遵循：

> **Preparation → Delivery → Contact → Reaction → Recovery → Continuation**

不是每次轻触都要写满六段，但重要打击必须能看出发力、接触、受力和后续动作。

## 9. 1vN 与 Target Handoff

每个 Beat 只保留一个主交战关系；其他对手处于明确的次级状态，例如逼近、被阻挡、被击退、倒地恢复、等待切入或重新包抄。

主目标切换必须经过：

> **Current Target → Target Handoff → Spatial Re-map → New Primary Target**

Handoff 可以由新目标入画、旧目标被击退、转身、环境遮挡、新威胁介入、兵器轨迹或动作动线完成。

切换后重新建立人物朝向、Range、Camera Axis 和其他人的位置。

## 10. Camera Choreography

镜头按功能选择：

> **镜头目的 → 主体关系 → 机位 → 镜头路径 → 景别变化 → 停止点**

支持三种模式：

- Continuous / Long-take：连续性优先，动作复杂度更克制；
- Hybrid：默认，连续运动为主，必要处功能性切镜；
- Cut-driven：允许更高频切镜，但每次 Cut 都必须有动作 / 空间 /冲击理由。

Battle Beat 与 Shot 不强制 1:1。

跨 Beat 优先继承屏幕方向、人物朝向、轴线、环境锚点、结束姿态和未完成运动。

允许跨轴，但必须通过连续绕位、中性重建或动作驱动换位让观众看懂。

## 11. Audio Choreography

Audio 与 Action / Camera 同一时间链设计。

按场景需要选择：

- 环境底噪；
- 脚步 / 急停；
- 呼吸；
- 衣料 / 衣袂；
- 破风；
- 身体 / 环境碰撞；
- 兵器挥动 / 接触 / 偏转；
- BGM；
- 静默或音乐让位。

声音服务动作可读性、重量、空间感和节奏，不给每个微动作机械配音效。

## 12. 时间与速度

先拆 Beat，再分配 Soft Time Window。复杂 Beat 获得更多时间，简单 Beat 更短。

允许关键重击、极限闪避、兵器交错、腾跃转折短暂减速，但必须说明慢下来是为了看清什么，并尽快回到正常速度。

不机械按固定秒数切动作。

## 13. Beat State Contract

每个 Beat 内部结束时至少继承：

- Actor：位置、朝向、姿态 / 重心、肢体、兵器、当前目标；
- Combat：Range、Advantage、Condition、攻防趋势、未结束 momentum；
- Camera：机位关系、Axis、屏幕运动方向、镜头运动趋势；
- Environment：当前锚点、障碍关系、可用空间；
- Continuity：Visual Handoff、Target Handoff、未结束动作趋势。

下一 Beat 必须从这个状态继续，不重新解释一套初始状态。

## 14. 环境互动

环境是一级变量，但每个 Beat 只突出真正有价值的主要互动。

环境可以承担：移动、遮挡、借力、碰撞、改变站位、镜头接力。

避免为“丰富”而让角色同时使用多个无关物体。

## 15. 动作复杂度预算

默认参考：

> **1 个主攻防目标 + 2–4 个连续攻防交互节点 + 1 个结束状态**

这是可读性预算，不是硬性模板。用户动作设计本身清楚且模型可执行时，可以灵活增减。

当信息过载时，优先：拆 Beat、降低镜头复杂度、保留主动作和关键反馈。

## 16. 最终 Prompt 组装

Combat 必须最终转译为可复制 Prompt，至少包含适用的信息块：

- 场景与视觉锁定；
- 战斗总体设定；
- 动作 / 镜头 / 声音时间线；
- 声音总体设计；
- 连续性与物理约束；
- 动态选择的高风险 Negative Constraints；
- 画质与输出约束。

单镜头 / 长镜头挂接现有 single-shot 输出合同；多镜头动作戏挂接现有 multi-shot 输出合同。

## 17. 推荐现有 Controls

按需选择，不全量加载：

- `timeline-rhythm`
- `subject-motion`
- `camera-direction`
- `spatial-blocking`
- `continuity-consistency`
- `audio-visual-sync`
- `prompt-assembly`
- `realism-quality`

## 18. Libraries 选择

最多按当前缺口读取 0–2 份：

- 现代格斗：`combat-fighting-profiles`
- 武术 / 武侠：`combat-martial-profiles`
- 兵器：`combat-weapon-profiles`
- 强环境交互：`combat-environment-patterns`

用户已经明确动作语言时不额外加载无关库。

## 19. 核心失败限制

按场景动态选择最危险项：

- 禁止人物瞬移和无理由换位；
- 禁止 Range 无动作因果跳变；
- 禁止命中无受力反馈；
- 禁止 Condition 无理由重置；
- 禁止 Target 无 Handoff 瞬间切换；
- 禁止 Camera Axis 无解释翻转；
- 禁止动作 / 镜头 / 音效互相抢占导致不可读；
- 兵器场景禁止兵器变形、消失、凭空换手。

## 20. 创作自由原则

> **约束错误，不约束创作。**

以上状态、默认节奏、镜头模式、动作预算和案例都是生成工具，不是固定动作模板。不要为了“满足规则”把所有状态都显式写进最终 Prompt，也不要把同一套路复用于所有战斗。
