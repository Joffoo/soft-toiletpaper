---
name: soft-toiletpaper
description: 生成 TOILETPAPER（厕纸风格）生图提示词：高反差纯色背景纸、小光源直闪硬光、刀刻硬阴影、画面纯净无字。用于用户点名「厕纸风格」/TOILETPAPER/卡特兰式波普大片感，或需要为文章配一张荒诞撞色无字底图时。
---

# TOILETPAPER 厕纸风格生图提示词

输出纯视觉、无字的高反差波普摄影 Prompt。气质取自莫瑞吉奥·卡特兰与皮埃尔保罗·费拉里的《TOILETPAPER》杂志：日常平凡实物 × 体面仪式的认知失调，剔除血腥与生理不适。排版与封面拼装由下游技能承接。

本技能只产提示词；全部数值（色值、光学实测、材质）只在 references 中有一份原文。

**范式边界**：只覆盖"高饱和纯色影棚底 + 中央孤立主体"这一支——在核心大片里占 **35%～40%**，另 60% 是实景置景，不属于本技能。用户要置景/实景气质时明说超出范围，别硬套纯色底。

---

## 一、工作流

### Step 1 · 冲突提炼与 3×3 解耦点菜板

用户给出文章路径（`@文章.md`、`_inbox/xxx.md`）或主题时，直接读取全文，提炼底层核心冲突（Core Tension）。将**剧情场景、镜头切口、色彩配方**三者解耦，向用户呈现 **3×3 点菜板**（每栏仅筛出最契合当前主题的 Top 3 候选项，并在每栏标记一个 `★ 推荐`）：

1. **选画面冲突（A / B / C）**：每个选项包含 `<荒诞实体道具> + <核心神态动作> + <文章冲突隐喻>`（神态四选一：`Deadpan 冷酷超然` / `Manic Smile 过载假笑` / `Naive Wonder 天真好奇` / `Campy Shock 浮夸惊骇`）：
   - **A 凝固的危机**：爆裂、倾覆或崩塌前一秒。
   - **B 荒谬的专注**：以主厨或外科医生的极致严谨，处理庸俗微不足道之物。
   - **C 优雅的对冲**：把现实困境包进高定大刊般极简纯净的构图与明艳色彩。
2. **选镜头切口（① / ② / ③）**：从第四节的 6 大镜头中，筛出最能放大当前动作张力的 3 个镜头，写明焦距/距离与构图裁切效果（如全身中景 vs 贴脸局部特写）。
3. **选色彩配方（Ⅰ / Ⅱ / Ⅲ）**：从 Top 8 单色底与 5 组双色配方中筛出 3 套互不相同的色调（冷调 `#DCF0F6` `#354E89` `#57ACC0`、暖调 `#CE3C2A` `#E2BA26` `#A33E4E` `#CE5C23`、绿调 `#115848` 或黑底明度差）。成组出图时不连续复用同一底色。

> **🔴 CHECKPOINT · STOP**
> 若环境支持 `ask_question` 交互弹窗，直接调用弹窗展示这 3 道单选（把 `★ 推荐` 项排在首位）；若为纯文本回复，在末尾提示：
> - **懒人直通**：回「默认」或「好」，直接按三栏的 `★ 推荐` 组合（及默认画幅）编译；
> - **自由混搭**：回三位代号（如 `B1Ⅱ`）或直接指定画幅（`2.35:1` / `16:9` / `3:4` / `1:1`，以及是否需要排版留白，默认不强加单侧压字留白）。

**完成判据**：三栏解耦呈现、每栏 3 个候选互不雷同、均标明 `★ 推荐` 项，且停在 Checkpoint 等待用户拍板后才进入 Step 2。

### Step 2 · 编译与自筛交付

先读取 `references/lenses.md` 与 `references/color_palette.md`，按五层骨架编译为**单段英文纯文本**：

1. **身份锁定**（仅垫图时）：`keep face, features, skin tone, hairstyle unchanged, no identity drift`
2. **镜头与空间几何**：该镜头的 Prompt 片段原文，逐字取用。
3. **道具与受力形变**：荒谬实体互动、接触面受压形变、指尖压力凹陷、波普糖果化材质。
4. **材质与高光**：从材质词典取 1~2 种（严格采用纯正向描述，严禁引入原片段中的负向词）。
5. **打光与构图模式**：裸灯直闪视觉目标 + 刀刻般接触硬阴影 + 第二节纯净背景恒量 + 第三节对应画幅的构图词（区分**「原刊饱满模式（无留白）」**与**「下游排版留白模式」**）。

**自筛前置闸门（防畸变与模型混淆）**：在拼接完成后、交付之前，必须内部通过 3 项确定性自筛。不合格立即就地重写：
- **肢体边界锁闭**：画面出现手足或人体局部时，必须显式声明裁切边界或单肢状态（如 `the ankle cropped by the frame edge` 或 `one single hand`），阻断生图模型补画多余肢体。
- **材质主谓解耦**：检查形容词（如 `high-gloss latex`, `translucent jelly`）是否与目标道具紧邻，避免模型将背景纸或非目标道具错误染上该材质。
- **正向表述校验**：扫描全文，绝对不出现任何含 `no / without / avoid / non-` 的负向词，所有留白与纯净要求全量收敛至第二节的恒量句。

交付四项：

