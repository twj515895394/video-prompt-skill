# Action Combat Video V2 Implementation Plan

> 状态：实施中
>
> 设计真源：`docs/action-combat-video-v2-spec.md`
>
> V1 基线：`docs/action-combat-video-spec.md` / `docs/action-combat-video-implementation-plan.md`
>
> 核心验收原则：**真实成片质量优先于静态规则覆盖；静态正确只是必要条件。**

## 1. 实施目标

V2 不推翻 V1 的 Combat State / Continuity Engine，而是在同一个 `action-combat-video` Task 内正式落地 **Combat Choreography Engine / 动作编排引擎**。

最终需要同时解决：

- 战斗时间真正被有效攻防占据，而不是 Timeline 写满但实际不打；
- 单位时间内存在足够丰富、连续、有因果的攻防交换；
- 不同角色真正表现出不同 Combat Character Identity；
- 环境参与战术和空间变化，而不是装饰性随机破坏；
- Strike / Grapple / Throw / Weapon / Environment 等接触具备可信 Combat Contact Solidity；
- 重要短片具有少量真正可记忆的 Signature Moment；
- Camera / Audio 服务动作可读性、节奏和实感，不替代动作本身；
- Final Prompt 由正向、可见、可执行的动作语言主导；
- Quick / Interactive 共用同一 Combat Planning Graph；
- 模型差异通过 Model Combat Capability Contract 反馈执行复杂度；
- 回归从静态规则检查升级为静态 + Generated Video Quality Benchmark 双层体系。

实施总原则：

> **Core 负责“打得对、接得上”；Choreography 负责“打得够、丰富、好看、有实感”；专项 Playbook 负责“这种战斗具体怎么表现”。**
>
> **Clarity Through Structure, Not Action Reduction.**
>
> **State Machine Internalized, Choreography Externalized.**

---

## 2. 实施策略与提交原则

### 2.1 分批实施

按依赖顺序推进：

```text
Phase 0 设计冻结与基线
→ Phase 1 Task 运行骨架
→ Phase 2 Choreography Engine 与专项 Playbook
→ Phase 3 Combat Libraries
→ Phase 4 Final Prompt / Output Contracts
→ Phase 5 Model Capability Contract
→ Phase 6 Diagnostics
→ Phase 7 Static Regression + Golden Benchmark Framework
→ Phase 8 Generated Video Quality Benchmark
→ Phase 9 文档与最终收口
```

禁止跨层同时大改后再一次性验证。每一阶段必须先达到自己的 Gate，再进入下一阶段。

### 2.2 每阶段 Gate

每个 Phase 至少满足：

1. 修改范围与当前 Phase 一致，不提前吸收后续职责；
2. 不复制既有通用 Control / Output Template 正文；
3. 不产生新的职业 → 固定打法映射；
4. 不重新引入固定 Battle Beat 动作数量模板；
5. 索引与实际文件路径一致；
6. Quick / Interactive 不分裂成两套生成逻辑；
7. 静态检查未发现职责冲突或旧原则残留；
8. 形成独立 commit，便于定位回归与回滚。

### 2.3 V1 兼容边界

V2 保留并继续使用 V1 已验证的：

- Combat Intent；
- Combat Spatial Map；
- Range / Advantage / Condition；
- Turning Event；
- Target Handoff；
- Beat State Contract；
- Spatial / Physical / Continuity Validation；
- 现有 single-shot / multi-shot 输出合同；
- 现有跨任务 Controls。

V2 明确替换 / 废止：

- Battle Beat 全局 `1 主目标 + 2–4 交互节点 + 结束状态` 动作数量锚点；
- “宁少而清晰”作为动作戏上位原则；
- 职业 / 角色身份直接映射固定 Fighting Profile；
- 大量状态术语直接 Dump 进 Final Prompt；
- 静态规则通过即视为 Combat 能力通过的验收方式。

---

## 3. Phase 0｜设计冻结、基线与实施计划

### 目标

把 Grill Me 设计阶段正式冻结为实施基线，避免开发期间继续漂移一级架构。

### 修改 / 新增

- `docs/action-combat-video-v2-spec.md`
- `docs/action-combat-video-v2-implementation-plan.md`（本文件）

### 工作项

- [x] 完成 V2-01 ～ V2-34 架构决策；
- [x] 确认 Combat Choreography Engine 属于 `action-combat-video` Task；
- [x] 确认新增 `choreography-playbook.md`；
- [x] 确认不新增 Combat Choreography Control；
- [x] 确认双层回归与 Golden Combat Scenario Contract；
- [x] 建立本分批实施计划。

