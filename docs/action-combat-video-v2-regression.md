# Action Combat Video V2 Regression & Quality Benchmark

> 状态：✅ Phase 7 Static / Structural Regression 通过；Generated Video Quality Benchmark 框架已建立；真实成片 Phase 8 待执行
>
> 设计依据：`docs/action-combat-video-v2-spec.md`
>
> 实施计划：`docs/action-combat-video-v2-implementation-plan.md`
>
> V1 对照：`docs/action-combat-video-regression.md`

## 1. 验证目标

V2 回归不再把“规则写进 Prompt / 文档”当作最终成功。

正式采用两层：

```text
Level 1｜Static / Structural Regression
检查架构、路由、规则和 Prompt 规划是否正确

        ↓

Level 2｜Generated Video Quality Regression
检查真实生成视频是否真正打得够久、够丰富、够实、看得够清楚
```

核心原则：

> **最终生成视频动作质量是第一验收目标；静态规则正确只是必要条件，不是充分条件。**

---

## 2. V2 主要失败假设

本轮必须重点证明 V2 是否解决 V1 真实测试暴露的问题：

- Timeline 写满，但真正 Combat Coverage 很低；
- 15 秒视频只有约 2–3 秒真实交战；
- 只有两三次有效攻防；
- 高手身份没有转成高水平 Counter / Re-counter；
- 职业身份导致双方同质化；
- Environment 只是装饰；
- 旧复杂度预算导致动作通缩；
- Contact 发软、命中没有持续后果；
- Camera / Audio 代替动作本身制造“冲击”；
- Prompt 被状态规则、连续性术语和 Negative Constraints 淹没。

---

## 3. 静态结构回归

### 3.1 Task / Runtime

| 检查项 | 预期 | 当前结果 |
|---|---|---|
| Combat Router 存在 | `action-combat-video/index.md` | ✅ PASS |
| Core / Choreography 文件职责拆分 | State vs Choreography | ✅ PASS |
| Modern / Wuxia 只做专项实例化 | 不复制 Core / Choreography | ✅ PASS |
| SKILL Combat 路由 | `index + core + choreography + 1 specialist` | ✅ PASS |
| Quick / Interactive 共用 Planning Graph | 模式只差 Decision Exposure | ✅ PASS |
| Two-stage Loading | Planning Context → 少量 Detail | ✅ PASS |

证据摘要：

- Task 目录已真实存在 `core-playbook.md`、`choreography-playbook.md`、`modern-combat-playbook.md`、`cinematic-wuxia-playbook.md`；
- `tasks/index.md`、`references/index.md`、`SKILL.md` 均已同步新运行链；
- Combat Choreography 没有被拆成独立全局 Control。

### 3.2 Choreography

| 检查项 | 预期 | 当前结果 |
|---|---|---|
| Active Combat Coverage | Low / Medium / High | ✅ PASS |
| Action Phrase | Pair → Phrase → Beat → Sequence | ✅ PASS |
| Exchange Depth | 因果深度，不是动词数量 | ✅ PASS |
| Character Identity | 动态推导 | ✅ PASS |
| Tactical Interaction | 可选内部因果层 | ✅ PASS |
| Environment Affordance | 改变战术 / 空间 | ✅ PASS |
| Contact Solidity | 多 Contact Modality | ✅ PASS |
| Signature Moment | Sequence 级少量记忆点 | ✅ PASS |
| Action Execution Budget | 控同窗口复杂度，不控 Beat 总动作数 | ✅ PASS |
| Action Sufficiency Check | 防 Combat Underfill | ✅ PASS |
| Camera Readability Budget | Camera 服务 Choreography | ✅ PASS |
| Combat Audio Choreography | 声音证明动作，不替动作表演 | ✅ PASS |

### 3.3 废弃规则检查

运行期 V2 已确认：

- ✅ 不再把 `1 个主攻防目标 + 2–4 个连续攻防交互节点 + 1 个结束状态` 作为 Battle Beat 默认动作数量；
- ✅ 不再使用 `宁少而清晰` 作为动作戏上位原则；
- ✅ 明确 `职业 ≠ Character Identity ≠ Fighting Profile`；
- ✅ Quick 不是简化 Combat，而是 Full Planning + Silent Resolution；
- ✅ Combat Final Prompt 不默认输出 State Table；
- ✅ Negative Constraint 使用 Positive-first、风险驱动策略；
- ✅ 模型能力未知时使用 `Unverified`，不会因此自动减少动作。

