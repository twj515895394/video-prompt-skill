# Action Combat Video Prompt Spec

> 状态：设计中（Grill Me 持续收敛）
>
> 定位：作为现有 `video-prompt-skill` 的一级专项任务能力，不建立独立 Skill。

## 1. 目标

建立一套适用于现代动作格斗与电影武侠的视频 Prompt 专项能力，重点解决：

- 动作因果与连续性；
- 攻防关系与主导权；
- Action / Camera / Audio 三线协同；
- Beat / Shot / 空间连续性；
- 打击、受力、收招与下一动作衔接；
- 多人战主交战对象管理；
- 环境参与战斗与镜头接力；
- 武侠身法、兵器与写实物理之间的尺度控制；
- 最终输出一份详细、完整、专业、可直接复制给视频模型使用的成品 Prompt。

核心哲学：

> **先建立可读的 Battle Beat，再同步设计动作、镜头与声音；空间、受力、环境、节奏和战斗目标共同服务攻防因果；复杂度必须服从连续性与可执行性。**

## 2. 第一版范围

正式支持：

1. 现代写实 / 电影化近身格斗；
2. 电影武侠 / 武术动作。

枪战暂不进入第一版正式实现，后续复用 Combat Core 扩展。

## 3. Task 架构

```text
references/tasks/action-combat-video/
├── index.md
├── core-playbook.md
├── modern-combat-playbook.md
└── cinematic-wuxia-playbook.md
```

Quick Mode 默认只加载：

> `Combat Core + 当前一个专项 Playbook`

不同时加载现代格斗与武侠分支。

## 4. Battle Beat

Combat 的核心组织单位是 **Battle Beat**，不是招式清单。

通用骨架：

```text
起势 / 观察
→ 首次接触 / 试探
→ 攻防交换
→ 爆发 / 战术转折
→ 缠斗 / 拉开 / 再组织
→ 终结 / 制服 / 收势
```

具体任务根据时长、人数、场景和 Combat Intent 裁剪，不要求机械包含全部阶段。

每个 Beat 至少维护：

- Combat Intent；
- 当前主交战关系；
- Combat Range State；
- Combat Advantage State；
- Combat Condition State；
- 主动作 / 反应动作链；
- 镜头目标与镜头路径；
- 景别 / 角度变化；
- 双方空间与站位变化；
- 接触与受力反馈；
- 速度状态；
- 主要环境交互；
- Audio Choreography；
- Beat 结束状态；
- 下一 Beat 的衔接条件。

## 5. 三线同步编排

> **Action Choreography + Camera Choreography + Audio Choreography 必须在同一个 Beat 内同步设计。**

每个 Beat 同时回答：战斗目的、攻防关系、动作转换、镜头目的与路径、声音同步点、Beat 最终落点。

声音服务动作可读性、打击重量、空间真实感和节奏变化；禁止为每个微动作机械堆音效。

## 6. 时间控制：Beat-first + Soft Time Window

> **Beat 优先，时间柔性约束。**

先设计 Beat，再按动作复杂度和叙事权重分配软时间窗口，例如：

```text
约 0–2s｜起势与空间建立
约 2–6s｜第一次连续攻防
约 6–10s｜主导权反转
约 10–13s｜核心爆点
最后约 2s｜收势与状态落点
```

允许对爆点、速度变化、关键转折设置时间锚点；禁止为了固定秒数强塞动作。

## 7. 功能驱动镜头

Combat Camera 使用：

> **镜头目的 → 主体关系 → 机位 → 镜头路径 → 景别变化 → 停止点**

镜头服务动作，不与主体动作同时拉满复杂度。

## 8. Combat Camera Mode

### Continuous / Long-take

- 连续镜头优先；
- 依赖走位、环境遮挡和镜头绕位；
- 动作复杂度更克制；
- 更严格维护空间关系；
- 切镜极少。

### Hybrid（默认）

