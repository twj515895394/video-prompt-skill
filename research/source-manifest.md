# Source Manifest

更新时间：2026-07-10

## 状态说明

- `incoming`：已进入临时区，尚未审计
- `reviewing`：正在核对来源、重叠和适用边界
- `extracted`：已形成提炼稿，尚未并入正式 Reference
- `merged`：已并入正式 Reference 真源
- `rejected`：不适合沉淀
- `archived`：仅保留追溯，不再参与迁移

## 用户上传资料

| ID | 临时文件 | 主要主题 | 候选沉淀层 | 状态 |
|---|---|---|---|---|
| U01 | `incoming/user/图生视频.md` | 图生视频题材入口与流程 | tasks / inputs | incoming |
| U02 | `incoming/user/写实电影短剧.md` | 写实短剧题材工作流 | styles / libraries | incoming |
| U03 | `incoming/user/AI漫剧.md` | 漫剧角色、分镜、动作与风格 | styles / libraries | incoming |
| U04 | `incoming/user/图像风格提取流程.md` | 参考图视觉信息提取 | inputs / controls | incoming |
| U05 | `incoming/user/电影感Prompt拆解公式.md` | 电影感可控变量 | controls / styles | incoming |
| U06 | `incoming/user/基础Prompt结构.md` | 通用 Prompt 要素 | controls/prompt-assembly | incoming |
| U07 | `incoming/user/故事版分镜到视频流程.md` | 故事板到视频 | tasks | incoming |
| U08 | `incoming/user/打击帧与动作戏结构.md` | 动作节拍与反馈 | controls / libraries | incoming |
| U09 | `incoming/user/AI视频风格选择器.md` | 设备视角与作者气质 | styles / libraries | incoming |
| U10 | `incoming/user/影视风格选择器.md` | 题材级风格模板 | styles / libraries | incoming |
| U11 | `incoming/user/电影光影与色调选择器.md` | 光影与色调 | controls / libraries | incoming |
| U12 | `incoming/user/导演级运镜术语选择器.md` | 运镜术语与适用情节 | libraries/camera-shot | incoming |
| U13 | `incoming/user/视角机位与景别选择器.md` | 景别、机位、焦段 | controls / libraries | incoming |
| U14 | `incoming/user/表情与微表情选择器.md` | 表演与微表情 | controls / libraries | incoming |
| U15 | `incoming/user/角色发型选择器.md` | 角色发型与动态锚点 | libraries / shared boundary | incoming |
| U16 | `incoming/user/文生视频Prompt结构.md` | 文生视频时间轴结构 | tasks/text-to-video | incoming |
| U17 | `incoming/user/图生视频Prompt结构.md` | 图生视频锚点与运动结构 | tasks/image-to-video | incoming |

## 外部 GitHub 资料

| ID | 来源 | 主要用途 | 注意事项 | 状态 |
|---|---|---|---|---|
| G01 | `dexhunter/seedance2-skill/zh/SKILL.md` | Seedance 多模态引用、编辑、延长、卡点和任务分类 | 模型规格与限制需继续核对官方来源；不直接复制完整示例 | reviewing |
| G02 | `YouMind-OpenLab/awesome-seedance-2-prompts` | 大量社区案例的结构归纳、任务覆盖和失败模式采样 | CC BY 4.0；社区案例不等于官方能力说明 | reviewing |
| G03 | `twj515895394/image-prompt-skill@refactor/reference-architecture-v2` | Reference 分层、路由预算、单一真源和迁移方法 | 只复用架构原则，不复制图片任务边界 | reviewing |

## 官方 / 产品资料

| ID | 来源 | 主要用途 | 注意事项 | 状态 |
|---|---|---|---|---|
| O01 | LTX 官方《LTX-2.3 Prompt Guide》 | LTX 的叙述方式、时序、镜头、动作、音频和图生视频写法 | 模型适配页需记录核验日期，避免把版本特性写成永久通用规则 | reviewing |

## 初步去重判断

以下主题存在明显重叠，不能直接多份入库：

1. `基础Prompt结构`、`文生视频Prompt结构`、`图生视频Prompt结构` 与当前旧版 Playbook。
2. `导演级运镜术语选择器`、`视角机位与景别选择器` 与旧版 `camera-movement-appendix`。
3. `AI视频风格选择器`、`影视风格选择器`、`电影感Prompt拆解公式`、`电影光影与色调选择器` 与旧版 `visual-style-appendix`。
4. `打击帧与动作戏结构` 与旧版 `action-beat-appendix`。
5. `图生视频`、`故事版分镜到视频流程` 与旧版 `task-image-to-video`。

后续必须按“控制方法 / 具体资料 / 风格实现 / 任务流程”拆开，而不是按原文件一比一搬迁。
