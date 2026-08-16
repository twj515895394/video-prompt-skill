# Combat Action Reference Catalog

> 状态：**Implemented Knowledge / NOT Runtime-Wired**  
> 来源：用户提供的 18 个国风漫剧打斗动作素材，经 Grill Me 抽象、去特效化与运行字段化整理。  
> 目的：提供可复用的**单动作级 Concrete Action Reference**。本文件回答“一个具体动作怎样成立、适合何时使用、会造成什么状态变化”，不决定 Battle Beat、Exchange Spine、Camera 或最终胜负。

---

# 1. 使用原则

## 1.1 最小知识颗粒度

最小颗粒度固定为：

> **Single Action Template / 单动作模板**

不把手、脚、肩胯、重心、支撑点继续拆成独立知识节点；它们属于动作内部机制。

连招不是基础知识条目，只通过：

- `Transition Compatibility`；
- 当前 Combat State；
- Runtime Exchange Spine；

动态形成。

## 1.2 Visual Medium 与 Physical Level 解耦

画面媒介与动作物理夸张程度完全独立。

同一个动作可以出现在：

- 真人写实影视；
- 国风漫剧；
- 2D 动画；
- 3D 动画；

只要 Selected Physical Level 落在该动作合法范围内。

### P1｜Grounded

现实人体物理为主，允许有限电影强化。

### P2｜Cinematic Exaggerated

保留明确动作因果，但强化速度、爆发、位移与环境反馈。

### P3｜Hyper-Cinematic / Supernatural

允许残影、超高速位移感、明显滞空、气劲、冲击波、剑气、地裂等超现实表现。

原则：

> **降低 Physical Level 可以削弱表现强度，但不能偷偷改变 Core Action Mechanic。**

## 1.3 Combat Role 固定枚举

本 Catalog 只使用以下 8 个核心 Combat Role：

```text
Entry
Pressure
Defense
Counter
Re-entry
Reversal
Signature
Finisher
```

`Range Change / Route Change / Base Disruption` 等效果由 `State Transition` 表达，不重复作为 Role。

## 1.4 Response Compatibility

保持轻量半结构化：

```text
Best Against
Poor Against
Best State
```

不建立复杂攻击方向 / 轨迹 / 速度状态机。

## 1.5 State Transition

采用**稀疏 Before → After**。

只写真正发生变化的状态，例如：

```text
Route: Frontal → Outside Angle
Balance: Stable → Disrupted
Initiative: Neutral → Steal
```

没有变化的字段不写。

---

# 2. 单动作 Schema

每个动作使用以下字段；无意义字段可省略，不机械填满。

```text
id
canonical_name
aliases
functional_category
applicable_range
core_action_mechanic
body_contact_relation
immediate_visible_result
physical_level_range: Min / Default / Max
combat_role
response_compatibility: Best Against / Poor Against / Best State
state_transition
initiative_effect
tempo_profile
risk_commitment: Commitment / Miss-Block Risk / Recovery Exposure / Payoff
prerequisites
transition_compatibility: Good Before / Good After
environment_impact
risks_failure_modes
metadata
```

---

# 3. 突进接敌类

## A01｜爆发瞬身接敌 / Explosive Burst Entry

- **Aliases**：极速瞬身突袭、爆发突进、瞬步接敌
- **Functional Category**：突进接敌
- **Applicable Range**：mid → close
- **Core Action Mechanic**：角色先压低重心，以一次爆发蹬地和短距离加速迅速压缩双方距离；P3 可表现为残影 / 瞬身感，但动作核仍是“高速接敌”。
- **Body & Contact Relation**：起始阶段通常无接触；进入 close 后才产生拳、掌、肩、武器或抓控入口。
- **Immediate Visible Result**：距离骤缩，对手必须立即封线、侧移、后撤或截击。
- **Physical Level Range**：Min P2 / Default P2 / Max P3
- **Combat Role**：Entry / Re-entry / Pressure
- **Response Compatibility**：
  - Best Against：对手后撤、短暂失去攻击线、双方距离被拉开
  - Poor Against：对手已建立稳定贴身控制；狭窄空间无前冲路线
  - Best State：对手刚完成 Recovery，正面路线短暂开放
