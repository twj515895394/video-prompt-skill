# Video Prompt Skill — Action Combat Current Handoff

> 更新时间：2026-08-16 21:10（UTC+8）  
> 仓库：`twj515895394/video-prompt-skill`  
> 分支：`main`  
> 当前阶段：**继续 Action Combat Integrated Regression。RF-22 Completion Gate 已连续出现正向时序证据但尚未满足固定 G01 ×2 close criteria；Concrete Action Selection / RF-17 已做最小修复；Damage Onset 已从错误的“clean start”修正为 `Initial Injury Baseline + Event-caused Delta`；Round 1 已补齐“太极 vs 散打”高价值 Pairing。下一会话优先分析用户的新一轮真实测试反馈。**

---

## 0. 新会话接管顺序

优先读取：

1. `.handoff/current.md`
2. `SKILL.md` 的 `Action Combat Post-Planning Mandatory Path`
3. `references/tasks/action-combat-video/interactive-combat-policy.md`
4. `references/tasks/action-combat-video/regression-fix-runtime-policy.md`
5. `references/tasks/action-combat-video/choreography-playbook.md`
6. `references/libraries/combat-choreography-patterns/index.md`
7. 如命中 Abstract Movement / Technique / Transition Gap：`minimum-validation-set.md`
8. 如命中 Concrete Action Selection Gap：`action-reference-catalog.md`
9. 如需设计背景：`docs/combat-action-reference-knowledge-spec.md`

不要重新 Grill 已确认的 Action Catalog Schema、Damage Baseline 语义或太极 / 八极槽位差异。

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

已实施：

```text
Interactive Planning Completion Gate
→ 所有当前高价值 Interactive 决策 resolved
→ Completion Gate PASS
→ 才允许 Direct READ regression-fix-runtime-policy.md
```

原 RF-22 修复 Commit：

`f465e4b61f9cc9aed7de73183001969a206b13bd`

RF-22 原关闭条件仍然是：

> **完全相同的固定 G01，连续 2 次 PASS-NATIVE。**

近期多个非固定 G01 测试中，实际顺序都已表现为：

```text
Combat System
→ Expression / Archetype
→ conditional Rhythm
→ Advantage
→ Camera
→ Physical Presentation
→ Runtime Policy READ
```

因此 Completion Gate / Runtime Read Timing 当前是**强正向 supporting evidence**，但这些不同选择的测试不能替代固定 G01 ×2 close count。

不要因为当前在验证 Catalog / Injury / Tai Chi 就擅自修改 RF-22 Completion Gate。

---

## 2. Concrete Action Catalog — 已接入

正式 Leaf：

`references/libraries/combat-choreography-patterns/action-reference-catalog.md`

来源：用户提供的 6 张《AI漫剧打斗动作提示词大全》图片，实际为 **17 个可见动作模板（1–17）**：

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

此前误加的“后撤蓄力重击”已经删除，不得重新引入。

核心结构：

```text
Single Action Template
+ Combat Role
+ Response Compatibility
+ Sparse State Transition
+ Min / Default / Max Physical Level
+ Tempo / Risk / Commitment / Initiative
+ Prerequisites
+ Environment Impact
```

Combat Role 固定为：

```text
Entry / Pressure / Defense / Counter / Re-entry / Reversal / Signature / Finisher
```

Visual Medium 与 Physical Level 解耦；真人画面可以使用 P3，P3-only 动作不能被静默改成 P1/P2 而改变 Core Mechanic。

---

## 3. Concrete Action Selection / RF-17 最小修复

此前真实测试出现：

```text
侧踹 / 前蹬
侧踢 / 低抽
短拳或掌缘
掌根或拳面
```

这类同层互斥动作候选把 Runtime 应完成的选择留给视频模型，属于：

> **Concrete Action Choice Leakage / RF-17 FAIL**

用户已确认最小修复，不扩知识库、不重构 Runtime：

```text
Pattern Resolution
→ 当前需要的战斗功能已知
→ 具体动作 Head 仍存在多个同层合理候选
→ Concrete Action Selection Gap
→ READ action-reference-catalog.md
→ filter candidates
→ choose ONE concrete action
→ Single Concrete Action Gate
→ Final Prompt
```

Catalog 过滤顺序：

```text
Prerequisites
→ Physical Level legality
→ Combat Role
→ Response Compatibility
→ Required State Transition
→ Tempo / Risk / Initiative
```

如果 Catalog 没有合适动作：

> 不强塞 Catalog；回 Fighting / Martial / Weapon / Pattern knowledge，但 Runtime 自己仍必须选定一个具体动作。

允许真实复合动作，例如：

```text
左前臂拨开直拳，同时右掌根推击胸口
```

