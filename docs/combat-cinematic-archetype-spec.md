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
   ├─ 人物气质 / 决策倾向
   │  ├─ 冷静 / 凶狠 / 克制 / 从容
   │  ├─ 主动压迫 / 后发反制 / 诱导 / 节奏破坏
   │  └─ 风险偏好 / 杀意 / 留手 / 再进入倾向
   └─ Cinematic Combat Archetype（可选）
      ├─ 李连杰型
      ├─ 吴京型
      ├─ 甄子丹型
      ├─ 成龙型
      └─ 李小龙型
```

因此：

> **Cinematic Combat Archetype 是 Combat Expression 的可选子维度，不是新的一级 Planning Node。**

---

## 3. Interactive 决策：不新增固定 Round 3

Action Combat Interactive 继续保持两个核心角色打斗节点：

```text
Round 1：Combat System / System Refinement
Round 2：Combat Expression / Performance Identity
```

已确认：

- Cinematic Combat Archetype 挂在 **Round 2** 内；
- 不新增固定 `Round 3：明星武打风格`；
- Round 2 可以同时解决：
  - 人物气质 / 决策倾向；
  - 可选 Cinematic Combat Archetype；
- 用户不需要明星参考时，Archetype 可以为空；
- 用户已经明确“李连杰式 / 吴京式 / 甄子丹式 / 成龙式 / 李小龙式”时，Round 2 直接继承，不重复确认；
- 用户只说“想要中国功夫电影那种打法”且不同 Archetype 会显著改变成片时，Round 2 可以把五种 Archetype 作为导演参考候选；
- 仍然遵守 `One Question, One Primary Decision Node`，因为它们都属于 `Combat Expression / Performance Identity`。

示例：

```text
女方：
Combat System = 太极
Combat Expression = 冷静诱导 / 后发反制
Cinematic Archetype = 李连杰型

男方：
Combat System = 八极
Combat Expression = 凶狠主动 / 持续压迫
Cinematic Archetype = 吴京型
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
+ Combat Expression
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

## 7. Anti-overdesign

本设计明确不做：

- 不新增固定 Round 3；
- 不给每位明星建立独立 Combat Engine；
- 不为每位明星建立固定 Combo；
- 不把电影作品逐片做招式库；
- 不因为存在明星 Archetype 就跳过 Combat System；
- 不把五种 Archetype 固定展示给所有 Combat 用户；
- 不无限收录“知名动作演员”，只有动作语言足够独立、稳定、可执行且能显著改变生成结果时才扩展。

---

## 8. 当前已确认决策

### CA-01

李连杰 / 吴京 / 甄子丹 / 成龙 / 李小龙作为少量稳定 `Cinematic Combat Archetype` 存在，明星名称用于用户易理解的导演参考，Runtime / Final Prompt 转换成中性动作语义。

### CA-02

`Cinematic Combat Archetype ≠ Combat System`；例如 `截拳道 / JKD` 是 Combat System，而 `李小龙型` 是电影动作表达。

### CA-03

Cinematic Combat Archetype 正式挂在 **Round 2 `Combat Expression / Performance Identity`** 下作为可选子维度，**不新增固定 Round 3**。

### CA-04

Round 2 可以同时决定人物气质 / 决策倾向与可选 Archetype；这仍属于同一个 Primary Planning Node，不违反 `One Question, One Primary Decision Node`。

---

## 9. 下一实施点

下一次修改 Interactive Runtime 时，需要把 Round 2 的职责扩展为：

```text
Combat Expression / Performance Identity
= Character combat temperament / decision tendency
+ optional Cinematic Combat Archetype
```

并保证：

- 用户不需要明星参考时不会多问；
- 用户已明确 Archetype 时直接继承；
- 中国功夫电影参考存在真实分叉时，可以在 Round 2 展示五种参考型；
- 不新增独立 Archetype 问卷轮次。
