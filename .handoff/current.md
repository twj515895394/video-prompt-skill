# Video Prompt Skill — Action Combat Regression Handoff

> 更新时间：2026-08-15 20:01（UTC+8）  
> 仓库：`twj515895394/video-prompt-skill`  
> 分支：`main`  
> 当前阶段：**Cinematic Combat Archetype + Chinese Cinematic Kung-fu Hybrid 已完成设计、Runtime 接线与静态回读；停止继续扩设计，下一会话直接接收真实 Prompt / Video Regression 反馈。**

---

## 0. 新会话接管指令

新会话开始后，优先读取本文件，不要重新 Grill 已确认结构，不要重新讨论为什么要做 Archetype / Hybrid，也不要先扩完整拳种知识库。

用户下一会话会带回实际测试内容，可能包括：

- 原始用户需求；
- 完整 Interactive 对话；
- 每轮候选与用户选择；
- Read List / Runtime 读取证据；
- Pattern / Library Hit Evidence；
- Final Prompt；
- 使用的视频模型；
- 如果已生成视频：视频结果、主观反馈、失败点截图 / 描述。

**下一会话的第一目标是 Regression Analysis，不是继续设计。**

推荐分析顺序：

```text
Input / Interactive Evidence
→ Round 1 Recommendation Gate
→ Hybrid UX Gate
→ Round 2 Double Sub-dimension Gate
→ Archetype Realization Gate
→ Stage-2 / Concrete Choreography Gate
→ Static Standing / Upper-body Dominance Gate
→ Action–Camera Gate
→ Final Prompt Serialization Gate
→ 如果有视频，再做 Generated-video Regression
→ 最后才决定：修 Routing / Runtime / Assembly，还是扩 Knowledge
```

核心原则：

> **先证明 Runtime 有没有用对，再判断 Knowledge 够不够。**

> **Routing First, Knowledge Second.**

---

## 1. 当前已确认的上游结构

Action Combat Interactive 保持两个核心角色打斗 Planning Node：

```text
Round 1：Combat System / Technique Backbone
Round 2：Combat Expression / Performance Identity
```

不是固定问卷：

```text
Unknown → Select
Known → Refine
```

1v1 时同一轮处理双方；多人战按主角 / 关键对手 / 次要功能组组织，不按角色数量机械拆轮。

旧的 `Fighting Direction / 怎么打` 不再作为独立用户问题：

```text
Per-Character Combat System
+ System / Hybrid Refinement
+ Character Combat Expression
+ optional Cinematic Combat Archetype
+ Physical Presentation Domain
+ Scene / Range / Environment / Intent
→ Derived Choreography Direction
→ MVP 写入 legacy Fighting Direction execution slot
→ Stage-2 Execution
```

---

## 2. CA-01～CA-08：Cinematic Combat Archetype / Hybrid 决策

主 Spec：

`docs/combat-cinematic-archetype-spec.md`

### CA-01 — 五种 Cinematic Combat Archetype

当前只收录 5 个动作语言足够稳定、明显、可复用的华语电影武打参考型：

1. **李连杰型｜轻灵流畅 / 武术线条**
   - 身法、步法、腿法、转身、高低位、路线和全身线路清晰；
   - 快但不乱，强调连续流动与技术可读性。

2. **吴京型｜硬朗爆发 / 全身压迫**
   - 爆发进入、Whole-body Drive、重接触、逼退、破平衡、再进入；
   - 有重量与压迫，但不能长期原地互殴。

3. **甄子丹型｜极速现代融合 / 近身连锁**
   - Rapid Interception、拳腿肘膝、短控、Burst Footwork、快速 Range Transition；
   - 可以融合现代格斗元素，但不能退化成 MMA 站桩。

4. **成龙型｜环境互动 / 空间即武器**
   - 跑、绕、翻、钻、跌扑恢复、障碍穿越；
   - Environment Affordance 必须真实改变 Route / Position / Recovery；
   - Comedy Tone 可选，不强制。

5. **李小龙型｜爆发截击 / 节奏破坏 / 极简直接**
   - Interception / Stop-hit / Broken Rhythm / Explosive Entry & Exit / Range Control；
   - 短促爆发后快速换距 / 换线，不写成长时间原地连打。