- **State Transition**：Range: Mid → Close；Initiative: Neutral → Gain；Route: Open Lane → Direct Pressure Lane
- **Initiative Effect**：Gain；明显扑空时 Open Counter Window
- **Tempo Profile**：Burst
- **Risk / Commitment**：Commitment Medium；Miss Risk Medium；Recovery Exposure 为前冲惯性和回正窗口；Payoff 为快速夺取 Entry
- **Prerequisites**：存在可用前冲 / 斜冲路线；落脚区可用
- **Transition Compatibility**：Good Before：侧身闪避、后撤蓄力；Good After：短打、贴身缠斗、飞踢入口
- **Environment Impact**：P2 可带脚步重响、纸张 / 衣摆受气流扰动；P3 可加明显残影、尘土拖尾，但不凭空传送
- **Risks & Failure Modes**：不要写成无起点瞬移；必须保留起势、方向和落脚状态
- **Metadata**：entry, burst, dash, re-entry

## A07｜低位滑步突入 / Low Slide Entry

- **Aliases**：低空滑步突袭、低位滑入
- **Functional Category**：突进接敌
- **Applicable Range**：mid → close / low line
- **Core Action Mechanic**：角色降低重心，以一侧腿承重、另一侧腿引导滑步，从对手高线攻击下方或侧下方快速进入。
- **Immediate Visible Result**：高低位发生变化，对手需要下压防线、换支撑或转轴。
- **Physical Level Range**：Min P1 / Default P2 / Max P3
- **Combat Role**：Entry / Re-entry / Counter
- **Response Compatibility**：Best Against：高线挥击、正面压迫、上肢封线；Poor Against：地面阻碍密集、支撑腿已被控制；Best State：对手上身前压且低线暂时开放
- **State Transition**：Level: High/Mid → Low；Range: Mid → Close；Route: Frontal → Low Inside/Outside
- **Initiative Effect**：Gain / Steal
- **Tempo Profile**：Burst / Quick Reactive
- **Risk / Commitment**：Medium；被截住时 Recovery Exposure 偏高；Payoff 为改变 Level + Entry
- **Prerequisites**：地面连续、无大型障碍；有滑入与起身空间
- **Transition Compatibility**：Good After：横扫腿击、贴身短打、摔控入口、轴线换位
- **Environment Impact**：鞋底摩擦、尘土 / 水迹拖痕；P3 可强化低位气流拖尾
- **Risks & Failure Modes**：不要让身体无支撑漂移；结束必须明确起身 / 单膝 / 低位支撑状态

## A16｜跃步突入 / Agile Jump Entry

- **Aliases**：灵活跳跃突袭、跃步突进
- **Functional Category**：突进接敌
- **Applicable Range**：mid → close
- **Core Action Mechanic**：通过短助跑 / 蹬地跃步越过低障碍或改变攻击高度，在落点附近完成接敌。
- **Immediate Visible Result**：Position / Height 改变，对手被迫抬线、转身或后退。
- **Physical Level Range**：Min P1 / Default P2 / Max P2
- **Combat Role**：Entry / Re-entry / Signature
- **Response Compatibility**：Best Against：低线封锁、矮障碍、对手视线集中地面；Poor Against：低顶空间、无安全落点；Best State：有明确落点且对手需要重新调整 Guard
- **State Transition**：Height: Grounded → Airborne → Grounded；Position: Original Lane → New Landing Lane
- **Initiative Effect**：Gain；落点被读到时 Open Counter Window
- **Tempo Profile**：Acceleration → Impact → Recovery
- **Risk / Commitment**：High；空中路线难改；落地有 Recovery；Payoff 为明显空间换位
- **Prerequisites**：足够起跳 / 落地空间
- **Transition Compatibility**：Good After：凌空飞踢、落地重击、快速短打
- **Environment Impact**：落地震动、衣物和头发惯性；P2 可有明显尘土 / 小物件震动
- **Risks & Failure Modes**：不能无理由长时间滞空；必须交代落地

---

# 4. 闪避走位类

## A05｜侧移离线 / Lateral Evasion Step

