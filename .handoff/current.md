# Video Prompt Skill — Action Combat Current Handoff

> 更新时间：2026-08-16 19:23（UTC+8）  
> 仓库：`twj515895394/video-prompt-skill`  
> 分支：`main`  
> 当前阶段：**RF-22 Completion Gate 修复仍待真实 ×2 PASS-NATIVE；用户已明确覆盖此前 Combat Knowledge Freeze，要求把新 Concrete Action Catalog 直接接入 Runtime，并与 RF-22 后续一起做 Integrated Regression。**

---

## 0. 新会话接管顺序

优先读取：

1. `.handoff/current.md`
2. `docs/action-combat-video-regression-fix-spec.md`
3. `docs/combat-action-reference-knowledge-spec.md`
4. `SKILL.md` 的 `Action Combat Post-Planning Mandatory Path`
5. `references/tasks/action-combat-video/interactive-combat-policy.md`
6. `references/tasks/action-combat-video/regression-fix-runtime-policy.md`
7. `references/libraries/combat-choreography-patterns/index.md`
8. 如命中 Abstract Pattern Gap：`minimum-validation-set.md`
9. 如命中 Concrete Action Selection Gap：`action-reference-catalog.md`

不要重新 Grill 已确认的 Action Catalog Schema。

---

## 1. RF-22 当前状态

历史失败：

```text
Round 1 / Round 2 / Ending 已 resolved
→ Runtime Policy 提前 READ
→ Camera / Physical Presentation 尚未 resolved
→ Early Direct Read
→ RF-22 FAIL
```

已实施最小修复：

```text
Interactive Planning Completion Gate
→ 所有当前高价值 Interactive 决策 resolved
→ Completion Gate PASS
→ 才允许 READ regression-fix-runtime-policy.md
```

实现 Commit：

`f465e4b61f9cc9aed7de73183001969a206b13bd`

RF-22 原关闭条件仍为：

> **完全相同 G01，连续 2 次 PASS-NATIVE。**

但用户已明确要求不再先单独隔离 RF-22；下一轮开始按 Integrated Regression 一起验证 Catalog Wiring。

---

## 2. 固定 G01 Regression

原始场景：

- 15 秒；
- 中国现代办公室；
- 22 岁中国女性，长发高马尾，正常职场服装；
- 55 岁中国男性领导，矮胖、秃顶，正常职场服装；
- 两人属于敌对杀手组织；
- 徒手贴身近战；
- 不隔办公桌 / 大型障碍；
- Interactive Mode；
- 无枪械刀具。

固定选择：

```text
Round 1 = A
女：中国功夫电影混合体系
男：摔跤 / 擒抱体系

Round 2 Expression = A
女：冷静诱导 / 后发反制
男：主动压迫 / 持续再进入

Archetype = none
Ending = A
Camera = A
Physical Scale = A
```

Physical Scale A：写实电影尺度、无威亚无超自然。

---

## 3. 新 Combat Action Reference Knowledge

用户补充 6 张《AI漫剧打斗动作提示词大全》图片。

重新逐张核对后，来源实际是 **17 个动作模板（1–17）**，不是 18 个。

正确来源清单：

```text
01 极速瞬身突袭
02 凌空飞踢
03 反手格挡防御
04 蓄力重拳冲击
05 侧身闪避走位
06 腾空旋转斩击
07 低空滑步突袭
08 双臂交叉防御
09 后仰规避反击
10 蓄力霸体冲击
11 灵活跳跃突袭
12 空中滞空连击
13 横扫腿击
14 贴身缠斗快打
15 侧身拔刀斩
16 抬手震气击退
17 落地震地重击
```

此前草稿误多出的“后撤蓄力重击”已从 Runtime Catalog 删除。

---

## 4. 已确认 Action Catalog Schema

最小知识颗粒度：

> **Single Action Template / 单动作模板**

正式 Combat Role 仅：

```text
Entry
Pressure
Defense
Counter
Re-entry
Reversal
Signature
Finisher
```

关键结构：

```text
Action Name / Alias
Functional Category
Applicable Range
Core Action Mechanic
Body / Contact Relation
Immediate Visible Result
Min / Default / Max Physical Level
Combat Role
Response Compatibility: Best Against / Poor Against / Best State
Sparse State Transition: Before → After
Initiative Effect
Tempo Profile
Risk / Commitment
Prerequisites
Transition Compatibility
Environment Impact
Risks / Failure Modes
Metadata
```