因为这是确定的并发，不是 `/` / `或` 候选。

相关 Commits：

```text
9db6010a05538e7b41af1a5582ac15ce04e9ae34
fix: route unresolved concrete actions through catalog

90d3fd53d1b2750b63343c12bc2815b7670f36a1
docs: enforce single concrete action selection gate
```

---

## 4. Catalog 命中判定 — 已纠正

不要再使用错误判断：

```text
没有 READ action-reference-catalog.md
→ 自动判 Catalog Routing FAIL
```

正确判定是：

```text
如果 Runtime 已经唯一解析出一个合法 Concrete Action
→ 不存在 Concrete Action Selection Gap
→ 不读 Catalog 完全可以 PASS
```

只有：

```text
同一 Active Technique 仍存在两个以上同层互斥 Concrete Mechanic
→ Concrete Action Selection Gap
→ Catalog MUST READ
```

Regression / Debug 中，一旦真实触发 Catalog，至少应有：

```text
Concrete Action Selection Gap
→ Catalog Read Evidence
→ Candidate Filter Basis
→ Selected Action ID / Canonical Name
→ Realized Concrete Action Phrase
```

如果 Final Prompt 已全部唯一具体化、没有 `/` / `或` 候选，而 Catalog 未读取：

> 定性为 **Catalog 未覆盖验证 / No Gap Triggered**，不是 FAIL。

---

## 5. Damage Onset / Injury Continuity — 最新正式语义

用户发现视频模型会把后段受创结果提前加载到人物首帧，例如：

- 后面才被打出的嘴角血迹，开场就存在；
- 后面才形成的淤青 / 红肿 / 擦伤，人物一开始就满脸带伤。

现有 Runtime 真源 `Impact Aftermath / Damage Continuity Gate` 已补 Damage Onset Timing，但第一版曾错误表达为“开场人物默认干净 / 首帧无伤”。用户明确纠正：**角色开场本来可能就带旧伤或参考图已有伤，不能强行洗干净。**

正式语义现已改成：

> **Initial Injury Baseline + Event-caused Delta**

核心链：

```text
Initial Injury Baseline
→ Triggering Contact / Force Event
→ Delta Injury Onset
→ Updated Injury State
→ Post-impact Continuity / Progressive Accumulation
```

### 5.1 Baseline

首帧必须继承已经成立的状态，包括：

- 用户明确设定的旧伤；
- 参考图 / 输入资产已有的血迹、淤青、擦伤；
- 前置剧情已经造成的伤势；
- 已经存在的衣损、污渍、环境破损等。

不得为了 Damage Timing 规则强行恢复成“干净完整”。

### 5.2 Delta Injury

只禁止：

> **后续事件才会产生的新伤势，在 Trigger 之前提前出现。**

例如：

```text
Baseline：右眉已有旧伤
→ 第 8 秒左嘴角被肘击
→ 从该肘击后新增左嘴角破皮 / 少量血迹
→ Ending：右眉旧伤 + 左嘴角新伤都保留
```

`Persistent / Progressive` 只表示**伤势产生后持续 / 累积**，绝不表示从视频开始就存在。

### 5.3 Failure

重点 Failure：

```text
Premature Injury / Damage Preload
= 后续 Combat 才产生的新伤在 Trigger 前出现

Baseline Injury Reset
= 输入里本来已有的伤势被 Runtime 为了“首帧干净”错误抹掉

Damage Continuity Reset
= 新伤产生后后续无因消失
```

不仅适用于 Human Injury，同一语义可以覆盖：

```text
Clothing Damage
Environment Damage
Dirt / Sweat / Blood / Scuff
Object Displacement
```

本质都是：

> **Baseline State + Event-caused Delta → Updated State**

相关 Commits：

```text
0e311ab35bd64a959ea0c6479c9e76701f878f39
fix: gate combat injury visibility on causal onset

606ecfce5312598fd3267dde3f15f161ad637a44
fix: preserve baseline injury state before combat deltas
```

下一轮必须特别检查 Final Prompt 是否还出现类似：

```text
首帧双方完好
初始状态脸部干净完整
```

这类把“不得预载新伤”错误扩大成“必须无旧伤”的表述。

---

## 6. 最新真实测试：太极修复前基线（2026-08-16）

用户上传完整真实 Interactive 对话记录，场景仍是：

```text
15 秒
现代办公室开阔区
22 岁中国女性，长发高马尾，正常职场装
55 岁中国男性领导，秃顶偏胖，正常职场装
双方属于不同杀手组织
不隔办公桌
```

本轮用户选择：

