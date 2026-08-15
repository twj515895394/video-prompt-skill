# Action Combat Video — Concrete Choreography Implementation Plan

> 状态：**Implementation Plan 已建立；尚未开始 Runtime 修改。**
>
> 设计真源：`docs/action-combat-video-concrete-choreography-knowledge-spec.md`
>
> 上游 V2 Spec：`docs/action-combat-video-v2-spec.md`
>
> 回归真源：`docs/action-combat-video-v2-regression.md`
>
> 上游历史实施计划：`docs/action-combat-video-v2-implementation-plan.md`
>
> 本计划职责：把 CK-13～CK-19 以及与其直接相关的 CK-01～CK-12，映射为最小 Runtime 修改、最小 Pattern 验证集、固定 G01 Prompt Regression 与 Knowledge Expansion Gate。本文不重写 V2-46～V2-49 已完成实施历史。

---

## 1. 实施目标

本轮只解决两个已经由固定 G01 暴露并确认的问题：

1. **颗粒度越细，动作链数量反而下降**；
2. **动作长期偏上肢控制 / Static Standing Combat，Movement 没有真正成为 Choreography Source。**

本轮不追求建设完整武术知识库，也不新增一级 Combat Engine。

目标链：

```text
Fighting Direction / 怎么打
→ Stage-2 按方向和当前 Gap 读取最小 Pattern Knowledge
→ Movement / Technique / Transition 参与 Concrete Action Phrase
→ Lightweight Granularity Budget 保留更多 Exchange
→ Final Preflight 拦截 Static Standing Combat / Upper-body Dominance
→ 固定 G01 Prompt Regression
→ PASS 后才允许 Knowledge Expansion
```

核心原则：

> **能通过一次高价值交互明确创作方向，就不堆复杂自动推断；Runtime 复杂度只用于把用户选择执行好。**

> **先用最小知识证明结构有效，再决定知识库要扩多大。**

---

## 2. 实施范围与明确不做

### 本轮实施

- Fighting Direction Interactive；
- 与旧“核心动作风格 / Choreography Profile”交互合并；
- Fighting Direction 候选答案动态生成规则；
- Stage-2 Gap-driven Routing；
- 最小 Movement / Technique / Transition Pattern 验证集；
- Lightweight Action Phrase Budget；
- Static Standing Combat / Upper-body Technique Dominance Preflight；
- 固定 G01 Prompt Regression；
- Regression Gate 与 Knowledge Expansion Gate。

### 本轮不做

- 不新增 Lower-body Engine；
- 不新增 Body Method State Machine；
- 不建立门派 / 拳种 Runtime 招式树；
- 不建立大型固定招式序列库；
- 不为 Modern / Traditional / Wuxia 各复制完整知识库；
- 不扩大型 Fighting / Martial / Weapon Library；
- 不修改 Model Adapter；
- 不新增固定动作数、字数、秒数或 Granularity 比例；
- 不固定每次 Stage-2 必须加载 Movement / Technique / Transition 三槽；
- 不修改已经验证有效的 V2-46 Camera Coverage 架构。

---

## 3. 两阶段实施门禁

```text
Phase CK-1｜Runtime Minimal Validation
→ Interactive Fighting Direction
→ Stage-2 Routing
→ Minimum Pattern Set
→ Lightweight Granularity Budget
→ Static Standing Combat Preflight
→ Static Read / Structural Gate

Phase CK-2｜Fixed G01 Prompt Regression
→ 同输入 Interactive
→ Fighting Direction Realization
→ Pattern Hit Evidence
→ Choreography Richness Preservation
→ Upper-body Dominance Improvement
→ Prompt PASS / FAIL

PASS
→ 才允许进入 Knowledge Expansion

FAIL
→ 先判断 Routing / Realization / Granularity / Preflight 哪一层失败
→ 不直接扩建知识库
```

只有 CK-2 PASS 后，才进入后续 Generated Video Re-run 与更大 Knowledge Coverage Audit。

---

## 4. Runtime File Mapping

### 4.1 `assets/templates/mode-interactive-output-contract.md`

**对应：CK-13 / CK-14 / CK-16。**

实施内容：