设计原则：

- Visual Medium 与 P1/P2/P3 Physical Level 解耦；
- 真人写实画面可以使用 P3；
- 降低 Physical Level 不能改变 Core Action Mechanic；
- Response Compatibility 保持轻量半结构化；
- State Transition 只记录真正变化的状态；
- Initiative Effect 不建结果状态机；
- Prerequisites 不拆体型 / 柔韧 / 武器 / 环境多个子系统；
- Environment Impact 不是独立破坏 Engine；
- 只保留能改善实际动作选择与成片的字段。

设计真源：

`docs/combat-action-reference-knowledge-spec.md`

---

## 5. Runtime Wiring — 已实施

正式 Concrete Action Leaf：

`references/libraries/combat-choreography-patterns/action-reference-catalog.md`

正式目录路由：

`references/libraries/combat-choreography-patterns/index.md`

全局 Library 路由已更新：

`references/libraries/index.md`

运行语义：

```text
Combat Planning Context / Exchange Spine
→ detect Stage-2 gap

缺抽象 Movement / Technique / Transition 策略
→ minimum-validation-set.md

缺一个符合当前 State 的具体动作
→ Concrete Action Selection Gap
→ action-reference-catalog.md

必要时
→ Abstract Pattern → Concrete Catalog Action

也可在 Gap 已明确到单动作时
→ Catalog Direct Resolution

→ Concrete Action Phrase
```

Catalog 不是默认必读大词典，不机械增加 Library 配额；没有匹配候选时继续使用 Fighting / Martial / Weapon / Pattern Knowledge。

选择顺序：

```text
Prerequisites
→ Physical Level legality
→ Combat Role
→ Response Compatibility
→ required State Transition
→ Tempo / Risk / Initiative
```

最终 Prompt 不输出这些内部标签，只输出具体动作、接触、反馈、状态后果和下一动作入口。

---

## 6. 本轮 Wiring Commits

```text
f9f25878a50ec16a0f90d46885e42736a949ad1e
feat: wire concrete combat action catalog into runtime

10ba83e1cb009e5f21b6d07dbb2470a2bd18efbf
feat: route combat stage-2 to concrete action catalog

64a5c16445402f6a5849afe6ae4bd10ba04aaefe
feat: expose concrete combat action catalog in library routing

c2109d343ac100c514838a34958bd4b1edceed47
test: update combat action catalog validation for runtime wiring

9f7bb8ff73bf5a9f69e2d182dede85058136ec8e
docs: mark combat action knowledge runtime-wired
```

---

## 7. Integrated Regression 下一步

下一次真实固定 G01 同时检查：

### RF-22

```text
Pending User Decision Guard
Planning Completion Gate
Runtime Policy Read Timing
PASS-NATIVE / PASS-RECOVERED / FAIL
```

### RF-14～RF-20

继续检查：

- Stage-2 Traceability；
- Granularity Distribution；
- Exchange Density；
- Concrete Compression；
- Duration-aware Planning；
- Two-pass Choreography；
- Serialization Dedup。

### New Catalog Wiring

必须能观察：

```text
Concrete Action Selection Gap
→ Catalog Read Evidence
→ Selected Action ID
→ 为什么 Response Compatible
→ Physical Level 是否合法
→ Prerequisites 是否成立
→ State Transition 是否真正实现
→ Realized Concrete Action Phrase
```

特别检查：

- 不把 Catalog 名称直接当最终招式句；
- 不机械塞动作；
- 不让 15 秒 Prompt 因新知识再次过度膨胀；
- 不让 P3-only 动作进入固定 G01 的 Physical Scale A；
- 不让 Catalog 覆盖女 / 男已经确认的 Combat System 与 Persistent Signature。

---

## 8. 当前目标

> **下一步执行固定 G01 Run 1。**

这次不再是纯 RF-22 隔离测试，而是：

> **RF-22 + existing RF checks + Concrete Action Catalog Wiring 的集成回归。**

如果出现失败：

```text
先定位 Failure Layer
→ Routing / Catalog Selection / Pattern Resolution / Phrase Realization / Compression / Assembly
→ 做最小修复
→ 再回归
```

不要因新 Catalog 失败就重新推翻已经确认的整套 Schema。
