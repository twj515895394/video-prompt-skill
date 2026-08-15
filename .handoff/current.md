# Video Prompt Skill — Action Combat Current Handoff

> 更新时间：2026-08-15 17:46（UTC+8）  
> 仓库：`twj515895394/video-prompt-skill`  
> 分支：`main`  
> 当前阶段：**Identity × Combat System 已通过真实 Interactive 验证；Advantage × Counterplay 本轮 Spec + Runtime 已实施完成，等待重新跑 G01 真实回归。**

---

## 0. 当前状态一句话

**本轮修改已经完成，不继续扩具体拳种 / 流派知识。下一步唯一高价值动作是重新跑办公室 G01，验证 Advantage × Counterplay 在真实 Interactive、Final Prompt 和 Generated Video 中是否生效。**

本轮由真实生成视频暴露的问题是：

```text
女方占优
→ Runtime 把男方写成长时间防守
→ 男方 Counterplay 大量停留在“等待 / 准备 / 即将反扑”
→ Ending 又在真正反击发生前结束
→ 成片几乎看不到男方真实还击
```

用户明确纠正了这个语义：

> **被压制不等于一直防守。劣势方完全可以多次还手、主动进攻、反击甚至短暂形成威胁，只是这些 Counterplay 不断被优势方化解、截断或反制，因此总体仍然处于下风。**

因此本批核心不再是“给男方多写几个拳击 / 摔跤动作”，而是把 **Advantage、Counterplay、Advantage Trajectory** 从上游交互一直贯通到最终动作执行。

---

## 1. 已完成上一批：Identity × Combat System

上一批已经完成并经过真实 Interactive 测试：

```text
Character / Narrative Identity
≠ Combat System

Round 1：Per-Character Combat System / System Refinement
Round 2：Per-Character Combat Expression

Physical Presentation Domain：条件暴露
Derived Choreography Direction：Runtime 自动派生
legacy Fighting Direction：只保留 compatibility execution slot
```

真实办公室 G01 与古代女剑客测试已经提供以下证据：

- “职业杀手 → Fighting Direction / 打法”混层已明显改善；
- Round 1 / Round 2 结构真实生效；
- Physical Presentation Domain 能与 Combat System 正交；
- Subject Motion / Stage-2 / Action-Camera / Prompt Assembly 的 Runtime Read Routing 已明显改善；
- Final Prompt 的 Whole-body / Movement / Persistent Signature 比旧版本明显更好；
- 但办公室 G01 真实生成视频仍暴露 **男方 Counterplay Starvation**。

上一批主 Spec：

`docs/combat-system-performance-identity-separation-spec.md`

本轮不要回头重新 Grill 太极、MMA、咏春、八极、散打等具体流派细节。

---

## 2. 本批：Advantage × Counterplay

主 Spec：

`docs/combat-advantage-counterplay-spec.md`

运行期正文真源：

`references/tasks/action-combat-video/advantage-structure-contract.md`

### 2.1 核心 Planning 结构

```text
Advantage Structure
├─ Outcome / Advantage
│  → 最终谁占优、是否分胜负
├─ Counterplay Shape
│  → 劣势方怎样还手 / 被压制 / 丢失主动
└─ Advantage Trajectory
   → 整段战斗中主动权怎样流动
```

三者属于**同一个 Primary Planning Node**，不要机械拆成三个连续问题。

核心原则：

```text
Advantage ≠ Attack Share
Outcome ≠ Advantage Trajectory
Disadvantaged ≠ Passive
```

---

## 3. 已确认 Counterplay Shape 基础模型

当一方总体占优时，至少允许三类高层结构：

### A. Sustained Suppression / 持续压制型

```text
优势方持续控制 Range / Route / Initiative
→ 劣势方主要防守 / 闪避 / 退让
→ 真正反攻机会较少
```

只有用户明确想要“碾压 / 基本还不了手 / 全程压制”或上下文高度支持时才优先使用。

