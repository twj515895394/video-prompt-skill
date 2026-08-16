# Combat Choreography Patterns Index

> Runtime status: **RF-22 FREEZE / new action catalog is NOT runtime-wired**  
> 本索引只负责本目录内部职责导航，不改变 `SKILL.md`、Action Combat Task Router、Stage-2 Mandatory Path 或当前 Library 加载预算。

## 1. 目录职责

本目录保存 Action Combat Stage-2 可用的“动作生产 / 具体动作参考知识”。

必须区分两种不同颗粒度：

```text
Abstract Choreography Pattern
→ 告诉 Runtime 当前 Movement / Technique / Transition 缺口可以怎样被解决

Concrete Action Reference
→ 告诉 Runtime 一个具体单动作怎样成立、适合回应什么、会改变什么状态、具有怎样的节奏 / 风险 / 物理表现
```

两者互补，不互相复制正文。

---

## 2. 当前文件

### `minimum-validation-set.md`

**当前正式 Runtime Leaf。**

职责：

- CK-18 / RF-22 当前 Stage-2 最小验证知识；
- Movement / Technique / Transition 三类抽象 Pattern；
- Pattern Hit Evidence；
- Pattern-to-Action Resolution；
- 当前 G01 Regression 的运行期知识证据。

RF-22 关闭前保持冻结。本轮不得为了新动作库修改其 Pattern、Schema、路由或样例。

### `action-reference-catalog.md`

**新建 Concrete Action Reference Knowledge；当前未接 Runtime。**

职责：

- 单动作模板作为最小知识颗粒度；
- Combat Role / Response Compatibility / State Transition；
- Physical Level Range；
- Tempo / Commitment / Initiative；
- Prerequisites / Environment Impact；
- 前后动作衔接参考；
- 把用户提供的 18 个动作素材抽象成可复用、模型无关的动作知识。

它不是：

- 固定 Combo；
- Battle Beat Engine；
- Camera Runtime；
- Style Library；
- Combat System / Martial Profile 的替代品。

### `action-reference-validation.md`

**静态知识验证文件；当前不参与生成。**

职责：

- Schema 完整性；
- Core Action Mechanic 与视觉特效解耦；
- Min / Default / Max Physical Level 合法性；
- Combat Role 枚举约束；
- Response / Transition 可执行性；
- 去重与 Alias 检查；
- 最小攻防链组合验证；
- RF-22 Freeze 边界验证。

---

## 3. 当前加载边界

RF-22 关闭前：

```text
Stage-2 Runtime
→ 继续按现有 Task Router 使用 minimum-validation-set.md

Stage-2 Runtime
-X- 不读取 action-reference-catalog.md
```

本轮故意不做：

- 不修改 `references/libraries/index.md` 的正式运行路由；
- 不修改 `references/tasks/action-combat-video/index.md`；
- 不修改 `SKILL.md`；
- 不修改 `regression-fix-runtime-policy.md`；
- 不增加默认 Library Detail Slot；
- 不改变 G01 Regression 变量。

RF-22 连续两次 PASS-NATIVE 后，再单独设计 Catalog Wiring / Selection Policy / Loading Budget。

---

## 4. 单一真源边界

```text
Combat System / Technique Backbone
→ combat-fighting-profiles / combat-martial-profiles / combat-weapon-profiles

Abstract Stage-2 Gap Pattern
→ minimum-validation-set.md

Concrete reusable single action
→ action-reference-catalog.md

Environment Affordance
→ combat-environment-patterns/library.md

Visual Style
→ references/styles/*

Battle State / Exchange Spine / Advantage / Coverage
→ Action Combat Task Playbooks / Contracts
```

如果内容同时涉及多个层级，只在对应真源保存完整正文，其余位置只写引用关系。