- 连续运动为主；
- 爆点、空间重建、攻守反转时允许功能性切镜。

### Cut-driven

- 允许更高频功能性切镜；
- 可使用冲击特写、正反打、快速空间重建；
- 仍必须遵守 Visual Handoff、轴线和空间连续性；
- 禁止用无动机乱切制造刺激。

## 9. Beat 与 Shot 解耦

Battle Beat 与 Camera Shot 不强制 1:1。

允许一个 Beat 一个连续镜头、一个 Beat 多个短镜头、多个 Beat 共享一个连续镜头。

切镜必须有功能理由，例如空间重建、爆点、攻守反转、关键受力或位置变化。

## 10. 跨 Beat 连续性与 Visual Handoff

> **连续运动优先，必要时才切镜。**

相邻 Beat 优先继承屏幕运动方向、人物朝向、镜头轴线、环境锚点、上一 Beat 结束姿态和未完成动作趋势。

切镜必须存在 Visual Handoff，可来自攻击方向、受击运动、兵器轨迹、转身 / 腾跃方向、衣摆 / 发丝、前景遮挡或主体出入画方向。

## 11. Axis Crossing

允许跨轴，但必须成为可解释的空间事件。

合法方式：

1. 连续镜头真实绕过人物完成跨轴；
2. 通过正面 / 背面 / 广角等中性镜头重新建轴；
3. 通过人物绕身、换位、腾跃越位、双方交换位置等动作驱动轴线迁移。

统一链路：

> **Old Axis → Axis-Crossing Event → Spatial Re-establish → New Axis**

禁止 Cut 后人物左右位置、朝向和攻击方向无解释翻转。

## 12. 打击反馈链

关键打击节点统一采用：

> **Preparation → Delivery → Contact → Reaction → Recovery → Continuation**
>
> **预备 → 发力 → 接触 → 受力反馈 → 收招 → 衔接**

现代格斗强调重量、惯性、失衡、疼痛感与恢复；电影武侠强调借力、身法、兵器轨迹与优雅但明确的受力因果。

## 13. Action–Reaction Pair

每个关键攻防节点采用：

> **Initiator Action → Defender Response → Contact / Outcome → State Change**

Combat 不生成彼此独立的招式列表，而生成连续交互式战斗链。

State Change 可更新 Range、Position、Advantage、Condition、Camera / Continuity State。

## 14. 动作复杂度预算

每个 Beat 默认：

> **1 个主攻防目标 + 2～4 个连续攻防交互节点 + 1 个明确结束状态**

用户输入过多招式时优先拆 Beat，而不是硬塞。

> **动作丰富度服从可读性；宁可少而清晰，也不要多而混乱。**

## 15. Combat Spatial Map

每场打斗在生成 Battle Beat 前，先建立轻量级 **Combat Spatial Map**，作为整场动作与镜头连续性的空间真源。

至少维护：环境锚点、障碍物、高低差、可移动区域、出口 / 死角、角色初始位置与朝向、初始 Range、可利用环境、主要移动通道、Camera Axis。

Beat 只能在 Spatial Map 上增量更新：

> **Position State → Movement / Interaction → New Position State**

禁止人物和环境锚点在 Beat 之间无因果漂移。

## 16. Beat State Contract

每个 Beat 必须输出内部 End State，下一 Beat 必须严格从该状态开始：

> **Beat N End State → Beat State Contract → Beat N+1 Start State**

至少维护：

- Actor State：位置、朝向、姿态 / 重心、肢体状态、武器状态、当前主目标；
- Combat State：Range、Advantage、Condition、当前攻防趋势、尚未结束的动作 / momentum；
- Camera State：机位关系、Camera Axis、屏幕运动方向、镜头运动趋势；
- Environment State：当前环境锚点、障碍物关系、可继续利用空间；
- Continuity State：Visual Handoff、Target Handoff、未完成动作趋势。

**Camera State 与 Actor State 同级进入 Contract。**