```text
Round 1:
女 = 咏春
男 = Wrestling / 抱摔控制

Expression:
A
女 = 冷静诱导 / 后发截击 / 被压后脱控再进
男 = 主动压迫 / 持续找抱摔入口 / 失控后再贴

Archetype:
女 = 甄子丹型
男 = 吴京型

Rhythm:
D. Impact Drop → Recovery → Rebuild

Advantage:
A. 男前中段压迫 → 重跌 → 女恢复反夺主动 → 女方收尾占优

Camera:
B. 电影冲击体验优先

Physical Presentation:
Modern Level 2
```

### 6.1 RF-22

实际顺序正确：

```text
Combat System
→ Expression / Archetype
→ Rhythm
→ Advantage
→ Camera
→ Physical Presentation
→ READ regression-fix-runtime-policy.md
→ Runtime / Stage-2 / Assembly
```

因此：

> **RF-22 Runtime Read Timing = PASS-NATIVE supporting evidence。**

但该选择不是固定 RF-22 close G01，因此不计入 ×2 close count。

### 6.2 RF-17 / Concrete Action

这轮 Final Prompt 已明显改善，没有再出现上一次的：

```text
侧踹 / 前蹬
短拳或掌缘
```

动作已唯一具体化，例如：

```text
前脚内侧横向扫击承重小腿外侧
右肘短促撞击下颌侧
掌根推击肩胛外侧
小腿从外侧勾带承重脚踝向内
```

因此：

> **RF-17 = PASS 倾向强。**

本轮没有 READ `action-reference-catalog.md`，但 Final 动作已经唯一 resolved，所以正确定性为：

> **Catalog 未覆盖验证 / No Concrete Action Selection Gap observed**

而不是 Catalog Routing FAIL。

### 6.3 Movement / Recovery Causality

表现良好：

```text
男方抱摔压迫
→ 女方撞玻璃跌落
→ 疼痛 / 呼吸中断产生 Recovery Burden
→ 男方继续压
→ 女方借其俯压路线旋出外侧
→ 男方重新扑抱
→ 女方截击 + 破支撑完成 Reversal
```

整体已经接近：

> **Action → Response → State Change → Next Action**

而不是轮流摆招。

### 6.4 Injury Onset

Prompt 已经出现正确的新伤触发：

```text
右肘命中下颌侧
→ 男方嘴角开始泛红并渗出少量血迹
→ 血迹从这次肘击后才出现并保持
```

这是正确的 Trigger → Delta Injury → Continuity。

但旧 Prompt 同时写了：

```text
首帧双方完好：无新增血迹、无破衣、环境完好
```

其中“无新增血迹”方向正确，但“首帧双方完好”可能被模型扩义为必须清除已有旧伤，因此这正是后续 `606ecf...` Baseline 修复解决的问题。

### 6.5 Per-Character Signature

整体仍可辨：

```text
女咏春 / 甄子丹型：中线截击、短桥、快速近身反制、换线
男 Wrestling / 吴京型：冲入、抓控、肩胸压迫、抱摔、再进入
```

但后半段女方出现：

```text
膝部顶肩胸下压
掌缘沿腕侧下压
控制其起身空间
```

尚不能直接判 FAIL，但后续需要继续观察：

> **女方会不会因为对手是 Grappler，而逐渐被同化成通用 Grappling / Control Character。**

不要第一反应禁止这些动作；只需检查整体 Signature 是否持续由咏春 / 已确认 Archetype 主导。

---

## 7. Round 1 太极候选缺失问题 — 已修复

太极修复前的真实 Round 1 候选为：

```text
1. Chinese Cinematic Kung-fu Hybrid vs 散打
2. 咏春 vs Wrestling / 抱摔控制
3. 八极 vs 散打
4. JKD vs MMA
5. 散打 vs MMA
6. Hybrid vs Wrestling / 抱摔
7. 泰拳 vs 八极
8. 自定义
```

问题：

- 八极出现两次；
- 太极虽然已经存在于 Policy 的通用候选池，但实际 Pairing 一次未出现；
- 这会让模型更容易把“传统中国功夫差异化”集中到八极硬爆发，而遗漏太极的 Counter / Reversal 路线。

用户确认：

> **保留八极，同时新增“太极 vs 散打”，两者不是替代关系。**

正式设计槽位：

```text
八极 vs 散打
→ 震脚 / 崩靠 / 贴身爆发 / 短劲 / 重接触
→ Hard Collision / Pressure / Heavy Contact

太极 vs 散打
→ 引化 / 借势 / 黏随 / 转轴 / 破重心 / 顺势反制
→ Defense / Counter / Reversal / State Redirection
```

太极不是：

```text
慢动作
养生
只做推手
软绵绵无攻击性
```

用于 Combat Prompt 时，应被实例化成可见的：

```text
对手线性压入
→ 让线 / 转轴 / 黏接
→ 借其动量带偏肩轴或重心
→ 迫使补步 / 换支撑
→ 顺势反制
```