说明：V1 历史文档可以保留旧设计记录，但现行运行期真源以 V2 Task / Controls / Libraries / Models / Diagnostics 为准。

### 3.4 Knowledge / Loading

| 检查项 | 当前结果 |
|---|---|
| `combat-choreography-profiles` 存在 | ✅ PASS |
| `signature-moment-patterns/index.md` 存在 | ✅ PASS |
| Pattern 按机制而非影视标题组织 | ✅ PASS |
| Runtime Pattern / Source Case 职责分离 | ✅ PASS |
| Fighting / Martial / Weapon / Environment 只负责专业知识 | ✅ PASS |
| 不存在 Combat Character Identity / occupation portrait Library | ✅ PASS |
| 默认约 2 个主要 Library Detail Slot | ✅ PASS |
| `source-cases/` 不作为默认运行时 Reference | ✅ PASS |

当前 Seed Pattern 暂不强行绑定具体影视 Source Case；这是刻意避免未经核实的案例事实进入生产知识。后续只有在可靠来源核实后才补研究档案。

### 3.5 Final Prompt

检查原则：

> **State Machine Internalized, Choreography Externalized.**

当前实现：

- ✅ Action Phrase / Reaction / Contact / Consequence 设为最高语义优先级；
- ✅ Position / Range / Environment 优先转译为可见动作变化；
- ✅ Camera / Audio 明确作为支持层；
- ✅ State Table 不作为默认输出；
- ✅ Negative 只针对真实高风险；
- ✅ Prompt 压缩时先删 Meta / 重复 Constraint，再考虑次要有效动作；
- ✅ 明确禁止无依据的 `no visible weapons` 等任意限制。

### 3.6 Model Adapter

统一 Contract 已实现：

- Motion Complexity Capacity；
- Multi-character Stability；
- Contact / Interaction Fidelity；
- Spatial Continuity；
- Camera Complexity Capacity；
- Temporal / Prompt Following。

当前 Generic / Seedance 2.0 / LTX-2.3 的 Combat 专项等级在缺少真实 Benchmark 时均使用 `Unverified`，未伪造 High / Medium / Low。

模型能力只影响执行路径，不得改变 Combat Intent / Coverage / 观看目标。

### 3.7 Diagnostics

Combat 三类主诊断已接入：

```text
打得不对 / 接不上
→ combat-state-continuity-failure

打得太少 / 不够丰富
→ combat-choreography-underfill

打到了但打不实
→ combat-contact-solidity-failure
```

人体穿模、普遍失重、Camera Chaos 等继续使用通用 Diagnostic。

目录与 `diagnostics/index.md`、`references/index.md`、`SKILL.md` 已同步。

---

## 4. Golden Combat Scenario Contract

每个 Golden Scenario 固定：

```text
Fixed Input
+ Quality Contract
+ Failure Contract
+ Optional Test Anchor
```

### 关键规则

- **不保存固定标准动作序列**；
- 动作设计可以创新；
- Quality Contract 锁“必须达到什么”；
- Failure Contract 锁“不能退化成什么”；
- Optional Test Anchor 只锁当前场景专门测试的抽象能力；
- Pattern / Profile 不是标准答案。

> **Benchmark 锁质量，不锁创意。**

---

## 5. Golden Scenario G01｜15 秒办公室高手近身对决

### Fixed Input

- 时长：约 15 秒；
- 场景：下班后的普通办公室；
- 人物：一名女性、一名男性，普通办公室穿着；
- 隐藏身份：来自敌对组织的专业杀手；
- 冲突：围绕一份文件发生争执并迅速升级；
- 风格：现实基础上的电影化近身格斗；
- Camera：medium / medium-wide 跟随为主，反转附近允许一次功能性近侧切镜；
- Ending：互相控制、胜负未分的僵持。

### Quality Contract

- High Active Combat Coverage 明显兑现；
- Active Exchange 占整段主体；
- 多个连续 Action Phrase；
- 双方 Character Identity 可区分；
- 至少存在明显 Counter / Re-counter 或同等级高手博弈；
- 重要 Contact 有 Solidity；
- 办公环境至少一次真正改变线路 / Range / Advantage / Position；
- 有一个主要 Signature Moment；
- Camera 能持续看清双方身体关系；
- Ending Pose 只占短收束，不提前数秒停止战斗。

