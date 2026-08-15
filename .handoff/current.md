# Action Combat Concrete Choreography — Session Handoff

> 更新时间：2026-08-15
>
> 当前状态：**Concrete Choreography Knowledge 设计已收口；CK-Step 1～6 Runtime 实施完成并通过 Static Read；下一步是固定 G01 的真实 Interactive → Final Prompt Regression。**
>
> 用途：下一个会话直接读取本文件，用户会带回实际生成提示词过程、Interactive 对话、Read List 和 Final Prompt；基于这些真实结果继续分析，不重新设计已经确认的规则。

---

## 1. 当前主目标

本轮工作始于固定 G01 办公室格斗测试暴露的两个问题：

1. **Executable Granularity 变细后，15 秒内动作链 / Exchange 数量反而下降**；
2. **动作长期偏上肢控制 / Static Standing Combat**：大量前臂、肩线、抓腕、顶肩，上肢在“打”，脚步 / 转髋 / 重心只是附属说明。

当前解决策略已经确认并实施为：

```text
Fighting Direction / 怎么打
→ Stage-2 Gap Detection
→ Movement / Technique / Transition Pattern
→ Concrete Action Phrase
→ High / Medium / Low Granularity Distribution
→ Prompt Assembly 保真
→ Static Standing / Upper-body Dominance Preflight
→ Fixed G01 Regression
```

核心原则：

> **能通过一次高价值交互明确“怎么打”，就不要为了同一件事堆复杂自动推断。**

> **先用最小 Pattern 验证结构有效，再决定是否扩知识库。**

---

## 2. 重要设计真源

### 新 Spec

`docs/action-combat-video-concrete-choreography-knowledge-spec.md`

承载 V2-49 之后的新设计，不再继续膨胀旧 V2 Spec。

### 新 Implementation Plan

`docs/action-combat-video-concrete-choreography-implementation-plan.md`

当前状态已经更新为：

> **CK-Step 1～6 已完成；Runtime Minimal Validation 已通过 Static Read；下一步进入固定 G01 Prompt Regression。**

### Regression 真源

`docs/action-combat-video-v2-regression.md`

继续作为唯一正式验收真源，没有另建第二套 Regression。

### 旧 V2 设计 / 实施历史

- `docs/action-combat-video-v2-spec.md`
- `docs/action-combat-video-v2-implementation-plan.md`
- `docs/action-combat-video-v2-traceability-audit.md`

这些主要保留 V2-01～V2-49 历史，不要再把本轮新设计大段追加进去。

---

## 3. 本轮已确认核心决策 CK-01～CK-19

### CK-01 / CK-17｜Lightweight Action Phrase Budget

颗粒度只控制**信息展开深度**，不规定固定动作数、字数、秒数或占比。

```text
Major Reversal / Initiative Theft / Signature Moment
→ High Granularity

普通 Exchange / Re-counter / Range Change
→ Medium Granularity

纯连接 / 非关键过渡
→ Low Granularity
```

额外规则：连续两个 High 之后，后续普通 Exchange 优先压缩成 Medium / Low，避免再次把 15 秒吃成 2～3 个大段。

Medium / Low 仍必须保留基本动作因果，不能退回“连续格挡 / 快速反制 / 持续缠斗”。

---

### CK-02｜Routing First, Knowledge Second

先证明 Stage-2 知识被真正读取 / 使用，再判断知识量够不够。

```text
Stage-2 Routing Audit
→ Knowledge Realization Test
→ Knowledge Coverage Audit
```

只有 Routing 正确、Pattern 真正进入 Final Prompt 之后仍持续退化，才扩知识库。

---

### CK-03～CK-10｜Movement + Technique + Transition

目标不是单独“多加腿法”，而是让**身体本身就在打**。

```text
Movement Pattern
+ Technique Pattern
+ Transition Pattern
+ Opponent Response
+ Current Combat State
→ Concrete Action Phrase
```

Movement 负责：

- 身法；
- 步法 / 步型；
- 重心转换；
- Level Change；
- Axis；
- Route / Angle；
- Position；
- 转身 / 绕位 / 穿越；
- 跌扑 / 滚转 / 起身；
- Wuxia 时 Ground↔Air / 轻功 / 腾空等。

Technique 负责具体 Strike / Kick / Grapple / Throw / Weapon。

Transition 负责前一个 Contact / Range / Axis / Momentum 为什么能进入下一动作。

Pattern 是一级生产知识；门派 / 拳种只是 source/style tags，不建立“人物属性 → 猜门派 → 固定招式树”。

---

### CK-11｜Shared small core Schema

最小 Shared Core：

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

