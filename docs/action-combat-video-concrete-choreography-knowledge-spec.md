# Action Combat Video — Concrete Choreography Knowledge Spec

> 状态：**Grill Me 设计进行中；已记录当前确认决策，尚未进入 Implementation Plan / Runtime 开发。**
>
> 上游设计真源：`docs/action-combat-video-v2-spec.md`
>
> 上游实施计划：`docs/action-combat-video-v2-implementation-plan.md`
>
> 回归真源：`docs/action-combat-video-v2-regression.md`
>
> 本文职责：承接 V2-49 之后暴露的 **Choreography Richness / Concrete Knowledge / Stage-2 Execution Knowledge** 新一轮设计，不再继续追加旧的超长 V2 Spec。

---

## 1. 背景与触发证据

最新固定 G01（15 秒办公室两名职业杀手近身对决）回归表明：

- V2-48 的 Camera Intent 条件询问已经明显生效；
- V2-49 的 Executable Action Granularity 已经生效，关键 Action Phrase 能表达具体身体动作、Contact、即时响应、Footwork / Axis / Range / Position 后果与下一动作入口；
- 但 15 秒内主要仍只有约 3 组较大的 Exchange；
- 颗粒度变细后，单个 Phrase 占用更多 Prompt / Execution Budget，出现“动作写得更具体，但整体动作链数量没有同步增加”的问题；
- Concrete Action 仍长期偏向 `前臂 / 肩线 / 抓腕 / 上臂控制 / 顶肩` 等站立上肢交互；
- 虽然脚步、转髋、重心等已有加入，但很多时候仍只是服务上肢控制，而不是作为独立 Choreography Source 创造新路线、新高度、新 Range 与新动作入口；
- 最新 G01 的实际 Read List 仍未命中 `combat-fighting-profiles/library.md` 等 Technique Detail，说明 Stage-2 Execution Knowledge 的真实加载需要先审计。

因此当前问题已经从：

> “动作是否足够具体”

进一步进入：

> **“具体动作知识是否足够丰富、是否真正被 Stage-2 调用，以及身体运动本身是否成为动作编排来源。”**

---

## 2. 当前阶段原则

### 2.1 不再单纯提高所有动作的描述精度

确认：颗粒度越细不等于动作越丰富。

如果所有 Action Phrase 都采用同等高颗粒度，可能导致：

```text
单 Phrase 信息量增加
→ Prompt / Model Execution Budget 被快速占满
→ 15 秒可容纳 Phrase 数量下降
→ Choreography Richness 反而受限
```

因此后续优化重点不是“继续把每个动作写得更细”，而是**颗粒度分配**。

### 2.2 Granularity Distribution / 颗粒度分配

确认采用分层颗粒度：

```text
High Granularity
→ Major Reversal / Initiative Theft / Signature Moment / 关键环境或状态转折

Medium Granularity
→ 普通 Counter / Re-counter / Range Change / Continuous Exchange

Low Granularity
→ 不承担关键因果的连接 / 过渡动作
```

原则：

> **关键因果动作具体，普通交换适度压缩，纯连接动作可以摘要。**

目标是在不牺牲 V2-49 可执行性的前提下，让 15 秒容纳更多真实 Exchange。

该规则优先并入现有 `Action Execution Budget + Executable Granularity + Temporal Packing`，不新建独立 Granularity Engine。

---

## 3. Concrete Choreography Knowledge Audit / 具体动作知识审计

正式确认进入下一阶段：**Concrete Choreography Knowledge Audit**。

但严格按依赖顺序执行：

```text
Step 1｜Stage-2 Routing Audit
→ 为什么 G01 没有真正加载 Technique / Fighting Detail？

Step 2｜Knowledge Realization Test
→ Stage-2 正确加载后，动作种类是否显著扩展？

Step 3｜Knowledge Coverage Audit
→ 如果仍长期偏上肢控制，再判断现有 Fighting / Martial / Weapon Knowledge 本身是否缺失
```

禁止看到“前臂 / 肩 / 抓腕”重复，就直接扩建大型 Library。

### 3.1 Stage-2 First, Knowledge Second

当前已确认的根因候选分为两类：

#### A. Routing / Selection 问题

Stage-2 设计存在，但实际运行没有命中 Technique Detail。