### Failure Contract

- 长时间站着对峙；
- 只有两三次攻防；
- 大量抓腕僵持；
- 两人打法完全一样；
- 命中后无受力 / 状态后果；
- 随机砸办公室道具；
- Camera Shake / 快切掩盖动作；
- 最后数秒提前摆 Pose。

### Optional Test Anchor

Environment Affordance：环境至少一次真实改变攻击线路 / Range / Advantage，而不是装饰破坏。

---

## 6. Golden Scenario G02｜力量型 vs 灵活反制型

### Fixed Input

- 1v1；
- 一方体型更大、力量更强、持续压迫；
- 另一方更轻、更灵活、偏 Counter / Angle Change；
- 无超能力；
- 中等空间室内或训练场。

### Quality Contract

- Character Identity 差异通过动作可见；
- 力量型角色不是只会慢重拳；
- 灵活型角色不是无重量瞬移；
- 至少一次 momentum / angle / range 机制使力量关系发生视觉 Payoff；
- Contact Solidity 与体型差一致，但不过度飞退。

### Failure Contract

- 两人使用相同节奏和动作；
- 小体型角色靠无原因力量硬扛；
- 大体型角色动作笨重到没有有效交换；
- “力量差”只靠 Camera / 声音表现。

### Optional Test Anchor

`momentum-redirection` 或同类抽象机制至少一次真正改变 Position / Balance / Advantage。

---

## 7. Golden Scenario G03｜狭窄走廊压迫与反制

### Fixed Input

- 1v1 或可控 1v2；
- 狭窄走廊 / 门框；
- 横向移动受限；
- 以空间压迫与反制为核心。

### Quality Contract

- 走廊真实限制移动 / 攻击线；
- 空间不是背景贴图；
- Position / Range 连续；
- 至少一次空间边界导致的 Turning Event；
- Camera 轴线清楚。

### Failure Contract

- 人物在窄走廊无原因大幅横跳；
- 走廊宽度不断变化；
- 环境只作为撞墙效果；
- 反转没有空间因果。

### Optional Test Anchor

`constrained-space-reversal` 抽象机制。

---

## 8. Golden Scenario G04｜硬派拳脚 Contact Solidity

### Fixed Input

- 1v1；
- 无武器；
- 重型硬派电影动作；
- 中近距离；
- 重点测试打击实感。

### Quality Contract

- Light / Solid / Heavy 接触有层级；
- 关键 Contact 看得到 Commitment；
- Contact 后 Guard / torso / balance / footwork / breath 至少有合适反馈；
- 后续动作继承 Consequence；
- Heavy Contact 稀缺、有 Payoff 价值。

### Failure Contract

- 每拳都 Heavy；
- 每拳都飞退；
- 只有表情反应；
- Camera Shake / Boom 替代身体反馈；
- 命中后立即 reset。

### Optional Test Anchor

至少一个关键 Contact 完整体现 `Contact → Reaction → Persistent Consequence`。

---

## 9. Golden Scenario G05｜短兵器刀战

### Fixed Input

- 1v1；
- 双方使用短刀 / 刀剑类短兵器；
- 现实或电影化但非超能力；
- 重点测试 Blade / Parry / Range / Contact。

### Quality Contract

- 威胁线路清楚；
- Dodge / Deflection / Parry 改变下一攻击窗口；
- Weapon Clash 改变 line / initiative；
- Weapon State 连续；
- Blade Contact 不使用统一钝器重击反馈。

### Failure Contract

- 兵器穿模 / 消失 / 换手；
- 兵器交击只发火花无线路变化；
- 所有接触都大幅震飞；
- 双方不断回到固定起手式。

### Optional Test Anchor

至少一次 parry / deflection 直接制造下一拍 initiative shift。

---

## 10. Golden Scenario G06｜长兵器 vs 短兵器

### Fixed Input

- 长枪 / 棍类 vs 剑 / 刀等短兵器；
- 1v1；
- 空间足以表现长兵器 Range；
- 可现代电影化或 Wuxia。

### Quality Contract

- 长兵器优势先通过 Range / threat line 建立；
- 短兵器不能无过程瞬间贴身；
- 贴身后长兵器动作语言真实改变；
- 重新拉开后长度优势可重建；
- Weapon State / Range 连续。

