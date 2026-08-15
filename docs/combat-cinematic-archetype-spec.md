# Combat Cinematic Archetype Spec

> 状态：已确认
> 日期：2026-08-15
> 作用：定义少量华语电影武打明星参考型在 Action Combat Interactive / Runtime 中的职责边界与交互位置。

## 1. 背景

用户明确希望将李连杰、吴京、甄子丹、成龙、李小龙这类具有稳定电影武打表达差异的参考型引入 Action Combat，但不希望它们被错误当作 MMA、咏春、八极、截拳道等 `Combat System / Technique Backbone`。

当前已确认：这类参考型数量有限，具有明显差异，不属于无边界扩张的明星名单；只在确实存在稳定、可复用、能显著改变生成动作结果的情况下扩展。

---

## 2. 核心分层

正式结构：

```text
Combat System / Technique Backbone
→ 角色真正会什么体系
→ 太极 / 咏春 / 八极 / 散打 / MMA / 泰拳 / 拳击 / 截拳道 / JKD ...

Combat Expression / Performance Identity
→ 角色以什么气质、决策方式和电影动作表达去使用该体系
   ├─ 子维度 A：Character Combat Expression
   │  ├─ 冷静 / 凶狠 / 克制 / 从容
   │  ├─ 主动压迫 / 后发反制 / 诱导 / 节奏破坏
   │  └─ 风险偏好 / 杀意 / 留手 / 再进入倾向
   └─ 子维度 B：Cinematic Combat Archetype（可选）
      ├─ 李连杰型
      ├─ 吴京型
      ├─ 甄子丹型
      ├─ 成龙型
      └─ 李小龙型
```

因此：

> **Cinematic Combat Archetype 是 Combat Expression 的可选子维度，不是新的一级 Planning Node。**

---

## 3. Interactive 决策：Round 2 同轮双子维度，不新增 Round 3

Action Combat Interactive 继续保持两个核心角色打斗节点：

```text
Round 1：Combat System / System Refinement
Round 2：Combat Expression / Performance Identity
```

Round 2 内部采用两个**分别选择、分别表达、同轮完成**的子维度：

```text
子维度 A：人物战斗表达
→ 冷静 / 凶狠 / 克制 / 主动压迫 / 后发反制 / 节奏破坏 ...

子维度 B：电影武打参考（optional）
→ 李连杰型 / 吴京型 / 甄子丹型 / 成龙型 / 李小龙型 / 不指定 / 自定义
```

已确认：

- Cinematic Combat Archetype 挂在 **Round 2** 内；
- 不新增固定 `Round 3：明星武打风格`；
- **两个子维度分开展示，不提前组合成套餐候选**；
- 用户可以选择任意人物战斗表达，再独立选择任意 Archetype；
- 系统不得把 `冷静后发 + 李连杰型`、`凶狠压迫 + 吴京型` 等预绑定成唯一组合；
- 用户不需要明星参考时，Archetype 可以为空 / 不指定；
- 用户已经明确“李连杰式 / 吴京式 / 甄子丹式 / 成龙式 / 李小龙式”时，Round 2 直接继承，不重复确认；
- 用户只说“想要中国功夫电影那种打法”且不同 Archetype 会显著改变成片时，Round 2 可以把五种 Archetype 作为导演参考候选；
- 仍然遵守 `One Question, One Primary Decision Node`，因为两个子维度都属于 `Combat Expression / Performance Identity`。

示例：

```text
Round 2｜Combat Expression / Performance Identity

人物战斗表达：
女方 = 冷静诱导 / 后发反制
男方 = 凶狠主动 / 持续压迫

电影武打参考（可选）：
女方 = 李连杰型
男方 = 吴京型
```

这仍然只占 Round 1 + Round 2 两个核心节点。

---

## 4. 五种 Archetype

执行语义真源：

`references/libraries/combat-cinematic-archetypes/library.md`

当前五种：

1. **李连杰型｜轻灵流畅 / 武术线条**
   - 身法、步法、腿法、转身、高低位、动作线条清楚；
   - 全身流动，避免站桩。

2. **吴京型｜硬朗爆发 / 全身压迫**
   - 爆发进入、重接触、逼退、破平衡、再进入；
   - 强冲击但仍保持空间移动。

3. **甄子丹型｜极速现代融合 / 近身连锁**
   - 高速截击、拳腿肘膝、短控、快速换距与 Counter Chain；
   - 现代融合不等于 MMA 站桩互殴。

4. **成龙型｜环境互动 / 空间即武器**
   - 跑、绕、翻、钻、跌扑恢复、障碍穿越；
   - Environment Affordance 是动作链核心；
   - Comedy Tone 可选，不强制。

5. **李小龙型｜爆发截击 / 节奏破坏 / 极简直接**
   - Interception / Stop-hit / Broken Rhythm / Explosive Entry / Exit / Range Control；
   - 短促爆发 + 快速换距，不写成长时间原地连打。

---

## 5. Combat System 与 Archetype 的边界

禁止把明星参考直接当体系：

```text
李小龙型 ≠ 截拳道 / JKD
甄子丹型 ≠ MMA
李连杰型 ≠ 某一固定传统拳种
成龙型 ≠ 喜剧格斗体系
吴京型 ≠ 军警 / 杀手职业体系
```

合法组合：

```text
截拳道 + 李小龙型
散打 + 李小龙型
咏春 + 甄子丹型
八极 + 吴京型
太极 + 李连杰型
任意合理 Combat System + 成龙型环境编排
```

