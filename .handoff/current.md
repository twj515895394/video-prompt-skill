# Video Prompt Skill — Action Combat Current Handoff

> 更新时间：2026-08-16 20:12（UTC+8）  
> 仓库：`twj515895394/video-prompt-skill`  
> 分支：`main`  
> 当前阶段：**RF-22 Completion Gate 已有一轮新的正向时序证据；Concrete Action Catalog 已接入，但最新真实测试没有实际 READ Catalog，且 Final Prompt 仍出现 `/` / `或` 的同层动作候选。已实施最小修复：`Concrete Action Selection Gap → Catalog READ → Single Concrete Action Gate`。下一步继续 Integrated Regression。**

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

已实施 Completion Gate：

```text
Interactive Planning Completion Gate
→ 所有当前高价值 Interactive 决策 resolved
→ Completion Gate PASS
→ 才允许 READ regression-fix-runtime-policy.md
```

原 RF-22 修复 Commit：

`f465e4b61f9cc9aed7de73183001969a206b13bd`

原关闭条件仍为：

> **完全相同固定 G01，连续 2 次 PASS-NATIVE。**

注意：用户已要求 Catalog 与 RF-22 一起验证，但这不自动改变 RF-22 原 close criteria。

---

## 2. 最新真实测试（2026-08-16）

用户提供完整 Interactive 对话记录。

本次选择不是固定 RF-22 close baseline：

```text
Combat System:
女 = Chinese Cinematic Kung-fu Hybrid
男 = 散打

Expression:
A
女冷静诱导 / 后发反制后提速
男主动压迫 / 持续再进入

Archetype:
女李连杰型
男吴京型

Rhythm:
Dynamic Wave

Advantage:
女方最终占优，男方高频还手

Camera:
完整动作可读优先

Physical Presentation:
Modern Level 2
```

因此：

> **本次不能计入 RF-22 固定 G01 ×2 Close Count。**

但它提供有效集成证据。

---

## 3. 最新测试：RF-22 时序观察

实际顺序：

```text
Combat System
→ Expression / Archetype
→ Rhythm
→ Advantage
→ Camera
→ Physical Presentation
→ READ regression-fix-runtime-policy.md
→ Core / Choreography / Archetype
→ Stage-2
→ Camera Handoff / Assembly / Adapter
→ Final Prompt
```

这次没有再次出现：

```text
Runtime Policy READ
→ Camera / Physical Presentation 仍未 resolved
```

所以：

> **RF-22 Completion Gate / Runtime Read Timing = PASS-NATIVE 倾向强。**

但因为本次不是固定 G01 baseline，只作为 supporting evidence，不计 Close Count。

---

## 4. 最新测试：Catalog Wiring 失败点

实际 Read List 中有：

```text
minimum-validation-set.md
combat-cinematic-archetypes/library.md
action-camera-handoff-playbook.md
prompt-assembly/control.md
subject-motion/control.md
generic.md
```

但没有：

`references/libraries/combat-choreography-patterns/action-reference-catalog.md`

因此正式定性：

> **Catalog Routing NOT HIT / Concrete Action Selection Gap 未被识别。**

不能用本次 Final Prompt 的改善证明 Catalog 有效，因为 Catalog 没有真实 READ Evidence。

---

## 5. 最新测试：RF-17 明确 FAIL

Final Prompt 仍出现同层互斥动作候选，例如：

```text
后腿侧踹/前蹬
先起腿侧踢/低抽
紧接短拳或掌缘
掌根或拳面擦击
```

这些表达把 Runtime 应该完成的动作选择留给视频模型。

正式判定：

> **Concrete Action Choice Leakage / RF-17 FAIL**

正确目标：

```text
不是：侧踹 / 前蹬
而是：选定一个，例如右腿前蹬中盘

不是：短拳或掌缘
而是：选定一个，例如左掌缘横切前臂
```

多个动作真实同时发生时可以共存，但必须有明确并发 / 先后关系，不属于候选。

---

## 6. 最新测试：其他观察

### Movement Causality

表现良好：

- 外侧斜切改变攻击线；
- 承重腿破坏迫使换支撑；
- 靠撞压力被转髋 / 转轴用于脱离；
- 新 Route / Axis / Support 会成为下一动作入口。

RF-13 保持 PASS 倾向强。

### Per-Character Signature

保持明显差异：

```text
女：侧切 / 沉身 / 转轴 / 腿法 / 外侧角度 / 后发提速
男：正面压迫 / 低踢 / 直摆拳 / 靠撞 / 追步 / 再进入
```

没有明显塌成同一种 Upper-body 短打模板。

### Advantage / Counterplay

实现较好：女最终占优，但男方持续拥有真实 Attack / Re-entry，不是沙袋。

### RF-14

`minimum-validation-set.md` 已读取，动作里能看到 M/T/X 思路，但没有完整可观察：

```text
Gap → Slot → Pattern → Detail → Concrete Phrase
```

因此 Stage-2 Traceability 仍为 PARTIAL / Evidence 不足。

