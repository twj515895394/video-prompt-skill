# Diagnostics Index

诊断层只在用户反馈结果失败、多个维度同时失效、参考素材冲突或无法从单一控制页定位原因时读取。

正常生成流程默认不读取诊断页。

## identity-drift

人物脸部、发型、服装、年龄感或主体身份跨帧漂移。

## motion-discontinuity

动作跳变、姿态重置、速度突变、重心不连续或相邻阶段无法衔接。

## camera-chaos

运镜无目的、镜头漂浮、多个运动互相冲突、焦点丢失或画面炫技过载。

## spatial-teleportation

人物、道具、背景、出入口或镜头位置在空间中瞬移。

## anatomy-contact-failure

肢体畸形、手部错误、接触点不成立、双人互动穿模或受力关系错误。

## physics-and-weightlessness

人物、服装、头发、物体或环境缺乏重量、惯性、碰撞和真实反馈。

## lip-sync-and-dialogue-failure

口型、对白长度、呼吸、停顿、情绪和说话人不一致。

## audio-visual-mismatch

声音事件与视觉事件错位，BGM 抢叙事，环境声空间不匹配或音效无来源。

## prompt-overload-and-conflict

单段动作过多、风格互斥、镜头命令冲突、负向词过量或核心目标被稀释。

## reference-role-conflict

多张图片、多个视频或音频在同一维度提供相互冲突的参考，或素材职责未绑定。

## 诊断流程

```text
确认失败现象
→ 定位主要失效维度
→ 检查任务和素材职责
→ 检查时间轴、运动、镜头和连续性
→ 只修改最关键变量
→ 必要时切换模型适配表达
```

诊断页应输出根因、证据、优先修复项和重写建议，不重新复制完整资料库。