- **Aliases**：侧身闪避走位、侧切闪避
- **Functional Category**：闪避走位
- **Applicable Range**：mid / close
- **Core Action Mechanic**：攻击将到时先移重心，以短侧步 / 斜步让躯干离开攻击线，同时保留双脚支撑和反击姿态。
- **Immediate Visible Result**：攻击落空或擦过，双方不再正面对线。
- **Physical Level Range**：Min P1 / Default P1 / Max P2
- **Combat Role**：Defense / Counter / Reversal
- **Response Compatibility**：Best Against：直线拳、直线突进、正面抓抱入口；Poor Against：已建立贴身控制、大范围连续横扫；Best State：对方路线明确且仍有侧向落脚点
- **State Transition**：Route: Frontal → Outside/Inside Angle；Axis: Face-to-face → Offset；Initiative: Opponent Pressure → Open Counter Window
- **Initiative Effect**：Open Counter Window / Steal
- **Tempo Profile**：Quick Reactive
- **Risk / Commitment**：Low；Recovery Exposure Low；Payoff 为线路改变
- **Prerequisites**：有侧向 / 斜向落脚空间
- **Transition Compatibility**：Good After：短打截击、横扫腿、反手格挡后反击、拔刀斩
- **Environment Impact**：轻微脚步摩擦；P2 可加衣物 / 发丝快速惯性
- **Risks & Failure Modes**：不要只写“侧身躲开”而无脚步 / 轴线变化

## A09｜后仰让线反击 / Lean-back Evade Counter

- **Aliases**：后仰规避反击、后仰闪击
- **Functional Category**：闪避走位
- **Applicable Range**：close / striking mid-close
- **Core Action Mechanic**：保持下肢支撑，骨盆和躯干后移让高线攻击掠过，随后借对方过伸或回收窗口迅速回正反击。
- **Immediate Visible Result**：攻击擦空，对手短暂过伸；防守者仍在反击距离内。
- **Physical Level Range**：Min P1 / Default P1 / Max P2
- **Combat Role**：Defense / Counter / Reversal
- **Response Compatibility**：Best Against：高线直拳、摆拳、掌击、部分横向挥击；Poor Against：低线扫腿、持续贴身压迫；Best State：双方距离很近但攻击线可读
- **State Transition**：Upper-body Line: In Path → Outside Path；Initiative: Opponent → Steal opportunity
- **Initiative Effect**：Steal
- **Tempo Profile**：Quick Reactive → Burst
- **Risk / Commitment**：Low-Medium；后仰过大时 Balance Risk；Payoff 为不退出距离的即时 Counter
- **Prerequisites**：脚下支撑稳定；后方无立即碰撞障碍
- **Transition Compatibility**：Good After：短拳、掌根、前臂截击、低线踢
- **Environment Impact**：通常轻微；P2 可强化擦击气流 / 衣物摆动
- **Risks & Failure Modes**：不能把后仰写成失去重心的“Matrix”式悬停，除非 P3 另有明确动作

---

# 5. 格挡防御类

## A03｜反手拨挡 / Reverse-hand Parry

- **Aliases**：反手格挡防御、反手拨架
- **Functional Category**：格挡防御
- **Applicable Range**：close / mid-close
- **Core Action Mechanic**：用前臂 / 手掌从侧面接触来袭肢体并把攻击线拨离中心线，同时身体小幅转轴而非原地硬挡。
- **Immediate Visible Result**：攻击线偏转，形成短暂侧向暴露。
- **Physical Level Range**：Min P1 / Default P1 / Max P2
- **Combat Role**：Defense / Counter
- **Response Compatibility**：Best Against：直拳、短打、直线抓入；Poor Against：重型大范围冲撞、已建立双手抱控；Best State：来招方向清楚、前臂可接触
- **State Transition**：Attack Line: Center → Outside；Axis: Neutral → Slight Turn；Initiative: Opponent → Open Counter Window
- **Initiative Effect**：Open Counter Window / Steal
- **Tempo Profile**：Instant / Quick Reactive
- **Risk / Commitment**：Low；Miss Risk 为拨挡过早 / 过大；Payoff 为保留近距反击
- **Prerequisites**：来袭肢体可接触；防守手没有被固定
- **Transition Compatibility**：Good After：短打、侧移、抓控入口
- **Environment Impact**：通常无；强调肢体接触声和 Guard 变化
- **Risks & Failure Modes**：不要写成手一挥对手整个人飞开，除非另有 P3 力量机制

## A08｜交叉臂硬架 / Cross-arm Guard