### B. High Counterplay, Repeatedly Neutralized / 高频还手但持续被化解型

```text
优势方总体占优
→ 劣势方多次真实发动 Attack / Counter / Re-entry
→ 这些动作真实形成威胁或状态变化
→ 优势方不断截断 / 化解 / 闪避 / 借势反制
→ 整体 Advantage 仍属于优势方
```

**这是没有其他强约束时的推荐默认。**

### C. Back-and-forth Then Advantage / 多次拉锯后最终占优型

```text
双方都阶段性取得主动
→ Advantage 经过真实 Turning Event 多次转移
→ 最终一方在关键交换后占优
```

禁止实现成机械“你一下我一下”。

---

## 4. Advantage Structure 的 Interactive Exposure Policy

Advantage Structure 是**高价值条件节点**，不是固定 Round 3 / Round 4。

### 直接继承

如果用户已经明确：

```text
Outcome
+ Counterplay Shape
+ 大致 Advantage Trajectory
```

直接继承，不再确认。

### 条件询问

如果用户只说：

- 谁赢；
- 谁占优；
- 势均力敌；
- 谁压制谁；

并且至少存在两个会显著改变成片的合理过程，则把 **Advantage Structure** 作为当前唯一 Primary Planning Node。

问题应一次让用户理解：

> **谁总体占优 + 对方怎么还手 + 主动权大致怎么流动。**

例如办公室 G01 可以出现：

```text
A. 女方持续压制，男方主要被迫防守，真正反攻很少
B. 女方总体占优，但男方频繁拳击反击 / 进入摔控，女方不断化解并反制（推荐）
C. 双方多次拉锯，男方中段短暂占优，女方最终重新夺回主动
```

候选必须与已确认 Combat System / Combat Expression 相容，但不能提前锁死具体 Combo。

### 静默推导

只有一个明显合理结构时可静默推导。

禁止为了“完整”机械增加 Advantage 问题。

---

## 5. Outcome = 势均力敌时的 Trajectory

`Outcome = 势均力敌 / 未分胜负` 不能自动等于全程 50/50。

允许：

### Continuous Deadlock / 持续胶着

双方持续互相破解，很少形成持续 Advantage。

### Alternating Advantage / 交替占优

```text
A 先拿主动
→ B 通过 Turning Event 夺回
→ 再次转移
→ 最终仍未分胜负
```

### One-sided Pressure Without Finish / 一方长期占优但无法终结

一方大部分时间保持压迫，但另一方始终能化解关键威胁，因此最终没有真正输掉。

因此：

> **Outcome 与 Advantage Trajectory 必须分别满足，不能用“平局 / 胜负结果”吞掉整段主动权流动。**

---

## 6. Advantage Trajectory 边界

Trajectory 只描述：

> **主动权 / 控制关系怎样变化。**

它不负责具体招式，也不写 Hard Timeline。

推荐内部语义可以类似：

```text
Opening Initiative
→ First Counterplay Window
→ Turning Event / Temporary Advantage Shift
→ Reversal / Re-entry
→ Final Advantage State
```

这些是语义位置，不是固定五段模板。

禁止默认：

```text
0–4s A
4–7s B
7–11s A
11–15s Ending
```

除非用户、外部同步或 Model Adapter 明确需要严格时间块。

---

## 7. Combat Expression × Advantage Structure

用户最终确认：**不要继续设计复杂自动协调矩阵。**

正常组合由 Runtime 直接实现。

只有出现真实语义冲突，而且存在两个以上明显不同、会显著改变成片的高价值解释时，才询问用户。

例如：

```text
男方 Combat Expression：沉稳、防守反击
+
Advantage Trajectory：中段男方短暂夺回主动
```

本身不冲突，应直接实现成：

```text
接住 / 避开一轮
→ 捕捉窗口
→ 真正 Counter
→ 迫使女方响应
→ 短暂拿回主动
```

不能翻译成：

```text
男方长期只防守
→ 最后才准备反击
```

但如果用户要求类似：

