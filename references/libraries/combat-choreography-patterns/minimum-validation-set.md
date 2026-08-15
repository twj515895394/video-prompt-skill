# Combat Choreography Patterns — Minimum Validation Set

> 状态：CK-18 最小验证集 + G01 Regression Trace / Movement Causality 补强。用途是验证 Stage-2 是否能真正打破 Upper-body Dominance / Static Standing Combat；不是完整武术知识库，也不是固定套路表。

## 1. Runtime 使用规则

仅在当前 Action Combat Planning Context 存在明确 Fighting Direction / Derived Choreography Direction，且 Stage-2 发现 Movement / Technique / Transition 缺口时按需读取。

```text
Planning Gap
→ Pattern Slot
→ 1 个主 Pattern
→ 必要时 1 个辅助 Pattern
→ Concrete Action Phrase
```

禁止：

- 三类 Pattern 每次全部加载；
- 为了“丰富”机械凑动作；
- 直接把样例串成固定 Combo；
- 用 Pattern 名替代可执行动作句；
- 只读本文件但不留下 Pattern Hit Evidence；
- 为了使用某个 Pattern 反过来硬改已经成立的 Exchange Spine。

Pattern 只提供动作生产知识；最终 Phrase 必须结合当前 Range / Contact / Axis / Position / Momentum / Opponent Response 重写。

### 1.1 Pattern Traceability

Regression / Debug 模式下，每次实际实例化本文件 Pattern，都必须能回答：

```text
当前 Gap 是什么
→ 命中哪个 Slot
→ Main Pattern 是什么
→ optional Auxiliary Pattern 是什么
→ 哪个字段 / Detail 真正进入了动作
→ Realized Concrete Action Phrase 是什么
```

仅仅出现：

```text
Read: minimum-validation-set.md
```

不能证明 Stage-2 已正确执行。

### 1.2 Archetype / Signature Weighting

当角色已确认 Cinematic Combat Archetype 或其他 Persistent Combat Signature 时：

- Pattern Selection 必须服从当前 System / Expression / Archetype Bias；
- Pattern 不是中立随机池；
- 不得因为本文件只有少量样例，就让不同角色最终都使用同一动作骨架；
- Archetype 只改变选择权重，不创建固定次数或固定 Combo。

---

## 2. Shared Core Schema

每个样例使用最小共享字段：

```text
id
name
type
intent
entry_conditions
resulting_state
applicable_range
applicable_level
physical_scale
compatible_patterns
incompatible_conditions
source_tags
```

专项字段按 type 增加，不要求其他类型承担无关字段。

---

## 3. Movement Patterns

### M01｜外侧斜切 / Outside Angle Cut

- type: Movement
- intent: 从正面对线切到对手外侧，改变攻击路线与肩轴关系
- entry_conditions: 中近距离；对手正在线性进入、封线或上肢接触后尚未完全回正
- resulting_state: front → outside angle；形成侧向攻击 / 脱离入口
- applicable_range: mid / close
- applicable_level: standing
- physical_scale: realistic
- route: diagonal outside
- axis: body turns with hip-shoulder alignment
- weight_transfer: 前脚切线，后脚跟随收窄距离
- spatial_effect: 改变双方朝向与 Position，而不是原地换手
- compatible_patterns: T01, T03
- incompatible_conditions: 极窄空间且无侧向落脚点
- source_tags: shared, modern, traditional-martial

### M02｜沉身换位 / Level Drop Reposition

- type: Movement
- intent: 通过降低重心和高低位变化避开高线并创造低位进入
- entry_conditions: 对手高线攻击、抓控或封线压迫
- resulting_state: high → low / close entry；对手需要重新调整防线
- applicable_range: mid / close
- applicable_level: high-to-low
- physical_scale: realistic
- route: slight diagonal / inside-or-outside by context
- axis: 膝髋屈曲，躯干不折叠失衡
- weight_transfer: 重心下沉后移入新支撑脚
- spatial_effect: 创造 Level + Range 改变
- compatible_patterns: T02, T04
- incompatible_conditions: 当前支撑腿被完全控制、无下沉空间
- source_tags: shared, modern, traditional-martial

### M03｜轴线旋转脱离 / Axis-turn Exit