- **Aliases**：双臂交叉防御、十字架挡
- **Functional Category**：格挡防御
- **Applicable Range**：close / mid-close
- **Core Action Mechanic**：双臂在头胸前交叉形成结构性防线，用下肢和躯干吸收正面冲击。
- **Immediate Visible Result**：攻击被挡住，但防守者可能后退 / 下沉，通常不自动获得反击权。
- **Physical Level Range**：Min P1 / Default P1 / Max P2
- **Combat Role**：Defense
- **Response Compatibility**：Best Against：正面重拳、下劈、爆发冲击；Poor Against：绕侧、低线攻击、贴身抱摔；Best State：无法及时侧移但仍有稳定支撑
- **State Transition**：Contact: Incoming → Absorbed/Blocked；Position: Stable → Possible Back-step；Initiative: Opponent Retains Pressure
- **Initiative Effect**：Neutral / Opponent Retains Pressure
- **Tempo Profile**：Heavy / Pause-and-Absorb
- **Risk / Commitment**：Medium；持续硬架会被压迫；Payoff 为保命 / 稳住结构
- **Prerequisites**：双臂可自由抬起；脚下支撑存在
- **Transition Compatibility**：Good After：后撤、侧移、下沉换位、短促 Counter
- **Environment Impact**：P2 可有鞋底滑动、地面摩擦、身体撞近处物体
- **Risks & Failure Modes**：不要让防守者格挡后瞬间无过渡切换到完全不同站位

---

# 6. 重击爆发类

## A04｜蓄势重拳 / Charged Heavy Punch

- **Aliases**：蓄力重拳冲击、重拳爆发
- **Functional Category**：重击爆发
- **Applicable Range**：mid-close / close
- **Core Action Mechanic**：先通过短暂蓄势将重心压入支撑脚，再由脚—髋—躯干—肩—拳完成一次高承诺直线 / 弧线重击。
- **Immediate Visible Result**：命中时目标明显失衡 / 后退；落空时攻击者产生较大回收窗口。
- **Physical Level Range**：Min P1 / Default P2 / Max P3
- **Combat Role**：Pressure / Signature / Finisher
- **Response Compatibility**：Best Against：对手被逼入可预测路线、Guard 已被打开、对手 Recovery；Poor Against：高速侧移、外侧角度、距离不足；Best State：攻击者已控制节奏并有完整发力空间
- **State Transition**：On solid hit Balance: Stable → Disrupted；Position: Held → Forced Back；On miss Initiative: Retain/Gain → Open Counter Window
- **Initiative Effect**：命中 Gain / Retain；明显落空 Lose / Open Counter Window
- **Tempo Profile**：Build-up → Impact
- **Risk / Commitment**：High；Miss / Block Risk High；Recovery Exposure High；Payoff High
- **Prerequisites**：有完整发力路线和拳击距离
- **Transition Compatibility**：Good Before：格挡压迫、逼退、假动作；Good After：追击 / Finisher 或落空后的防守恢复
- **Environment Impact**：P2 可轰退目标撞墙 / 家具；P3 可强化局部破裂、冲击波，但拳必须有明确接触或命中机制
- **Risks & Failure Modes**：不能把“蓄力”写成长时间静止；不要用模糊“能量拳”替代具体拳路

## A12｜稳架爆发冲撞 / Braced Power Charge

- **Aliases**：蓄力霸体冲击、霸体冲撞
- **Functional Category**：重击爆发
- **Applicable Range**：mid → close
- **Core Action Mechanic**：角色先压低重心并收紧躯干结构，随后用肩胸 / 前臂 / 全身框架向前强势推进，以身体质量而非单手攻击打开空间。
- **Immediate Visible Result**：目标被迫后退、转轴或失去站位；攻击者继续占据前进路线。
- **Physical Level Range**：Min P2 / Default P2 / Max P3
- **Combat Role**：Entry / Pressure / Signature
- **Response Compatibility**：Best Against：对手 Guard 高但脚下空间有限、对手正在后撤；Poor Against：外侧闪避、借力转向、低位摔控；Best State：攻击者有正面推进通道
- **State Transition**：Range: Mid → Close；Position: Neutral → Forward Occupation；Opponent Position: Held → Forced Back/Turned
- **Initiative Effect**：Gain / Retain；被侧切后 Open Counter Window
- **Tempo Profile**：Pause-and-Explode / Heavy
- **Risk / Commitment**：High；Route Commitment High；Payoff 为强制位移
- **Prerequisites**：前方有推进路线；支撑稳定
- **Transition Compatibility**：Good After：贴身短打、墙边压迫、重拳；被化解后转 Re-entry
- **Environment Impact**：P2 可撞动桌椅 / 门板；P3 可强化墙面裂纹、碎屑与冲击
- **Risks & Failure Modes**：不要把“霸体”理解为绝对无敌；受击仍要有结构 / 惯性反馈

