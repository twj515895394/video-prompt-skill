# Combat Action Reference Catalog — Static Validation

> Scope: `action-reference-catalog.md` knowledge quality only.  
> Runtime status: **NOT WIRED while RF-22 is open.**  
> 本文件不证明任何视频模型真实生成效果，也不计入 RF-22 PASS-NATIVE。

---

# 1. Validation Goals

验证以下问题：

1. 单动作是否真正可执行，而不是只有招式名；
2. Core Action Mechanic 是否与特效 / 风格解耦；
3. Physical Level Range 是否不会偷偷改变动作身份；
4. Combat Role 是否只使用已确认的 8 个核心枚举；
5. Response Compatibility 是否能改善一攻一守匹配；
6. State Transition 是否只记录真实发生的状态变化；
7. High Commitment 动作是否留下合理 Recovery / Counter Window；
8. Prerequisites 是否能阻止无武器、无空间、无前序状态的错误动作；
9. Environment Impact 是否服务动作因果，而非独立堆特效；
10. Catalog 是否与现有 Abstract Stage-2 Pattern / Combat Profile 保持职责分离。

---

# 2. Schema Validation

## V-S01｜Core Action Mechanic 可见

PASS 条件：删除动作标题与 Alias 后，正文仍能回答：

```text
角色从什么状态开始
→ 身体怎样运动
→ 通过什么接触 / 非接触机制作用于目标
→ 目标产生什么立即结果
→ 动作在哪里结束
```

Catalog 当前 18 条均满足最低要求。

结果：**PASS-STATIC**

## V-S02｜Visual Medium / Physical Level 解耦

检查：

- 没有把“漫剧”写成 P3 的必要条件；
- 没有把“真人写实”写成只能使用 P1；
- P3 只表示超现实物理表现，不表示媒介。

结果：**PASS-STATIC**

## V-S03｜Min / Default / Max 边界

重点检查：

```text
A15 非接触震劲击退
Min = P3
→ 不允许降级成普通推掌

A11 超现实滞空连击
Min = P3
→ 不允许在 P2 继续长时间悬浮

A18 下落震地重击
Min = P2
→ 必须保留前序下落与明确落点
```

结果：**PASS-STATIC**

## V-S04｜Combat Role 枚举

允许值固定：

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

Catalog 未把 Range Change / Route Change / Base Disruption / Recovery 重新塞回 Combat Role。

结果：**PASS-STATIC**

---

# 3. Response Compatibility Validation

## V-R01｜直线突进 → 侧移离线

Input State：

```text
A 发起正面直线突进
B 有侧向落脚空间
```

Candidate：A05 侧移离线

Expected：

```text
Best Against = 直线进入
Route: Frontal → Outside/Inside Angle
Initiative: Opponent Pressure → Open Counter Window
```

结果：**PASS-STATIC**

## V-R02｜重拳 → 双臂交叉防御

Input State：

```text
A 正面重击
B 无法及时脱线但支撑稳定
```

Candidate：A08 交叉臂硬架

Expected：

- 可以挡住；
- 不自动抢回 Initiative；
- B 可能后退 / 下沉；
- A 可继续 Pressure。

结果：**PASS-STATIC**

## V-R03｜前压承重脚暴露 → 横扫腿

Input State：

```text
A 重心前压
一侧支撑明显
B 位于 mid-close
```

Candidate：A10 低位横扫

Expected：

```text
Support: Stable → Disturbed
Balance: Stable → Forced Re-step / Off-balance
Initiative → Steal
```

结果：**PASS-STATIC**

---

# 4. Tempo / Commitment Validation

## V-T01｜Burst → Quick Reactive → Counter

Sequence Candidate：

```text
A01 爆发瞬身接敌
→ A05 侧移离线
→ A10 低位横扫
```

检查：

- A01 = Burst / Medium Commitment；
- A05 = Quick Reactive / Low Commitment；
- A10 = Support Disruption / Medium Commitment；
- 三者不是固定 Combo，只在当前 State 匹配时成立。

结果：**PASS-STATIC**

## V-T02｜High Commitment Miss → Counter Window

Sequence Candidate：

```text
A04 蓄势重拳落空
→ Recovery Exposure
→ 对手 Counter Candidate 权重提高
```

Catalog 明确：

```text
Initiative Effect on clear miss = Lose / Open Counter Window
```

结果：**PASS-STATIC**

## V-T03｜Airborne Action 必须落地

检查：A02 / A06 / A16 / A18。

要求：

- 起跳来源可读；
- 空中路线可读；
- 有落点 / 下落状态；
- Recovery 不被省略。

结果：**PASS-STATIC**

---

# 5. Prerequisite Validation

## V-P01｜无刀不得拔刀

Candidate：A13 Draw-and-Slash

没有真实刀剑 / 鞘状态：**REJECT CANDIDATE**

结果：**PASS-STATIC**

## V-P02｜无下落不得震地

Candidate：A18 Descending Ground Impact

当前人物站在地面且无腾空 / 坠落前序：**REJECT CANDIDATE**

