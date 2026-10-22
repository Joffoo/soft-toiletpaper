# soft-toiletpaper

> 用《TOILETPAPER》的计算视觉规律，生成**纯净无字**的高反差波普生图提示词。

[English](README.en.md) · [安装](#安装) · [工作流](#工作流) · [边界](#边界) · [数据来源](#数据来源)

一个 Markdown-only 的 Agent Skill：把一篇文章的底层冲突，翻译成 3 个荒诞实体场景，再编译成可直接投喂 FLUX / GPT Image / NanoBanana 的单段英文 Prompt。

产出永远是**纯视觉底图**——画面里没有标题、刊头、印章、贴条、UI。文字排版交给下游封面技能（如 `cover-maker`）。

## 它和"波普风提示词"哪里不同

三条规则不是形容词堆出来的，是实测数据支撑的：

| 规则 | 依据 |
| :--- | :--- |
| 无缝纯色底纸才是主战场 | 311 张核心大片里高饱和纯色纸占 **35.0%**，影棚单色合计 **39.5%**；影棚单色内部的彩色纸偏好率 **88.62%** |
| 底纸是红蓝双峰，不是"随便一个亮色" | 青蓝 **44.6%** + 正红 **17.5%** ≈ 62%；Top 1 是 `#DCF0F6` 冰青（41.0%） |
| 硬光 = 边缘陡峭，不是"对比度高" | 阴影 10%→90% 过渡中位 **8.5 px**（P10 2.5 px），不是柔光箱那种虚化半影 |

以及两条不许违反的推论：

- **撞色不必是互补**。全集色相差中位 114°，强互补（ΔH ≥ 140°）只占核心大片 **17.7%**；同族暖撞（ΔH ≈ 38°）与明度断崖（ΔL\* ≈ 46）同等合法。
- **光只写可观测项**。色温、灯具型号、机位、投影角度一律不断言——原片无 EXIF 可证，45° 投影是滤波区间造成的数学假象。

## 安装

```bash
git clone https://github.com/Joffoo/soft-toiletpaper.git \
  "<skills 目录>/soft-toiletpaper"
```

| 宿主 | skills 目录 |
| :--- | :--- |
| Claude Code | `~/.claude/skills/` |
| Codex | `~/.codex/skills/` |
| Gemini CLI | `~/.gemini/skills/` |
| 项目级 | `<vault>/.agents/skills/` |

纯 Markdown，零依赖，复制即用。

## 触发

- "用厕纸风格给这篇文章配张图"
- "TOILETPAPER 那种大片感"
- "卡特兰式的荒诞撞色"

## 工作流

两步，一个检查点。

**Step 1 · 冲突提炼与场景发散**
读全文 → 提炼核心冲突 → 输出 3 个荒诞实体场景，每个一行四元组：

```
<荒诞实体道具> — <文章冲突隐喻> — <核心神态动作> — <预设：配方 # 或 纯色底 # / 镜头 # / 画幅>
```

三个方案分别走**凝固的危机 / 荒谬的专注 / 优雅的对冲**三条戏剧路径，且底色必须互不相同——先用一遍色轮，别三个方案全穿冰青。

**Step 2 · 编译与交付**
按五层骨架拼成单段英文 Prompt：镜头与空间 → 道具与受力形变 → 材质与高光 → 打光与留白。交付四项：完整 Prompt、三条决定性光学机制、一句话测试版、下游留白指引。

唯一的 🔴 CHECKPOINT 在两步中间：选 A/B/C，或直接说改哪一项。

## 示例

主题："待办清单永远清不完"

| | 方案 | 预设 |
| :--- | :--- | :--- |
| A | 一整座柠檬果冻砌成的清单塔正向左倾倒，果冻内部悬着无字纸条 | 配方 2（`#FDCF00` + `#E4471D`）｜镜头 4｜3:4 |
| B | 主厨用手术镊子，给一颗 1cm 的樱桃番茄缝合 | 纯色底 `#DCF0F6`｜镜头 2｜1:1 |
| C | 大理石托盘上摆一枚比托盘还大的薄荷绿树脂药丸 | 配方 5（`#020202` + 高光浅色主体）｜镜头 3｜2.35:1 |

选 B 之后编译出的 Prompt：

```text
extreme macro lens perspective focused at ultra-close 4cm distance, physical compression
with subject pressed hard against the frame boundary, visible dermal pressure blanching,
glistening specular micro-droplets, razor-sharp shallow focal plane with subject dominating
80% of canvas, clean background perimeter, stainless steel tweezers stitching a single
cherry tomato with translucent surgical thread, tomato skin denting under the tweezer tips,
cold porcelain enamel tray, small-source bare-bulb flash, razor-sharp contact drop shadow,
completely blank featureless seamless paper sweep in one flat solid saturated color (#DCF0F6),
uniform matte studio surface, razor-sharp clean silhouette contour with crisp edge separation,
cutout-ready high-contrast isolation, square 1:1 framing, bold centered pop composition,
uniform negative space all around
```

## 边界

- **只覆盖纯色影棚底**。核心大片里 60.4% 是实景与置景，那一路不属于本技能；要置景气质请直接说。
- **只产提示词**。默认不调用生图工具，需要出图请明确要求。
- **不做排版**。标题、刊头、印章、贴条文字归下游封面技能。
- **画面无字**。这是硬约束：排版信息一律不进 Prompt，用正面描述锁定纯净背景，不用负向排除句。

## 数据来源

对 3,440 张官方图包（含 311 张核心摄影母版）做 CIELab K-Means 聚类与物理光学量化。数字以 `references/` 为准，README 里的只作摘要：

- **`references/color_palette.md`** — 语料拓扑、色相八分区、Top 8 色谱、5 组对撞配方、光学实测、材质词典
- **`references/lenses.md`** — 6 大戏剧物理镜头的原理与 Prompt 片段，编译时逐字取用、不得改写

关于"为什么仓库里没有 5600K、24.91% 高光、45° 投影"：这些旧结论经全库复测已证伪，只在勘误说明里留痕，不再作为参数使用。

## License

MIT © 2026 Joffoo