Movement / Technique / Transition 各自追加少量专项字段，不建立巨型万能 Schema。

---

### CK-12｜Stage-2 Gap-driven Routing

不再固定加载 Technique + Enhancement，也不固定三槽全读。

```text
当前 Phrase 缺什么？
├─ 路线 / 身法 / Level / 重心 / Axis / Position
│  → Movement Slot
├─ 具体攻击 / 防守 / 腿法 / 摔控 / Weapon
│  → Technique Slot
└─ 前后动作怎么从 Contact / Range / Axis / Momentum 接起来
   → Transition Slot
```

每个被命中的 Slot：

```text
1 个主 Pattern
+ 必要时 1 个辅助 Pattern
```

High / Expert Combat 如果长期 Upper-body 主导、Movement 只是附属脚步说明，则视为 `Movement Knowledge Gap / Static Standing Combat Risk`，提高 Movement Slot 优先级。

---

### CK-13 / CK-14 / CK-16｜Fighting Direction / “怎么打”

Interactive 模式增加一个条件暴露的高价值问题：

> **你希望这场战斗具体怎么打？**

这是比旧“核心动作风格 / Choreography Profile”更上游的决策。

旧 Choreography Profile 不再作为另一轮重复交互；其中节奏、写实度、重量感、电影化程度等并入 Fighting Direction 的执行属性。

暴露条件：

```text
Fighting Direction 已明确？
├─ yes → inherit，不重复问
└─ no
   └─ 不同打法是否会显著改变动作内容？
      ├─ no → silently infer baseline
      └─ yes → 直接问“怎么打”
```

候选答案规则：

- 至少 5 个；
- 正常 6～8 个；
- 复杂场景可到 10 个；
- 始终支持自定义；
- 不能为凑数量提供同义项；
- 每个候选必须在 Movement / Technique / Range / Physical Scale / Rhythm 等动作层面有真实差异。

已给 G01 准备的候选池：

1. 现代职业杀手近身格斗
2. 中国武术电影化近身格斗
3. 综合格斗 / MMA
4. 硬派实战短打
5. 灵活身法 / 角度争夺
6. 摔控 / 反摔
7. 腿法 + 全身攻防
8. 电影化混合动作
9. 指定武术 / 格斗体系
10. 自定义

本轮推荐用于 G01 Regression 的方向：

> **2. 中国武术电影化近身格斗**

原因：最容易同时验证 Movement、步法、腿法、Level、Axis、Route、Transition 是否真的进入动作构造，而不是只“多加一脚”。

---

### CK-15｜Static Standing Combat / Upper-body Dominance Gate

High / Expert Combat 如果连续多个关键 Phrase 都主要由上肢 Contact 主导，而 Movement 没有主动创造以下变化，则 FAIL / REWRITE：

- Level；
- Route / Angle；
- Axis；
- Range；
- Position；
- Support / Balance；
- Ground / Standing 或 Ground / Air（适用时）。

即使 Prompt 写了“转髋 / 脚步 / 降低重心”，但这些只服务上肢控制、没有改变战斗空间或下一动作入口，也不能判 PASS。

Failure Signatures：

- `Static Standing Combat`
- `Upper-body Technique Dominance`
- 继续兼容旧 `Upper-body Combat Lock / Kinetic Underfill`

---

### CK-18｜Minimum Pattern Validation Set

只建立一个很小的验证集，不做完整武术知识库。

实际落地文件：

`references/libraries/combat-choreography-patterns/minimum-validation-set.md`

注意：Implementation Plan 最初曾设计成 4 文件，Static Read 后已经改回与实际实现一致的**单文件最小集**。

当前包含：

#### Movement

- M01 外侧斜切 / Outside Angle Cut
- M02 沉身换位 / Level Drop Reposition
- M03 轴线旋转脱离 / Axis-turn Exit
- M04 支撑转换 / Support-base Transfer

#### Technique

- T01 短打截入 / Short Strike Interception
- T02 低线破支撑 / Low-line Base Disruption
- T03 破平衡摔控入口 / Off-balance Takedown Entry
- T04 全身连动反击 / Whole-body Linked Counter

#### Transition

- X01 Contact → Movement Re-entry
- X02 High → Low → High
- X03 Strike → Off-balance / Takedown
- X04 Failed Control → Angle Exit → Re-entry

这些 Pattern 不能直接拼成固定 Combo；必须结合当前 Range / Contact / Axis / Position / Momentum / Opponent Response 重写成 Concrete Action Phrase。

---

### CK-19｜Two-stage Implementation Gate