## 17. 1v1 与 1vN

第一版支持 `1v1 + 1vN`。

多人战采用主交战对象机制：每 Beat 只有一个主交战关系，其他对手必须处于逼近、包抄、被阻挡、被击退、倒地恢复、等待切入等明确状态。

### Target Handoff

主交战对象切换必须经过：

> **Current Target → Target Handoff → Spatial Re-map → New Primary Target**

合法 Handoff 可包括新对手入画、原目标被击退后暴露新目标、转身顺势带出新目标、借环境遮挡切换、新目标主动形成威胁、武侠中通过兵器轨迹 / 腾跃落位 / 衣摆 / 建筑结构切换。

切换后必须重新建立当前主目标、其他人位置、Range State、Camera Axis 与人物朝向。

## 18. 环境作为一级战斗变量

环境可参与：

> **移动 → 遮挡 → 借力 → 碰撞 → 改变站位 → 镜头接力**

每个 Beat 最多突出 1 个主要环境交互。

## 19. 速度变化

Skill 可自动设计有限速度变化，但必须功能驱动：正常速度承担主要攻防推进；重击、兵器交错、极限闪避、腾跃转折可短暂减速；一个 Beat 原则上最多一个速度变化重点；减速后尽快恢复正常速度；必须明确慢下来是为了看清什么。

## 20. 默认 Beat 节奏画像

### 现代格斗默认倾向

> **快速观察 → 首次接触 → 连续压迫 → 攻守反转 → 近身缠斗 / 控制 → 终结**

停顿更短、交换更直接、接触密度更高、冲击峰值更短促，强调压迫、失衡、恢复。

### 电影武侠默认倾向

> **对峙 / 留白 → 试招 → 拆招往复 → 身法 / 兵器转折 → 高潮交换 → 收势**

留白更明显，强调读招、接招、化解，爆发前允许呼吸空间，更强调身法 / 兵器轨迹和节奏美感。

以上仅是默认倾向，不是固定模板；Combat Intent、时长、人数、强度等级可以覆盖。

## 21. Combat Range State

显式维护攻防距离，现代格斗与电影武侠共用。

基础状态：远距离、长兵器距离、中距离、近距离、缠斗距离、脱离 / 重置距离。

距离变化必须经过明确动作：

> **Current Range State → Range Transition Action → New Range State**

禁止人物无因果从远距瞬间进入贴身状态。

## 22. Combat Advantage State

显式维护双方 Combat Advantage State。

基础状态：均势、A 轻度占优、A 明显压制、B 轻度占优、B 明显压制、暂时脱离 / 重置。

采用：

> **优势状态 + 优势来源 + 转折原因**

优势来源可以是距离、速度、力量、技术、兵器长度、地形、人数、失衡、受伤、死角等。

## 23. Advantage Turning Event

Beat 之间的明显主导权转移必须经过明确 Turning Event：

> **原优势状态 → Turning Event → 优势来源改变 → 新优势状态**

一个 Beat 原则上最多只发生一次主要主导权反转；若没有 Turning Event，则默认延续上一 Beat 的主导权趋势。

## 24. Combat Condition State

角色的受伤、疲劳与呼吸状态必须跨 Beat 累积维护，但不做数值化 RPG 模拟。

采用：

> **状态标签 + 对后续动作的可见影响**

可维护体力、呼吸、受伤、局部功能状态；Condition 必须真正改变后续 Beat 的速度、站姿、防守方式、动作选择、Range、Advantage 和镜头表现。

## 25. Combat Intent

Combat Intent 作为 Combat Core 显式核心变量，至少支持：制服、脱身、压制、保护、拖延、试探、击败 / 终结、展示实力。

直接影响：

> **Beat 顺序 → 攻防策略 → 动作选择 → 镜头重点 → 最终落点**

Quick Mode 用户未指定时自动从剧情推断，不追问。

## 26. 强度等级

