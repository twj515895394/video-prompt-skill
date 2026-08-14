# Tasks Index

任务层负责判断当前要完成什么，以及最终输出应采用什么执行流程。每次只读取一份主任务 Playbook。

## 文生视频

读取：`text-to-video/playbook.md`

适用：没有视觉参考，需要用文字建立场景、主体、动作、镜头和时间轴。

## 图生视频

读取：`image-to-video/playbook.md`

适用：以一张或多张图片作为首帧、尾帧、角色、场景、关键帧或分镜参考，并生成运动。

## 多模态参考视频

读取：`multimodal-reference-video/playbook.md`

适用：图片、视频、音频中的至少两种共同决定人物、场景、动作、运镜、特效、节奏或声音。

## 视频参考复刻 / 视频转视频

读取：`video-reference-and-video-to-video/playbook.md`

适用：复用现有视频的动作、表演、运镜、节奏、特效或整体动态结构，或以视频为主要输入重新生成。

## 视频局部编辑

读取：`video-editing/playbook.md`

适用：保留原视频主体结构，只修改角色、物体、服装、动作、背景、文字、声音或局部剧情。

核心约束是：必须保留、必须修改、允许变化、禁止变化。

## 视频延长

读取：`video-extension/playbook.md`

适用：向前或向后延长已有视频。

延长不是独立续写新故事，必须从原视频的动作、镜头、光影、声音和空间状态自然接续。

## 音频驱动与音乐卡点

读取：`audio-driven-and-beat-sync/playbook.md`

适用：对白、旁白、口型、音色、BGM、节拍、拟音或音效主导视频时间结构。

## 故事板 / 多镜头 / 多片段到视频

读取：`storyboard-and-multi-shot-video/playbook.md`

适用：根据剧本、分镜、故事板或多个片段规划完整镜头顺序，并管理镜间承接与跨段一致性。

## 动作格斗 / 电影武侠

读取：`action-combat-video/index.md`

适用：战斗视频的成败主要依赖攻防因果、距离变化、受力反馈、1vN 目标切换、兵器状态、战斗空间与动作 / 镜头 / 声音同步时。

先读取 `action-combat-video/core-playbook.md`，再只选择一个专项分支：

- 现代格斗：`action-combat-video/modern-combat-playbook.md`；
- 电影武侠：`action-combat-video/cinematic-wuxia-playbook.md`。

这是一条因执行流程显著不同而存在的专项任务，不代表所有“动作题材”都进入本任务。简单挥拳、跑跳、体育动作继续使用原主任务 + `action-motion`。

## 判断边界

- 题材不同通常不等于任务不同。写实短剧、漫剧、广告、悬疑、纪录等优先进入同一任务，再加载不同 style 或 library。
- Action Combat 是例外：只有当战斗需要独立的 Battle Beat、Range / Advantage / Condition、Target Handoff、兵器连续性或三线同步工作流时，才进入专项任务。
- 有图片和视频混合参考时，如果素材职责本身是主要难点，优先进入多模态参考任务；如果核心难点明确是复杂战斗编排，可由 Action Combat 作为主任务并继续使用对应输入 Reference。
- 用户提供完整故事板并要求管理整部镜头链路时，优先使用故事板任务；单个或局部镜头中的复杂战斗可引用 Combat 专项规则。
- 只替换视频中的一个元素且其余内容保持不变，属于视频局部编辑。
- 以原视频的动态结构整体重生成，属于视频参考复刻 / 视频转视频。
- 模型专属能力由 `references/models/` 决定，不在任务层写死平台语法。
