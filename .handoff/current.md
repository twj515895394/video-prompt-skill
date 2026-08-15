# Video Prompt Skill — Action Combat Current Handoff

> 更新时间：2026-08-15 16:25（UTC+8）
> 仓库：`twj515895394/video-prompt-skill`
> 分支：`main`
> 当前阶段：**角色身份 × 打斗方式 MVP 已实现，等待真实 G01 Interactive 回归。**

---

## 0. 当前状态一句话

不要继续扩具体拳种 / 流派知识，也不要继续 Grill 细节。

本轮已经把旧的：

```text
职业 / 身份
→ Fighting Direction 候选
```

改成：

```text
Character / Narrative Identity
+ Per-Character Combat System / System Refinement
+ Per-Character Combat Expression
+ Physical Presentation Domain（必要时条件暴露）
→ Derived Choreography Direction
→ legacy Fighting Direction execution slot（MVP 兼容）
→ 现有 Stage-2 / Subject Motion / Persistent Signature / Action–Camera / QA
```

**当前只完成静态 / 配置级实现，还没有新的真实 Skill Runtime PASS，更没有 Generated-video PASS。下一步必须先跑固定 G01 Interactive 回归。**

---

## 1. 用户工作方式

项目继续使用 Grill-Me，但用户最新明确要求采用**批次式设计**：

```text
一个主题批次
→ Grill 相关设计分支
→ 每个确认结论进入该批 Spec
→ Spec 完整收口
→ 统一修改 Runtime
→ 先测试
→ PASS 后再进入下一批 / 深化
```

当前批次：

> **角色身份 × 打斗方式设计**

本批已经收口。用户明确要求：

> **先不要针对每个打法继续细化，先实现并测试，避免方向错误后浪费大量时间。**

因此下一会话不要继续追问太极、MMA、咏春、八极等细节体系实现。

---

## 2. 本批已确认设计结论

### 2.1 Identity ≠ Combat System

职业杀手、特工、警察、武术宗师、年龄、性别、外貌、体型都不能直接决定 Combat System。

例如全部合法：

```text
职业杀手 + MMA
职业杀手 + 太极
职业杀手 + 咏春
职业杀手 + 八极
```

### 2.2 Interactive 两个固定核心角色打斗节点

```text
Round 1：Combat System / Technique Backbone
Round 2：Combat Expression / Performance Identity
```

固定的是决策节点，不是重复确认：

```text
Unknown → Select
Known → Refine
```

### 2.3 两个字段都是角色级

1v1 中双方可以同体系，也可以不同体系：

```text
太极 vs 太极
太极 vs MMA
咏春 vs 八极
```

Combat Expression 也按角色独立。

### 2.4 1v1 同轮处理双方

1v1：

```text
Round 1 → 同时定义双方 System / Refinement
Round 2 → 同时定义双方 Expression
```

1vN：主角 + 关键对手独立，次要敌人可按功能组共享，禁止角色数量机械变成交互轮数。

### 2.5 Combat Expression 边界

Combat Expression = **人物战斗气质 + 战斗决策倾向**。

可以影响：主动 / 反制、压迫 / 诱导、节奏、风险、杀意、再进入方式。

不能直接定义：固定 Combo / 具体招式链。

### 2.6 Primary + Optional Secondary System

每个关键角色 MVP 结构：

```text
Primary Combat System：1
Secondary Combat System：0~1
```

MMA 这类完整混合体系可直接作为 Primary；内部拳摔 / Wrestling / 站立偏向属于 System Refinement，真正跨体系才进入 Secondary。

### 2.7 Combat System 与 Physical Presentation Domain 正交

```text
Combat System
→ 角色会什么体系

Physical Presentation Domain
→ 世界允许什么物理尺度 / 电影表现尺度
```

因此：

```text
太极 + Modern Grounded
太极 + Cinematic Wuxia
MMA + Modern Grounded
MMA + Cinematic Wuxia
```

都合法。

Physical Presentation Domain 不是固定第三轮，只在真正存在高价值歧义时条件暴露。

### 2.8 legacy Fighting Direction 降级

旧 `Fighting Direction / 怎么打` 不再是 Interactive 独立用户问题。

改为 Runtime 自动派生：

```text
System
+ Refinement
+ Expression
+ Domain
+ Scene / Range / Environment / Intent
→ Derived Choreography Direction
```

MVP 阶段临时映射到 legacy `Fighting Direction` execution slot，避免立即重构整个 Stage-2 / Choreography 下游。

---

## 3. 本批 Spec

主 Spec：

`docs/combat-system-performance-identity-separation-spec.md`

状态：**MVP 测试版已收口**。

本轮不要再扩 Spec 到每一种具体拳种知识；先看真实回归结果。

---

## 4. 本批已修改 Runtime

### 4.1 Interactive Contract

`assets/templates/mode-interactive-output-contract.md`

已实现：

- Round 1 System / Refinement；
- Round 2 Expression；
- 1v1 同轮双方；
- Unknown → Select / Known → Refine；
- Primary + optional Secondary；
- Physical Presentation Domain 条件暴露；
- Derived Choreography Direction；
- legacy Fighting Direction 不再暴露为用户问题；
- 用户要求先测试时停止继续 Grill。

Commit：

`2c2af011e3041f1499953ae36b8e59d30aafc9d4`

### 4.2 Top-level Skill

`SKILL.md`

已对齐新 Interactive 语义，并明确本轮只验证 Interactive，Quick 暂留 legacy 规划。

Commit：

`09f109a7532695cd26828940c56c6b86c18b180a`