### Failure Contract

- 长短兵器实际距离完全一样；
- 武器长度变化；
- 贴身 / 脱离没有 Transition；
- 长兵器在极近距离仍像短刀一样使用。

### Optional Test Anchor

`weapon-distance-transition` 抽象机制。

---

## 11. Golden Scenario G07｜Grapple / Takedown / Control

### Fixed Input

- 1v1；
- 站立打击可进入 clinch / grapple；
- 至少一次 takedown / throw / control；
- 现实物理尺度。

### Quality Contract

- Strike → Grapple 有进入窗口；
- Grapple 有持续连接、Pressure Direction / Leverage；
- Takedown 前先破坏 Balance；
- 落地改变 Position / Range / Advantage；
- Escape / reversal 有代价。

### Failure Contract

- 远距瞬间抱摔；
- 静态抱住不动；
- 人物像动画直接倒地；
- 地面位置和身体朝向跳变；
- 摔完立即站回原位置。

### Optional Test Anchor

至少一次 `Balance Break → Takedown → Position Consequence`。

---

## 12. Golden Scenario G08｜1vN Target Handoff

### Fixed Input

- 1v3；
- 中等复杂空间；
- 主角需要持续移动；
- 重点测试 Target Handoff / Multi-character Readability。

### Quality Contract

- 当前 Primary Target 清楚；
- 其他对手有明确 Secondary State；
- Target Handoff 有动作 / 空间 / 威胁触发；
- Camera 不丢失主目标与下一威胁；
- 环境可帮助制造单线接触；
- 多人战仍保持足够 Active Combat。

### Failure Contract

- 三人同时无序出拳；
- 主角瞬间转向新目标；
- 被击退的人下一帧立即出现在另一侧；
- Camera 乱转隐藏空间错误；
- 为稳定多人把动作压缩成极少交换。

### Optional Test Anchor

至少两次清楚 Target Handoff，并保持 Position / Range 可解释。

---

## 13. Generated Video Quality Metrics

每个成片按统一维度评价，不要求所有场景同权重。

### M01｜Active Combat Coverage Realization

计划 Coverage 与实际成片真正交战时间是否匹配。

### M02｜Exchange / Choreography Richness

是否存在足够有效 Action Phrase、Counter / Continuation，而不是动作动词数量。

### M03｜Character Distinction

双方 Character Identity 是否能从 Movement / Attack / Defense / Rhythm 看出来。

### M04｜Tactical Interaction Realization

要求高手博弈的场景，Feint / Read / Counter-to-Counter 等是否真正可见。

### M05｜Combat Contact Solidity

Contact 的 Commitment / Transfer / Reaction / Consequence 是否可信且符合模态。

### M06｜Environment Integration

环境是否真正改变线路、Position、Range、Advantage、Target 或 Payoff。

### M07｜Signature Moment

是否存在少量真正可记忆、由前后因果支撑的动作时刻。

### M08｜Camera Readability

是否能看懂双方身体关系、Contact 与空间变化。

### M09｜Spatial / Physical Continuity

Position、Range、Advantage、Condition、Weapon / Environment State 是否连续。

### M10｜Rhythm Variation

是否符合目标 Rhythm，并避免整段同速 / 同强度。

---

## 14. Prompt Intent → Generated Result Gap

每个 Golden Scenario 必须显式记录“计划了什么”和“成片实际发生什么”的差距。

示例：

```text
Planned Active Combat Coverage: High / target ~80%
Observed Active Combat Coverage: ~30%
Gap: -50 percentage points
Failure Signature: long setup + prolonged wrist control + early ending pose
```

Prompt 写了 `High Coverage` 但成片没有兑现，必须判为生成质量失败，而不是因为 Prompt 字段存在就 PASS。

其他 Gap 可记录：

- Planned Exchange Depth vs Observed Effective Exchange；
- Planned Signature Moment vs Observed Payoff；
- Planned Character Distinction vs Observed Similarity；
- Planned Contact Solidity vs Observed Soft Contact；
- Planned Environment Affordance vs Observed Decorative Interaction。

---

## 15. 成片记录格式