Archetype 只改变电影动作表达权重，不覆盖已确认的 Technique Backbone。

---

## 6. Runtime 合成

Runtime 使用：

```text
Per-Character Combat System
+ System Refinement
+ Character Combat Expression
+ Cinematic Combat Archetype（optional）
+ Physical Presentation Domain
+ Scene / Range / Environment / Intent
→ Derived Choreography Direction
```

随后进入现有：

```text
Stage-2 Gap Detection
→ Pattern / Technique Knowledge
→ Concrete Action Phrase
→ Subject Motion / Motion Carry-over
→ Action–Camera
→ Prompt Assembly
→ Final Preflight
```

最终 Prompt 优先使用中性动作语义实现 Archetype，不只写明星姓名。

---

## 7. Round 1 推荐联动：功夫电影观感优先，不默认把 MMA 放首位

当用户明确表达以下任一目标：

- 中国功夫电影 / 华语武打片观感；
- 李连杰 / 吴京 / 甄子丹 / 成龙 / 李小龙式电影武打；
- 不要站桩；
- 希望更丰富的身法、步法、腿法、转身、高低位、路线和空间移动；

Round 1 的 Combat System 推荐必须响应这个**观看目标 / 动作表达意图**，而不是因为场景是“现代、办公室、杀手、警匪”就机械把 MMA 放在默认推荐首位。

推荐策略：

```text
用户明确中国功夫电影观感
→ 优先展示更容易支持 Whole-body Movement / Footwork / Body Method / Kick Integration / Route Change 的合理体系
→ 例如散打、八极、长拳、咏春、截拳道 / JKD，以及其他与角色 / 场景相容的中国武术体系
→ MMA 仍可作为候选，但不默认占首位
```

注意：

- 这不是“中国武术永远比 MMA 好”的全局偏置；
- 用户明确要竞技综合格斗、笼斗、真实 MMA 时，MMA 仍应优先；
- 不能因为选择某个 Cinematic Archetype 就自动锁定某一 Combat System；
- 推荐系统只调整候选排序和解释，不把 Archetype 与拳种预绑定；
- 最终是否能避免 Static Standing Combat，仍由 Choreography / Movement / Stage-2 / Final Preflight 保证，不能只靠换一个体系名称。

核心原则：

> **题材身份不能决定 Combat System，但用户明确的动作观感目标可以影响 Round 1 的推荐排序。**

> **Modern 场景 ≠ MMA 默认。Chinese cinematic kung-fu intent → whole-body-capable systems first.**

---

## 8. Anti-overdesign

本设计明确不做：

- 不新增固定 Round 3；
- 不给每位明星建立独立 Combat Engine；
- 不为每位明星建立固定 Combo；
- 不把电影作品逐片做招式库；
- 不因为存在明星 Archetype 就跳过 Combat System；
- 不把五种 Archetype 固定展示给所有 Combat 用户；
- 不把人物战斗表达和明星 Archetype 预组合成套餐；
- 不无限收录“知名动作演员”，只有动作语言足够独立、稳定、可执行且能显著改变生成结果时才扩展。

---

## 9. 当前已确认决策

### CA-01

李连杰 / 吴京 / 甄子丹 / 成龙 / 李小龙作为少量稳定 `Cinematic Combat Archetype` 存在，明星名称用于用户易理解的导演参考，Runtime / Final Prompt 转换成中性动作语义。

### CA-02

`Cinematic Combat Archetype ≠ Combat System`；例如 `截拳道 / JKD` 是 Combat System，而 `李小龙型` 是电影动作表达。

### CA-03

Cinematic Combat Archetype 正式挂在 **Round 2 `Combat Expression / Performance Identity`** 下作为可选子维度，**不新增固定 Round 3**。

### CA-04

Round 2 可以同时决定人物气质 / 决策倾向与可选 Archetype；这仍属于同一个 Primary Planning Node，不违反 `One Question, One Primary Decision Node`。

### CA-05

Round 2 采用**同轮双子维度分别选择**：`Character Combat Expression` 与 `Cinematic Combat Archetype` 分开展示、分开选择；不得预先组合成“气质 + 明星型”的绑定套餐。

### CA-06

当用户明确追求中国功夫电影 / 华语武打 / 不站桩 / 明星型功夫电影观感时，Round 1 不再默认优先推荐 MMA；优先给更有利于 Whole-body Movement、身法、步法、腿法、路线与高低位变化的合理中国武术体系。MMA 保留为合法候选，不做全局降级。

---

## 10. 下一实施点

Interactive Runtime 需要同时落实两件事：

1. Round 2：

```text
Combat Expression / Performance Identity
├─ Character Combat Expression
└─ optional Cinematic Combat Archetype
```

2. Round 1 Recommendation Policy：

```text
Chinese cinematic kung-fu intent
→ Chinese whole-body-capable system candidates first
→ MMA remains available but is not mechanically top-ranked
```

并保证：

- 用户不需要明星参考时不会多问；
- 用户已明确 Archetype 时直接继承；
- 中国功夫电影参考存在真实分叉时，可以在 Round 2 展示五种参考型；
- 两个子维度独立，不做组合套餐；
- 不新增独立 Archetype 问卷轮次；
- 不把现代身份 / 场景重新变成 MMA 的快捷映射；
- 不把某个明星 Archetype 强绑定某个拳种。