### Gate

- Spec 中一级设计问题无未决项；
- 后续仅允许实现级微调，不重新打开已确认的一级设计树，除非实际回归证明设计假设错误。

---

## 4. Phase 1｜Task 运行骨架重构

### 目标

先把运行时职责边界拆干净，让 V2 有正确的“骨架”，但不急于一次塞入所有 Library / Model / Diagnostic 细节。

### 主要文件

```text
references/tasks/action-combat-video/index.md
references/tasks/action-combat-video/core-playbook.md
references/tasks/action-combat-video/choreography-playbook.md   # 新增
SKILL.md
```

### 工作项

#### 4.1 Task Router

- [ ] 路由改为：`core-playbook + choreography-playbook + 1 个专项 Playbook`；
- [ ] 写入 Two-stage On-demand Loading；
- [ ] 建立轻量 `Combat Planning Context`；
- [ ] Quick / Interactive 明确共用同一 Planning Graph；
- [ ] Quick = Full Planning + Silent Resolution；
- [ ] Interactive 只暴露高影响、低置信度分叉。

#### 4.2 `core-playbook.md`

保留 / 强化：

- Combat Intent；
- Spatial Map；
- Range / Advantage / Condition；
- Turning Event；
- Action–Reaction 基础因果合同；
- 1vN / Target Handoff；
- Battle Beat / Beat State Contract；
- Position / Environment / Weapon State 继承；
- Continuity / Physics Validation；
- Task 调用 Controls / Libraries / 专项 Playbook 的总协调关系。

必须移除：

- `2–4 个连续攻防交互节点` 全局锚点；
- “动作过载优先减少有效攻防”的隐含倾向；
- 与新 `choreography-playbook.md` 重复的导演逻辑。

#### 4.3 新增 `choreography-playbook.md`

第一版就建立完整运行骨架，至少包含：

- Choreography Profile；
- Active Combat Coverage + 四类时间预算；
- Action Exchange Rhythm；
- Action Phrase；
- Exchange Depth；
- Combat Character Identity；
- Tactical Interaction；
- Environment Action Affordance；
- Signature Moment；
- Combat Contact Solidity；
- Action Execution Budget；
- Action Sufficiency Check；
- Camera Readability Budget；
- Combat Audio Choreography；
- Clarity Through Structure；
- State Machine Internalized / Choreography Externalized；
- Model Capability 输入接口占位；
- Library Detail Slot 路由原则。

#### 4.4 `SKILL.md`

- [ ] Combat 任务入口增加 `choreography-playbook.md`；
- [ ] Quick / Interactive 统一规划原则接入入口说明；
- [ ] 继续保持 `0–3 Controls / 少量 Libraries / 可选 Model Adapter`；
- [ ] 不向用户暴露内部 Planning Context。

### Phase 1 Static Gate

- 搜索并确认 Combat Runtime 中不再存在 `2–4` 全局动作锚点；
- `index.md`、`SKILL.md` 与实际文件路径一致；
- `core-playbook` 与 `choreography-playbook` 不互相复制大段正文；
- 现代 / 武侠专项仍只加载一个；
- Quick Mode 不因输入简短而跳过 Choreography Planning。

---

## 5. Phase 2｜Choreography Engine 完整化与专项实现层

### 目标

让通用 Choreography 机制与 Modern / Wuxia 的具体动作语言真正解耦。

### 主要文件

```text
references/tasks/action-combat-video/choreography-playbook.md
references/tasks/action-combat-video/modern-combat-playbook.md
references/tasks/action-combat-video/cinematic-wuxia-playbook.md
```

### 工作项

- [ ] 补齐 Combat Core-agnostic Contact Modality；
- [ ] 把 Strike / Grapple / Throw / Blade / Weapon Clash / Environment Impact 的表现差异留给专项层；
- [ ] Modern Combat 增加高手连续攻防、混合节奏、角色打法差异与 Contact Solidity 实例化；
- [ ] 明确“assassin / 军人 / 警察”等身份不能 1:1 映射 Tactical Close Combat；
- [ ] Wuxia 保留电影化物理尺度，不被现代格斗“真实重拳逻辑”污染；
- [ ] Weapon / Martial Profile 作为专项知识来源，而非 Core 规则；
- [ ] Camera / Audio 的专项表现只能覆盖表现倾向，不能改变 Core 质量合同。

### Phase 2 Gate