`Action → Response → State Change → Next Action` 尤其适合太极的 Counter / Reversal 表达。

已修改：

`references/tasks/action-combat-video/interactive-combat-policy.md`

Commit：

`d69ad0a51983035cefd94a2533878a190a591c7f`

目标不是让所有 Round 1 都机械出现太极，而是：

> **当当前场景同时适合八极硬爆发与太极借力反制时，两种高价值设计空间都应有机会进入动态候选，不应互相吞掉。**

---

## 8. 近期关键 Commits

```text
9db6010a05538e7b41af1a5582ac15ce04e9ae34
fix: route unresolved concrete actions through catalog

90d3fd53d1b2750b63343c12bc2815b7670f36a1
docs: enforce single concrete action selection gate

0e311ab35bd64a959ea0c6479c9e76701f878f39
fix: gate combat injury visibility on causal onset

606ecfce5312598fd3267dde3f15f161ad637a44
fix: preserve baseline injury state before combat deltas

d69ad0a51983035cefd94a2533878a190a591c7f
feat/fix: expose taiji as distinct high-value combat pairing
```

更早的 Catalog Wiring commits：

```text
f9f25878a50ec16a0f90d46885e42736a949ad1e
10ba83e1cb009e5f21b6d07dbb2470a2bd18efbf
64a5c16445402f6a5849afe6ae4bd10ba04aaefe
c2109d343ac100c514838a34958bd4b1edceed47
9f7bb8ff73bf5a9f69e2d182dede85058136ec8e
```

---

## 9. 下一会话推荐测试

用户表示下一会话继续反馈。

如果继续使用同一个办公室场景，当前最高价值测试是：

> **Round 1 观察并选择“太极 vs 散打”。**

目的不是只测太极，而是一次同时覆盖：

```text
A. Round 1 Candidate Diversity
- 太极是否真实进入候选，而不是八极重复占槽

B. Tai Chi Realization
- 是否体现引化 / 借势 / 黏随 / 转轴 / 破重心 / Counter / Reversal
- 是否错误退化成慢推手 / 养生动作

C. RF-22
- Runtime Policy 是否仍在所有高价值 Planning resolved 后才 READ

D. RF-17 / Concrete Technique
- Final 是否继续保持单一具体动作
- 是否重新出现 `/` / `或` 候选

E. Catalog
- 只有真实出现 Concrete Action Selection Gap 时才要求 Catalog READ
- 没有 Gap 时不读 Catalog不算失败

F. Damage Baseline / Onset
- 首帧是否继承已有伤势状态
- 是否不再出现“首帧双方必须完好 / 干净”的错误 blanket rule
- 新伤是否只在 Trigger 后新增
- 新伤出现后是否保持 / 合理累积

G. Signature
- 太极角色是否持续以借势换轴 / Counter / Reversal 为主导
- 散打角色是否持续保持拳腿直线压迫 / 低扫 / 再进入
```

如果用户下一会话直接上传新测试对话，**先分析真实 Read Trace + Final Prompt，不要重新问设计问题。**

---

## 10. 当前判断摘要

```text
RF-22:
强正向 supporting evidence，固定 G01 ×2 尚未关闭

RF-17:
最新咏春 vs Wrestling 测试 = PASS 倾向强

Action Catalog:
已接入；只有 Concrete Action Selection Gap 时必须命中
最新测试无 Gap，因此属于未覆盖验证，不是 FAIL

Movement / Recovery Causality:
PASS 倾向强

Damage Onset:
Trigger → Delta Injury → Continuity 已落地

Damage Baseline:
已修正为 Initial Injury Baseline，不再要求 clean start

Tai Chi Candidate Diversity:
旧测试确认存在遗漏；已修复 Pairing / semantic slot

Per-Character Signature:
整体良好，但继续观察 Counter-character 被 Grappler 同化的问题

Granularity / Density:
仍是后续观察项，不在当前几次最小修复中扩大处理
```

---

## 11. 当前原则

1. 不因一个失败就扩知识库；先定位 Routing / Selection / Realization / Assembly / Adapter。
2. 不要求 Catalog 每次必读；它是按 Gap 读取的 Concrete Action Leaf。
3. 不把“后续伤不能提前出现”错误实现成“人物首帧必须无伤”。
4. 不把太极等同慢动作；Combat 中强调可见的借势、换轴、破重心与反制因果。
5. 八极与太极是不同设计槽位，不互相替代。
6. 不修改 RF-22 Completion Gate，除非新的真实测试再次证明时序 Failure。
7. 下一会话收到测试反馈后，优先给出 Evidence-based regression diagnosis，再决定是否最小修复。