结果：**PASS-STATIC**

## V-P03｜P2 不得使用 literal 气劲击退

Candidate：A15 Non-contact Force Push

Selected Physical Level = P2：**REJECT CANDIDATE**

不能自动改写成接触推掌。

结果：**PASS-STATIC**

---

# 6. Environment Impact Validation

## V-E01｜环境反馈必须有动作来源

例如 A04 重拳：

合法：

```text
拳命中
→ 对手后退撞墙
→ 墙面局部裂纹 / 家具位移
```

不合法：

```text
拳尚未命中
→ 周围墙体随机爆炸
```

除非题材 / P3 另有明确超自然机制。

结果：**PASS-STATIC**

## V-E02｜持久环境后果不得 Reset

如果椅子已经被撞翻、墙体已裂、物体已移动，下一 Phrase 必须继承这一新环境状态，除非有明确恢复原因。

结果：**PASS-CONTRACT**

---

# 7. Dedup / Single Source Validation

## V-D01｜与 `minimum-validation-set.md` 的职责边界

`minimum-validation-set.md`：

> Abstract Movement / Technique / Transition Pattern + Stage-2 Pattern Hit Evidence

`action-reference-catalog.md`：

> Concrete reusable single action + Response / State / Tempo / Commitment / Physical realization

允许存在语义映射，例如：

```text
T02 Low-line Base Disruption
→ A10 低位横扫
```

但不复制 `minimum-validation-set.md` 的完整 Pattern Schema / Runtime Gate。

结果：**PASS-STATIC**

## V-D02｜与 Combat Fighting / Martial Profiles 的职责边界

Profiles 决定：

- 某 Combat System / Technique Backbone 通常偏好什么距离、发力、攻防语言；

Catalog 决定：

- 某一个具体动作怎样成立。

Catalog 不把动作归属强绑定到 Boxing / Sanda / Wing Chun / Baji 等单一流派。

结果：**PASS-STATIC**

## V-D03｜与 Environment Patterns 的职责边界

Catalog 只写动作造成的轻量 Environment Impact；

复杂空间 Affordance / 环境战术仍由 `combat-environment-patterns/library.md` 负责。

结果：**PASS-STATIC**

---

# 8. Minimum Choreography Assembly Cases

这些 Case 只验证知识能否被组合，不定义固定 Runtime 流程。

## C01｜高速攻防反转

```text
A01 爆发瞬身接敌
→ B05 侧移离线
→ B10 低位横扫破坏支撑
→ A 被迫补步
```

验证目标：

- 一攻一守不是轮流表演；
- Response 与 State Transition 连续；
- Initiative 可以自然翻转。

结果：**PASS-STATIC**

## C02｜重击风险制造反击

```text
A04 蓄势重拳
→ B09 后仰让线
→ A 重拳落空产生 Recovery
→ B14 后撤蓄势重反击 / 其他 Context-compatible Counter
```

验证目标：High Commitment 的风险真实影响下一动作选择。

结果：**PASS-STATIC**

## C03｜P3 真人武侠式超现实动作

Visual Medium：真人写实影视  
Physical Level：P3

```text
A15 非接触震劲击退
→ 目标沿掌劲方向退开
→ 纸张 / 衣物 / 灰尘同方向响应
→ A01 P3 瞬身感重新接敌
```

验证目标：真人视觉媒介与 P3 超现实物理解耦。

结果：**PASS-STATIC**

## C04｜空中动作因果闭环

```text
A16 跃步突入
→ A02 凌空飞踢
→ 明确落地 / Recovery
```

或 P3：

```text
已有腾空来源
→ A11 超现实滞空连击
→ A18 下落震地重击
```

验证目标：任何 Airborne Action 都有进入、持续和退出状态。

结果：**PASS-STATIC**

---

# 9. RF-22 Freeze Validation

本次知识实施必须同时满足：

```text
SKILL.md unchanged
references/tasks/action-combat-video/index.md unchanged
references/tasks/action-combat-video/regression-fix-runtime-policy.md unchanged
references/libraries/combat-choreography-patterns/minimum-validation-set.md unchanged
Quick Mode unchanged
Camera Runtime unchanged
```

新文件当前只能由维护 / 审核显式读取，不能进入 G01 Runtime Read List。

结果：**PASS by implementation contract; verify with final diff review.**

---

# 10. Current Conclusion

当前静态结论：

- Knowledge Schema：PASS-STATIC
- 18 Action Entries：PASS-STATIC
- Physical Level boundaries：PASS-STATIC
- Response / State causality：PASS-STATIC
- Tempo / Commitment：PASS-STATIC
- Prerequisites：PASS-STATIC
- Environment Impact：PASS-STATIC
- Single-source boundary：PASS-STATIC
- Runtime integration：**NOT TESTED / INTENTIONALLY NOT WIRED**
- Generated video quality：**NOT TESTED**
- RF-22 close criteria：**UNAFFECTED / still requires fixed G01 ×2 PASS-NATIVE**