## A14｜后撤蓄势重反击 / Retreat-load Heavy Counter

- **Aliases**：后撤蓄力重击、撤步蓄力反击
- **Functional Category**：重击爆发
- **Applicable Range**：close → mid-close → close
- **Core Action Mechanic**：先撤半步 / 一步让开来招并把重心装入后腿，随即前送髋肩释放一记重击。
- **Immediate Visible Result**：防守与蓄势合成一拍，利用对手追入造成的前压完成重反击。
- **Physical Level Range**：Min P1 / Default P2 / Max P2
- **Combat Role**：Defense / Counter / Reversal / Signature
- **Response Compatibility**：Best Against：对手连续前压、直线追击；Poor Against：对手不追、远距离停手、侧向进入；Best State：可安全撤出半步且对手仍在追入
- **State Transition**：Range: Close → Mid-close → Close；Initiative: Opponent Pressure → Steal
- **Initiative Effect**：Steal
- **Tempo Profile**：Quick Retreat → Build-up → Impact
- **Risk / Commitment**：Medium-High；若对手不追会落空 / 距离断裂；Payoff High Counter
- **Prerequisites**：后方有撤步空间
- **Transition Compatibility**：Good Before：交叉臂防御、后仰闪避；Good After：重拳 / 掌 / 肩撞后的追击
- **Environment Impact**：P2 可产生明显脚步摩擦、目标撞物
- **Risks & Failure Modes**：撤步与回击不能断成两个无关姿势

## A18｜下落震地重击 / Descending Ground Impact

- **Aliases**：落地震地重击、震地落击
- **Functional Category**：重击爆发 / 空中动作
- **Applicable Range**：airborne → ground / area around landing
- **Core Action Mechanic**：角色从明确的腾空 / 下落状态聚集身体质量，以脚、膝、拳、武器或整体落地动作把下落动量传给地面。
- **Immediate Visible Result**：落点产生强烈冲击；附近对手 / 环境因震动、碎屑或冲击波作出反馈。
- **Physical Level Range**：Min P2 / Default P2 / Max P3
- **Combat Role**：Signature / Finisher / Re-entry
- **Response Compatibility**：Best Against：对手位于落点附近、需要制造区域压力；Poor Against：无前序腾空状态、脆弱地面无法合理承载；Best State：已有明确下落轨迹和可读落点
- **State Transition**：Height: Airborne → Grounded；Environment: Stable → Impacted；Range: Vertical Separation → Local Close/Area Pressure
- **Initiative Effect**：Gain / Retain
- **Tempo Profile**：Acceleration → Impact → Recovery
- **Risk / Commitment**：Very High；落点可预测；Recovery Exposure Medium-High；Payoff Very High Visual
- **Prerequisites**：必须存在前序腾空 / 下落；落点明确
- **Transition Compatibility**：Good Before：跃步突入、空中连击；Good After：低位起身压迫 / Finisher Freeze
- **Environment Impact**：P2 灰尘震起、小型家具震动；P3 地裂、碎石、冲击波扩散
- **Risks & Failure Modes**：不能从站立状态无过渡“突然落地”；P3 地裂仍需围绕明确落点展开

---

# 7. 腿法攻击类

## A02｜凌空直线飞踢 / Airborne Driving Kick

- **Aliases**：凌空飞踢、飞踢突击
- **Functional Category**：腿法攻击 / 空中动作
- **Applicable Range**：mid → close
- **Core Action Mechanic**：助跑或短蹬地起跳，支撑腿离地后攻击腿沿明确直线 / 斜线伸展命中目标，随后回收并落地。
- **Immediate Visible Result**：目标后退 / 失衡；攻击者必须进入落地 Recovery。
- **Physical Level Range**：Min P1 / Default P2 / Max P2
- **Combat Role**：Entry / Pressure / Signature
- **Response Compatibility**：Best Against：目标位置相对固定、正面路线开放；Poor Against：低顶空间、对手已贴身、对手明显侧切；Best State：有清楚起跳距离和安全落点
- **State Transition**：Height: Grounded → Airborne → Grounded；Range: Mid → Contact; Position: Start → Landing Point
- **Initiative Effect**：命中 Gain；落空 Open Counter Window
- **Tempo Profile**：Acceleration → Impact → Recovery
- **Risk / Commitment**：High；空中路线难改；落地 Recovery High；Payoff High
- **Prerequisites**：起跳 / 落地空间；目标在踢击轨迹内
- **Transition Compatibility**：Good Before：爆发接敌、跃步；Good After：落地短打 / 侧移恢复
- **Environment Impact**：落地脚步、目标撞物；P2 可强化击退
- **Risks & Failure Modes**：必须写落地；不能让攻击者击中后继续无支撑漂浮

