# Video Prompt Skill — Action Combat Current Handoff

> 更新时间：2026-08-15 18:54（UTC+8）  
> 仓库：`twj515895394/video-prompt-skill`  
> 分支：`main`  
> 当前阶段：**Cinematic Combat Archetype + Chinese Cinematic Kung-fu Hybrid 已完成设计并接入 Interactive Runtime；下一步停止纸面扩设计，进入真实 Prompt / Video Regression。**

---

## 0. 新会话先做什么

新会话不要重新 Grill 已确认结构，也不要继续扩完整拳种知识库。

用户会带回：

- 实际 Interactive 对话；
- Read List / Runtime 读取证据；
- 最终视频 Prompt；
- 如果有，实际生成视频结果 / 用户主观反馈。

优先按真实结果分析：

```text
1. Round 1 是否仍错误偏向 MMA
2. Hybrid 是否真的减少了不必要门派追问
3. Round 2 双子维度是否清晰生效
4. Archetype 是否真正改变动作语言，而不是只留下明星标签
5. Static Standing / Upper-body Dominance 是否改善
6. Stage-2 / Action Phrase / Camera / Final Preflight 是否仍保持旧门禁
```

---

## 1. 已确认的新结构 CA-01～CA-08

主设计 Spec：

`docs/combat-cinematic-archetype-spec.md`

### CA-01 — Cinematic Combat Archetype

当前五种少量稳定电影武打表达参考：

- 李连杰型｜轻灵流畅 / 武术线条；
- 吴京型｜硬朗爆发 / 全身压迫；
- 甄子丹型｜极速现代融合 / 近身连锁；
- 成龙型｜环境互动 / 空间即武器；
- 李小龙型｜爆发截击 / 节奏破坏 / 极简直接。

这些是 **电影动作表达原型**，不是 Combat System。

执行语义真源：

`references/libraries/combat-cinematic-archetypes/library.md`

### CA-02 — Archetype ≠ Combat System

例如：

```text
截拳道 / JKD
→ Combat System

李小龙型
→ Cinematic Combat Archetype
```

```text
MMA
→ Combat System

甄子丹型
→ Cinematic Combat Archetype
```

Archetype 不得覆盖已经确认的 Technique Backbone。

### CA-03 / CA-04 / CA-05 — Round 2 双子维度

Action Combat Interactive 保持两个核心角色节点：

```text
Round 1：Combat System / Technique Backbone
Round 2：Combat Expression / Performance Identity
```

Round 2 内部同一轮分成：

```text
子维度 A：Character Combat Expression
→ 冷静 / 凶狠 / 克制 / 主动压迫 / 后发反制 / 节奏破坏 ...

子维度 B：Cinematic Combat Archetype（optional）
→ 李连杰型 / 吴京型 / 甄子丹型 / 成龙型 / 李小龙型 / 不指定 / 自定义
```

关键约束：

- 不新增固定 Round 3；
- 两个子维度分开展示；
- 不预组合“冷静 + 李连杰型”“凶狠 + 吴京型”套餐；
- 用户已明确 Archetype 时直接继承；
- 用户不需要明星参考时 Archetype 可以为空。

### CA-06 — Chinese cinematic intent 不再默认 MMA

当用户明确要求：

- 中国功夫电影 / 华语武打片；
- 李连杰 / 吴京 / 甄子丹 / 成龙 / 李小龙式；
- 不要站桩；
- 更丰富身法 / 步法 / 腿法 / 高低位 / 路线 / 空间移动；

Round 1 推荐排序必须优先考虑更有利于 Whole-body Movement 的合理中国武术体系。

MMA 仍是合法候选，但：

> **Modern / office / assassin / police ≠ MMA default.**

用户明确要 MMA / cage fight / realistic MMA 时，MMA 仍可优先。

### CA-07 — Chinese Cinematic Kung-fu Hybrid

新增合法宽泛 Technique Backbone：

> **中国功夫电影混合体系 / Chinese Cinematic Kung-fu Hybrid**

用途：用户想要中国武打电影的完整动作语言，但不想被单一真实门派锁死。

允许合理组合：

- 拳 / 掌；
- 腿法；
- 身法 / 步法；
- 转身 / 绕位；
- 高低位；
- 摔控 / 破平衡；
- Range / Route / Axis / Support 变化。

但 Hybrid 不是随机动作大杂烩，仍必须由 Stage-2 Movement / Technique / Transition Knowledge 具体化。

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
```

才记录为 `Hybrid Refinement`。

---

## 2. 本批 Runtime 已实施

### 2.1 新增 Interactive 专项 Runtime 叶子

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
- Planning Context 输出；
- G01 Regression 验收点。

### 2.2 SKILL 主入口已 wiring

文件：

`SKILL.md`

Commit：

`d21500e0c1e70a8741871783a4149354b79c5375`

Interactive Action Combat 现在额外固定读取：

`references/tasks/action-combat-video/interactive-combat-policy.md`

并明确：

- 该 Policy 是 Action Combat Round 1/2 专项真源；
- 通用 `mode-interactive-output-contract.md` 继续负责 One Question、High-value Budget、Decision Purity、Camera / Ending 条件暴露；
- Policy 不占普通 Controls / Libraries 预算；
- Round 2 = Character Combat Expression + optional Cinematic Combat Archetype；
- Hybrid 不固定追问门派；
- selected Archetype 最终应转成中性动作语义，而不是只写明星姓名。

### 2.3 Archetype 执行语义库

文件：

`references/libraries/combat-cinematic-archetypes/library.md`

已包含五类 Runtime 偏置：

```text
李连杰型
→ Footwork / Route / Axis / Level / Kick / Whole-body Linkage

