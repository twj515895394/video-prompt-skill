# Action Combat Generated-Video Execution Regression Spec

> 状态：V1 / 2026-08-15
>
> 触发来源：固定 G01「15 秒办公室职业杀手近身对决」真实成片反馈。
>
> 重要澄清：本文件记录的成片问题来自 **Action–Camera / Stage-2 Runtime 本轮修改之前** 用户实际生成的 Final Prompt。该 Prompt 就是本轮最初贴出的“生成一段 15 秒、电影化写实真人风格的现代办公室徒手近身格斗片段……”版本。

---

## 1. 真实成片结论

用户明确反馈：该版 Final Prompt 生成的视频效果相比上一版 **差很多很多**：

- 动作明显不连贯；
- 镜头明显不灵活；
- 几乎全部是上肢动作；
- 整体动作电影感下降，而不是提升。

因此本轮不能只把问题描述为“Prompt 仍有优化空间”。

正式判定：

```text
Prompt-level textual specificity ↑
但
Generated-video continuity ↓
Camera mobility ↓
Whole-body choreography ↓
```

这是一次真实的 **Generated Video Quality Regression**。

Failure Signature：

```text
Prompt–Video Execution Divergence
Instruction Saturation / Micro-choreography Overconstraint
Upper-body Semantic Dominance
Camera Strategy Overconstraint
```

---

## 2. 为什么 Prompt 看起来更具体，成片反而更差

### 2.1 具体化 ≠ 可执行化

该 Prompt 在文字上包含大量细节：

- 前臂偏开；
- 肩线压缩；
- 掌根；
- 短肘；
- 抓前臂；
- 转髋；
- 墙边换轴；
- 支撑线；
- 多次 Contact / Position / Momentum 描述；
- Camera 中景 / 接触切近 / 回中景；
- 大量连续性 Negative。

这些信息在文本逻辑上都可以成立，但 15 秒视频模型并不等价于动作模拟器。

当同一短窗口需要同时执行：

```text
多个精细肢体动作
+ 对手即时响应
+ Contact 后果
+ Footwork / Axis / Position
+ Camera Change
+ 身份一致性
+ 物理限制
+ Negative Constraints
```

模型可能不是“执行得更具体”，而是发生选择性丢失：

- 只保留最反复、最显眼的上肢动作；
- 丢失 Footwork / Support / Route；
- 把连续链切成若干孤立动作；
- Camera 退回最安全的稳定中景。

因此必须区分：

> **Choreography Specificity** 与 **Model Execution Realizability**。

---

## 3. ACV-01｜新增 Model Execution Realizability Gate

Final Prompt 不能只问：

> “动作是否足够具体？”

还必须问：

> **“这些具体信息是否以模型容易执行的层级组织？”**

High-detail Combat Phrase 应只展开真正决定：

- 动作方向；
- 身体主驱动；
- 对手反应；
- 空间 / 支撑后果；
- 下一动作入口；

的关键事实。

不要求把每个前臂角度、肩线、抓握、衣料、脚底、重心、Camera、音效都同时塞进同一个动作窗口。

---

## 4. ACV-02｜Motor Driver First

对于要求 Whole-body / 中国武术电影化 / 身法角度争夺的 Fighting Direction，Action Phrase 应优先让模型理解：

> **身体整体怎样移动，为什么这个移动产生下一次攻防。**

优先结构：

```text
Whole-body / Support / Route Driver
→ Technique
→ Opponent Response
→ New Position / Balance
→ Continuation
```

而不是长期：

```text
Forearm / Wrist / Shoulder Technique
→ 再补一句侧步 / 转髋 / 降低重心
```

### Feet-fixed Test

内部检查：

> 如果把脚步、支撑、Route、Level、Axis 变化全部删掉，这段主要攻防是否仍几乎可以原地完成？

如果答案是 yes，且 Fighting Direction 明确需要 Whole-body / Movement-driven Combat，则判：

`Upper-body Semantic Dominance / Static Standing Combat`

必须重写动作主驱动，而不是再补一个腿法词。

---

## 5. ACV-03｜Upper-body Semantic Dominance

本次真实 Prompt 的高频动作骨架包括：

```text
掌击
→ 前臂偏开
→ 肩线封堵
→ 短肘 / 掌根
→ 抓前臂
→ 肩部顶入
→ 肩膀反压
→ 前臂改变肩线
→ 前臂控制结尾
```

即使期间出现：

- 侧切；
- 转髋；
- 降低重心；
- 扫支撑线；

模型仍可能把这些理解成“上肢攻防的辅助说明”。

因此不使用机械词频配额，但增加语义检查：

> **连续多个关键 Phrase 的主要因果是否仍由 Hand / Forearm / Wrist / Shoulder / Arm Control 驱动？**

若 yes，Movement 没有真正改变下一动作入口，则 FAIL。

---

## 6. ACV-04｜Concrete Compression，压描述，不压动作

出现 Instruction Saturation 时，压缩顺序：

```text
删除重复身体细节
→ 删除重复 State 解释
→ 合并同一动力链中的局部上肢动作
→ 删除低价值 Camera / Audio 描述
→ 删除重复 Negative
→ 保留 Whole-body Driver
→ 保留 Opponent Response
→ 保留关键 Contact / Balance / Position 后果
→ 保留下一动作入口
```

