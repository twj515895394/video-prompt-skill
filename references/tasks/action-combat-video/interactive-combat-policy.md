# Action Combat Interactive Policy

## 1. 作用

本文件是 Action Combat Interactive 中角色级打斗决策的运行期叶子规则，负责把用户可理解的交互问题映射到：

- Per-Character Combat System / Technique Backbone；
- System Refinement / Hybrid Refinement；
- Character Combat Expression；
- optional Cinematic Combat Archetype；
- Derived Choreography Direction 输入。

它只负责 Interactive 决策暴露与推荐策略，不替代 `core-playbook.md`、`choreography-playbook.md`、Stage-2 Pattern Selection、Camera 或 Final Preflight。

---

## 2. 固定两个核心 Planning Node

Action Combat Interactive 的角色打斗设计保持两个核心节点：

```text
Round 1：Combat System / Technique Backbone
Round 2：Combat Expression / Performance Identity
```

采用：

```text
Unknown → Select
Known → Refine
```

不新增固定 Round 3。

1v1 时同一轮同时覆盖双方；多人战按主角 / 关键对手 / 次要功能组组织，不按角色数量机械拆轮。

---

## 3. Round 1 — Combat System / Technique Backbone

Round 1 回答：

> 每个关键角色主要依靠什么格斗 / 武术技术体系解决战斗？

### 3.1 Character Identity 不得替代 Combat System

禁止：

```text
职业杀手 → Tactical Close Combat / MMA
特工 → MMA
年轻女性 → 速度型
年长男性 → 力量抱控
现代办公室 → MMA
```

职业、年龄、性别、外貌和体型可以影响表现与物理条件，但不能直接锁定 Technique Backbone。

### 3.2 通用候选池

按场景动态筛选真正的 Combat System，例如：

- 散打；
- 八极；
- 咏春；
- 长拳 / 传统武术长桥大马与全身线路；
- 太极；
- 截拳道 / JKD；
- MMA；
- 泰拳；
- Boxing；
- Wrestling / Grappling；
- BJJ；
- 其他当前任务合理体系；
- 自定义。

候选池不是固定问卷，也不要求每次全部展示。

### 3.3 Chinese Cinematic Kung-fu Intent 推荐排序

当用户明确表达以下任一目标：

- 中国功夫电影 / 华语武打片；
- 李连杰 / 吴京 / 甄子丹 / 成龙 / 李小龙式电影武打；
- 不要站桩；
- 希望身法、步法、腿法、高低位、转身、路线、空间移动更丰富；

则 Round 1 必须响应这个动作观感目标：

```text
Chinese cinematic kung-fu intent
→ 优先展示 Whole-body Movement / Footwork / Body Method / Kick Integration / Route Change 更丰富的合理中国武术体系
→ 同时提供 Chinese Cinematic Kung-fu Hybrid（当用户不关心严格门派还原时）
→ MMA 可以保留，但不得因为“现代 / 杀手 / 办公室 / 警匪”机械放在首位
```

这不是全局降低 MMA：用户明确要 MMA、笼斗、竞技综合格斗或写实 MMA 时，MMA 仍应优先。

### 3.4 Chinese Cinematic Kung-fu Hybrid

合法宽泛 Backbone：

> **中国功夫电影混合体系 / Chinese Cinematic Kung-fu Hybrid**

适用于：用户想要中国武打电影的完整动作语言，但不想被单一真实拳种 / 门派锁死。

它允许合理组合：

- 拳 / 掌；
- 腿法；
- 身法 / 步法；
- 转身 / 绕位；
- 高低位；
- 摔控 / 破平衡；
- Range / Route / Axis / Support 变化。

但它不是“随机动作大杂烩”。具体动作仍必须由当前 State / Range / Contact 与 Stage-2 Movement / Technique / Transition Knowledge 实例化。

### 3.5 Hybrid 默认不追加门派问卷

用户选择 Hybrid 后：

```text
默认
→ 不再固定问“具体混哪些拳种 / 门派？”
→ Runtime 根据：
   Cinematic Archetype
   + Character Combat Expression
   + Scene
   + Range
   + Environment
   + 当前 Movement / Technique / Transition Gap
→ 静默选择合理 Execution Knowledge
```

只有用户主动给出主 / 辅偏好时才进入 Hybrid Refinement，例如：

```text
以八极为主，混散打腿法
长拳身法为主，近身加入咏春
截拳道式进退 + 中国武术电影腿法
```

用户已明确的 Hybrid Refinement 不得被 Runtime 偷换。

---

## 4. Round 2 — Combat Expression / Performance Identity

Round 2 仍然只占一个 Primary Planning Node，但内部包含两个**分开展示、分开选择、同轮回答**的子维度。

### 子维度 A：Character Combat Expression

回答：

> 这个角色以什么气质和战斗决策倾向使用已确认的 Combat System？

可以涉及：

- 冷静 / 凶狠 / 克制 / 从容；
- 主动压迫 / 后发反制 / 诱导 / 节奏破坏；
- 风险偏好；
- 杀意 / 留手 / 竞技感；
- 抢到主动后的延续方式；
- 失去主动后的再进入倾向。