执行语义真源：

`references/libraries/combat-cinematic-archetypes/library.md`

### CA-02 — Archetype ≠ Combat System

必须保持分层：

```text
Combat System
→ 角色真正会什么 / Technique Backbone

Cinematic Combat Archetype
→ 这套技术在电影里怎么呈现
```

典型边界：

```text
截拳道 / JKD = Combat System
李小龙型 = Cinematic Combat Archetype

MMA = Combat System
甄子丹型 = Cinematic Combat Archetype
```

禁止明星 Archetype 自动覆盖已经确认的 System。

### CA-03 / CA-04 / CA-05 — Round 2 同轮双子维度

Round 2 仍然只有一个 Primary Planning Node，但同一轮里分两个子维度：

```text
子维度 A：Character Combat Expression
→ 冷静 / 凶狠 / 克制 / 从容
→ 主动压迫 / 后发反制 / 诱导 / 节奏破坏
→ 风险偏好 / 杀意 / 留手 / 再进入倾向

子维度 B：Cinematic Combat Archetype（optional）
→ 李连杰型 / 吴京型 / 甄子丹型 / 成龙型 / 李小龙型 / 不指定 / 自定义
```

要求：

- 不新增固定 Round 3；
- 两个子维度分开展示、分开选择；
- 不做“冷静李连杰 / 凶狠吴京”这种套餐绑定；
- 用户已经明确 Archetype 时直接继承；
- 用户不关心明星参考时 Archetype = none，不额外追问。

### CA-06 — 中国功夫电影观感下，不机械默认 MMA

当用户明确追求：

- 中国功夫电影 / 华语武打片；
- 李连杰 / 吴京 / 甄子丹 / 成龙 / 李小龙式观感；
- 不要站桩；
- 更丰富的身法、步法、腿法、高低位、转身、Route / Axis / Position 变化；

Round 1 推荐排序必须优先展示更适合 Whole-body Movement 的合理体系，例如：

- 散打；
- 八极；
- 长拳 / 传统武术全身线路；
- 咏春；
- 太极；
- 截拳道 / JKD；
- Chinese Cinematic Kung-fu Hybrid；
- 其他与当前人物 / 场景相容的体系。

MMA 仍然合法，但：

> **Modern / office / assassin / police ≠ MMA default.**

如果用户明确要 MMA / cage fight / realistic MMA，则 MMA 仍可优先。

### CA-07 — Chinese Cinematic Kung-fu Hybrid

新增合法宽泛 Technique Backbone：

> **中国功夫电影混合体系 / Chinese Cinematic Kung-fu Hybrid**

适用于：用户想要中国武打电影完整动作语言，但不想被单一真实拳种 / 门派锁死。

允许合理组合：

- 拳 / 掌；
- 腿法；
- 身法 / 步法；
- 转身 / 绕位；
- 高低位；
- 摔控 / 破平衡；
- Range / Route / Axis / Support 变化。

但 Hybrid 不是随机动作大杂烩，仍必须通过 Stage-2 Movement / Technique / Transition Knowledge 具体化。

### CA-08 — Hybrid 默认静默展开

用户选择 Hybrid 后：

```text
默认
→ 不再固定追问“具体混哪些拳种 / 门派？”
→ Runtime 根据：
   Cinematic Archetype
   + Character Combat Expression
   + Scene
   + Range
   + Environment
   + 当前 Movement / Technique / Transition Gap
→ 静默选择合理 Execution Knowledge
```

只有用户主动明确：

```text
以八极为主，混散打腿法
长拳身法为主，近身加入咏春
截拳道式进退 + 中国武术电影腿法
```

才进入 `Hybrid Refinement`。

---

## 3. 本批 Runtime 已完成

### 3.1 Interactive Combat Policy

文件：

`references/tasks/action-combat-video/interactive-combat-policy.md`

Commit：

`4670356b6b9e6b1bc0ebc93a43f7f2371af4911a`

职责：