禁止为了降低复杂度直接变成：

```text
双方高速连续攻防
```

正确目标：

> **动作链仍然丰富，但每个 Phrase 只有一个清晰的运动主驱动和少量必要局部细节。**

---

## 7. ACV-05｜High / Medium / Low 必须真的产生模型注意力层级

过去 High / Medium / Low 主要定义“文字展开深度”。

本轮追加真实成片约束：

- High：只给 Major Reversal / Signature Moment 足够细的局部因果；
- Medium：优先写整身运动 + 关键 Technique + 后果，不展开所有接触部位；
- Low：只保留能维持 Motion Handoff 的动作桥梁；
- 如果所有段落都要求模型追踪多个独立肢体、多个 Contact 和多个状态，则即使文字长度不同，也仍属于 **Effective High Granularity Everywhere**。

Failure：

`Effective Granularity Flattening / Instruction Saturation`

---

## 8. ACV-06｜Camera Strategy 不得预先锁死为“稳定中景 + 接触特写”

本次 Prompt 明确写：

```text
稳定中景开始
→ 中景跟随为主
→ 真正接触瞬间短暂切近
→ 立刻回到中景
→ 结尾中近景推进
```

虽然文本上允许 Cut，但整体摄影策略实际上已经非常保守。

对于用户选择“中景跟随、关键接触短暂切近”，Runtime 应把它理解成 **观看偏好**，而不是固定 Shot Pattern。

允许：

- Movement / Route 改变时侧跟；
- Level Drop 时 Camera 随身体降位；
- Initiative Reversal 时改变 Relationship Angle；
- 支撑 / 低线信息真正决定动作时使用局部镜头；
- Fight-space 改变时重新组织机位。

禁止自动序列化成：

```text
Medium → Contact Close → Medium → Contact Close
```

该问题继续由 `action-camera-handoff-playbook.md` 的 Action-triggered Camera Change 解决。

---

## 9. ACV-07｜Generated Video Regression Baseline

从现在开始，G01 不能只验证：

- Static Read；
- Prompt-level Contract；

还必须保留上一轮真实成片作为比较基线。

新版本只有在真实生成视频至少不劣于已有较好版本时，才能宣称改善。

比较维度：

```text
A. Action Continuity
B. Whole-body / Lower-body Contribution
C. Fight-space Mobility
D. Camera Mobility / Coverage Flexibility
E. Initiative / Reaction Continuity
F. Fighting Direction Realization
G. Overall Action-film Readability
```

### Regression Rule

如果新 Prompt：

- 文本更具体；
- Static Gate 更多；

但真实成片在上述核心维度明显下降：

> **直接判 Generated Video Regression，不允许用 Prompt-level PASS 抵消。**

---

## 10. ACV-08｜Prompt–Video Execution Divergence 的诊断顺序

成片退化时按以下顺序排查：

```text
1. 是否 Stage-2 根本没 Hit
2. 是否 Upper-body Semantic Dominance
3. 是否 Effective High Granularity Everywhere
4. 是否 Instruction Saturation
5. 是否 Motion / Energy Carry-over 在最终 Prompt 中变成复杂解释而非清晰动作
6. 是否 Camera Strategy 被序列化得过于保守
7. 是否 Negative / Continuity 文本抢占模型注意力
8. 最后才判断 Knowledge Coverage 是否不足
```

避免：

> 成片差 → 继续增加更多 Pattern / 更多动作术语 / 更多镜头术语。

---

## 11. G01 下一轮必须验证

继续使用完全相同的 G01。

Prompt-level 除现有 Gate 外追加：

- [ ] `minimum-validation-set.md` 或等价 leaf knowledge 真实 Hit；
- [ ] 主要 Action Phrase 通过 Feet-fixed Test；
- [ ] 不再由前臂 / 肩线 / 抓腕语义长期主导；
- [ ] High / Medium / Low 形成真实执行层级，而不是所有段都微操；
- [ ] Action–Camera Handoff 不固化为 Medium / Close 循环；
- [ ] Negative / Meta 不抢动作主体；
- [ ] Prompt 可以清楚看出 Whole-body Driver。

Generated-video 必须检查：

- [ ] 相比本次退化版，动作连续性显著恢复；
- [ ] 相比本次退化版，全身 / 下肢 / 支撑变化明显增加；
- [ ] Camera 不再长期保守中景；
- [ ] 镜头变化与动作状态相互配合；
- [ ] 不出现因为 Prompt 过细而导致的动作碎片化。

---

## 12. 当前结论

本轮真实反馈证明：

> **更多 Concrete Detail 并不单调地提升视频质量。**

正确目标不是：

```text
Prompt 越具体越好
```

而是：

```text
明确的 Whole-body Motor Driver
+ 可执行的具体 Technique
+ 清晰的 Reaction / Consequence
+ 动力连续的 Transition
+ 动作触发的 Camera
+ 受控的信息密度
→ 更高 Generated-video Realizability
```

最终验收以真实成片为准，而不是以 Prompt 文本复杂度为准。
