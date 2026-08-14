# Combat Choreography Underfill Diagnostic

## 1. 何时使用

当 Combat Prompt / 成片**状态和连续性大体成立，但真正有效交战明显不足**时使用本页。

典型现象：

- 15 秒动作视频只有约 2–3 秒真正交战；
- High / Medium Active Combat Coverage 在计划或成片中没有兑现；
- 高手 / Mixed / 高速交换型设定，实际只有两三次孤立攻防；
- 大量时间被站立观察、重新起势、走位等待、抓腕僵持或 Ending Pose 占用；
- Battle Beat 写满，但 Active Exchange Budget 大量空置；
- 有很多动作词，却缺少 Defense → Counter → Re-counter → Continuation 的有效因果；
- Camera / 氛围 / 状态说明很丰富，但真正 Action Phrase 太少。

如果主问题是人物瞬移、Advantage / Condition / Target 状态矛盾，优先 `combat-state-continuity-failure`。如果动作数量够但接触发软，优先 `combat-contact-solidity-failure`。

---

## 2. 核心判断

Underfill 不是“动作词数量少”，而是：

> **Coverage、Rhythm、Exchange Depth、Active Exchange Budget 与用户观看目标没有被实际兑现。**

检查：

```text
用户 Combat Intent / 观看目标
→ 目标 Coverage
→ Active Exchange Budget
→ 实际 Action Phrase 数量与持续时间
→ 每个 Phrase 的有效 Exchange Depth
→ Downtime 是否有价值
→ Ending 是否过早停止战斗
```

---

## 3. 常见根因

### 3.1 把 Timeline Coverage 当 Combat Coverage

每个时间段都有文字，但内容是对峙、表情、镜头、走位、控制或收势，真正攻防只占很少。

### 3.2 旧式动作预算通缩

把“清晰”理解成一个 Beat 只能发生很少交互，或隐含采用“宁少而清晰”。

### 3.3 Battle Beat 被误当成单个小动作

每个 Beat 都重新观察 / 起势 / 接触，导致连续战斗被频繁 reset。

### 3.4 Tactical Close Combat / Grapple 过度占时

快速抓控本来只应服务某个战术目的，却变成长时间静态抓腕 / 抱持。

### 3.5 Camera 抢占动作预算

为了复杂运镜而主动把主体动作削减到很少。

### 3.6 Final Prompt Meta 语言过多

状态、连续性、物理、禁止项、风格描述占据大部分语义，Action Phrase 被压缩。

### 3.7 Ending 过早

最后数秒已经进入摆 Pose / 对视 / 定格，却仍被算作“动作段”。

---

## 4. 检查步骤

### Step 1｜确认 Coverage 目标

根据用户要求和 Choreography Profile 判断 Low / Medium / High。

不要因为模型未知就自动选择更低 Coverage。

### Step 2｜标记真正 Active Combat

只有直接推动下一次攻防的内容算 Active Combat，例如：

- Attack / Defense / Counter；
- 失衡后立即恢复并继续；
- 躲闪后形成新线路；
- 有主动争夺的 Grapple / Control；
- 换距后立即进入新攻击窗口；
- Environment Action 直接改变下一次攻防。

纯站立、无进展控制、重复观察、装饰性镜头和提前 Ending 不算。

### Step 3｜检查 Phrase

确认是否存在多个真实 Action Phrase，且前一个动作制造下一个动作机会。

不要只数动词。

### Step 4｜检查 Exchange Depth

高手 / 高速 / Mixed 场景若大多数 Phrase 都只停在：

```text
Attack → Block
```

则仍然可能 Underfill。

### Step 5｜找无价值 Downtime

定位：

- reset pose；
- 无战术价值的绕场；
- 重复对视；
- 长时间静态抓控；
- 过早收尾；
- 镜头独立表演。

---

## 5. 修复顺序

> **修复 Underfill 的目标是增加有效攻防，不是堆动作动词。**

优先：

1. 删除 / 压缩无价值 Downtime；
2. 把孤立 Attack–Block 扩展成有因果的 Counter / Re-counter / Continuation；
3. 在同一 Battle Beat 内增加无缝 Action Phrase；
4. 让 Contact / 失衡 / Environment Result 直接制造下一次攻击窗口；
5. 把长静态 Control 改成压力变化、挣脱尝试、位置争夺或快速过渡；
6. 降低无必要 Camera Complexity，释放动作可读性 / 执行预算；
7. Final Prompt 删除 Meta / 重复 Negative，把语义预算还给动作；
8. 缩短过早 Ending Pose。

禁止优先通过“加入更多独立招式名”修复。

---

## 6. 与 Action Execution Budget 的关系

Underfill 修复不能造成同一短窗口过载。

双向约束：

```text
Action Sufficiency Check
↔ Action Execution Budget
↔ Clarity Through Structure
```

动作不足时优先增加**更多连续 Phrase**；单个 Phrase 过载时拆开，但 Phrase 之间不需要停战。

> **高信息密度，但低混乱度。**

---

## 7. 重写方向示例

### 失败结构

```text
0–3s 对视争执
3–5s A 出拳，B 挡住
5–8s 双方抓住手腕僵持
8–10s B 推开 A
10–15s 两人对峙并摆出戒备姿态
```

问题不是“时间轴没写满”，而是 Active Combat 严重不足。

### 修复结构

```text
短促冲突直接进入第一条 Action Phrase：A 压近攻击，B 偏转并立即 Counter，A 在 B 反击尚未回收前改角度截击；接触让 B 的重心被迫侧移，B 借桌边稳住并从侧面重新切入。第二条 Phrase 紧接着由 B 主动压迫，A 用短防守化解后进入身体控制，B 不停顿地转髋破开控制，两人围绕桌角换位，A 的追击线路被桌边限制，B 借这个窗口完成一次环境辅助反击。最后一条 Phrase 在优势尚未完全确定时继续高速 Counter / Re-counter，并在最后约一秒收束为互相控制的僵持结局。
```

这里增加的是连续因果，而不是机械招式数量。

---

## 8. 与其他 Diagnostics 的边界

- Advantage / Condition / Target / Weapon / Beat State 矛盾：`combat-state-continuity-failure`；
- 接触点 / 肢体结构穿模：`anatomy-contact-failure`；
- 动作有数量但整体漂浮无重量：`physics-and-weightlessness`；
- Contact 缺乏模态正确的 Transfer / Reaction / Consequence：`combat-contact-solidity-failure`；
- Camera 本身失控：`camera-chaos`；
- Prompt 多维要求互相矛盾：`prompt-overload-and-conflict`。

本页只处理：**战斗设计在有效交战时间和因果交换丰富度上明显不足。**

---

## 9. 完成标准

修订后应满足：

- Coverage 与用户观看目标大体一致；
- Active Exchange 占据应有主体时间；
- Action Phrase 之间可以无缝衔接；
- Rhythm / Exchange Depth 与高手 / 重击 / Mixed 等目标匹配；
- Downtime 有明确价值，不再大量空耗；
- Ending 不过早停止战斗；
- Final Prompt 的动作语言明显多于 Meta 状态说明；
- 没有为了增加动作而破坏 State / Continuity / Camera Readability。