1. 把 `Fighting Direction / 怎么打` 加入 Conditional High-value Question Pool；
2. 暴露条件：

```text
Fighting Direction already clear?
├─ yes → inherit, don't ask
└─ no
   └─ 不同打法会显著改变成片动作内容？
      ├─ no → silently infer baseline
      └─ yes → ask Fighting Direction
```

3. 原“核心动作风格 / Choreography Profile”不再作为另一轮高度重叠问题；
4. Fighting Direction 一轮同时承载必要的 Rhythm / Realism / Impact / Physical Scale 属性；
5. 候选答案：
   - 至少 5 个有实质差异的候选；
   - 默认 6～8 个；
   - 复杂场景可到 10 个；
   - 始终允许自定义；
   - 不机械凑数；
   - 每个候选必须在 Movement / Technique / Range / Physical Scale / 节奏等至少一个动作维度有真实差异；
6. 继续遵守 One Question / One Primary Decision Node；
7. 不改变 10-round Safety Cap，也不把 Fighting Direction 改成所有场景固定必问。

**静态验收：**

- 用户已明确 MMA / 咏春 / 轻功剑战等时不会重复问；
- 用户未明确且存在多个高价值打法时可以问；
- 不再连续出现“核心动作风格？”和“怎么打？”两轮同义问题；
- 候选数量与差异性满足 Spec。

---

### 4.2 `references/tasks/action-combat-video/choreography-playbook.md`

**对应：CK-01 / CK-05 / CK-12 / CK-15 / CK-17。**

实施内容：

#### A. Fighting Direction Consumption

Planning / Choreography 必须消费已经确认的 Fighting Direction，并把它映射到：

- Movement 倾向；
- Technique 倾向；
- Range / Level 倾向；
- Physical Scale；
- Rhythm / Realism / Impact 属性。

不允许只把 Fighting Direction 写成 Meta 标签而不改变动作构造。

#### B. Stage-2 Gap-driven Routing

Stage-2 从当前 Planning / Phrase Gap 判断缺口：

```text
Movement Gap
→ 路线 / 身法 / 高低位 / 重心 / Axis / Position / Support

Technique Gap
→ 具体攻击 / 防守 / 腿法 / 摔控 / 兵器动作

Transition Gap
→ Contact / Range / Axis / Momentum 如何进入下一动作
```

每个被命中 Slot 默认：

```text
1 主 Pattern
+ 必要时 1 辅 Pattern
```

不是固定三槽全开，也不是必须填满 1 主 + 1 辅。

#### C. Lightweight Action Phrase Budget

```text
Major Reversal / Initiative Theft / Signature Moment
→ High Granularity

普通 Exchange / Re-counter / Range Change
→ Medium Granularity

纯连接 / 非关键过渡
→ Low Granularity
```

规则：

- 连续两个 High Granularity 后，后续普通 Exchange 优先压缩为 Medium / Low；
- High 只展开承担关键因果的细节；
- Medium / Low 仍必须保留基本动作因果，不能退化成“连续格挡 / 快速反制”；
- 不规定固定 Phrase 数、动作数、字数、秒数。

#### D. Static Standing Combat Risk

High / Expert Combat 若连续关键 Phrase：

- 主要依靠前臂 / 肩线 / 抓腕 / 上臂控制；
- Movement 只是辅助脚步说明；
- 没有主动创造 Level / Route / Axis / Range / Position / Support / Balance 变化；

则标记：

`Movement Knowledge Gap / Static Standing Combat Risk`

并提高 Movement Slot 的路由优先级。

**静态验收：**

- Fighting Direction 被 Choreography 明确消费；
- Stage-2 不再只是泛化“读取 Execution Knowledge”；
- Granularity 有 High / Medium / Low 信息深度规则；
- 没有动作数量配额；
- Upper-body Dominance 有明确 Routing 修正入口。

---

### 4.3 `references/tasks/action-combat-video/index.md`

**对应：CK-12 / CK-18 / CK-19。**

只做最小 Mandatory Path 强化，不新增一级 Engine：