```text
Phase CK-1｜Runtime Minimal Validation
→ Interactive Fighting Direction
→ Stage-2 Routing
→ Minimum Pattern Set
→ Lightweight Granularity Budget
→ Static Standing Combat Preflight
→ Static Read

Phase CK-2｜Fixed G01 Prompt Regression
→ Fighting Direction Realization
→ Pattern Hit Evidence
→ Choreography Richness Preservation
→ Upper-body Dominance Improvement
```

只有 CK-2 三个核心 Gate 全 PASS，才允许更大的 Knowledge Expansion。

---

## 4. 已实施 Runtime 文件与当前状态

### 4.1 Interactive Contract

`assets/templates/mode-interactive-output-contract.md`

已实现：

- Fighting Direction 条件暴露；
- 5～10 个候选答案；
- 支持自定义；
- 不再重复问旧 Choreography Profile；
- 继续遵守 One Question / One Primary Decision Node；
- Camera Intent 仍是条件高价值问题，不固定必问；
- 10-round Safety Cap 不变。

相关 commit：

`53957536b60534ba1203e7aeb519033150d562b6`

---

### 4.2 Task Router / Index

`references/tasks/action-combat-video/index.md`

已实现：

- Planning Context 加入 Fighting Direction；
- Stage-2 改成 Gap-driven Routing；
- 当前最小知识源明确指向 `minimum-validation-set.md`；
- Pattern → Concrete Phrase 不能跳过；
- Upper-body Dominance 触发 Movement Gap；
- Final Preflight 加入 Static Standing / Upper-body Dominance；
- Lightweight Granularity Budget 接入 Mandatory Path。

相关 commit：

`5beb047e8640ab6dc547d2d56690f5c244de1946`

---

### 4.3 Choreography Playbook

`references/tasks/action-combat-video/choreography-playbook.md`

Static Read 时发现它仍残留旧：

```text
Cinematic Choreography Profile
+ fixed Technique / Enhancement slots
```

已修正为：

```text
Fighting Direction
→ Stage-2 Knowledge Gap Detection
→ Relevant Movement / Technique / Transition Pattern
→ Concrete Action Phrase
```

旧 Choreography Profile 只保留为 execution attributes / evidence，不再是第二套上游用户决策。

相关 commit：

`e949349b508a75895d5b966d999708902f22c6c3`

---

### 4.4 Prompt Assembly

`references/controls/prompt-assembly/control.md`

Static Read 时发现：原本能保留 V2-49 Concrete Choreography，但不知道：

- High / Medium / Low Granularity Distribution；
- Fighting Direction Realization。

已补齐：

- Granularity Distribution Preservation；
- 连续两个 High 后普通 Exchange 不重新展开成第三个大段；
- Medium / Low 仍保持可执行因果；
- Fighting Direction 必须通过可观察动作语言兑现；
- 如果不同 Fighting Direction 最终仍退化成同一套上肢控制骨架，判 Assembly / Pattern Realization 失败。

相关 commit：

`c000ffc1d47b238a87e94442beb9a12d2e0ad87e`

---

### 4.5 Minimum Pattern Validation Set

`references/libraries/combat-choreography-patterns/minimum-validation-set.md`

相关 commit：

`8c98828729970e25aeee612a6d5426d293d8f160`

---

### 4.6 Regression

`docs/action-combat-video-v2-regression.md`

已加入并更新：

- Fighting Direction Realization；
- Stage-2 Pattern Hit；
- Granularity Distribution；
- Choreography Richness Preservation；
- Static Standing / Upper-body Dominance；
- Knowledge Expansion Gate；
- M16 Fighting Direction Realization；
- M17 Movement Contribution；
- M18 Upper-body Dominance / Static Standing Combat。

Static Read 后状态已经同步为 CK-1 Runtime / Static PASS，CK-2 G01 Pending。

相关 commit：

`efd7c7db02fd84de7e50ade2ca665c47111e3629`

---

### 4.7 Concrete Choreography Implementation Plan

`docs/action-combat-video-concrete-choreography-implementation-plan.md`

已同步实际物理结构和实施状态。

当前顶部状态：

> **CK-Step 1～6 已完成；Runtime Minimal Validation 已通过 Static Read；下一步进入固定 G01 Prompt Regression。**

相关 commit：

`f8ac47ec7841ff8e19cd7d178ebe6c11d4b0772d`

---

## 5. CK-Step 6 Static Read 结论

Static Read 检查链：

```text
Fighting Direction
→ Stage-2 Gap
→ Pattern Hit
→ Concrete Phrase
→ Granularity Distribution
→ Assembly
→ Static Standing / Richness Preflight
```

结论：**PASS**。