可能表现为：

```text
Choreography 要求“写具体”
→ 未加载专业动作叶子知识
→ 模型依赖自身默认近身格斗原型
→ 反复回到前臂 / 肩线 / 抓腕 / 站立控制
```

#### B. Knowledge Coverage 问题

只有 Stage-2 已正确加载后仍持续发生同类退化，才判定可能存在知识覆盖不足。

原则：

> **先证明知识被用上，再判断知识够不够。**

---

## 4. 核心知识模型：Technique + Movement + Transition

确认：解决“长期站着打 / 偏上肢控制”不能只增加腿法。

Concrete Choreography Knowledge 至少由三种一级生产知识共同组成：

```text
Movement Pattern
+ Technique Pattern
+ Transition Pattern
→ Concrete Action Phrase
```

三者职责分离，但共享统一基础 Schema，并允许互相引用。

不建立一个万能“大招式 Pattern”。

---

## 5. Technique Vocabulary / 技法知识

Technique 描述：**角色具体用什么攻击、防守、控制或兵器技术。**

建议覆盖方向包括但不限于：

```text
Technique Vocabulary
├─ Upper-body Techniques
├─ Lower-body Techniques
├─ Grapple / Control
├─ Throw / Takedown
└─ Weapon Techniques
```

### 5.1 Lower-body 不能只理解为“偶尔踢一脚”

腿法、脚法可以参考传统武术与现代格斗知识，例如不同类型的踢、蹬、扫、踹、摆、勾等，但它们不能以孤立动作清单存在。

必须能与 Movement / Transition 组合，使腿部技术改变：

- Range；
- Support Base；
- Balance；
- Route；
- Height / Level；
- Axis；
- 下一次 Entry。

否则会退化成：

```text
站着打手
→ 踢一下
→ 继续站着打手
```

这不能解决当前问题。

---

## 6. Movement Vocabulary / 身体运动知识

确认：Movement 不是 Technique 的附属，而是独立 Choreography Source。

基础覆盖至少包括：

```text
Movement Vocabulary
├─ 身法 / Body Method
├─ 步法 / Footwork
├─ 步型 / Stance Transition
├─ 重心转换 / Weight Transfer
├─ 高低位变化 / Level Change
├─ Body Axis / 肩胯腰身协同
├─ 空间路线 / Angle / Route Change
├─ 转身 / 绕位 / 穿越
└─ 跌扑 / 滚转 / 起身 / 姿态转换
```

Movement 的目标不是给上肢动作补“脚步说明”，而是直接创造新的战斗条件：

```text
步法改变路线
→ 身法改变暴露面 / 攻击线
→ Level Change 创造新 Entry
→ 重心变化改变支撑 / 失衡关系
→ Axis / Route Change 改变双方 Position
→ Technique 从新的身体状态启动
```

原则：

> **身体本身就在“打”，而不是上肢在打、下肢负责搬运。**

---

## 7. Transition Knowledge / 动作转换知识

确认：知识库不能只是招式大全；真正决定连续战斗丰富度的是不同 Movement / Technique 之间如何合法衔接。

Transition 至少应覆盖：

```text
Technique → Movement
Movement → Technique
Technique → Technique
Range Transition
Level Transition
Position / Angle Transition
Standing → Low Level → Standing
Strike → Control
Control → Strike
Strike → Takedown
Failed Takedown → Re-entry
Front → Outside → Rear Angle
Ground / Roll / Recovery → Re-entry
```

Transition Pattern 回答：

> **前一个身体 / Contact / Range / Axis / Momentum 状态，为什么能够进入下一个动作。**

这与 V2 的 Motion Handoff / Initiative Handoff 对齐，但提供的是更具体的生产知识，而不是新增状态机制。

---

## 8. Pattern 是生产知识一级结构，门派 / 拳种是来源与风格标签

确认选择：**Pattern-first，而不是 Style/School-first。**

不把 Runtime 构造成：

```text
南拳
→ 招式树

长拳
→ 招式树

八极
→ 招式树
...
```

而是把南拳、长拳、八极、咏春、太极等作为：

- 知识来源；
- 风格倾向；
- 动作气质；
- Pattern 证据 / 标签；
- 用户明确指定某武术风格时的优先检索条件。