## A10｜低位横扫 / Sweeping Leg Attack

- **Aliases**：横扫腿击、扫腿、低线扫击
- **Functional Category**：腿法攻击
- **Applicable Range**：close / mid-close
- **Core Action Mechanic**：支撑脚转轴，髋部带动攻击腿沿低位弧线扫向对手小腿 / 脚踝 / 支撑线，目标是改变 Support Base 而非单纯造成疼痛。
- **Immediate Visible Result**：对手被迫抬脚、补步、转身或失衡。
- **Physical Level Range**：Min P1 / Default P1 / Max P2
- **Combat Role**：Counter / Pressure / Reversal
- **Response Compatibility**：Best Against：对手重心前压、承重脚明显、突进刚落脚；Poor Against：目标已腾空、距离过近无法展开；Best State：支撑线暴露
- **State Transition**：Support: Stable → Disturbed；Balance: Stable → Forced Re-step/Off-balance；Initiative: Neutral/Opponent → Steal
- **Initiative Effect**：Steal / Gain
- **Tempo Profile**：Quick / Heavy depending execution
- **Risk / Commitment**：Medium；被抬腿 / 后撤会空扫；Payoff 为 Base Disruption
- **Prerequisites**：攻击腿有弧线路径；目标支撑区域可达
- **Transition Compatibility**：Good Before：侧移、反手拨挡；Good After：短打、摔控、重击
- **Environment Impact**：P1 鞋底摩擦 / 尘土；P2 对手失衡后撞翻近处物体
- **Risks & Failure Modes**：不要只写“扫腿把人打飞”；必须体现支撑变化

---

# 8. 空中动作类

## A06｜腾空旋转斩 / Airborne Spinning Slash

- **Aliases**：腾空旋转斩击、旋空斩
- **Functional Category**：空中动作 / 武器攻击
- **Applicable Range**：mid / close around arc
- **Core Action Mechanic**：持刀 / 剑角色起跳后由髋肩带动身体旋转，武器沿一条可读弧线完成斩击，随后以明确姿态落地。
- **Immediate Visible Result**：武器攻击覆盖角度扩大，对手需要后撤、架挡或改变轴线。
- **Physical Level Range**：Min P2 / Default P2 / Max P3
- **Combat Role**：Pressure / Signature / Finisher
- **Response Compatibility**：Best Against：需要跨越低障碍 / 扩大斩击角度；Poor Against：狭窄空间、无武器、贴身抱控；Best State：有起跳与旋转空间且对手位于弧线范围
- **State Transition**：Height: Grounded → Airborne → Grounded；Axis: Forward → Rotated; Weapon Line: Ready → Sweeping Arc
- **Initiative Effect**：Gain；落空或落地被读到时 Open Counter Window
- **Tempo Profile**：Build-up → Rotation Burst → Recovery
- **Risk / Commitment**：Very High；路线难改、落地 Recovery High；Payoff Very High Visual
- **Prerequisites**：刀剑可用；足够旋转与落地空间
- **Transition Compatibility**：Good Before：跃步 / 闪避换位；Good After：落地重击 / 防守恢复
- **Environment Impact**：P2 武器带风、布料旋转；P3 可加入剑气 / 强气流，但真实武器轨迹仍需可读
- **Risks & Failure Modes**：武器不得漂移 / 变长；不要用镜头旋转替代人物动作旋转

## A11｜超现实滞空连击 / Supernatural Aerial Combination