使用至少 4 个静态场景做 Prompt Blueprint 检查：

1. 现代高手 1v1；
2. 力量型 vs 灵活型；
3. 电影武侠空手；
4. 刀 / 剑短兵器对决。

要求同一 Core 机制在不同专项下表现明显不同，但状态连续性合同一致。

---

## 6. Phase 3｜Combat Libraries 与按需加载知识层

### 目标

把“稳定专业知识”与“动态导演决策”分离，同时保持运行时上下文小而有针对性。

### 新增

```text
references/libraries/combat-choreography-profiles/library.md
references/libraries/signature-moment-patterns/index.md
references/libraries/signature-moment-patterns/patterns/*.md
references/libraries/signature-moment-patterns/source-cases/*.md
```

### 修改

```text
references/libraries/combat-fighting-profiles/library.md
references/libraries/combat-martial-profiles/library.md
references/libraries/combat-weapon-profiles/library.md
references/libraries/combat-environment-patterns/library.md
references/libraries/index.md
```

### 工作项

#### 6.1 `combat-choreography-profiles`

第一版保持约 5–7 个稳定基础 Profile，例如：

- 写实战术型；
- 凌厉电影动作型；
- 高手连续攻防型；
- 重型硬派型；
- 环境技巧型。

每条描述 Coverage 倾向、Rhythm、Exchange Depth、重量反馈、Range、环境参与、Phrase 节奏、Camera Complexity、冲突条件。

#### 6.2 Signature Moment Pattern

- `index.md` 只保留轻量路由字段；
- Runtime 默认命中 Top 1–3 Pattern；
- `patterns/` 保存生产知识；
- `source-cases/` 保存研究 / 证据；
- 正常生成禁止加载 `source-cases/`；
- Pattern 不能要求复刻影视完整动作。

#### 6.3 现有 Combat Libraries 修订

- Fighting Profile：明确技术 Profile ≠ Character Identity ≠ 职业；
- Martial / Weapon：补 Contact Modality 与 Range / Initiative 相关知识；
- Environment：从“物体互动清单”升级为 Affordance / 战术改变；
- Libraries 不承担 Coverage / Rhythm / Execution Budget 等导演流程。

### Phase 3 Gate

- 任一典型 Combat 运行默认只展开约 2 个主要 Library Detail Slot；
- Knife / Sword 等专业任务优先 Weapon Knowledge，而非 Signature Pattern；
- 不存在角色画像 / 职业画像 Library；
- Source Case 不进入正常运行上下文。

---

## 7. Phase 4｜Final Prompt、Prompt Assembly 与 Output Contract

### 目标

确保内部复杂状态最终被压缩成视频模型真正需要的动作画面语言。

### 主要文件

```text
references/controls/prompt-assembly/control.md
assets/templates/mode-quick-output-contract.md
assets/templates/mode-interactive-output-contract.md
assets/templates/model-adapted-output-template.md
# single-shot / multi-shot 仅在确有必要时做最小修改
```

### 工作项

- [ ] 加入 Action-first Semantic Priority；
- [ ] 明确 `State Machine Internalized, Choreography Externalized`；
- [ ] Combat Final Prompt 的主体语义用于 Action Phrase / Reaction / Contact / Spatial Change；
- [ ] 约束只保留真正高风险且正向表达不足以解决的少数项；
- [ ] 禁止通用“避免错误”Negative Boilerplate；
- [ ] 删除无根据的“no visible weapons”等任意限制；
- [ ] Quick / Interactive 最终质量相同，仅中间决策暴露不同；
- [ ] Model Adapter 可改变序列化方式，但不能改变导演意图。

### Phase 4 Gate

对同一 Combat Blueprint 输出 Final Prompt，检查：

- 动作语言是主体；
- 没有大量 Range / Advantage / Condition 标签 Dump；
- Negative Constraints 数量受控且有明确风险来源；
- Prompt 没有因连续性说明挤掉有效攻防描述。

---

## 8. Phase 5｜Model Combat Capability Contract

### 目标

把“根据模型可执行性调整”从抽象判断变成统一 Adapter 接口。

### 主要文件

```text
references/models/index.md
references/models/generic.md
references/models/seedance-2.md
references/models/ltx-2-3.md
```

### 第一版能力维度

- Motion Complexity Capacity；
- Multi-character Stability；
- Contact / Interaction Fidelity；
- Spatial Continuity；
- Camera Complexity Capacity；
- Temporal / Prompt Following。