```text
Combat Planning Context
→ Fighting Direction resolved / inherited
→ Stage-2 Knowledge Gap Detection
→ Relevant Pattern Detail
→ Concrete Action Phrase Construction
→ Core State Validation
→ Camera / Audio / Spatial Coordination
→ Prompt Assembly
→ Final Preflight
```

需要明确：

- Fighting Direction 是 Stage-2 选择知识的上游条件之一；
- Stage-2 必须能够命中最小 Pattern Set；
- Pattern Detail 与 Concrete Action Phrase 之间不能跳过；
- 最小验证阶段不要求扩完整 Library。

**静态验收：** Read List / Mandatory Path 能解释为什么某个 Pattern 被读取。

---

### 4.4 新增最小 Pattern 验证集

**对应：CK-03～CK-12 / CK-18。**

推荐新增轻量知识目录：

```text
references/libraries/combat-choreography-patterns/
├─ index.md
├─ movement-patterns.md
├─ technique-patterns.md
└─ transition-patterns.md
```

这是验证期物理结构，不承诺最终长期必须保持四文件结构。

#### `index.md`

只包含：

- Pattern 三分类；
- Shared Core Schema；
- Specialist / Physical Scale 标签说明；
- Routing 索引；
- 何时读取哪一个叶子文件。

#### `movement-patterns.md`

只放少量、明显不同的验证 Pattern，例如：

- 外侧切入 / 绕侧换位；
- Level Change / 沉身进入；
- 轴线旋转 / 转身换侧；
- 支撑 / 重心改变；
- 跌扑 / 恢复 / Re-entry（如 G01 可用）。

#### `technique-patterns.md`

少量验证 Pattern：

- 上肢短打；
- 低线腿法 / 踢蹬扫；
- 摔控 / 破平衡入口；
- 全身连接式攻击。

#### `transition-patterns.md`

少量验证 Pattern：

- Contact → Movement Re-entry；
- High → Low → High；
- Strike → Control / Takedown；
- Failed Control → Angle Exit → Re-entry。

这些只是验证类型，不是最终固定 Pattern 名单。

#### Schema

共享核心：

```text
id
name
type
intent / function
entry_conditions
resulting_state
applicable_range
applicable_level
physical_scale
compatible_patterns
incompatible_conditions
source_tags
```

Movement / Technique / Transition 只追加各自必要专项字段，不建立全字段巨型 Schema。

**最小集验收：**

- G01 能实际命中不同 Pattern；
- Movement Pattern 能真正改变动作路线 / Level / Axis / Position，而不是只生成“向前一步”；
- Pattern 可组合，不是一整个固定招式套路；
- 不出现门派 → 固定招式树；
- 不出现 Wuxia 能力污染 Modern G01。

---

### 4.5 `references/controls/prompt-assembly/control.md`

**对应：CK-15 / CK-17。**

实施内容保持最小：

1. 保留 V2-49 Concrete Choreography In → Out；
2. 增加 Granularity Distribution 的序列化原则：
   - High 保留关键因果；
   - Medium 压缩次要身体细节；
   - Low 保留连接但不膨胀；
3. 不把经过 Pattern 具体化的动作重新总结为抽象词；
4. Fighting Direction 选定后，Final Prompt 的动作语言必须有可观察差异；
5. 不因 Movement 细节增加而破坏 Camera Coverage / Action Continuity。

**静态验收：** Prompt Assembly 不重新吃掉 CK-17 给动作链释放的预算。

---

### 4.6 Combat Final Preflight（沿现有文件落地，不新建 Gate Engine）

**对应：CK-15 / CK-17 / CK-19。**

新增 / 强化两个检查：

#### Static Standing Combat / Upper-body Technique Dominance

FAIL / REWRITE 条件：

- High / Expert Combat 连续多个关键 Phrase 都主要由上肢 Contact 主导；
- Movement 没有主动创造 Level / Route / Axis / Range / Position / Support / Balance 等变化；
- Prompt 虽写“转髋 / 脚步 / 降低重心”，但它们只服务上肢控制，没有改变战斗空间或动作入口。

#### Choreography Richness Preservation

FAIL / REWRITE 条件：

- 因高颗粒度展开导致 15 秒再次只有约 2～3 个大 Exchange；
- 连续普通 Exchange 被全部写成 High Granularity 大段；
- 为保留数量又退回抽象动作块。