- **Aliases**：空中滞空连击、滞空连续攻击
- **Functional Category**：空中动作
- **Applicable Range**：airborne close / mid-close
- **Core Action Mechanic**：角色在明显超现实的持续空中状态中，对同一目标完成连续可读攻击，并保持每次 Contact / Reaction 的方向连续。
- **Immediate Visible Result**：目标在空中 / 近空中持续被压制，双方 Height 与 Momentum 成为主要战斗状态。
- **Physical Level Range**：Min P3 / Default P3 / Max P3
- **Combat Role**：Pressure / Signature / Finisher
- **Response Compatibility**：Best Against：P3 武侠 / 超现实战斗，双方已进入空中状态；Poor Against：P1/P2 写实物理、无腾空入口；Best State：已有明确起跳 / 击飞 / 腾空来源
- **State Transition**：Height: Grounded/Airborne → Sustained Airborne；Initiative: Gain → Retain under aerial pressure
- **Initiative Effect**：Retain / Gain
- **Tempo Profile**：Sustained Rapid
- **Risk / Commitment**：High；如果连击断裂，需要明确下落 / 换位；Payoff 为高密度空中 Signature
- **Prerequisites**：Selected Physical Level 必须 P3；已有合理腾空入口
- **Transition Compatibility**：Good Before：飞踢、击飞、跃步；Good After：下落震地 / 空中脱离
- **Environment Impact**：气流、衣物、碎屑 / 烟尘随空中运动；不得让环境反馈与运动方向相反
- **Risks & Failure Modes**：不能降级成 P2 后仍写长时间悬浮；每次攻击必须有具体动作头而不是“连续连击”四字

---

# 9. 贴身缠斗 / 近身快打类

## A17｜贴身快打链 / Close-range Flurry

- **Aliases**：贴身缠斗快打、近身快攻
- **Functional Category**：贴身缠斗 / 近身快打
- **Applicable Range**：close
- **Core Action Mechanic**：双方保持可读近身关系，攻击者以短拳、掌、前臂、肘等短距离动作连续抢线，对手同时封挡、偏轴、抓控或短反击；不是单方木桩连打。
- **Immediate Visible Result**：高频攻防持续，Guard / Axis / Contact 不断变化但 Range 基本保持 close。
- **Physical Level Range**：Min P1 / Default P2 / Max P2
- **Combat Role**：Pressure / Counter / Re-entry
- **Response Compatibility**：Best Against：已经进入贴身距离、双方 Guard 活跃；Poor Against：距离过远、其中一方已倒地且未重新建立关系；Best State：双方仍有持续交换能力
- **State Transition**：Contact: Intermittent → Sustained Close Exchange；Axis: Repeated micro changes；Initiative: Can Retain / Steal dynamically
- **Initiative Effect**：Retain / Steal depending exchange
- **Tempo Profile**：Sustained Rapid
- **Risk / Commitment**：Medium；持续近身会增加被抱控 / 低线反击风险；Payoff 为高 Exchange Density
- **Prerequisites**：双方已处 close；必须允许对手真实回应
- **Transition Compatibility**：Good Before：爆发接敌、格挡、摔控失败；Good After：侧移、摔控、重击、Reversal
- **Environment Impact**：衣物、呼吸、脚步、墙边 / 家具小范围碰撞；不需要每一下都破坏环境
- **Risks & Failure Modes**：避免“拳掌肘膝一串名词”；必须把关键 1-2 个动作具体化并让其造成状态后果

---

# 10. 武器瞬杀类

## A13｜侧身拔刀斩 / Draw-and-Slash

- **Aliases**：侧身拔刀斩、拔刀反斩
- **Functional Category**：武器瞬杀
- **Applicable Range**：mid-close / close
- **Core Action Mechanic**：角色先通过侧身 / 斜切让出正面攻击线，同时一手稳定刀鞘 / 起始位置，另一手拔出刀刃并沿连续弧线完成一次斩击。
- **Immediate Visible Result**：防守换位与武器攻击在同一动作链完成，对手被迫退让 / 架挡 / 改轴。
- **Physical Level Range**：Min P1 / Default P2 / Max P3
- **Combat Role**：Counter / Reversal / Signature / Finisher
- **Response Compatibility**：Best Against：直线进入、对手攻击过伸、已有外侧角度；Poor Against：无刀剑、贴身抱控使拔刀空间不足；Best State：刀仍在鞘 / 起始位置且拔刀路径开放
- **State Transition**：Weapon State: Sheathed/Ready → Drawn; Route: Frontal → Offset；Initiative: Opponent → Steal
- **Initiative Effect**：Steal / Gain
- **Tempo Profile**：Instant → Burst
- **Risk / Commitment**：Medium-High；拔刀失败会产生暴露；Payoff High
- **Prerequisites**：真实刀剑 / 刀鞘状态；手部与武器位置连续
- **Transition Compatibility**：Good Before：侧移、后仰闪避；Good After：武器压迫 / 收刀 / 继续斩击
- **Environment Impact**：P2 刀风 / 布料响应；P3 可加入剑气 / 物件被斩开，但必须沿刀刃轨迹发生
- **Risks & Failure Modes**：禁止武器凭空出现；刀长度 / 持握 / 鞘的位置必须连续

