# Video Prompt Skill — Action Combat Current Handoff

> 更新时间：2026-08-15 17:38（UTC+8）  
> 仓库：`twj515895394/video-prompt-skill`  
> 分支：`main`  
> 当前阶段：**角色身份 × 打斗方式 MVP 已通过真实 Interactive 验证；Advantage × Counterplay 批次已完成 Spec + Runtime 接入，下一步重新跑 G01。**

---

## 0. 当前状态一句话

不要继续扩具体拳种 / 流派知识。

当前真实视频暴露的新核心问题不是“男方没有拳击 / 摔跤标签”，而是：

```text
女方占优
→ Runtime 把男方写成长时间防守
→ 男方大量 Counterplay 被延迟成“准备 / 即将反扑”
→ 成片几乎看不到男方还击
```

用户已确认新的核心原则：

> **被压制不等于一直防守；劣势方可以还手很多次，但不断被化解 / 截断 / 反击，因此总体仍处于下风。**

---

## 1. 已完成上一批：Identity × Combat System

上一批已经完成并经过真实 Interactive 测试：

```text
Character / Narrative Identity
≠ Combat System

Round 1：Per-Character Combat System / System Refinement
Round 2：Per-Character Combat Expression

Physical Presentation Domain：条件暴露
Derived Choreography Direction：Runtime 自动派生
legacy Fighting Direction：只保留 compatibility execution slot
```

真实 G01 / 女剑客测试说明：

- “职业杀手 → 打法”混层已明显改善；
- Round 1 / Round 2 结构真实生效；
- Subject Motion / Stage-2 / Action-Camera / Prompt Assembly 的 Read Routing 已明显改善；
- 但 G01 真实生成视频中男方 Counterplay 不足。

上一批主 Spec：

`docs/combat-system-performance-identity-separation-spec.md`

---

## 2. 本批：Advantage × Counterplay

主 Spec：

`docs/combat-advantage-counterplay-spec.md`

运行期正文真源：

`references/tasks/action-combat-video/advantage-structure-contract.md`

### 2.1 核心数据语义

```text
Advantage Structure
├─ Outcome / Advantage
├─ Counterplay Shape
└─ Advantage Trajectory
```

核心原则：

```text
Advantage ≠ Attack Share
Outcome ≠ Advantage Trajectory
Disadvantaged ≠ Passive
```

---

## 3. 已确认 Counterplay Shape

当一方总体占优时：

### A. 持续压制型

劣势方主要防守 / 退让，真正反攻较少。

### B. 高频还手但持续被化解型

劣势方会多次真实 Attack / Counter / Re-entry，但不断被优势方截断、化解或反制。**这是通用推荐默认。**

### C. 多次拉锯后最终占优型

双方都阶段性拿到主动，最终由一方占优。

禁止从“女方占优”直接推导“男方攻击份额接近零”。

---

## 4. Advantage Structure 交互策略

它是**高价值条件节点**，不是固定第三轮 / 第四轮。

```text
用户已明确 Outcome + Counterplay + Trajectory
→ 直接继承

用户只说“谁赢 / 谁占优 / 势均力敌”
+ 存在多个会显著改变成片的合理过程
→ 条件询问 Advantage Structure

只有一个明显合理方向
→ 静默推导
```

一次问题解决同一个 Primary Node，不把 Outcome / Counterplay / Trajectory 拆成三个机械问题。

---

## 5. 势均力敌也不等于全程 50/50

允许：

- 持续胶着；
- 交替占优；
- 一方长期占优但无法终结。

因此：

> `Outcome = 未分胜负` 不代表 `Advantage Trajectory = 全程均势`。

---

## 6. Ending 已降级为条件节点

Ending / Final Visual Ending 不再固定询问。

默认：

```text
Final Advantage State
+ Last Active Contact / Motion / Position / Momentum
→ Runtime 自然收束
```

只有用户明确击倒 / 制服 / 死亡 / 撤离 / 互相架剑 / 特定定格，或存在多个高价值 Final Visual 分叉时，才单独询问。

特别禁止：

```text
男方本应有高 Counterplay
→ 但所有反击都写成“准备 / 即将”
→ 在真正反击发生前 Ending
```

---

## 7. Combat Expression × Advantage Structure

用户最后确认：**不要继续设计复杂自动协调矩阵。**

正常组合直接 Runtime 实现。

只有真实语义冲突、并且存在两个以上明显不同的高价值解释时才询问用户。

例如：