- Round 1 Combat System Recommendation Ordering；
- Chinese cinematic kung-fu intent；
- Chinese Cinematic Kung-fu Hybrid；
- Hybrid 默认静默展开 / explicit Hybrid Refinement；
- Round 2 Character Combat Expression；
- optional Cinematic Combat Archetype；
- 五种 Archetype 用户候选语义；
- System / Archetype 分层；
- Derived Choreography Direction 输入边界；
- G01 Regression Gate。

### 3.2 SKILL 主入口 wiring

文件：

`SKILL.md`

Commit：

`d21500e0c1e70a8741871783a4149354b79c5375`

现在 **Interactive Action Combat 固定读取**：

`references/tasks/action-combat-video/interactive-combat-policy.md`

该 Policy：

- 不占普通 Controls / Libraries 预算；
- 负责 Action Combat Round 1 / Round 2 专项语义；
- 通用 `assets/templates/mode-interactive-output-contract.md` 继续负责 One Question、High-value Budget、Decision Purity、Camera / Ending 等条件暴露。

SKILL 主流程已明确：

```text
Confirmed Per-Character Combat Context
→ Derived Choreography Direction
→ legacy Fighting Direction execution slot（MVP compatibility only）
→ Stage-2 Gap Detection
→ Stage-2 Pattern Hit Evidence Gate
→ leaf execution knowledge Read
→ Concrete Action Phrase
→ State / Continuity Validation
→ Model Execution Realizability
→ Motion / Energy Carry-over
→ Action–Camera Handoff
→ Camera Handoff Realization Gate
→ Prompt Assembly
→ Model Adapter
→ Camera Handoff Preservation Gate
→ Combat Final Preflight
→ Delivery
```

### 3.3 Archetype Runtime Library

文件：

`references/libraries/combat-cinematic-archetypes/library.md`

Router 已接入：

`references/libraries/index.md`

原则：只有中国功夫电影 / 明星型动作表达真正相关时读取，不污染普通 Combat。

Final Prompt 应优先转译为中性动作语义，而不是只留下明星姓名。

---

## 4. 仍然必须保留的既有 Combat 门禁

本批 Archetype / Hybrid 只是上游交互与动作表达方向增强，**没有替换**已有 Stage-2、Concrete Choreography、Advantage、Action–Camera、Prompt Assembly、Final Preflight。

### 4.1 Stage-2 Gap-driven Routing

现有执行链继续有效：

```text
Planning / Phrase Gap
├─ Route / Body Method / Level / Weight / Axis / Position 缺口
│  → Movement Slot
├─ 具体 Attack / Defense / Kick / Throw / Weapon 缺口
│  → Technique Slot
└─ 前后动作 Handoff 缺口
   → Transition Slot
```

每个命中 Slot：

```text
1 main Pattern
+ optional 1 auxiliary
```

不是三槽必须填满的固定配额。

当前最小验证知识：

`references/libraries/combat-choreography-patterns/minimum-validation-set.md`

原则：

> **最小样例是 Stage-2 可验证探针，不是完整知识库 MVP。**

### 4.2 Executable Action Granularity

关键 Action Phrase 应尽量包含足够的因果：

```text
Current Body / Range State
→ Specific Physical / Weapon Action
→ Contact / Evasion / Interception
→ Opponent Immediate Response
→ Footwork / Body Axis / Range / Position Consequence
→ Immediate Continuation Entry
```

这是信息合同，不是六步固定句式。

禁止关键动作被这些抽象词替代：

- 连续攻击；
- 连续格挡；
- 快速反制；
- 贴身缠斗；
- 持续压迫；
- 不断换位；
- 连续拆招；
- 高频攻防。

同时也禁止每拳每脚都写成机械微动作清单。

### 4.3 Lightweight Granularity Distribution

继续使用：

```text
High
→ reversal / initiative theft / signature / key turn

Medium
→ ordinary exchange / re-counter / meaningful range change

Low
→ connective transition
```

目标不是 `High → High → High → Ending`，而是保留更多完整 Exchange Chain。

### 4.4 Static Standing / Upper-body Dominance Gate

即使用户选了 Hybrid / 李连杰型 / 吴京型等，也不能自动 PASS。