- type: Movement
- intent: 利用现有 Contact / Pressure 改变身体轴线并从正面压力线脱离
- entry_conditions: close contact；肩臂、躯干或武器线存在可借用压力
- resulting_state: frontal pressure → side/rear-facing relation or reset angle
- applicable_range: close
- applicable_level: standing / low
- physical_scale: realistic
- axis: hip-led rotation, torso follows
- weight_transfer: pivot on loaded support, recover base after turn
- spatial_effect: Route / Axis / Position 同时变化
- compatible_patterns: T01, T04
- incompatible_conditions: 双脚完全失去支撑、被固定在墙角且无旋转余量
- source_tags: shared, modern, traditional-martial

### M04｜支撑转换 / Support-base Transfer

- type: Movement
- intent: 改变支撑脚与重心，使下肢 Technique / Takedown / Re-entry 获得入口
- entry_conditions: 对手压迫、踢击前后、摔控争夺或方向变化
- resulting_state: support base changed；产生新的攻击 / 防守路线
- applicable_range: close / mid
- applicable_level: standing
- physical_scale: realistic
- weight_transfer: one leg unloads while the other accepts body mass
- spatial_effect: Balance / Range / Direction 改变
- compatible_patterns: T02, T03
- incompatible_conditions: 当前完全腾空或支撑脚被锁死
- source_tags: shared, modern, traditional-martial

---

## 4. Technique Patterns

### T01｜短打截入 / Short Strike Interception

- type: Technique
- intent: 在对手动作尚未完成时，用短距离打击截断其进入
- entry_conditions: close range；存在肩轴、肘线、躯干或头部暴露窗口
- resulting_state: opponent line interrupted；形成继续压迫或换位入口
- applicable_range: close
- applicable_level: standing / mixed
- physical_scale: realistic
- contact_modality: strike / intercept
- target_area: context-dependent legal visible body target
- attacking_surface_or_weapon: fist / palm / forearm / elbow as context fits
- defensive_answer: 对手缩肘、偏轴、退步、封线或抓控
- force_or_control_effect: 打断节奏而非单次“必杀”
- compatible_patterns: M01, M03, X01
- source_tags: shared, modern, traditional-martial

### T02｜低线破支撑 / Low-line Base Disruption

- type: Technique
- intent: 用低线踢、蹬、扫或脚部干扰改变对手 Support Base / Balance
- entry_conditions: mid-close；对手一侧支撑明显或重心转移中
- resulting_state: base disturbed；Range / Axis / Recovery Window 改变
- applicable_range: mid / close
- applicable_level: low
- physical_scale: realistic
- contact_modality: low-line kick / sweep / stomp-like disruption by context
- target_area: lower leg / support line as appropriate for cinematic choreography
- attacking_surface_or_weapon: foot / shin
- defensive_answer: lift/check/withdraw/step/rebalance
- force_or_control_effect: 支撑变化，给下一次 Entry 让路
- compatible_patterns: M02, M04, X02
- source_tags: shared, modern, traditional-martial

### T03｜破平衡摔控入口 / Off-balance Takedown Entry

- type: Technique
- intent: 通过肩胯、躯干、腿部或握控关系破坏重心，而非原地抓腕
- entry_conditions: close contact；对手重心偏移或脚步尚未稳定
- resulting_state: opponent forced to step, bend, rotate or descend
- applicable_range: close
- applicable_level: standing-to-low
- physical_scale: realistic
- contact_modality: clinch / body control / off-balance
- target_area: torso / hip line / support relation
- attacking_surface_or_weapon: body frame / arms / leg reap when appropriate
- defensive_answer: widen base / post / turn / sprawl / re-step
- force_or_control_effect: Balance / Level / Position 改变
- compatible_patterns: M03, M04, X03
- source_tags: shared, modern, grappling

### T04｜全身连动反击 / Whole-body Linked Counter