```text
男方：沉稳、防守反击
+ 中段短暂夺回主动
```

不冲突，应直接实现成：

```text
接住 / 避开一轮
→ 捕捉窗口
→ 真正 Counter
→ 迫使女方响应
→ 短暂拿回主动
```

不能翻译成“长期只防守”。

---

## 8. Counterplay Realization 强制合同

当 Counterplay = 中 / 高时，以下只算 Setup：

- 等待反击；
- 寻找机会；
- 准备抱摔；
- 即将反扑；
- 手臂开始发力；
- 在真正反击前结束。

必须出现真实：

- Attack；
- Counter；
- Re-counter；
- Re-entry；
- Grapple / Weapon Entry；

并至少造成一种真实状态后果：

- 迫使对方 Defense；
- 改变 Range / Route / Guard；
- 迫使对方退步 / 重新支撑；
- 形成短暂 Clinch / Grapple；
- 抢到短暂 Initiative。

攻击可以失败，但必须真实发生。

不使用“每人必须攻击 N 次”的配额。

---

## 9. 本批 Runtime 已修改

### 新增 Spec

`docs/combat-advantage-counterplay-spec.md`

Commit：`859e8321fa0b2cd296dd2b9dd027db61d9b97a29`

### 新增运行期合同

`references/tasks/action-combat-video/advantage-structure-contract.md`

Commit：`b4ec63c483010d37638ae85138122f18530501ca`

### Tasks Index

`references/tasks/index.md`

Combat 复合主 Task 现在包含：

```text
index
+ core
+ choreography
+ advantage-structure-contract
+ specialist
```

Commit：`88249a28a994db5b536ba2c502a53ce56896f4f2`

### Action Combat Router

`references/tasks/action-combat-video/index.md`

已加入：

- Advantage Contract 固定 Read；
- Planning Context 的 Advantage Structure；
- Advantage 条件询问；
- Ending 条件暴露；
- Counterplay Realization Gate；
- Counterplay Starvation / Deferred Counterplay Collapse 等 Failure；
- Final Preflight 的 Counterplay / Trajectory / Ending 检查。

Commit：`7880e7797082baa89ce4450b7647d3231e864830`

---

## 10. 本批故意没做的事

- 不扩散打 / 拳击 / 摔跤 / MMA 细节；
- 不新增固定攻击次数；
- 不建立 Expression × Advantage 组合矩阵；
- 不大重构 Modern / Wuxia Specialist；
- 不做 Quick Mode 全量上游迁移；
- 不因为每个 Failure Signature 新建 Runtime 子系统。

原则仍然是：

> **先测试真实 G01，再决定下一刀。**

---

## 11. 下一轮 G01 Regression

继续使用原始办公室请求。

### 重点验证 Interactive

如果用户只确定“女方占优 / 未分胜负”等粗结果，而 Counterplay 存在明显分叉，应出现 Advantage Structure 条件问题。

推荐测试方向：

```text
Outcome：女方总体占优但未完全制服
Counterplay：男方高频还手但持续被化解
Trajectory：
女方先抢主动
→ 男方中段通过拳击 / 拳摔真正 Counter 并短暂夺回
→ 女方通过散打切线与反制重新压住
→ 男方后续仍有真实还击
→ 女方最终保持总体优势
```

这只是 Regression 推荐，不写死 Runtime。

### 重点验证 Final Prompt

必须看见：

- 男方真实 Counter / Re-entry 不止停留在意图词；
- 男方攻击能迫使女方真实响应；
- 男方可以一直“打不赢”，但不能一直“不打”；
- 女方仍能通过自己的散打 System / Expression 持续保持总体优势；
- Ending 不再把男方主要反击推到 15 秒之外。

### 最终 Generated-video PASS

只有真实视频同时满足：

- 男方可见地多次还击；
- 女方总体仍占优；
- Whole-body / Persistent Signature / Continuity 没有回退；

才算本批真正 PASS。

---

## 12. 下一会话行动顺序

```text
重新跑 G01 Interactive
→ 检查 Runtime Read List 是否包含 advantage-structure-contract.md
→ 检查 Advantage Structure 是否按条件暴露
→ 检查是否没有固定 Ending 问题
→ 检查 Final Prompt Counterplay 是否真实发生
→ 生成真实视频
→ 对比旧失败：男方是否仍 Counterplay Starvation
```

如果 FAIL，优先修 Advantage / Counterplay Realization，不继续扩具体格斗流派细节。
