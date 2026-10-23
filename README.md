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

**Step 1 · 冲突提炼与 3×3 解耦点菜板**
读全文 → 提炼核心冲突 → 将**剧情场景、镜头切口、色彩配方**三者解耦，输出 **3×3 点菜板**（每栏标记 `★ 推荐` 项）：
1. **画面冲突（A / B / C）**：凝固的危机 / 荒谬的专注 / 优雅的对冲（包含 `<荒诞实体道具> + <核心神态动作> + <文章冲突隐喻>`）
2. **镜头切口（① / ② / ③）**：从 6 大物理光学镜头中筛选最能放大动作张力的 3 个
3. **色彩配方（Ⅰ / Ⅱ / Ⅲ）**：从 Top 8 单色底与 5 组双色对撞中选出 3 套互不相同的色调

中间唯一的 🔴 CHECKPOINT：
- **懒人直通**：回复「默认」或「好」，直接按三栏 `★ 推荐` 组合编译；
- **自由混搭**：回复三位代号（如 `B2Ⅱ`）或直接指定画幅（`2.35:1` / `16:9` / `3:4` / `1:1`）。

**Step 2 · 编译与自筛交付**
按五层骨架编译成单段英文 Prompt（身份锁定 → 镜头空间 → 道具形变 → 材质高光 → 打光与留白）。
在拼接完成、交付之前，必须通过 **3 项确定性自筛前置闸门**：
- **肢体边界锁闭**：出现手足或人体局部时，显式声明裁切边界或单肢状态，阻断生图模型补画多余畸变肢体；
- **材质主谓解耦**：限制高光、乳胶等修饰词与目标道具紧邻，避免模型将背景纸或非目标道具错误染上该材质；
- **正向表述校验**：扫描全文，清零所有 `no / without / avoid` 负向词，将纯净度与留白全量收敛至纯净背景恒量句。

最终交付四项：完整英文 Prompt、三条决定性光学机制说明、一句话测试版 Prompt、下游留白指引。

## 示例

主题："待办清单永远清不完"

**Step 1 生成的 3×3 解耦点菜板**：

| 栏目 | 选项 1 | 选项 2 | 选项 3 |
| :--- | :--- | :--- | :--- |
| **画面冲突** | **A. 凝固的危机 (★ 推荐)**<br>柠檬果冻清单塔正向左倾倒，果冻内悬着无字纸条（浮夸惊骇） | **B. 荒谬的专注**<br>主厨用手术镊子给一颗 1cm 樱桃番茄缝合（冷酷超然） | **C. 优雅的对冲**<br>大理石托盘上摆一枚比托盘还大的薄荷绿树脂药丸（过载假笑） |
| **镜头切口** | **① 24mm 广角贴脸微畸变 (★ 推荐)**<br>距主体 25cm，桶形膨胀打断社交距离 | **② 100mm 1:1 微距压迫**<br>距主体 4cm，物理挤压边缘紧贴画框 | **③ 90° 垂直俯视**<br>解剖台几何秩序，绝对审判感 |
| **色彩配方** | **Ⅰ. 配方 2 暖色硬撞 (★ 推荐)**<br>太阳黄底 `#FDCF00` 撞番茄红 `#E4471D` | **Ⅱ. 纯色冰青**<br>经典 `#DCF0F6` 冰青底纸 | **Ⅲ. 配方 5 明度断崖**<br>纯黑底 `#020202` 配高光浅色主体 |

选 **`B2Ⅱ`**（荒谬的专注 + 微距压迫 + 冰青底纸）编译并自筛后的 Prompt：

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