### RF-15 / RF-16

Final Prompt 仍偏长；15 秒内动作与解释密度较高。动作质量提高，但 Granularity / Execution Budget 仍需后续观察，不在本次最小修复中处理。

---

## 7. Concrete Action Catalog

来源为用户提供 6 张《AI漫剧打斗动作提示词大全》图片。

重新核对后实际为 **17 个动作模板（1–17）**：

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

此前误加的“后撤蓄力重击”已删除。

正式 Leaf：

`references/libraries/combat-choreography-patterns/action-reference-catalog.md`

核心字段：

```text
Core Action Mechanic
Min / Default / Max Physical Level
Combat Role
Response Compatibility
Sparse State Transition
Initiative Effect
Tempo Profile
Risk / Commitment
Prerequisites
Transition Compatibility
Environment Impact
```

Combat Role 固定 8 个：

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

---

## 8. 本次最小修复 — 已实施

用户确认只修：

> **Concrete Action Selection Gap → Action Catalog READ → Single Concrete Action Gate**

不修改：

- RF-22 Completion Gate；
- Camera Runtime；
- Quick Mode；
- Combat Role / Schema；
- Catalog Knowledge Coverage；
- Granularity / Density 其他 Runtime。

### 8.1 `minimum-validation-set.md`

新增正式触发规则：

```text
Pattern-to-Action Resolution
→ 已知道需要什么战斗功能
→ 仍有两个以上同层互斥 Concrete Action Head
→ Concrete Action Selection Gap
→ MUST READ action-reference-catalog.md
```

典型触发：

```text
侧踹 / 前蹬
侧踢 / 低抽
短拳或掌缘
掌根或拳面
```

Catalog 过滤：

```text
Prerequisites
→ Physical Level
→ Combat Role
→ Response Compatibility
→ Required State Transition
→ Initiative / Tempo / Risk
→ ONE concrete action
```

若 Catalog 无匹配，不强塞 Catalog；回现有 Fighting / Martial / Weapon / Pattern 知识，但 Runtime 仍必须自己选定一个动作。

### 8.2 Single Concrete Action Gate

Prompt Assembly 前扫描关键 Technique Head：

```text
A / B
A 或 B
A、B、C 任选
```

存在则：

> **Concrete Action Choice Leakage / RF-17 FAIL**

必须回 Concrete Selection 重选，不能交给视频模型。

允许真实复合动作：

```text
左前臂拨开直拳，同时右掌根推击胸口
```

因为这是明确并发，不是未决选择。

### 8.3 Regression Trace

Catalog 一旦触发，Regression / Debug 至少需要：

```text
Concrete Action Selection Gap
→ Catalog Read Evidence
→ Candidate Filter Basis
→ Selected Action ID / Canonical Name
→ Realized Concrete Action Phrase
```

Catalog 读取了但 Final Prompt 仍有 `/`、`或` 候选，不算 Wiring PASS。

---

## 9. 最新修复 Commits

```text
9db6010a05538e7b41af1a5582ac15ce04e9ae34
fix: route unresolved concrete actions through catalog

90d3fd53d1b2750b63343c12bc2815b7670f36a1
docs: enforce single concrete action selection gate
```

此前 Catalog Wiring commits：

```text
f9f25878a50ec16a0f90d46885e42736a949ad1e
10ba83e1cb009e5f21b6d07dbb2470a2bd18efbf
64a5c16445402f6a5849afe6ae4bd10ba04aaefe
c2109d343ac100c514838a34958bd4b1edceed47
9f7bb8ff73bf5a9f69e2d182dede85058136ec8e
```

---

## 10. 下一轮 Integrated Regression 重点

继续使用真实 Interactive 测试时，按顺序检查：

```text
1. Planning Completion Gate / Runtime Read Timing
2. Stage-2 Pattern Hit Evidence
3. 是否产生 Concrete Action Selection Gap
4. 是否真实 READ action-reference-catalog.md
5. 是否记录 Selected Action ID / Canonical Name
6. Selected Action 是否通过 Physical / Prerequisite / Response / State Transition 过滤
7. Final Prompt 是否不再出现同层 `/` / `或` 候选
8. Per-Character Signature / Advantage / Movement Causality 是否保持
9. Prompt 是否因新 Catalog 进一步膨胀
```

目标不是要求每次 Combat 都必须命中 Catalog。

正确 PASS 语义：

```text
有 Concrete Action Selection Gap
→ Catalog 正确命中并选定动作

没有 Concrete Action Selection Gap
→ 不读 Catalog 也可以 PASS
```

错误语义：

```text
Final Prompt 出现互斥动作候选
→ 却没有触发 Catalog / Concrete Selection
→ FAIL
```

---

## 11. 当前目标

> **继续下一轮 Integrated Regression。**

当前最重要的新增验证目标：

> **让 Runtime 自己决定“到底是哪一招”，而不是把 `侧踹还是前蹬、短拳还是掌缘` 留给视频模型。**