```text
Benchmark Run ID:
Date:
Golden Scenario ID:
Skill / Commit:
Prompt Version:
Model:
Model Version:
Generation Parameters:
Seed (if supported):
Input Assets:
Final Prompt:
Output Video / Artifact:

Planned Quality Contract:
Observed Result:
Metric Scores / Notes:
Prompt Intent → Generated Result Gap:
Failure Signature:
Pass / Partial / Fail:
Next Adjustment:
```

禁止在 Model / Version / Parameters 不同的情况下直接把质量变化全部归因给 Skill。

---

## 16. V1 vs V2 对比原则

当平台支持尽量固定模型版本 / 参数 / Seed 时，对同一 Golden Input 比较 V1 与 V2。

重点不比较“Prompt 谁更长”，而比较：

- Active Combat Coverage；
- Effective Exchanges；
- Contact Solidity；
- Character Distinction；
- Environment Integration；
- Signature Moment；
- Camera Readability；
- Continuity；
- 失败模式是否迁移成新的过载问题。

如果 V2 动作更丰富但 Camera / Continuity 明显恶化，不能简单判 V2 胜出。

---

## 17. Phase 8 验收门槛

V2 最终不能只以静态回归完成作为“实施完成”。

至少核心 Golden Scenarios 应完成真实生成，并证明：

- 原始办公室高手案例的 Combat Coverage / Exchange Richness 明显改善；
- Contact Solidity 不再主要依赖 Shake / Audio；
- Character Identity 能产生可见打法差异；
- Environment 至少在专门测试场景中真正参与战术；
- Camera Readability 没有因动作增加而显著退化；
- 没有重新出现固定模板化动作。

如果真实成片不提升，优先回溯：

1. Final Prompt Externalization；
2. Action Execution Budget；
3. Model Combat Capability Contract；
4. Choreography Profile / Phrase 组织；
5. Coverage / Sufficiency；

而不是继续增加更多抽象字段。

---

## 18. Phase 7 Static Regression Result

### 18.1 结果

> **PASS — V2 运行期架构、动作导演规则、知识层、输出层、模型合同和诊断路由已完成静态接线。**

### 18.2 本轮发现并修复的问题

静态 Gate 首次检查发现两个接线遗漏：

1. `references/tasks/index.md` 仍是 V1 式 `core + specialist` 描述，没有登记 `choreography-playbook.md`；
2. `references/index.md` / `SKILL.md` 尚未完整登记新 Choreography Library、Signature Pattern 与两个新 Diagnostic。

以上均已在 Phase 7 内修复后重新检查。

### 18.3 确定性目录检查

- Combat Task：存在 Core / Choreography / Modern / Wuxia；
- Combat Libraries：存在 `combat-choreography-profiles` 与 `signature-moment-patterns`；
- Diagnostics：存在 `combat-state-continuity-failure`、`combat-choreography-underfill`、`combat-contact-solidity-failure`；
- Controls：没有新增 `combat-choreography` 全局 Control；
- Model Layer：Generic / Seedance 2.0 / LTX-2.3 均接入统一 Combat Capability Contract。

### 18.4 正文检查

- Core 明确 `Battle Beat 不是固定动作数量容器`；
- Choreography 明确 `Active Combat Coverage`、`Action Phrase`、`Action Sufficiency`、`Contact Solidity`、`Clarity Through Structure`；
- Character Identity 明确动态推导，职业不能自动等于 Tactical Close Combat；
- Prompt Assembly 明确 Action-first、Positive-first；
- Models 无证据时明确 `Unverified`；
- Quick / Interactive 使用同一 Planning Graph。

### 18.5 尚未验证的内容

Static PASS **不能证明真实成片质量 PASS**。

尚未完成：

- 8 个 Golden Scenario 的实际视频生成；
- V1 / V2 同模型 / 同参数对照；
- Active Combat Coverage 实测；
- Contact Solidity 成片评分；
- Model Combat Capability High / Medium / Low 实测校准。

这些属于 Phase 8。

---

## 19. 当前状态

- Golden Scenario Contract：✅ 已建立；
- 8 个首批 Golden Scenario：✅ 已定义；
- Generated Video Metric：✅ 已定义；
- Result Record Schema：✅ 已定义；
- V1 / V2 对比方法：✅ 已定义；
- Static Regression：✅ PASS；
- Actual Generated Video Runs：⏳ **尚未执行，不得伪造 PASS。**
