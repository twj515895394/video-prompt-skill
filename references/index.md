# Video Prompt References Index v2

## 1. 路由目标

用最少量 Reference 支撑当前任务，避免把视频 Skill 变成大而散的资料堆。

v2 采用：

```text
输入理解
→ 任务 Playbook
→ 按需控制
→ 按需资料库与风格
→ 模型适配
→ 输出合同
→ 失败时诊断
```

索引只负责导航，不复制叶子正文。

---

## 2. 默认加载预算

固定读取：

- `1` 份 input Reference；
- `1` 份 task Playbook。

按需读取：

- `0-3` 份 controls；
- `0-2` 份 libraries；
- `0-1` 份 style；
- `0-1` 份 model adapter；
- 失败诊断时 `0-1` 份 diagnostic；
- `1` 份输出合同。

分类索引只用于导航，不计入业务 Reference 数量。

---

## 3. 信息优先级

冲突时按以下顺序执行：

```text
用户当前明确要求
→ 用户指定的必须保留 / 必须修改项
→ 当前任务 Playbook
→ 当前输入 Reference
→ 已加载 controls
→ 已加载 libraries 与 style
→ model adapter 的能力边界和语法
→ 自动补全
```

模型适配页可以限制表达方式和能力边界，但不能擅自改变用户剧情目标。

---

## 4. 第一步：判断输入

读取：`inputs/index.md`

由输入索引继续路由到唯一主输入路线：

- 纯文字；
- 单张图片；
- 多张图片；
- 一个或多个视频；
- 音频；
- 图片 / 视频 / 音频混合输入。

混合输入只读取 `mixed-multimodal-input.md`，不同时加载多份单模态输入页。

---

## 5. 第二步：判断任务

读取：`tasks/index.md`

由任务索引继续路由到唯一主任务 Playbook：

- 文生视频；
- 图生视频；
- 多模态参考视频；
- 视频参考复刻 / 视频转视频；
- 视频局部编辑；
- 视频向前 / 向后延长；
- 音频驱动与音乐卡点；
- 故事板 / 多镜头 / 多片段到视频。

题材差异不新增任务 Playbook，优先进入 `styles/` 或 `libraries/genre-patterns/`。

---

## 6. 第三步：按缺口加载控制页

读取：`controls/index.md`

控制层主要方向：

- 时间轴与节拍；
- 主体运动；
- 镜头与机位；
- 空间调度；
- 连续性与一致性；
- 表演与微表情；
- 音画同步；
- 多模态参考绑定；
- Prompt 组装；
- 去 AI 感和物理可信。

不为了增加细节默认加载控制页。任务 Playbook 已经能解决的问题，不重复读取。

---

## 7. 第四步：按需加载资料库

读取：`libraries/index.md`

资料库提供：

- 镜头、景别、机位和运镜术语；
- 动作、打击帧和运动结构；
- 表情、微表情和对白表演；
- 转场和视觉特效；
- 光影与色调；
- 对白、环境音、拟音和 BGM；
- 写实短剧、AI 漫剧、广告、动作等题材方案。

资料库回答“有哪些选择”，不代替控制规则。

---

## 8. 第五步：按需加载风格

读取：`styles/index.md`

只有风格真正影响实现方式时才读取一份主 style Reference：

- 电影化写实；
- 写实短剧；
- 动画；
- AI 漫剧 / 动态漫画；
- 商业广告；
- 纪录 / UGC；
- 实验视觉。

不要用风格名替代主体、空间、动作、镜头和声音。

---

## 9. 第六步：模型适配

读取：`models/index.md`

正式模型范围固定为：

- `models/generic.md`：默认模型无关输出；
- `models/seedance-2.md`：Seedance 2.0；
- `models/ltx-2-3.md`：LTX-2.3。

路由规则：

- 用户未指定模型 → Generic；
- 用户明确使用 Seedance 2.0 → Seedance；
- 用户明确使用 LTX-2.3 → LTX；
- 不创建或加载其他模型适配页。

模型页只转换通用导演方案，不重新设计任务内容。

---

## 10. 第七步：输出合同

根据模式和任务读取 `assets/templates/` 中的一份输出合同或模板。

快速模式：

- 默认零追问；
- 直接输出可复制结果；
- 不展示内部迁移、路由和资料加载过程。

交互模式：

- 只有用户明确要求共创、讨论、逐步设计或 Grill Me 时启用；
- 每次只问一个最关键的问题；
- 能推断则不追问；
- 再问只影响轻微细节时立即收口。

---

## 11. 第八步：失败诊断

读取：`diagnostics/index.md`

只有以下情况进入：

- 用户反馈生成效果不好；
- 多个维度同时失效；
- 参考素材职责冲突；
- Prompt 过载或要求互相矛盾；
- 无法从单一任务页或控制页定位根因。

---

## 12. 运行规则

- 同一轮只读取一份主 input 和一份主 task。
- 同一叶子文件被多个入口命中时只读取一次。
- 主体运动和镜头运动必须分开判断。
- 多模态素材必须分配职责，禁止平均融合。
- 一段视频必须有开始、推进和落点。
- 负向限制只针对当前最危险的失败模式。
- 不一次性读取整个目录。
- 不把研究区原始资料直接作为运行期 Reference。

---

## 13. 迁移期兼容路由

在 Phase 6 切换 `SKILL.md` 前，旧运行入口仍可能读取以下文件。这些文件暂时保留，但不再作为 v2 新增内容的真源：

### 旧模式

- `mode-quick/quick-mode.md`
- `mode-interactive/interactive-mode.md`

### 旧输入

- `input-text-only/text-expansion.md`
- `input-image-ref/image-reference-analysis.md`

### 旧任务

- `task-text-to-video/playbook.md`
- `task-image-to-video/image-to-video-playbook.md`

### 旧时间轴、连续性和质量控制

- `timeline/timeline-assembly.md`
- `timeline/lifestyle-beat-and-landing.md`
- `continuity/continuity-guardrails.md`
- `continuity/human-motion-consistency.md`
- `style-control/anti-ai-video-realism.md`
- `style-control/camera-failure-patterns-negative.md`

### 旧附录与输出

- `appendix/`
- `output-single-unit/output-spec.md`
- `output-multi-unit/output-spec.md`

迁移状态和目标真源见：`../docs/migration-inventory.md`。

在新任务、控制、模板和 `SKILL.md` 验证完成前，不删除这些兼容文件。
