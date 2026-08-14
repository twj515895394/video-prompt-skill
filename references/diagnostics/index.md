# Diagnostics Index

诊断层只在用户反馈生成失败、多个维度同时失效、参考素材冲突或无法从单一控制页定位原因时读取。正常生成流程不加载诊断层。

## 使用规则

- 每次只选择 `1` 份主诊断叶子；
- 先确认最明显、最能解释整体失败的主因；
- 次要问题通过相关 controls 修复，不同时加载全部诊断；
- 诊断输出应包含：失败现象、主因、证据、最小修复、重写方向；
- 不以追加大量负向词代替结构修复。

## 精确路由

### identity-drift

现象：脸部、发型、服装、年龄感或主体身份跨帧漂移。

读取：`identity-drift/diagnostic.md`

### motion-discontinuity

现象：动作跳变、姿态重置、速度突变、重心不连续或相邻阶段无法衔接。

读取：`motion-discontinuity/diagnostic.md`

### camera-chaos

现象：运镜无目的、镜头漂浮、多个运动冲突、焦点丢失或炫技过载。

读取：`camera-chaos/diagnostic.md`

### spatial-teleportation

现象：人物、道具、背景、出入口或镜头位置在空间中瞬移。

读取：`spatial-teleportation/diagnostic.md`

### anatomy-contact-failure

现象：肢体、手部、接触点、双人互动或受力关系错误。

读取：`anatomy-contact-failure/diagnostic.md`

### physics-and-weightlessness

现象：人物、服装、头发、物体、环境或镜头缺乏重量、惯性和反馈。

读取：`physics-and-weightlessness/diagnostic.md`

### lip-sync-and-dialogue-failure

现象：口型、对白长度、呼吸、停顿、情绪和说话人不一致。

读取：`lip-sync-and-dialogue-failure/diagnostic.md`

### audio-visual-mismatch

现象：声音节点与视觉事件错位，BGM、环境声、拟音或声音空间不匹配。

读取：`audio-visual-mismatch/diagnostic.md`

### prompt-overload-and-conflict

现象：动作、运镜、风格、光影和限制互相竞争，核心目标被稀释。

读取：`prompt-overload-and-conflict/diagnostic.md`

### reference-role-conflict

现象：多图、多视频或音频在同一维度冲突，或素材职责没有绑定。

读取：`reference-role-conflict/diagnostic.md`

### combat-state-continuity-failure

现象：复杂战斗中单个动作看似连续，但 Advantage、Condition、Target、Weapon State 或 Beat End / Start State 前后矛盾。

读取：`combat-state-continuity-failure/diagnostic.md`

只在现有 motion / spatial / anatomy / physics / camera / audio 诊断无法解释“Combat 状态链整体断裂”时使用。

## 诊断流程

```text
确认用户描述的失败现象
→ 选择一个主诊断叶子
→ 定位主因和次因
→ 检查对应 task、input 和 controls
→ 只修改最关键的结构变量
→ 必要时重新进行模型适配
→ 输出可直接使用的修订 Prompt
```

## 常见主因选择

- 角色像换人：优先 identity-drift；
- 动作断裂但身份稳定：优先 motion-discontinuity；
- 镜头乱导致主体不可读：优先 camera-chaos；
- 人和道具位置跳变：优先 spatial-teleportation；
- 接触穿模或手部错误：优先 anatomy-contact-failure；
- 动作漂浮无重量：优先 physics-and-weightlessness；
- 台词和嘴部错误：优先 lip-sync-and-dialogue-failure；
- 卡点或声音错位：优先 audio-visual-mismatch；
- Prompt 本身互相矛盾：优先 prompt-overload-and-conflict；
- 多素材混合错误：优先 reference-role-conflict；
- 战斗的 Advantage / Condition / Target / Weapon / Beat State 前后无法同时成立：优先 combat-state-continuity-failure。

## 输出边界

- 诊断页不重新复制完整资料库；
- 术语选项从 libraries 获取；
- 判断和协调规则从 controls 获取；
- 模型语法从 models 获取；
- 输出仍遵循当前 quick / interactive contract。