1. 完整英文 Prompt（单段；通过自筛闸门；无负向子句、无 Midjourney 参数、无任何文字元素）。
2. 三条决定性光学机制说明——为何是硬阴影、高光为何呈点状死白、撞色为何产生边缘震颤。不逐句翻译。
3. 一句话测试版 Prompt（中英双语）。
4. 下游留白指引：安全区比例与建议版面位置。

**完成判据**：五层齐全；通过自筛闸门；每个 HEX、每段镜头片段都能在 references 原文中找到（凭记忆改写即为未完成）；画面上不出现字样、刊头、印章、贴条、UI。

---

## 二、纯净背景恒量

所有画幅共用这一句，只按第三节追加留白词。**不得改写、不得负向化**：

```text
completely blank featureless seamless paper sweep in one flat solid saturated color, uniform matte studio surface, razor-sharp clean silhouette contour with crisp edge separation, cutout-ready high-contrast isolation
```

旧版用负向句（"没有 X""不得出现 X"）描述留白，已废止：现代模型（FLUX、GPT Image、NanoBanana 2.x、Imagen）以 LLM/T5 理解语义，负向词会把被排除的视觉特征一并激活。

## 三、画幅与构图模式（饱满原刊 vs 排版留白）

根据是否需要下游压字，画幅构图分为两档：**「原刊饱满模式（不留白，贴合原片主体占 60%–80% 的波普视觉冲击）」**与**「排版留白模式（预留 35%–40% 负空间供下游压字）」**：

| 画幅比例 | 模式 A：原刊饱满模式（无压字留白，纯视觉冲击） | 模式 B：下游排版留白模式（供封面/海报压字） |
| :---: | :--- | :--- |
| `3:4` | `vertical 3:4 portrait framing, bold full-frame pop composition, subject tightly filling the central 80% of the canvas with balanced studio backdrop edge` | `vertical 3:4 portrait framing, subject centered or low, top 35% reserved as clean solid backdrop` |
| `16:9` | `wide 16:9 horizontal framing, bold centered pop composition filling the frame with tight dramatic crop` | `wide 16:9 horizontal framing, subject comfortably off-center, 40% of the frame left as clean solid backdrop` |
| `2.35:1` | `cinematic ultra-wide 2.35:1 framing, close-cropped horizontal pop tension filling the widescreen canvas` | `cinematic ultra-wide 2.35:1 banner framing, horizontal linear composition, ample breathing room at both sides` |
| `1:1` | `square 1:1 framing, bold full-frame centered pop composition dominating the canvas` | `square 1:1 framing, bold centered pop composition, uniform negative space all around` |

## 四、镜头速查

原理说明与 Prompt 片段见 [references/lenses.md](references/lenses.md)，片段逐字取用。

| # | 镜头 | 焦距 / 距离 | 戏剧功能 |
| :---: | :--- | :--- | :--- |
| 1 | 平视静物 | `85–100mm` | 零畸变，商品画册式仪式感 |
| 2 | 微距压迫 | `100mm 1:1`，`3–5cm` | 物理压迫，受压泛白与甘油折射 |
| 3 | 90° 垂直俯视 | `50mm` | 解剖台几何秩序，绝对审判 |
| 4 | 15° 荷兰倾角 | `35–50mm` | 倾覆前一秒的失衡悬念 |
| 5 | 广角贴脸微畸变 | `24mm`，`20–30cm` | 桶形膨胀，打断社交距离 |
| 6 | 边缘微窥视 | `50mm` | 前景硬剪影遮挡 35%，偷窥感 |

## 五、硬约束

- **光学只写可观测项**：硬阴影边缘宽度、点状镜面高光、背景与主体的轮廓分离。色温、灯具型号、机位、投影角度一律不作断言——原片无 EXIF 可证，且 45° 投影已由全库复测证伪。
- **打光写视觉目标，不写器材参数**：小发光面积、点状死白高光、零羽化零光晕、阴影边界陡峭。
- **数值必须具体**：HEX 色值、焦距、厘米距离、画面占比。杜绝「亮黄色」「稍微俯视」这类模糊措辞。
- **器官与液体糖果化**：大脑、心脏等意象一律人造化——太阳黄柠檬果冻、荧光薄荷绿树脂、电光青霓虹体、多巴胺塑料积木；液体改用亮电光青苏打、阳光橙汁、纯白牛奶、清水。
- **默认交付文本**：仅当用户明确要求出图时才调用生图工具。
- **撞色不等于强互补**：全集色相差中位 **114°**，强互补（ΔH ≥ 140°）只占核心大片 **17.7%**。同族暖撞（ΔH ≈ 38°，柠檬黄配赤橙）与明度断崖（ΔL\* ≈ 46，纯黑配浅肉色）同等合法，别把每条配方都写成互补。
- **留白是排版配套，不是原片特征**：原片主体集中在中央 60%、背景向四边均匀延展；第三节的 35%～40% 单侧留白是为下游压字刻意让出的，不能反过来当成《TOILETPAPER》的构图规律来陈述。
- **不接排版**：标题、刊头、印章、贴条文字归下游封面技能。

## 六、数据指针

- 语料拓扑、色相分布、Top 8 色谱、5 组对撞配方、光学实测、5 种高反射材质词典 → [references/color_palette.md](references/color_palette.md)
- 6 大镜头的戏剧原理与 Prompt 片段原文 → [references/lenses.md](references/lenses.md)