不能直接变成固定 Combo / 具体招式。

### 子维度 B：Cinematic Combat Archetype（optional）

回答：

> 如果希望有明确的华语功夫电影动作表达参考，更接近哪一型？

当前候选：

1. **李连杰型｜轻灵流畅・武术线条**
   - 身法、步法、腿法、转身、高低位与全身线路清晰；
   - 快但不乱，强调连续流动与技术可读性。

2. **吴京型｜硬朗爆发・全身压迫**
   - 爆发进入、重接触、逼退、破平衡、再进入；
   - 强重量与压迫，但仍持续换位。

3. **甄子丹型｜极速现代融合・近身连锁**
   - 快速截击、拳腿肘膝、短控与快速换距连续衔接；
   - 允许现代格斗元素，但不得退化成 MMA 站桩互殴。

4. **成龙型｜环境互动・空间即武器**
   - 跑、绕、翻、钻、跌扑恢复、障碍穿越；
   - Environment Affordance 成为动作链原因；喜剧感可关闭。

5. **李小龙型｜爆发截击・节奏破坏・极简直接**
   - Stop-hit / Interception / Broken Rhythm / Explosive Entry & Exit / Range Control；
   - 短促爆发后立即换距 / 换线，不原地持续挥拳。

6. 不指定明星参考 / 自定义。

执行语义读取：

`references/libraries/combat-cinematic-archetypes/library.md`

### 4.1 两个子维度不得预绑定

禁止做成套餐：

```text
冷静后发 + 李连杰型
凶狠压迫 + 吴京型
高速抢先 + 甄子丹型
```

用户可以自由组合任何 Character Combat Expression 与任何 Archetype。

例如：

```text
冷静后发 + 吴京型
凶狠主动 + 李连杰型
克制诱导 + 李小龙型
```

### 4.2 Archetype 继承

如果用户已经明确：

- “像李连杰那种”；
- “甄子丹式”；
- “成龙那种环境武打”；
- “李小龙式截击节奏”；

直接继承，不重复询问。

如果用户只说“中国功夫电影风格”，且五种参考型存在真实高价值分叉，Round 2 可以展示上述 Archetype 候选。

如果用户不关心明星参考，则 Archetype = none，不强行多问。

---

## 5. Combat System 与 Cinematic Archetype 必须分层

```text
Combat System
→ 角色真正会什么 / 技术骨架是什么

Cinematic Combat Archetype
→ 这套技术在电影里如何呈现
```

特别区分：

```text
截拳道 / JKD → Combat System
李小龙型 → Cinematic Combat Archetype

MMA → Combat System
甄子丹型 → Cinematic Combat Archetype
```

选择 Archetype 不得自动修改已经确认的 Combat System。

---

## 6. Planning Context 输出

Round 1 / 2 完成后，Planning Context 至少保留：

```text
Per-Character Primary Combat System
Optional Secondary Combat System
System Refinement / Hybrid Refinement（if explicit）
Character Combat Expression
Cinematic Combat Archetype（optional）
Physical Presentation Domain
Scene / Range / Environment / Intent
```

Runtime 再推导：

```text
以上角色级信息
→ Derived Choreography Direction
→ legacy Fighting Direction execution slot（MVP compatibility only）
→ Stage-2 Gap Detection
→ Movement / Technique / Transition Knowledge
→ Concrete Action Phrase
```

Archetype 名称不得只作为标签丢给 Final Prompt；最终 Prompt 应优先外显其中性的动作语义。

---

## 7. G01 / Regression 验收重点

真实 Interactive 回归至少检查：

1. **MMA Default Bias**
   - 现代办公室 + 职业杀手不再自动推荐 MMA 首位；
   - 用户明确中国功夫电影观感时，应优先出现中国武术 / Hybrid 候选。

2. **Hybrid UX**
   - 用户选择 Hybrid 后，不应紧接着固定追问“具体混哪些门派”。

3. **Round 2 Double Sub-dimension**
   - 同一轮分别展示 Character Combat Expression 与 optional Cinematic Archetype；
   - 不增加固定 Round 3；
   - 不把气质与明星型预绑定成套餐。

4. **Archetype Realization**
   - 选中 Archetype 后，最终动作语言应有可辨识的 Movement / Rhythm / Range / Environment / Transition 偏置；
   - 不能只在 Prompt 写明星名字。

5. **No Static Standing Shortcut**
   - 选择 Hybrid 或任何 Archetype 不等于自动 PASS；
   - Final Preflight 仍必须检查 Static Standing Combat / Upper-body Technique Dominance。

---

## 8. Anti-overdesign

不新增：

- Round 3；
- 明星独立 Combat Engine；
- 每明星固定 Combo；
- Hybrid 门派强制问卷；
- MMA 全局降级；
- 明星 Archetype → 固定 Combat System 映射。

核心原则：

> **用户决定高价值动作方向；Runtime 负责把专业动作知识补完整。**

> **Modern identity does not imply MMA. Chinese cinematic intent changes recommendation ordering, not technical truth.**