High / Expert Combat 如果关键动作长期主要由：

```text
前臂
肩线
抓手
顶肩
拳肘上肢 Contact
```

驱动，而 Movement 没有主动创造：

- Level；
- Route / Angle；
- Axis；
- Range；
- Position；
- Support / Balance；
- Ground / Standing 或 Ground / Air 状态变化；

则仍判：

- `Static Standing Combat`
- `Upper-body Technique Dominance`

不要用“加几次踢腿 / 换位配额”作弊。

### 4.5 Persistent Combat Signature

已经确认的 System / Refinement / Archetype 必须持续改变动作状态和决策逻辑，不能只出现一次后消失。

失败：

`Technique Identity Evaporation / Persistent Signature Collapse`

### 4.6 Advantage / Counterplay

仍然有效：

```text
Advantage ≠ Attack Share
Outcome ≠ Advantage Trajectory
Disadvantaged ≠ Passive
```

不要因为某角色总体占优，就让另一方长期只等待 / 防守。

### 4.7 Action–Camera

继续执行：

```text
Action–Camera Runtime
→ Camera Handoff Realization Gate
→ Prompt Assembly
→ Model Adapter
→ Camera Handoff Preservation Gate
→ Combat Final Preflight
```

高价值 Camera Moment 必须有：

```text
Concrete Action Anchor
+ Camera Response / Viewer Task
+ Live Motion / State Continuation
+ Camera Hard Constraint Compliance
```

不要退回：

```text
“第一次接触时切近”
“关键时刻特写”
```

这种泛化 Camera 描述。

---

## 5. 下一会话：固定办公室 G01 Regression

建议继续使用同一个 Golden Scenario，便于横向比较旧结果：

- 15 秒；
- 普通现代办公室；
- 中国女性，22 岁，长高马尾，正常职场服装；
- 中国男性，55 岁，矮胖、秃顶领导，正常职场服装；
- 两人分别属于敌对杀手组织，都是职业杀手；
- Close Combat；
- 两人之间不要隔办公桌；
- 目标：中国功夫电影式、高手连续攻防、不要站桩。

不要在测试输入里直接指定 MMA。

### Gate A — Round 1 Recommendation Bias

检查：

- 是否仍因为“现代办公室 / 职业杀手”把 MMA 放第一推荐；
- 是否能出现合理的中国武术体系；
- 是否出现 `Chinese Cinematic Kung-fu Hybrid`；
- 推荐理由是否围绕用户动作观感，而不是职业身份。

PASS 目标：

> Chinese cinematic intent 能真实改变 Round 1 候选排序；MMA 保留但不机械首位。

### Gate B — Hybrid UX

如果用户选择 Hybrid：

- 下一轮不得固定追问“具体混哪些门派”；
- 应进入 Round 2 或其他真实更高价值节点；
- 只有用户主动提出具体主 / 辅体系时才做 Hybrid Refinement。

### Gate C — Round 2 Double Sub-dimension

同一轮应分别处理：

```text
Character Combat Expression
+
optional Cinematic Combat Archetype
```

检查：

- 是否真的同轮；
- 是否分开展示；
- 是否没有套餐绑定；
- 是否没有新增固定 Round 3；
- 用户已明确 Archetype 时是否直接继承。

### Gate D — Archetype Realization

Final Prompt / Choreography 中检查：

**李连杰型**
- Footwork / Route / Axis / Level / Kick / Whole-body Linkage 是否真实增加；
- 是否流畅、清晰、全身驱动。

**吴京型**
- Explosive Entry / Whole-body Drive / Hard Contact / Base Disruption 是否真实出现；
- 是否有持续换位，不只是重拳互殴。

**甄子丹型**
- Rapid Interception / Burst Footwork / Range Transition / close-range chain 是否真实出现；
- 是否避免退化为 MMA 站桩。

**成龙型**
- Environment Affordance 是否真实改变 Route / Recovery / Position；
- 不是只写“利用环境”。

**李小龙型**
- Stop-hit / Broken Rhythm / Explosive Entry / Exit / Range Control 是否真实出现；
- 是否有 in-out Footwork，而非高速原地挥拳。