期间发现并修复两个真实断点：

1. `choreography-playbook.md` 仍保留旧 Profile / fixed slot 路径；
2. `prompt-assembly/control.md` 未消费 Granularity Distribution 和 Fighting Direction Realization。

修复后 Runtime 当前没有已知结构断点。

注意：Static PASS 只表示规则链条接线完整，**不表示真实 Prompt 或真实成片已经 PASS。**

---

## 6. 下一步固定 G01 Prompt Regression

### G01 固定输入

继续使用同一个办公室案例，不换测试场景：

> 使用交互模式，帮我做一段一个女生和男生在办公室打架的15秒电影片段，实际两个人穿着正常的职场服装但其实是2个杀手组织的职业杀手。中国男女，女的22岁长发高马尾漂亮身材完美，男性是一个秃顶又矮又胖的55岁领导，贴身搏斗，不要隔着什么办公桌。

要求：

- Interactive；
- 15s；
- Generic model，除非测试时另行指定；
- 不改变人物 / 场景条件；
- 不换 Golden Scenario；
- 本轮 Fighting Direction 推荐选择：**中国武术电影化近身格斗**。

---

## 7. 下个会话用户需要带回的真实结果

用户会在新会话反馈实际运行结果。优先收集：

1. **完整 Interactive 对话**
   - 每一轮问题；
   - 每轮给出的候选答案；
   - 用户选择；
   - 是否真的出现 Fighting Direction / “怎么打”；
   - 是否又重复问旧“核心动作风格”；
   - Camera Intent 是否在合理时机出现。

2. **Read List / Knowledge Hit Evidence**
   - 实际读取了哪些 Runtime 文件；
   - 是否命中 `references/libraries/combat-choreography-patterns/minimum-validation-set.md`；
   - 如果能看到内部说明，记录实际命中的 Movement / Technique / Transition Pattern。

3. **Final Prompt 全文**
   - 不要只给摘要；
   - 需要看到完整 Action Spine / Camera / Ending。

4. **如果已经生成视频**
   - 可进一步带回视频结果 / 截图 / 观察描述；
   - 但 Prompt-level Gate 必须先独立判断，不能因为视频“看起来还行”跳过 Prompt 分析。

---

## 8. 下个会话分析顺序

收到真实对话 / Prompt 后，**不要继续 Grill Me 新设计**，先做 Regression。

### Gate A｜Fighting Direction Realization

检查：

- 用户未明确时是否真的问“怎么打”；
- 候选是否 5～10 个且有实质动作差异；
- 是否与旧 Choreography Profile 重复询问；
- 用户选择“中國武术电影化近身格斗”后，Final Prompt 是否真的出现：
  - 身法；
  - 步法；
  - 腿法；
  - 高低位；
  - Axis / Route / Position 变化；
  - 全身动作链。

FAIL 示例：只在 Prompt 开头写“中国武术电影化”，动作骨架仍是旧的前臂 / 肩线 / 抓腕。

---

### Gate B｜Choreography Richness Preservation

检查：

- V2-49 的具体因果是否还在；
- 是否出现 High / Medium / Low 信息深度差异；
- 普通 Exchange 是否适度压缩；
- 是否还只有约 2～3 个巨大 Exchange；
- 是否为了增加数量又退回抽象“连续攻防”。

特别比较旧 G01：旧版虽然具体，但大约只有 3 组主要 Exchange。

目标不是固定“必须 N 个 Exchange”，而是验证**颗粒度变细不再明显挤压动作链数量**。

---

### Gate C｜Upper-body Dominance Improvement

检查 Movement 是否主动创造：

- Level；
- Route / Angle；
- Axis；
- Range；
- Position；
- Support / Balance。

核心判断：

> 是否仍然主要是“人物站在原地，上半身复杂地打”。

FAIL 示例：

```text
前臂偏转
→ 肩线封堵
→ 抓腕 / 顶肩
→ 加一次踢腿
→ 又回到前臂偏转 / 抓腕
```

这仍应判 Upper-body Dominance。

---

## 9. Pattern Hit 重点

如果 Runtime Read List 没有读取 `minimum-validation-set.md`：

> 优先判 Stage-2 Routing / Mandatory Path 未真正命中，不要立刻扩 Knowledge。

如果确实读取了，但 Final Prompt 没体现 Pattern：

> 判 Pattern Realization / Choreography Consumption / Assembly 问题。

如果读取了、动作也体现了，但仍然贫乏：

> 才考虑 Knowledge Coverage Audit。

不要跳过这个依赖顺序。

---

## 10. Knowledge Expansion Gate

只有下面全部成立才允许扩更大知识库：