```text
男方始终避免主动交锋
+
男方全程持续主动压制
```

这种真实冲突再询问用户，不建立复杂规则矩阵自动猜。

---

## 8. Counterplay Realization 强制合同

当 Counterplay Shape = 中 / 高时，以下内容**只能算 Setup，不能算 Counterplay 已实现**：

- 等待反击；
- 寻找机会；
- 保持防守；
- 准备抱摔；
- 即将反扑；
- 反击刚刚开始；
- 手臂开始发力；
- 在真正反击发生前结束。

必须真实发生：

- Attack；
- Counter；
- Re-counter；
- Re-entry；
- Grapple Entry；
- Weapon Counter；
- 其他符合当前 System / Refinement 的主动战斗行为。

而且至少造成一种真实状态后果：

- 迫使对方 Defense；
- 改变 Range / Route / Guard；
- 迫使对方退步 / 重新支撑；
- 改变 Balance / Position / Axis；
- 形成真实 Clinch / Grapple Window；
- 抢到短暂 Initiative。

**Counterplay 可以失败，但必须真实发生。**

不使用“每个角色必须攻击 N 次”的机械配额。

---

## 9. Ending 已降级为条件节点

Ending / Final Visual Ending 不再固定询问。

默认：

```text
Final Advantage State
+ Last Active Contact / Motion / Position / Momentum
→ Runtime 自然收束
```

只有以下情况才单独暴露 Ending：

- 用户明确要求击倒 / 制服 / 死亡 / 撤离；
- 用户明确要求相互架剑 / 某个定格动作；
- 存在多个真正高价值 Final Visual 分叉，而且无法高置信度代替用户决定。

特别禁止：

```text
男方本应有高 Counterplay
→ 但所有反击都写成“准备 / 即将”
→ 在真正反击发生前 Ending
```

Ending 不能吞掉主要 Combat Budget。

---

## 10. Advantage Structure 如何接现有 Runtime

本批没有建立第二套状态机。

正式映射：

```text
Advantage Structure.Outcome
→ Core Final / Global Advantage Intent

Advantage Structure.Advantage Trajectory
→ Core Battle Beat Advantage State + Turning Event sequence

Advantage Structure.Counterplay Shape
→ Choreography Initiative / Attack / Counter / Re-entry realization
```

Core 继续维护：

- Current Advantage；
- Advantage Source；
- Turning Event；
- Range / Position / Condition；
- Beat State Contract。

Choreography 继续负责：

- Action Phrase；
- Initiative Handoff；
- Exchange Depth；
- Movement / Technique / Transition；
- Counter / Re-counter；
- Persistent Combat Signature。

Prompt Assembly 继续负责把这些内容外显成具体动作，而不是把内部状态字段 Dump 给模型。

---

## 11. 本批新 Failure Signatures

本批 Runtime / Final Preflight 已正式识别：

### Counterplay Starvation

用户选择中 / 高 Counterplay，但劣势方几乎没有真实主动动作。

### Initiative Starvation

角色理论上有反击 / 再进入倾向，但成片动作链里长期无法真正获得 Initiative Window。

### Deferred Counterplay Collapse

主要 Counterplay 被持续推迟成：

```text
等待
→ 准备
→ 即将
→ Ending
```

### Advantage-to-Passivity Shortcut

Runtime 把“处于劣势”错误简化成“低 Attack Share / 长期只防守”。

### Outcome-Trajectory Collapse

Runtime 只保留最终胜负 / 平局，丢失用户确认的整段主动权流动。

---

## 12. 本批 Runtime 已实施完成

### 12.1 新增 Spec

`docs/combat-advantage-counterplay-spec.md`

Commit：

`859e8321fa0b2cd296dd2b9dd027db61d9b97a29`

### 12.2 新增运行期正文真源

`references/tasks/action-combat-video/advantage-structure-contract.md`

Commit：

`b4ec63c483010d37638ae85138122f18530501ca`

### 12.3 Tasks Index 接入主 Task