使用：`High / Medium / Low + capability notes + known risks`。

### 工作项

- [ ] Generic 定义合同格式与保守默认；
- [ ] Seedance 2 / LTX-2.3 只填写有资料或 Benchmark 支撑的能力；
- [ ] 不使用伪精确评分；
- [ ] 明确模型能力只能影响实现路径；
- [ ] 降载顺序优先 Camera / 同窗口复杂度 / Phrase 拆分，再考虑次要动作；
- [ ] 不允许模型弱就把 High Coverage 改成低动作量。

### Phase 5 Gate

同一 High Coverage 目标在不同 Adapter 下允许得到不同执行策略，但 Combat Intent / Coverage / 观看目标必须保持不变。

---

## 9. Phase 6｜Combat Diagnostics

### 目标

把“打得不对”与“打得不够好”分开诊断。

### 新增建议

```text
references/diagnostics/combat-choreography-underfill/diagnostic.md
references/diagnostics/combat-contact-solidity-failure/diagnostic.md
```

### 继续复用

- `combat-state-continuity-failure`；
- `camera-chaos`；
- `prompt-overload-and-conflict`；
- `physics-and-weightlessness`；
- `anatomy-contact-failure`；
- `audio-visual-mismatch`；
- `spatial-teleportation` / `motion-discontinuity`。

### 新 Diagnostic 职责

#### Combat Choreography Underfill

识别：

- High / Medium Coverage 未兑现；
- 长时间站立、观察、摆 Pose、抓腕僵持；
- 高速 / Mixed Rhythm 但实际 Exchange Depth 很低；
- 高手对决只有 2–3 次有效攻防；
- Active Exchange Budget 大量未使用。

#### Combat Contact Solidity Failure

识别：

- Contact 无 Force / Pressure Transfer；
- Contact 后 Reaction 太弱或不存在；
- Reaction 不产生持续 Consequence；
- Grapple / Throw / Weapon Clash / Environment Impact 使用错误模态反馈；
- 用 Camera Shake / 大音效代替真实接触。

### Phase 6 Gate

同一个失败只能优先命中最具体 Diagnostic；避免 Underfill、Physics、State Continuity 三个页面同时重复同一正文。

---

## 10. Phase 7｜Static Regression + Golden Combat Benchmark Framework

### 目标

先建立可重复的测试基线，再进入真实视频生成。

### 新建 / 更新

```text
docs/action-combat-video-v2-regression.md
# 如需要，可建立 tests / benchmark 数据目录，但不复制 Spec 正文
```

### 静态回归

至少验证：

- V2 路由是否加载 Choreography；
- 旧 `2–4` 锚点是否彻底移除；
- Quick / Interactive 是否共用 Planning Graph；
- 两阶段 Library Loading 是否成立；
- Character Identity 是否动态推导；
- Contact Solidity 是否覆盖多种 Contact Modality；
- Prompt 是否 Action-first；
- Model Adapter 是否只调整执行路径；
- Diagnostics 路由是否无职责重叠。

### Golden Combat Scenarios

第一版保持约 6–10 个稳定场景，优先包含：

1. 15 秒办公室高手近身对决；
2. 力量型 vs 灵活型；
3. 狭窄走廊 / 受限空间；
4. 硬派拳脚高 Contact Solidity；
5. 短兵器刀战；
6. 长兵器距离切换；
7. 摔控 / Takedown；
8. 1vN Target Handoff。

每个场景采用：

```text
Fixed Input
+ Quality Contract
+ Failure Contract
+ Optional Test Anchor
```

禁止保存固定标准动作答案。

### Phase 7 Gate

所有 Golden Scenario 在“不实际生成视频”的静态 Prompt / Blueprint 层已能检查目标是否被正确规划，并形成统一结果记录格式。

---

## 11. Phase 8｜Generated Video Quality Benchmark

### 目标

用真实生成视频验证 V2 是否真正优于 V1，而不是只证明 Prompt 更复杂。

### 每次记录

- Golden Scenario ID；
- Skill / Prompt 版本；
- Model / Model Version；
- 生成参数；
- Seed（模型支持时）；
- Final Prompt；
- 输出视频标识 / 文件；
- 人工或多模态评分；
- Failure Signature；
- Prompt Intent → Generated Result Gap。

### 核心成片指标

- Active Combat Coverage Realization；
- Exchange / Choreography Richness；
- Character Distinction；
- Tactical Interaction Realization；
- Combat Contact Solidity；
- Environment Integration；
- Signature Moment；
- Camera Readability；
- Spatial / Physical Continuity；
- Rhythm Variation。