```text
Fighting Direction 正确
+ Stage-2 Routing 正确
+ Pattern 实际读取
+ Pattern 进入 Concrete Phrase
+ Granularity Distribution 正确
+ Assembly 保真
+ Preflight 有效
+ G01 仍持续动作贫乏 / 上肢主导
```

否则优先修 Routing / Realization / Assembly，不要继续堆武术知识。

---

## 11. 与旧 G01 的比较基线

旧版 G01 已有明显提升：

- Camera Intent 询问效果好；
- V2-49 后动作颗粒度明显更具体；
- Initiative / Motion Handoff 也改善；

但仍有两个主要不足：

1. 约 15s 主要只有 3 组大 Exchange；
2. 上肢控制占主导，Movement 没有真正创造编排。

旧 Prompt 常见动作骨架包括：

- 男方肩驱直拳；
- 女方头部外闪 + 前臂偏转 + 外侧切步；
- 男方肩 / 前臂封出口；
- 女方转身控肘 + 短肘；
- 男方抓上臂 + 前臂压玻璃；
- 女方降低重心 + 转髋 + 拉肘过中线；
- 男方轴线旋转后退到墙；
- 女方前臂压胸形成结尾缠抱。

新回归重点就是看：

- 是否增加真正由 Movement / Lower-body / Balance / Transition 驱动的动作；
- 是否不再重复该上肢骨架；
- 是否在保留可执行颗粒度的同时提高 Exchange richness。

---

## 12. 当前不可宣称的结论

当前**不能**宣称：

- G01 Prompt PASS；
- G01 Generated Video PASS；
- 最小 Pattern 已证明有效；
- Upper-body Dominance 已解决；
- Knowledge Expansion Gate 已开放。

当前只能宣称：

> **CK-Step 1～6 Runtime 结构实施完成，Static Read PASS。**

---

## 13. 下一会话起手建议

新会话中，如果用户贴出实际 Interactive 对话 / Final Prompt，直接按下面顺序开始：

```text
1. 读取本 handoff
2. 读取最新 Regression 真源
3. 对照实际 Read List / Interactive / Final Prompt
4. Gate A：Fighting Direction
5. Gate B：Choreography Richness
6. Gate C：Upper-body Dominance
7. 定位失败发生在 Interactive / Routing / Pattern / Choreography / Assembly / Preflight 哪一层
8. 只有有证据时才修改 Runtime
9. 修改后继续同一 G01，不换案例
```

如果用户只给 Final Prompt，没有 Read List：仍可先做 Prompt-level Gate，但不要猜 Pattern 是否真的被读取；要明确区分“Prompt 结果可见证据”和“Runtime Routing 尚无法证实”。

---

## 14. 本轮关键 commits

设计 / 文档：

- Concrete Choreography Spec：多次增量 commit，最终已含 CK-01～CK-19
- 新 Implementation Plan 初建：`58f58d978e947b15cbbe3c3de62a68224c3c2ab5`
- Regression 新 Gate：`b6c492335a4776bb6a562b0e45ec0ec3026e9587`

Runtime：

- Interactive Fighting Direction：`53957536b60534ba1203e7aeb519033150d562b6`
- Combat Router / Stage-2 Gap Routing：`5beb047e8640ab6dc547d2d56690f5c244de1946`
- Minimum Pattern Validation Set：`8c98828729970e25aeee612a6d5426d293d8f160`
- Choreography Playbook Static Read Fix：`e949349b508a75895d5b966d999708902f22c6c3`
- Prompt Assembly Static Read Fix：`c000ffc1d47b238a87e94442beb9a12d2e0ad87e`
- Regression Status Sync：`efd7c7db02fd84de7e50ade2ca665c47111e3629`
- Implementation Plan Status / Physical Structure Sync：`f8ac47ec7841ff8e19cd7d178ebe6c11d4b0772d`

---

## 15. 当前最终状态

```text
Design                    ✅ CLOSED
CK-Step 1 Interactive     ✅ Implemented
CK-Step 2 Minimum Pattern ✅ Implemented
CK-Step 3 Stage-2 Routing ✅ Implemented
CK-Step 4 Granularity     ✅ Implemented
CK-Step 5 Preflight       ✅ Implemented
CK-Step 6 Static Read     ✅ PASS
CK-Step 7 Fixed G01       ⏳ NEXT
Generated Video           ⏸ Prompt PASS 后
Knowledge Expansion       🔒 Gate Closed
```

下一步不再继续抽象设计，等待真实 G01 Prompt / Interactive 运行结果，用同一 Regression Gate 做证据驱动分析。