### 现代格斗

- Level 1｜写实近身格斗；
- Level 2｜电影化现代动作（默认）；
- Level 3｜强化动作片，但不进入超级英雄式无重量感战斗。

### 电影武侠

- Level 1｜写实武术；
- Level 2｜电影武侠（默认）；
- Level 3｜高武武侠，但不进入剑气、能量波、御剑、法器、长距离无支撑飞行等仙侠体系。

## 27. 武侠兵器

第一版正式支持：刀、剑、枪、棍。

兵器 Beat 重点控制：持握、攻防距离、轨迹、格挡 / 招架、借力 / 偏转、接触反馈、重心、镜头协同与最终落位。

## 28. 流派动作画像

支持流派动作画像，但不建设招式百科。

每个流派重点定义典型交战距离、重心和站姿、发力方式、攻防节奏、常见动作类别、连续攻击与防守倾向、空间移动方式、镜头重点。

现代候选：Boxing、Muay Thai、Sanda、MMA、摔跤 / 柔术倾向、电影化战术近身动作语言。

武侠候选：咏春、八极、太极式借力、长拳、南拳、刀法、剑法、枪法、棍法。

## 29. 混合流派

支持：

> **主流派 + 辅助流派**

但一个 Beat 只能有一个主动作语言；辅助流派只能在明确攻防转换节点介入。

## 30. Audio Choreography

音频不是 Prompt 最后统一补一句“紧张音乐 + 打击音效”，而是与 Battle Beat 同步编排。

可包含环境底噪、脚步 / 急停摩擦、衣料 / 衣袂、呼吸、拳脚破风、身体 / 环境碰撞、兵器挥动 / 接触 / 偏转、音乐，以及必要的静默或音乐让位。

音乐不是强制项；如果无 BGM 或极弱配乐更适合压迫感，应主动采用。

## 31. Final Prompt 输出原则

无论 Quick Mode 还是 Interactive Mode，最终用户都必须拿到：

> **一份详细、完整、专业、可直接复制给视频模型使用的成品 Prompt。**

两种模式的差异只存在于生成过程和是否展示中间设计，不存在于最终 Prompt 完成度。

### Quick Mode

零追问；自动推断 Intent、建立 Spatial Map、选择强度、拆 Beat、维护 Range / Advantage / Condition、识别 Turning / Handoff、协调 Action / Camera / Audio；内部状态不默认 Dump；直接输出详细完整成品 Prompt。

### Interactive Mode

用户明确要求讨论 / Grill Me 时启用；一次只问一个关键问题并给推荐答案；可按需展示 Combat Blueprint / Beat Sheet；最终仍必须汇总为完整、可复制成品 Prompt。

## 32. Combat Final Prompt Contract

最终 Combat Prompt 使用统一专业结构，信息完整度固定，可根据任务删去不适用区块，但不得遗漏关键执行信息。

推荐结构：

```text
【场景与视觉锁定】
【战斗总体设定】
【动作 / 镜头 / 声音时间线】
【声音总体设计】
【连续性与物理约束】
【专项禁止项】
【画质与输出约束】
```

Action / Camera / Audio 应按时间线协同表达，不应变成彼此割裂的三份说明。

## 33. 模型 / 平台适配原则

Combat Prompt 以 **模型无关、平台通用** 为第一目标。

> **只要提示词本身专业、详细、明确、因果连续，就应作为可直接使用的通用成品 Prompt。**

Combat 不要求用户先选择 Seedance、LTX 或其他平台才能获得完整 Prompt。

现有模型适配层仅作为可选最后微调层：只有目标模型确实存在明确输入特性、参考素材语法、长度限制、音频能力或特殊控制格式时，才进行轻量转换。

> **Generic Professional Combat Prompt 是最终产品本身；Model Adapter 不是必经步骤。**

## 34. Combat 专项 Negative Constraints

根据场景自动附带 Combat 专项禁止项，而不是只做正向描述。