Runtime 真正消费的是可组合 Pattern，例如：

```text
外侧切入
沉身换位
支撑腿攻击
斜向穿步
轴线旋转脱离
低位进入再起身
转身换侧
贴身桥接
扫腿破支撑
跌扑恢复
```

原则：

> **拳种负责提供知识来源和风格，Pattern 才是运行时生产知识。**

避免 `人物属性 → 某门派 → 固定打法` 的模板化路由。

---

## 9. 共享基础 Knowledge + Specialist 扩展

确认选择：**共享基础 Pattern + Specialist Expansion**，不为 Modern / Traditional Martial / Wuxia 各复制一整套知识库。

推荐概念结构：

```text
combat-choreography-knowledge/
├─ movement-patterns/
│  ├─ shared/
│  ├─ modern/
│  ├─ traditional-martial/
│  └─ wuxia/
│
├─ technique-patterns/
│  ├─ striking/
│  ├─ kicking/
│  ├─ grapple-control/
│  ├─ throw-takedown/
│  └─ weapon/
│
└─ transition-patterns/
   ├─ movement-to-technique/
   ├─ technique-to-movement/
   ├─ range-transition/
   ├─ level-transition/
   ├─ position-transition/
   └─ ground-air-transition/
```

这是概念结构，不代表最终必须按这些目录机械拆文件；实施阶段根据索引大小和运行加载成本决定物理文件结构。

### 9.1 Shared 层

保存跨战斗形式稳定成立的：

- Footwork / Route / Axis；
- Weight Transfer；
- Level Change；
- Position Transition；
- Balance / Recovery；
- Ground / Standing 基础转换；
- Technique ↔ Movement 通用衔接。

### 9.2 Specialist 层

Specialist 不复制 Shared，而是增加：

- 允许的运动尺度；
- 物理边界；
- 专项动作语言；
- 专项 Technique / Transition Pattern；
- Pattern 选择倾向。

---

## 10. Modern / Traditional Martial / Wuxia 运动尺度分层

确认：三类专项共用底层 Pattern 结构，但允许不同运动尺度。

```text
Modern Combat
→ 现实人体运动尺度与现实物理边界

Traditional / Martial-grounded Combat
→ 更丰富的身法、步法、腿法、高低位与传统武术动作语言
→ 仍保持接近现实或可接受的电影化现实

Wuxia
→ 允许轻功、腾空、空中换向、借物位移、空中攻防等明显电影化运动
```

禁止 Wuxia 专项能力反向污染 Modern Combat 默认物理合同。

---

## 11. Wuxia Movement / 轻功与空中战斗扩展

确认：Wuxia 不建立另一套知识架构，而是在同一：

```text
Movement Pattern
+ Technique Pattern
+ Transition Pattern
```

结构上扩展更高运动尺度。

Wuxia Movement 可以覆盖：

```text
轻功
├─ 踏墙
├─ 借物腾跃
├─ 连续点地 / 点物
├─ 高低落差穿越
└─ 长距离空中位移

腾空动作
├─ 起跳进入
├─ 空中转体
├─ 空中换向
├─ 空中攻防
└─ 落地衔接

空中战斗
├─ 空中追击
├─ 空中格挡 / Counter
├─ 武器空中交锋
├─ 高低位交错
└─ 落点争夺

环境借力
├─ 墙面
├─ 屋檐
├─ 栏杆
├─ 树木
└─ 场景物件 / 武器
```

### 11.1 Ground ↔ Air Transition 是关键知识

空中战斗不能写成：

```text
跳起来
→ 空中打两招
→ 落地
```

需要显式知识：

```text
Ground Entry
→ Takeoff Cause
→ Airborne Axis / Momentum
→ Mid-air Attack / Defense
→ Opponent Airborne Response
→ Relative Height / Distance Change
→ Landing Target
→ Landing Handoff
```

避免：

- 无原因漂浮；
- 空中静止挥拳 / 挥剑；
- 起跳与落地无因果；
- 落地后动作状态 Reset。

原则：

> **Wuxia 的特殊性主要来自更高的 Movement Scale、电影化物理边界和 Ground↔Air Transition，而不是另建一套 Choreography Engine。**

---

## 12. 三类 Pattern 职责分离，共享统一基础 Schema

确认：

### Movement Pattern