吴京型
→ Explosive Entry / Whole-body Drive / Hard Contact / Base Disruption

甄子丹型
→ Rapid Interception / Close-range Chain / Burst Footwork / Range Transition

成龙型
→ Environment Affordance / Route Change / Recovery / Obstacle Traversal

李小龙型
→ Interception / Stop-hit / Broken Rhythm / Explosive Entry / Exit / Range Control
```

Final Prompt 应优先外显中性动作语言。

---

## 3. 仍然有效的旧 Combat 门禁

这批设计没有替换 CK / Camera / Advantage 旧机制。

### Stage-2 / Concrete Choreography

仍然保留：

```text
Planning Gap
→ Movement / Technique / Transition Slot
→ leaf execution knowledge
→ Concrete Action Phrase
→ Executable Granularity
```

核心回归失败：

- `Static Standing Combat`
- `Upper-body Technique Dominance`
- `Stage-2 Routing Evidence Missing`
- `Technique Identity Evaporation / Persistent Signature Collapse`
- `Non-executable Choreography Summary`

### Archetype / Hybrid 不自动 PASS

选择：

```text
Hybrid
李连杰型
吴京型
甄子丹型
成龙型
李小龙型
```

都不能替代：

- Movement Realization；
- Technique / Transition Knowledge；
- Action Phrase 因果；
- Opponent Response；
- Range / Position / Axis / Support Consequence；
- Final Preflight。

最终仍必须通过 Static Standing / Upper-body Dominance Gate。

### Action–Camera

仍然保留：

```text
Action–Camera Planning
→ Camera Handoff Realization Gate
→ Prompt Assembly
→ Model Adapter
→ Camera Handoff Preservation Gate
→ Final Preflight
```

不要因为新增 Archetype 再建立第二套 Camera Runtime。

---

## 4. 下一轮真实 Regression 建议

优先重新跑固定办公室 G01，但这次测试目的变化为：

### Gate A — MMA Default Bias

用户只说：

```text
现代办公室
两个职业杀手
中国功夫电影式
不喜欢站桩
```

观察 Round 1：

- 是否仍把 MMA 放第一推荐；
- 是否出现散打 / 八极 / 长拳 / 咏春 / JKD / Hybrid 等合理方向；
- 是否出现 `Chinese Cinematic Kung-fu Hybrid`。

### Gate B — Hybrid UX

如果选 Hybrid：

- 下一轮不应固定追问“具体混哪些门派”；
- 应直接进入 Round 2 或其他更高价值节点。

### Gate C — Round 2 Double Sub-dimension

检查同一轮是否分别展示：

```text
Character Combat Expression
+
optional Cinematic Combat Archetype
```

而不是：

- 变成 Round 3；
- 变成“冷静李连杰 / 凶狠吴京”套餐。

### Gate D — Archetype Realization

最终 Prompt 中检查：

- 李连杰型是否真实增加身法 / 步法 / 高低位 / 转身 / 腿法 / Route；
- 吴京型是否真实增加爆发 Entry / Contact / Balance Disruption；
- 甄子丹型是否真实增加快速 Interception / Range Transition，而不是 MMA 站桩；
- 成龙型是否让 Environment 真正改变动作路线；
- 李小龙型是否体现 Broken Rhythm / Stop-hit / in-out Footwork。

不能只找到：

```text
“李连杰风格”
“吴京式”
```

就判 PASS。

### Gate E — Static Standing / Upper-body Dominance

即使 Archetype Realization 看起来正确，仍检查：

```text
Movement 是否主动创造：
Level
Route / Angle
Axis
Range
Position
Support / Balance
Ground / Standing 或 Ground / Air
```

如果仍是：

```text
前臂格挡
抓手
顶肩
拳肘
+
少量“转髋 / 脚步”修饰
```

仍判 FAIL。

---

## 5. 新会话建议提交的材料

最好一次给出：

1. 用户原始 Prompt；
2. 完整 Interactive 对话；
3. 每轮候选与用户选择；
4. Read List；
5. Pattern / Library Hit Evidence；
6. Final Prompt；
7. 使用的模型；
8. 如果已经生成视频：
   - 哪些动作好；
   - 哪些地方仍站桩；
   - 哪个 Archetype 看得出来 / 看不出来；
   - Camera 是否帮助动作；
   - 视频里最明显的失败点。

---

## 6. 新会话不要做什么

除非真实 Regression 证明必要，否则不要：

- 扩完整中国武术百科；
- 给每个明星建独立 Engine；
- 给每个明星建 Combo Library；
- 强制 Hybrid 指定几个门派；
- 把 MMA 全局降级；
- 把 Archetype 变成 Combat System；
- 建新的 Lower-body Engine；
- 建新的 Body Method State Machine；
- 建第二套 Camera Runtime；
- 用固定踢腿 / 换位次数解决 Static Standing。

核心原则：

> **先用真实 Prompt / Video Regression 证明 Runtime 会不会用这批新语义，再决定是否需要扩 Knowledge。**

> **用户负责高价值创作方向；Runtime 负责专业动作具体化。**