### 通用高风险禁止项

- 禁止人物瞬移；
- 禁止无缘由左右位置互换；
- 禁止拳脚 / 身体穿模；
- 禁止肢体粘连或异常扭曲；
- 禁止动作无重量感；
- 禁止命中后缺少受力反馈；
- 禁止前一 Beat 的受伤 / 疲劳在下一 Beat 无理由消失；
- 禁止镜头无动机跳轴；
- 禁止切镜后空间关系无法解释；
- 禁止多人同时无序成为主目标；
- 禁止背景人物突然消失、复制或位置漂移。

### 武侠 / 兵器附加禁止项

- 禁止兵器变形或长度无理由变化；
- 禁止兵器凭空换手 / 消失 / 出现；
- 禁止无起跳过程直接悬空；
- 禁止无落地过程；
- 禁止无因果长距离飞行；
- 非高武设定下禁止仙侠能量、剑气、御剑、法器等效果。

Negative Constraints 按场景动态选择，不机械堆满全部禁止项。

## 35. 与现有 single-shot / multi-shot Output Contract 的组合

确认采用：

> **Combat 是专项编排层，不建立第二套平行输出模板。**

内部流程：

```text
Combat Blueprint / Combat Final Prompt Contract
→ 判断最终属于单镜头还是多镜头表达
→ 挂接现有 single-shot / multi-shot Output Contract
→ 注入 Combat 专项动作、镜头、声音、连续性、物理反馈与 Negative Constraints
→ 输出最终可复制成品 Prompt
```

规则：

- 单镜头 / 长镜头打斗优先挂接现有 single-shot 输出结构；
- 多 Beat、多切镜、明确镜头段落的动作戏挂接现有 multi-shot 输出结构；
- Combat 只维护战斗专业编排知识，不复制通用 Prompt 输出结构真源；
- 后续如果现有 single-shot / multi-shot Contract 更新，Combat 应继承其通用格式变化，而不是维护独立副本；
- Combat Final Prompt Contract 定义“战斗必须提供哪些专业信息”，现有 Output Contract 定义“这些信息最终如何组织输出”。

## 36. 与现有 v2 架构的候选关系

正式实现前必须先审计现有真源，避免重复。

### Controls 候选

```text
references/controls/combat-choreography/control.md
references/controls/combat-camera-coordination/control.md
references/controls/combat-spatial-continuity/control.md
```

需与现有 `subject-motion`、`camera-direction`、`spatial-blocking`、`continuity-consistency`、`timeline-rhythm`、`realism-quality`、`audio-visual-sync` 做职责审计。

### Libraries 候选

- 现代格斗动作画像；
- 武侠动作画像；
- 兵器动作画像；
- 打斗镜头功能映射；
- 战斗环境交互模式。

### Diagnostics 候选

新增前优先审计现有 `motion-discontinuity`、`camera-chaos`、`spatial-teleportation`、`anatomy-contact-failure`、`physics-and-weightlessness`、`audio-visual-mismatch`、`prompt-overload-and-conflict`。

## 37. 已确认决策记录