回答：

> **身体怎么移动、换位、换轴、换高度、改变路线。**

### Technique Pattern

回答：

> **角色具体用什么攻击、防守、控制、摔投或兵器技术。**

### Transition Pattern

回答：

> **前一个身体 / Contact / Range / Momentum 状态如何合法进入下一动作。**

最终由 Choreography Runtime 组合：

```text
Movement Pattern
+ Technique Pattern
+ Transition Pattern
+ Opponent Response
+ Current Combat State
→ Concrete Action Phrase
```

禁止把“侧切 + 三拳 + 摔投 + 腾空 + 落地”保存成巨大固定套路并直接套用。

原则：

> **知识原子要足够可组合，Action Phrase 才负责形成当前场景的完整动作句。**

---

## 13. 当前已确认决策记录

| # | 决策 | 当前结论 |
|---|---|---|
| CK-01 | Granularity Distribution | 不再所有动作同等高颗粒度；关键转折高颗粒度、普通交换中颗粒度、连接动作低颗粒度，以保留 Choreography Richness |
| CK-02 | Concrete Knowledge Audit 顺序 | 先 Stage-2 Routing Audit，再验证 Knowledge Realization；只有正确加载后仍退化才扩 Knowledge |
| CK-03 | 下肢问题范围 | 不只补腿法；腿法必须与 Range / Balance / Route / Axis / Entry 等身体运动知识组合 |
| CK-04 | Movement Vocabulary | 身法、步法、步型、重心、高低位、Axis、空间路线、转身绕位、跌扑滚转起身等作为独立 Choreography Source |
| CK-05 | Knowledge 三分法 | Movement Pattern + Technique Pattern + Transition Pattern 共同构造 Concrete Action Phrase |
| CK-06 | Pattern vs 门派 | Pattern 是生产知识一级结构；南拳 / 长拳 / 八极 / 咏春等作为来源、风格和检索标签，不建设 Runtime 门派招式树 |
| CK-07 | Shared + Specialist | 共享基础 Movement / Transition Pattern；Modern / Traditional Martial / Wuxia 只做专项扩展，不复制整库 |
| CK-08 | Wuxia 扩展 | 同一 Pattern 架构上允许轻功、腾空、空中攻防、环境借力与电影化运动尺度 |
| CK-09 | Ground↔Air | Wuxia 需要显式 Ground → Air → Ground Transition，避免漂浮、静止空中打斗和落地 Reset |
| CK-10 | Pattern Schema 方向 | Movement / Technique / Transition 职责分离，但共享统一基础 Schema 并允许互相引用，不建立万能大 Pattern |

---

## 14. Anti-overdesign 边界

当前明确禁止：

- 因“上肢过多”就新增 Lower-body Engine；
- 因“站着打”就新增 Body Method State Machine；
- 为每个拳种建立独立 Runtime 路由树；
- 建立大型固定招式序列库；
- 把 Wuxia 另做一套平行 Combat Engine；
- 在 Stage-2 Routing 尚未验证前扩建大规模 Fighting Library；
- 通过固定“每段必须几次踢腿 / 几次换位 / 几次腾空”配额保证丰富度。

原则：

> **先修知识调用，再补知识覆盖；先提供可组合动作原子与转换知识，再由 Choreography 动态组句。**

---

## 15. 当前未决设计树

当前已经确认知识架构的大方向，下一步仍需 Grill Me 的关键问题包括：

1. 统一 Pattern 基础 Schema 具体需要哪些字段；
2. Stage-2 Routing 如何从 Planning Context 选择 Movement / Technique / Transition Detail，而不一次加载过多知识；
3. 一个 Action Phrase 默认应组合多少类知识，如何与 Action Execution Budget 协调；
4. Pattern 的适用条件 / 禁用条件 / Range / Level / Contact / Environment / Physical Scale 如何表达；
5. 传统武术来源知识如何研究、归纳和去门派模板化；
6. Wuxia 的电影化物理尺度如何由 Specialist 约束，避免仙侠化或无重力漂浮；
7. Regression 如何单独识别 Upper-body Technique Dominance、Static Standing Combat 与 Knowledge Diversity 是否真正改善。

本文在上述设计完成后，再进入 Implementation Plan；在此之前不直接扩建 Runtime Library。