---

# 11. 气劲 / 能量外放类

## A15｜非接触震劲击退 / Non-contact Force Push

- **Aliases**：抬手震气击退、掌劲震退、气劲推退
- **Functional Category**：气劲 / 能量外放
- **Applicable Range**：close → mid / mid
- **Core Action Mechanic**：角色抬掌 / 推掌后，在**无身体接触**的情况下通过明确可见的超现实掌劲 / 气压 / 能量冲击把目标沿固定方向推退。
- **Immediate Visible Result**：目标衣物、身体和脚步先受同一方向冲击，再被迫滑退 / 飞退；环境轻物体沿同方向响应。
- **Physical Level Range**：Min P3 / Default P3 / Max P3
- **Combat Role**：Defense / Counter / Reversal / Signature / Finisher
- **Response Compatibility**：Best Against：对手正面压入、需要强制拉开距离；Poor Against：P1/P2 现实尺度、遮挡物完全阻隔且没有穿透设定；Best State：目标处于清楚掌劲方向线上
- **State Transition**：Range: Close/Mid → Mid/Far；Position: Forward Pressure → Forced Back；Initiative: Opponent → Steal/Gain
- **Initiative Effect**：Steal / Gain
- **Tempo Profile**：Pause-and-Explode
- **Risk / Commitment**：Medium；动作本身短但 P3 表现强；Payoff Very High Range Reset
- **Prerequisites**：Selected Physical Level = P3；题材允许非接触超现实力量
- **Transition Compatibility**：Good Before：格挡 / 引诱 / 被压迫；Good After：脱离、远距对峙、瞬身追击
- **Environment Impact**：纸张、衣摆、灰尘、小物件沿同一方向被推开；更高表现可加入冲击波 / 门窗震动
- **Risks & Failure Modes**：不可为了适配 P2 改写成普通接触推掌；若需要接触推掌，应新建另一动作条目

---

# 12. 归一化与去重说明

## 12.1 与现有 Abstract Pattern 的关系

本 Catalog 不替代 `minimum-validation-set.md`。

示例映射：

```text
minimum-validation-set T02 Low-line Base Disruption
→ 可实例化为本 Catalog A10 低位横扫

minimum-validation-set M01 Outside Angle Cut
→ 可与本 Catalog A05 侧移离线组合

minimum-validation-set T04 Whole-body Linked Counter
→ 可实例化为 A14 后撤蓄势重反击，或其他符合当前 Combat System 的具体动作
```

Abstract Pattern 仍负责“解决什么 Gap”；本 Catalog 负责“具体动作怎样成立”。

## 12.2 不做固定 Combo

允许记录：

```text
A05 侧移离线
→ Good After: A10 横扫腿 / A03 反手拨挡后的 Counter
```

但 Runtime 不得把它解释成：

> A05 后永远必须接 A10。

组合仍由 Current State / Combat System / Expression / Advantage / Exchange Spine 决定。

## 12.3 Style 与 Physical Level

`真人写实 + P3` 合法；`国风漫剧 + P1` 也合法。

本 Catalog 不保存“真人版 / 漫画版”两套重复动作正文；视觉媒介由 Style / Visual Medium 决定，动作物理尺度由 P1-P3 决定。

---

# 13. 当前 Runtime Freeze

RF-22 关闭前：

```text
本文件可以被维护 / 审核 / 扩展
但不得加入当前 Stage-2 Mandatory Read / Default Routing
```

禁止本轮修改：

- `SKILL.md` Runtime Direct READ；
- `references/tasks/action-combat-video/index.md` Stage-2 路由；
- `regression-fix-runtime-policy.md`；
- `minimum-validation-set.md`；
- Quick Mode；
- Camera Runtime。

RF-22 连续两次 PASS-NATIVE 后，再单独决定：

- Catalog Selection Policy；
- Pattern → Concrete Action 二阶段命中方式；
- 是否占用现有 Library Detail Slot；
- Regression Cases。