Preflight 只要求修正信息展开深度和动作构造，不使用固定动作数量配额。

---

### 4.7 本轮冻结文件

除非实施中发现直接阻断，不主动修改：

- `references/tasks/action-combat-video/core-playbook.md`；
- `references/tasks/action-combat-video/modern-combat-playbook.md`；
- `references/tasks/action-combat-video/cinematic-wuxia-playbook.md`；
- `references/libraries/combat-fighting-profiles/library.md`；
- `references/controls/camera-direction/control.md`；
- `assets/templates/single-shot-video-template.md`；
- Model Adapters。

特别说明：

> 当前 G01 最新 Read List 没有命中原 `combat-fighting-profiles/library.md`。本轮先通过新的最小 Pattern Routing 证明 Stage-2 调用链有效，不顺手扩原大库。

---

## 5. 开发执行顺序

### CK-Step 1｜Interactive Fighting Direction

修改：

- `assets/templates/mode-interactive-output-contract.md`

验收：

- G01 会在打法未明确时产生一轮“怎么打”；
- 5～10 个有效候选；
- 不再单独重复问旧核心动作风格；
- 若用户输入已明确打法则不问。

---

### CK-Step 2｜Minimum Pattern Knowledge

新增：

- `references/libraries/combat-choreography-patterns/index.md`
- `movement-patterns.md`
- `technique-patterns.md`
- `transition-patterns.md`

验收：

- 三类职责清楚；
- Schema 小核心 + 专项扩展；
- 每类只含最小验证样例；
- 无门派套路树 / 无大知识库扩建。

---

### CK-Step 3｜Stage-2 Routing / Choreography Consumption

修改：

- `references/tasks/action-combat-video/choreography-playbook.md`
- `references/tasks/action-combat-video/index.md`

验收：

- Fighting Direction 可以影响 Pattern 选择；
- Planning Gap 决定 Slot；
- Read List 能命中 Pattern；
- 不是三槽强制全读；
- Upper-body Dominance 能触发 Movement Gap。

---

### CK-Step 4｜Granularity Distribution / Assembly

修改：

- `references/tasks/action-combat-video/choreography-playbook.md`
- `references/controls/prompt-assembly/control.md`

验收：

- High / Medium / Low 信息深度区分；
- 连续高颗粒度后普通 Exchange 会压缩；
- Medium / Low 仍具体；
- 无动作数 / 字数 / 秒数固定配额。

---

### CK-Step 5｜Final Preflight

在现有 Combat Preflight 中加入：

- Static Standing Combat；
- Upper-body Technique Dominance；
- Choreography Richness Preservation。

验收：

- “有脚步词但仍原地打手”不能通过；
- “动作很具体但只有 2～3 大段”不能直接通过；
- Failure rewrite 不靠固定踢腿 / 换位配额。

---

### CK-Step 6｜Static Read / Structural Gate

逐文件回读：

- Interactive Contract；
- Combat Index；
- Choreography Playbook；
- Pattern Index + 三类叶子知识；
- Prompt Assembly；
- Regression。

确认：

```text
Fighting Direction
→ Stage-2 Gap
→ Pattern Hit
→ Concrete Phrase
→ Granularity Distribution
→ Assembly
→ Static Standing / Richness Preflight
```

真实闭环存在。

Static PASS 前不运行 G01。

---

### CK-Step 7｜Fixed G01 Prompt Regression

固定输入、Interactive、15s、Generic，不换场景。

必须记录：

- Read List；
- Interactive Questions / Answers；
- Fighting Direction 选项与用户选择；
- Stage-2 Pattern Hit Evidence；
- Final Prompt；
- High / Medium / Low Granularity Evidence；
- Exchange / Action Chain 变化；
- Static Standing / Upper-body Dominance 证据；
- Camera 是否保持 V2-46 能力；
- PASS / PARTIAL / FAIL。

---

## 6. CK-2 Fixed G01 三个核心 Gate

### Gate A｜Fighting Direction Realization

PASS：

- 询问在需要时出现；
- 候选答案 5～10 个且有真实动作差异；
- 用户选择被 Final Prompt 具体兑现；
- 不只是写一个打法标签。