`references/tasks/index.md`

Action Combat 复合主 Task 现在包含：

```text
action-combat-video/index.md
+ core-playbook.md
+ choreography-playbook.md
+ advantage-structure-contract.md
+ 一个 specialist
```

Commit：

`88249a28a994db5b536ba2c502a53ce56896f4f2`

### 12.4 Action Combat Router 接入

`references/tasks/action-combat-video/index.md`

已经加入：

- `advantage-structure-contract.md` 固定 Runtime Read；
- Planning Context 的 Advantage Structure；
- Advantage Structure 条件询问；
- Ending 条件暴露；
- Expression × Advantage 真冲突才问；
- Counterplay Realization Gate；
- Advantage / Counterplay / Trajectory Realization；
- 新 Failure Signatures；
- Final Preflight 的 Counterplay / Trajectory / Ending 检查；
- Prompt QA 中保护用户已确认 Outcome / Counterplay / Trajectory。

Commit：

`7880e7797082baa89ce4450b7647d3231e864830`

### 12.5 当前 Handoff

`.handoff/current.md`

本文件已更新为本轮最新交接状态。

---

## 13. 静态实施验证结论

已经确认 Router 当前会把：

`references/tasks/action-combat-video/advantage-structure-contract.md`

作为 Action Combat 主 Task 的固定 Reference，而不是“只写了一份文档但 Runtime 不读”。

Planning Gate 已包含：

- Advantage Structure 是否已明确 / 条件询问 / 静默推导；
- 是否错误把“谁占优”映射成“另一方长期不攻击”；
- Outcome 只有粗结果时是否存在高价值 Counterplay / Trajectory 分叉；
- Expression 与 Advantage 是否存在真实语义冲突；
- Ending 是否被错误固定询问。

Execution / Final Preflight 已包含：

- 中 / 高 Counterplay 是否真实发生；
- 劣势方攻击是否迫使对方真实响应；
- Advantage Shift 是否经过真实 Turning Event；
- 是否出现 Counterplay Starvation / Deferred Counterplay Collapse；
- Ending 是否吞掉本应发生的有效攻防。

**这些只是静态 / 配置级实施验证，不等于真实 Runtime PASS，更不等于 Generated-video PASS。**

---

## 14. 本批故意没有做的事情

为了继续控制测试变量，本轮明确没有：

- 扩散打 / 拳击 / 摔跤 / MMA / 太极 / 剑法细节；
- 新增固定攻击次数；
- 建立 Expression × Advantage 自动组合矩阵；
- 大重构 Modern / Wuxia Specialist；
- 扩大 Stage-2 Pattern Library；
- 全量迁移 Quick Mode 上游架构；
- 因每个 Failure Signature 新建独立 Runtime 子系统；
- 为 Advantage / Counterplay 新建第二套 Battle State。

原则仍然是：

> **先跑真实回归，再决定下一刀。**

---

## 15. 固定办公室 G01 — 下一轮 Regression 输入

继续使用原始请求：

```text
使用交互模式，帮我做一段一个女生和男生再办公室打架的15秒电影片段，实际两个人穿着正常的职场服装但其实是2个杀手组织的职业杀手。中国男女，女的22岁长发高马尾漂亮身材完美，男性是一个秃顶又矮又胖的55岁领导，贴身搏斗，不要隔着什么办公桌
```

上一轮实际选择可作为回归参考：

```text
女方 Combat System：散打
男方 Combat System：拳击 + 摔跤

女方 Combat Expression：主动切线、强势抢节奏
男方 Combat Expression：沉稳防守、等待反击
```

但不要把 Advantage Structure 偷偷预填成唯一答案；应该观察新 Runtime 是否在真正存在高价值分叉时正确暴露 Advantage Structure。

---

## 16. G01 下一轮重点验证

### 16.1 Runtime Read List

必须确认实际读取：

`references/tasks/action-combat-video/advantage-structure-contract.md`

仍应继续命中已有关键执行 Reference：