**不能因为 Prompt 出现明星名字就判 PASS。**

### Gate E — Stage-2 Evidence

Read List / Evidence 中检查：

```text
Gap
→ Slot
→ 实际读取 leaf knowledge
→ Pattern / Detail
→ Concrete Action Phrase
```

如果动作看似具体，但没有真实 leaf Read Evidence，不应假定 Stage-2 已执行。

### Gate F — Choreography Richness

检查 15 秒是否仍只有约 3 个主 Exchange Chain，或者已经在保持颗粒度的同时恢复更多连续交换。

目标：

- 关键 reversal / signature 细；
- 普通 exchange 中等颗粒度；
- connector 压缩；
- 不因所有动作都 High-detail 而吃掉动作数量。

### Gate G — Static Standing / Upper-body Dominance

检查 Movement 是否是战斗本身，而不是给上肢动作补脚步。

重点看是否真实产生：

- 斜切；
- 绕侧；
- 转轴；
- 沉身 / 起身；
- 高低位切换；
- 支撑转换；
- 低线攻击 / 破支撑；
- Range / Position 改变；
- 摔控失败后的重新进入；
- Route / Axis / Balance 连续变化。

### Gate H — Action–Camera

如果选择电影冲击优先等 Camera Intent：

- Camera Change 是否锚定具体 Action Moment；
- 是否说明 Viewer Task；
- Cut / Reframe 后是否继续 live motion；
- 是否没有凭空引用未建立 Camera State；
- Model Adapter 后是否仍 Preserve。

---

## 6. 如果已经生成视频：Generated-video Regression

Prompt PASS 不代表视频 PASS。

如果用户带回视频结果，分开判断：

### 6.1 Prompt-level

- Interactive 是否正确；
- Routing 是否正确；
- Pattern 是否真实加载；
- Final Prompt 是否具体；
- Archetype / Hybrid 是否已外显；
- Camera 是否正确序列化。

### 6.2 Generated-video-level

重点看：

- 是否仍站桩；
- 下肢 / 身法 / 重心是否真的参与；
- 是否出现“Prompt 写了路线变化，视频模型没执行”；
- 是否动作数量明显不足；
- 是否接触变成无受力滑动；
- 是否角色打法中途同质化；
- 是否镜头抢动作；
- 是否 Cut 造成 Motion Reset；
- 哪个 Archetype 最能 / 最不能看出来。

如果：

```text
Runtime Read / Routing / Prompt 都正确
+
Final Prompt 已明显全身化
+
视频仍站桩 / 上肢主导
```

再考虑：

- Knowledge Coverage Audit；
- Model Capability / Adapter；
- Prompt Saturation；
- Generated-video model limitation。

不要第一反应就继续扩知识库。

---

## 7. 下一会话最好一次提交的材料

推荐用户直接粘贴：

```text
【原始需求】
...

【完整 Interactive 对话】
...

【每轮最终选择】
Round 1：...
Round 2：...
Camera：...
Advantage / Ending（如有）：...

【Read List】
...

【Pattern / Library Hit Evidence】
...

【Final Prompt】
...

【模型】
Seedance / LTX / Generic / 其他

【生成结果反馈】
1. 最满意：...
2. 最明显失败：...
3. 是否站桩：...
4. 是否看得出所选 Archetype：...
5. 动作数量 / 连续性：...
6. Camera：...
```

不要求格式完全一致；材料不全时，先基于已有证据分析，不让用户重复已经提供的信息。

---

## 8. 下一会话故障分流原则

### 情况 A：Round 1 仍默认 MMA

```text
→ Interactive Policy / Routing Failure
→ 先修推荐策略或读取路径
→ 不扩 Choreography Knowledge
```

### 情况 B：Hybrid 后仍追问门派

```text
→ CA-08 UX / Policy Failure
→ 修 Interactive Policy
```

### 情况 C：Round 2 没有 Archetype 子维度

```text
→ CA-05 Runtime Wiring Failure
→ 检查 interactive-combat-policy.md 是否实际读取
```