FAIL：

- Fighting Direction 未出现且存在明显高价值分叉；
- 与旧 Profile 重复询问；
- 选择不同方向却输出几乎同样动作骨架。

### Gate B｜Choreography Richness Preservation

PASS：

- V2-49 的具体因果仍保留；
- 普通 Exchange 使用 Medium / Low 压缩后，15 秒动作链不因“写得更细”继续减少；
- 不靠抽象词伪造动作数量。

FAIL：

- Final Prompt 仍只有约 2～3 个巨大 Exchange；
- 每个 Phrase 都以 High Granularity 展开；
- 为增加数量又退回“快速反制 / 持续缠斗”。

### Gate C｜Upper-body Dominance Improvement

PASS：

Movement 至少真实创造部分：

- Level；
- Route / Angle；
- Axis；
- Range；
- Position；
- Support / Balance；
- Ground / Standing（适用时）。

并且动作骨架不再主要反复：

`前臂偏转 → 肩线封堵 → 抓腕 / 顶肩 → 再重复`

FAIL：

- 仍长时间原地上肢控制；
- Movement 只作为“脚步补充说明”；
- 加了一次腿法后又回到同一上肢骨架。

---

## 7. Knowledge Expansion Gate

只有 Gate A + B + C 全部 PASS，才允许扩更大 Knowledge Coverage。

如果失败，先定位：

```text
A FAIL
→ Interactive / Fighting Direction Consumption

B FAIL
→ Granularity Distribution / Prompt Assembly / Temporal Packing

C FAIL
→ Stage-2 Routing / Pattern Realization
```

只有以下情况才进入 Knowledge Coverage Audit：

```text
Routing 正确
+ Pattern 实际读取
+ Fighting Direction 已兑现
+ Granularity 正确
+ Assembly 保真
+ Preflight 有效
+ G01 仍持续动作贫乏 / 上肢主导
```

此时才扩 Movement / Technique / Transition Pattern 数量或研究更多来源知识。

---

## 8. Regression 文件映射

正式验收真源继续使用：

`docs/action-combat-video-v2-regression.md`

实施后需要保持以下记录：

- Static Gate；
- Fighting Direction Realization；
- Stage-2 Pattern Hit；
- Granularity Distribution；
- Choreography Richness Preservation；
- Static Standing Combat / Upper-body Technique Dominance；
- Prompt Intent → Result Gap；
- Knowledge Expansion Gate。

不另建第二套同级 Regression 真源。

---

## 9. Traceability Matrix

| CK | Runtime / Artifact | 主要验收 |
|---|---|---|
| CK-01 / CK-17 | choreography-playbook + prompt-assembly | High / Medium / Low；动作链不因细化继续减少 |
| CK-03～CK-11 | minimum Pattern set | Movement / Technique / Transition 可组合；小核心 Schema |
| CK-12 | choreography-playbook + index + pattern index | Planning Gap → Slot → Pattern Hit |
| CK-13 | interactive contract | 条件询问“怎么打” |
| CK-14 | interactive contract | 5～10 个有实质差异候选 |
| CK-15 | choreography + Final Preflight + Regression | Static Standing / Upper-body Dominance Gate |
| CK-16 | interactive contract | 合并旧核心动作风格，不重复问 |
| CK-18 | minimum Pattern set + G01 | 最小知识验证架构，不扩大库 |
| CK-19 | 本 Plan + Regression | CK-1 → CK-2 → Knowledge Expansion Gate |

---

## 10. 当前状态

| 项目 | 状态 |
|---|---|
| Concrete Choreography Spec | ✅ 已确认 |
| CK-13～CK-19 Regression Gate | ✅ 已写入回归真源 |
| 本 Implementation Plan | ✅ 已建立 |
| Runtime CK-Step 1～5 | ⏳ 未实施 |
| Static Read Gate | ⏸ 等 Runtime 修改 |
| Fixed G01 Prompt Regression | ⏸ 等 Static PASS |
| Knowledge Expansion | 🔒 Gate 未开放 |

当前准确状态：

> **设计已收口；实施计划已建立；下一步可以开始 CK-Step 1 Runtime 实施。**