| # | 决策 | 结论 |
|---|---|---|
| 1 | 第一版打斗类型 | 现代格斗 + 电影武侠并行 |
| 2 | 武侠尺度 | 电影武侠，不默认仙侠 |
| 3 | 集成形式 | 现有 Skill 一级专项任务 |
| 4 | Playbook 架构 | 总路由 + Combat Core + 两个专项 Playbook |
| 5 | 核心组织粒度 | Battle Beat |
| 6 | 动作与镜头 | Beat 内同步编排 |
| 7 | 时间控制 | Beat-first + Soft Time Window |
| 8 | 镜头设计 | 功能驱动 |
| 9 | 跨 Beat 镜头 | 连续运动优先 + Visual Handoff |
| 10 | 打击反馈 | 六段完整反馈链 |
| 11 | 动作复杂度 | 1 主目标 + 2～4 攻防交互节点 + 1 结束状态 |
| 12 | 多人战 | 1v1 + 1vN，主交战对象机制 |
| 13 | 武侠兵器 | 刀 / 剑 / 枪 / 棍 |
| 14 | 武侠强度 | 三级，Level 2 默认 |
| 15 | 现代格斗强度 | 三级，Level 2 默认 |
| 16 | 流派 | 动作画像，不做招式百科 |
| 17 | 混合流派 | 主流派 + 辅助流派 |
| 18 | 环境 | 一级战斗变量，每 Beat 最多 1 个主要环境交互 |
| 19 | 速度变化 | 功能驱动的有限速度变化 |
| 20 | Beat 与 Shot | 解耦，不强制 1:1 |
| 21 | Combat Intent | 显式核心变量，Quick Mode 自动推断 |
| 22 | Combat Advantage State | 显式维护优势状态、来源和转折原因 |
| 23 | 主导权转移 | 必须经过 Turning Event；每 Beat 原则上最多一次主要反转 |
| 24 | 默认 Beat 节奏 | 现代格斗与电影武侠使用不同默认节奏画像 |
| 25 | Combat Range State | 显式维护；距离变化必须有动作因果 |
| 26 | Combat Condition State | 受伤 / 疲劳 / 呼吸跨 Beat 累积 |
| 27 | 1vN Target Handoff | 主目标切换必须经 Handoff + Spatial Re-map |
| 28 | Combat Camera Mode | Continuous / Hybrid / Cut-driven，Hybrid 默认 |
| 29 | Combat Spatial Map | 每场战斗先建立轻量空间真源 |
| 30 | Beat State Contract | Beat End State 强制传递给下一 Beat，Camera State 同级维护 |
| 31 | Axis Crossing | 允许，但必须有动机并重新建立空间关系 |
| 32 | Action–Reaction Pair | Action → Response → Outcome → State Change |
| 33 | 最终输出 | Quick / Interactive 最终都必须给详细完整可复制 Prompt |
| 34 | Audio Choreography | 与 Action / Camera 同 Beat 同步设计 |
| 35 | Final Prompt Contract | 使用统一专业结构，不 Dump 内部状态表 |
| 36 | 平台适配 | 通用专业 Prompt 为主，模型适配仅可选轻量微调 |
| 37 | Negative Constraints | 按场景自动附带 Combat 专项禁止项 |
| 38 | 输出模板组合 | Combat 挂接现有 single-shot / multi-shot Contract，不建立平行模板 |

## 38. 尚待继续 Grill Me 的主要设计树

1. 现有 controls / libraries / styles / diagnostics 哪些扩展、哪些新增；
2. Combat 专项静态回归测试场景；
3. 后续枪战如何复用 Combat Core。

## 39. 禁止倾向

- 不把打斗写成招式名词堆砌；
- 不默认一个 Beat 塞大量动作；
- 不让镜头与主体同时高复杂度运动；
- 不无理由频繁切镜；
- 不允许切镜后方向和站位无接力；
- 不把“命中”当作完整打击反馈；
- 不让多人同时成为主交战对象；
- 不让环境同时承担过多交互；
- 不滥用慢动作；
- 不让流派名成为装饰标签；
- 不默认把电影武侠扩成仙侠；
- 不允许战斗主导权无原因突然翻转；
- 不允许一个 Beat 内连续多次大幅反转主导权；
- 不允许 Combat Range 无动作因果瞬间跳变；
- 不允许 Condition 无理由重置；
- 不允许 Target 无 Handoff 瞬间切换；
- 不允许 Camera Axis 无解释翻转；
- 不把内部状态机原样 Dump 给视频模型；
- 不因 Quick Mode 而降低最终 Prompt 的专业度和完整度；
- 不复制现有 v2 通用真源；
- 不建立独立 Combat single-shot / multi-shot 模板副本。