### 情况 D：Archetype 被选择，但 Final Prompt 只有明星标签

```text
→ Archetype Consumption / Serialization Failure
→ 检查 Library Read → Derived Direction → Choreography → Assembly
→ 先修消费链
```

### 情况 E：Archetype 已转成具体动作，但仍站桩

先检查：

```text
Stage-2 Pattern Hit Evidence
→ Movement Slot 是否命中
→ Movement 是否创造状态变化
```

如果 Routing 未命中：先修 Routing。

如果 Routing 已正确命中并且具体动作仍不足：再做 Knowledge Coverage Audit。

### 情况 F：Prompt 很好，视频执行仍差

```text
→ Generated-video Regression
→ 检查 Model Capability / Prompt Saturation / Adapter
→ 不自动把问题归因到 Choreography Knowledge
```

---

## 9. 当前禁止继续做的事情

除非下一轮真实 Regression 明确证明必要，不要：

- 扩完整中国武术百科；
- 给每位明星建独立 Engine；
- 给每位明星建固定 Combo Library；
- 强制 Hybrid 选择几个门派；
- 把 MMA 全局降级；
- 把 Archetype 当成 Combat System；
- 建 Lower-body Engine；
- 建 Body Method State Machine；
- 建每个拳种独立 Runtime Tree；
- 建第二套 Camera Runtime；
- 用固定踢腿次数 / 换位次数解决 Static Standing；
- 在没有真实测试证据前继续增加复杂推断机制。

Anti-overdesign 原则：

> **Simple Interactive Choice Upstream; Professional Execution Downstream.**

> **用户负责高价值创作方向；Runtime 负责专业动作具体化。**

---

## 10. 当前关键文件

### Interactive / Archetype

- `docs/combat-cinematic-archetype-spec.md`
- `references/tasks/action-combat-video/interactive-combat-policy.md`
- `references/libraries/combat-cinematic-archetypes/library.md`
- `assets/templates/mode-interactive-output-contract.md`
- `SKILL.md`

### Choreography / Stage-2

- `references/tasks/action-combat-video/index.md`
- `references/tasks/action-combat-video/choreography-playbook.md`
- `references/libraries/combat-choreography-patterns/minimum-validation-set.md`
- `references/controls/prompt-assembly/control.md`

### Camera

- `references/tasks/action-combat-video/action-camera-handoff-playbook.md`
- `docs/action-combat-video-action-camera-handoff-spec.md`

### Advantage / Counterplay

- `references/tasks/action-combat-video/advantage-structure-contract.md`
- `docs/combat-advantage-counterplay-spec.md`

---

## 11. 当前实施提交

本轮 Cinematic Archetype / Hybrid 相关：

- Archetype Library：`e069f31c7ec0f3d189eec695e93e11aa9ec07eec`
- Library Router：`b97f73f09b1a923d68945a30066bcd609c230c28`
- Archetype Spec 初始：`a3588f4550c95d55ac74bf2206805e66a43df993`
- Round 2 双子维度 Spec：`a37664d3d81082649cd129ecbbca0db704f8385e`
- Chinese cinematic intent 推荐策略：`595ad8eb08bb60f0591193e75874dc91ba42d4e9`
- Hybrid：`3e1d8872925ba4cc5394feb9ca7df68fb2435213`
- CA-08 Hybrid Silent Expansion：`89aab3b6d66913c4c27bc2c01c684ea67b0547c1`
- Interactive Runtime Policy：`4670356b6b9e6b1bc0ebc93a43f7f2371af4911a`
- SKILL Runtime Wiring：`d21500e0c1e70a8741871783a4149354b79c5375`

---

## 12. 下一会话结束条件

下一会话不要以“又设计了多少规则”为完成标准。

完成标准应该是：

```text
真实测试结果
→ 定位到具体 Failure Layer
→ 确认 Routing / Runtime / Knowledge / Assembly / Model 中哪一层负责
→ 给出最小修复
→ 再 Regression
```

如果真实结果已经 PASS，则不要继续为了“更完整”主动扩系统。

最终判断口令：

> **先看真实结果，再决定修哪里。**