- type: Technique
- intent: 让脚步、髋、躯干与上肢攻击成为一个连续动力链，而不是“脚步辅助上肢”
- entry_conditions: 对手刚造成 Contact / Miss / Axis deviation；当前可借 Momentum
- resulting_state: counter changes Range / Axis / Position
- applicable_range: mid / close
- applicable_level: standing / mixed
- physical_scale: realistic
- contact_modality: counter strike / body check / combined response
- attacking_surface_or_weapon: context-dependent
- defensive_answer: pivot / retreat / cover / re-intercept
- force_or_control_effect: whole-body displacement / initiative change
- compatible_patterns: M01, M02, M03, X01, X04
- source_tags: shared, modern, traditional-martial

---

## 5. Transition Patterns

### X01｜Contact → Movement Re-entry

- type: Transition
- intent: 把尚未断开的 Contact 直接转成换位 / 侧切 / 轴线变化入口
- from_state: contact exists; opponent action incomplete
- trigger: pressure direction or limb line changes
- handoff_basis: contact + axis + footwork
- to_state: new angle / range / position with immediate next Technique entry
- failure_or_fallback_path: contact lost → use visible footwork re-entry, do not reset pose
- source_tags: shared

### X02｜High → Low → High

- type: Transition
- intent: 让高低位变化成为连续攻防，而非单独蹲下或踢一脚
- from_state: high-line exchange
- trigger: opponent commits high / closes upper line
- handoff_basis: level + support + range
- to_state: low-line attack / takedown entry → rise into next counter
- failure_or_fallback_path: low entry blocked → angle exit while rising
- source_tags: shared, traditional-martial, modern

### X03｜Strike → Off-balance / Takedown

- type: Transition
- intent: 把打击造成的缩肘、偏轴、退步或重心移动直接交给摔控入口
- from_state: strike/contact causes defensive reaction
- trigger: opponent base narrows / weight shifts / axis turns
- handoff_basis: reaction + balance + close range
- to_state: takedown / body control / forced step
- failure_or_fallback_path: takedown denied → release into angle exit / short strike
- source_tags: shared, modern, grappling

### X04｜Failed Control → Angle Exit → Re-entry

- type: Transition
- intent: 摔控 / 抓控失败后不原地僵持，而是利用失败产生的方向变化继续战斗
- from_state: control attempt fails, contact partially remains
- trigger: opponent posts / turns / strips grip
- handoff_basis: momentum + axis + route
- to_state: side angle / renewed range with immediate attack or defense
- failure_or_fallback_path: full separation → maintain pressure with footwork, no neutral reset
- source_tags: shared, modern

---

## 6. Movement Causality Gate

Movement Pattern 命中不等于自动 PASS。

每次 Movement Pattern 实例化后必须检查：

```text
Movement
→ 是否真实改变 Level / Route / Axis / Range / Position / Support / Balance
→ 对手是否因此必须产生新的即时响应
→ 新 State 是否直接成为下一 Technique / Defense / Re-entry 的入口
```

PASS 示例逻辑：

```text
对手直线压入
→ 外侧斜切改变其对线
→ 对手必须旋髋 / 调步重新追线
→ 新暴露的 Support / Axis 成为下一动作入口
```

FAIL 示例逻辑：

```text
先用上肢完成格挡
→ 同时侧移一步
→ 再抓腕
```

如果去掉“侧移一步”后主要动作链基本不变，则 Movement 很可能只是装饰性 Footwork，判：

> **Movement Causality Failure / Upper-body Technique Dominance**

不能通过再补一个 Movement 词修复，必须重写动作因果。

---

## 7. G01 验证要求

这个验证集只有在以下结果出现时才算有价值：

- Movement 主动创造 Level / Route / Axis / Range / Position / Support 变化；
- Movement 产生的状态变化真实迫使对手响应，并成为下一动作入口；
- Lower-body / Balance / Takedown 在合适 Fighting Direction 下真实进入链条；
- 关键 Exchange 不再反复依赖“前臂偏转 → 肩线封堵 → 抓腕 / 顶肩”；
- Pattern Hit 可以从 `Gap → Slot → Pattern → Detail → Concrete Phrase` 被追踪；
- 不同角色已确认的 System / Expression / Archetype 不因共享本最小集而被同质化；
- 仍保持 V2-49 的具体因果与 Motion / Initiative Handoff；
- 不因为更具体而把 15 秒压缩回少量大 Phrase。

若最小集正确命中、Movement Causality 与 Trace 都 PASS 后仍持续退化，才进入 Knowledge Coverage Audit。