### V1 / V2 对比

在模型与生成参数可控时，尽量对同一 Golden Input 做 V1 / V2 对照，关注：

- 真正交战时间是否明显增加；
- 有效交换是否明显增加；
- 打击 / 接触是否更实；
- Camera 是否更看得清；
- 是否仍存在长对峙 / 抓腕僵持 / 提前 Ending Pose；
- 是否出现新的过载或执行丢失问题。

### Gate

至少核心 Golden Scenarios 证明 V2 在主要失败项上优于 V1，且没有以明显连续性 / 可读性退化为代价。

> 若真实成片不提升，应优先回溯 Prompt 表达、Execution Budget、Model Capability Contract 与 Choreography 规则，而不是继续增加更多抽象字段。

---

## 12. Phase 9｜文档、索引与最终收口

### 目标

让仓库运行期内容、设计文档和回归记录一致。

### 工作项

- [ ] 更新 `docs/action-combat-video-v2-spec.md` 状态为实施完成 / 验证状态；
- [ ] 更新本实施计划 Phase 状态；
- [ ] 完成 `docs/action-combat-video-v2-regression.md`；
- [ ] 更新 `references/tasks/index.md`、`references/libraries/index.md`、`references/diagnostics/index.md`、`references/models/index.md`；
- [ ] 检查 `references/index.md` 与 `SKILL.md`；
- [ ] 搜索废弃规则残留；
- [ ] 记录最终文件清单和已知限制。

### 最终验收

必须同时满足：

1. 架构职责清楚；
2. 单次运行 Reference 加载量受控；
3. Final Prompt 动作语言占主导；
4. V2 静态回归通过；
5. Golden Benchmark Framework 可重复；
6. 至少核心场景完成真实生成质量评估；
7. 没有把测试案例、Profile、Pattern 重新固化成动作模板。

---

## 13. 预计新增文件

```text
references/tasks/action-combat-video/choreography-playbook.md
references/libraries/combat-choreography-profiles/library.md
references/libraries/signature-moment-patterns/index.md
references/libraries/signature-moment-patterns/patterns/*.md
references/libraries/signature-moment-patterns/source-cases/*.md
references/diagnostics/combat-choreography-underfill/diagnostic.md
references/diagnostics/combat-contact-solidity-failure/diagnostic.md
docs/action-combat-video-v2-implementation-plan.md
docs/action-combat-video-v2-regression.md
```

是否增加额外 Pattern / Source Case 文件由 Phase 3 的第一批 Seed 数据规模决定，不为了数量预先创建空文件。

## 14. 预计重点修改文件

```text
SKILL.md
references/tasks/action-combat-video/index.md
references/tasks/action-combat-video/core-playbook.md
references/tasks/action-combat-video/modern-combat-playbook.md
references/tasks/action-combat-video/cinematic-wuxia-playbook.md
references/tasks/index.md
references/libraries/index.md
references/libraries/combat-fighting-profiles/library.md
references/libraries/combat-martial-profiles/library.md
references/libraries/combat-weapon-profiles/library.md
references/libraries/combat-environment-patterns/library.md
references/controls/prompt-assembly/control.md
assets/templates/mode-quick-output-contract.md
assets/templates/mode-interactive-output-contract.md
assets/templates/model-adapted-output-template.md
references/models/index.md
references/models/generic.md
references/models/seedance-2.md
references/models/ltx-2-3.md
references/diagnostics/index.md
references/index.md
```

---

## 15. 当前实施状态

| Phase | 状态 | 说明 |
|---|---|---|
| Phase 0 | ✅ 完成 | V2 设计冻结、实施计划建立 |
| Phase 1 | 🚧 进行中 | Task 运行骨架重构 |
| Phase 2 | ⏳ 待开始 | Choreography 与专项实现层 |
| Phase 3 | ⏳ 待开始 | Combat Libraries |
| Phase 4 | ⏳ 待开始 | Final Prompt / Output |
| Phase 5 | ⏳ 待开始 | Model Capability Contract |
| Phase 6 | ⏳ 待开始 | Diagnostics |
| Phase 7 | ⏳ 待开始 | Static Regression + Golden Framework |
| Phase 8 | ⏳ 待开始 | Generated Video Quality Benchmark |
| Phase 9 | ⏳ 待开始 | 最终收口 |

开发从 **Phase 1** 开始，按 Gate 逐阶段推进。