### 4.3 Action Combat Router

`references/tasks/action-combat-video/index.md`

已移除 Interactive 必须重新问旧 Fighting Direction 的冲突逻辑，Planning Context 改为角色级 System / Refinement / Expression + Derived Direction。

Commit：

`28a399cecf6266a8faaa5ae76ad64ac4c5379aea`

### 4.4 Choreography Playbook

`references/tasks/action-combat-video/choreography-playbook.md`

已把 Interactive Planning Graph 改成新结构，旧 Fighting Direction 只保留兼容 execution slot。

Commit：

`15cdf400ba46c9489b76534bc93ef986a8bc2390`

### 4.5 Spec 收口

`docs/combat-system-performance-identity-separation-spec.md`

Commit：

`82b76ea589419c792b2805968626d34d4dca2a30`

---

## 5. 本轮故意没有改的内容

为了减少测试变量，本轮明确暂不迁移：

- Quick Mode 全量角色 System 架构；
- `modern-combat-playbook.md` 大重构；
- `cinematic-wuxia-playbook.md` 大重构；
- 大规模拳种 / 武术流派知识；
- Stage-2 Pattern Library 扩展；
- Model Adapter 新逻辑。

如果 Interactive MVP 方向 FAIL，优先修上游；不要先扩这些下游。

---

## 6. Golden Scenario G01 — 本次测试输入

继续使用原始请求，不改场景：

```text
使用交互模式，帮我做一段一个女生和男生再办公室打架的15秒电影片段，实际两个人穿着正常的职场服装但其实是2个杀手组织的职业杀手。中国男女，女的22岁长发高马尾漂亮身材完美，男性是一个秃顶又矮又胖的55岁领导，贴身搏斗，不要隔着什么办公桌
```

注意：旧 G01 的 MMA + 女拳腿 / 男拳肘抱摔仍作为对照参考，但由于本轮正在验证新的角色级 System 交互，**不要在 Runtime 里偷偷预填成用户已确认；应该观察新的 Round 1 是否正确提出 System 选择 / 推荐。**

---

## 7. G01 Interactive MVP 预期行为

### Round 1

必须是：

> **Per-Character Combat System / System Refinement**

不得再出现把以下作为与 MMA / 太极同级的 Combat System：

```text
现代职业杀手短打
职业杀手近身格斗
```

推荐可以是例如：

```text
女方：MMA，拳腿倾向
男方：MMA，拳肘 + 抱摔倾向
```

但这是系统推荐，不是由“职业杀手”身份强制映射。

### Round 2

必须是：

> **Per-Character Combat Expression**

例如：

```text
女方：冷静、诱导、反制后快速夺主动
男方：主动压迫、持续抢先手、被反制后快速再进入
```

Round 2 不得偷换 Round 1 的 System。

### Physical Presentation Domain

当前办公室场景如果没有额外歧义，通常应静默推导 Modern Cinematic Grounded，不需要机械增加第三轮。

### Fighting Direction

不得再出现独立旧问卷：

> “你希望整体怎么打？”

Runtime 应自动得到 Derived Choreography Direction，再映射到 legacy execution slot。

---

## 8. 本次 Interactive 回归 PASS / FAIL

### PASS

- 职业 / 身份不再成为 Combat System 候选；
- Round 1 同时定义双方 System / Refinement；
- Round 2 独立定义双方 Expression；
- Known → Refine / Unknown → Select 生效；
- Domain 只在真实歧义时暴露；
- 不再多问一次旧 Fighting Direction；
- 后续仍能进入现有 Stage-2 / Subject Motion / Persistent Signature / Action–Camera / Prompt QA 链。

### FAIL

- 仍出现“现代职业杀手短打”与 MMA / 太极同级；
- 因年龄 / 性别 / 体型 / 职业自动分配某体系；
- 1v1 被机械拆成四轮；
- Round 2 偷换 Round 1 的 System；
- 又问一次旧 Fighting Direction；
- 为新结构立刻加载大量流派细节并导致交互失控。

---

## 9. 本轮测试顺序

下一步必须按这个顺序：

```text
固定 G01 原始请求
→ 收集完整实际 Interactive 对话
→ 检查 Round 1 / Round 2 / Domain / 是否出现旧 Fighting Direction
→ 检查 Runtime Read List
→ 检查 Final Prompt
→ Prompt-level PASS 后再决定是否生成真实视频
→ Generated-video Regression
```

当前最重要的是**先验证交互架构方向**，不是马上追求最终视频 PASS。

---

## 10. 旧的下游质量 Gate 仍有效

本轮没有废除已有：

- Stage-2 Pattern Hit Evidence；
- Subject Motion 条件必读；
- Persistent Combat Signature；
- Model Execution Realizability；
- Motion / Energy Carry-over；
- Action–Camera Handoff；
- Perceptual Impact；
- Camera Base Viewing Priority / Camera Hard Constraint；
- Prompt Assembly；
- Final Prompt QA / Silent Self-Repair。

如果新 Interactive PASS，再继续验证这些下游是否正确消费新的角色级上下文。

---

## 11. 下一会话怎么开始

用户下一步最可能带回新的 G01 实际 Skill 对话。

不要继续 Grill 新设计。

第一步只回答：

> **这次 Round 1 / Round 2 是否真的按新的 Combat System / Combat Expression 结构运行？旧“职业杀手 → Fighting Direction”是否已经消失？**

只有这个交互层 PASS，才继续检查 Runtime Read List / Final Prompt；没有真实证据前不能宣称新架构已经成功。