- `minimum-validation-set.md`（条件命中时）；
- `subject-motion/control.md`（本 G01 应继续命中）；
- `action-camera-handoff-playbook.md`；
- `prompt-assembly/control.md`。

### 16.2 Interactive

如果用户只确定粗粒度：

```text
女方占优
或
不分胜负但女方稍占优势
```

而 Counterplay / Trajectory 存在明显不同方向，应出现 Advantage Structure 条件问题。

理想回归方向可以是：

```text
Outcome：女方总体占优但未完全制服

Counterplay：
男方高频还手但持续被化解

Trajectory：
女方先抢主动
→ 男方通过拳击 / 拳摔真正 Counter 并短暂夺回
→ 女方利用散打切线 / 反制重新压住
→ 男方后续仍有真实 Counter / Re-entry
→ 女方最终保持总体优势
```

这是 Regression 推荐，不是固定模板。

### 16.3 Final Prompt

必须看见：

- 男方的 Counter / Re-entry 是**已经发生的动作**，而不是意图词；
- 男方攻击能迫使女方真实 Defense / Footwork / Range / Guard / Position Response；
- 男方可以持续打不赢，但不能持续不打；
- 女方仍通过自己的散打 System / Expression 保持总体优势；
- Advantage Shift 有真实 Turning Event；
- Ending 不把男方主要 Counterplay 推到 15 秒之外；
- Whole-body / Persistent Signature / Motion Handoff / Camera Readability 不因本轮修正而回退。

---

## 17. Generated-video PASS 标准

只有真实生成视频同时满足：

- 男方可见地多次还击 / Counter / Re-entry；
- 这些还击真实迫使女方响应，而不是空挥；
- 女方总体仍然占优；
- 男方“防守反击”的 Expression 仍然成立，没有被改成疯狂主动压迫；
- 散打 vs 拳击 + 摔跤的 Persistent Combat Signature 仍清楚；
- Whole-body / Footwork / Balance / Range / Position 连续性没有回退；
- Ending 没有再次吞掉主要 Counterplay；

才算本批真正 Generated-video PASS。

如果 Prompt 看起来 PASS，但视频仍然表现为男方长期只防守，应优先诊断：

```text
Prompt Execution Load
/ Instruction Saturation
/ Model-specific Serialization
```

而不是马上继续扩 Combat System / 武术流派知识。

---

## 18. 下一会话行动顺序

严格按以下顺序：

```text
重新跑 G01 Interactive
→ 收集完整实际对话
→ 检查 Runtime Read List 是否包含 advantage-structure-contract.md
→ 检查 Advantage Structure 是否按条件暴露
→ 检查是否没有机械固定 Ending 问题
→ 检查 Final Prompt 中 Counterplay 是否真实发生
→ Prompt-level PASS / FAIL
→ PASS 后生成真实视频
→ Generated-video PASS / FAIL
→ 再决定下一批修改
```

如果 FAIL：

- 先诊断最小语义 / Routing / Serialization 原因；
- 优先修 Advantage / Counterplay Realization；
- 不继续扩具体格斗流派细节；
- 不重新从头 Grill 已经确认的 Identity × Combat System 架构。

---

## 19. 下一会话不要做的事

- 不重新讨论“职业杀手是不是一种打法”；
- 不重新讨论 Combat System 与 Combat Expression 是否要分开；
- 不重新讨论 Physical Presentation Domain 是否与 Combat System 正交；
- 不继续细化太极 / MMA / 散打 / 咏春 / 八极 / 剑法内部知识；
- 不新增固定“每人至少攻击几次”的动作配额；
- 不为了 Advantage Structure 再增加固定三轮问卷；
- 不把 Ending 恢复成固定 Planning Node；
- 不在没有真实 G01 回归证据前继续扩大 Runtime 设计。

当前最重要的是：

> **验证这一轮“Advantage ≠ Attack Share”是否真的让成片中的劣势方能够真实还手，同时仍保持正确的总体优势关系。**
