# 《TOILETPAPER》6 大经典戏剧功能物理镜头标准词典

本文档彻底废除旧版随机哈希抽样，将镜头机位收敛为 6 种具有明确戏剧张力、物理光学规律和构图功能性的标准镜头词典。

> **本文件是镜头 Prompt 片段的唯一原文出处**：`SKILL.md` 只做速查，编译 Prompt 时必须从本文件逐字取用片段，不改写、不转述。
>
> **勘误（与全库复测口径对齐）**：旧片段中 `cast at 45 degrees` 与"对角长斜向投影"等指定投影方向的措辞已删除——原片无 EXIF，45° 系滤波区间造成的数学假象，投影方向不构成约束。打光只写可观测形态（小发光面积、点状死白高光、零羽化），不指定色温与灯具型号。

---

## 镜头 1：平视静物 (Clinical Eye-Level Still Life)

- **戏剧功能**：冷酷解构日常、商品画册式神圣仪式感。将最庸俗、微不足道或荒诞的物品，以大英博物馆展品或顶级奢侈品的尊崇仪式正襟危坐呈现。
- **物理光学参数**：
  - 焦距：`85mm - 100mm` 中长焦定焦
  - 拍摄高度与夹角：`0°` 严格水平平视，相机光轴平行于台面
  - 畸变：零光学透视畸变，背景纸垂直无逃逸线
  - 阴影：刀刻般接触硬阴影紧贴物体轮廓，投射方向不指定
- **下游排版留白**：主体置于中心或三分线，左右两侧各预留 35%~40% 纯净均匀背景。
- **结构化 Prompt 描述片段**：
  ```text
  clinical straight-on eye-level still life perspective, 85mm medium-telephoto lens, zero perspective distortion, subject perfectly aligned parallel to the seamless solid backdrop, razor-sharp contact drop shadow falling directly beneath the object, immaculate luxury catalog formality, generous clean negative space surrounding the subject
  ```

---

## 镜头 2：微距压迫 (Macro Oppression & Physical Squeeze)

- **戏剧功能**：显微级物理压迫感、侵入式材质窥探。极力强化道具与人体皮肤接触受压后的泛白、拉伸褶皱与甘油折射，让荒谬细节产生强烈的触觉刺激。
- **物理光学参数**：
  - 焦距：`100mm 1:1` 微距镜头
  - 对焦距离：仅 `3cm - 5cm` 极限近距
  - 景深：极浅景深，焦点精准咬合在受压接触点
  - 高光：微观凸透镜点状反光与汗珠折射
- **下游排版留白**：主体占据画面 75%~80% 核心面积，边缘留出整洁切口，为顶部或底角字卡预留高反差纯色角。
- **结构化 Prompt 描述片段**：
  ```text
  extreme macro lens perspective focused at ultra-close 4cm distance, physical compression with subject pressed hard against the frame boundary, visible dermal pressure blanching, glistening specular micro-droplets, razor-sharp shallow focal plane with subject dominating 80% of canvas, clean background perimeter
  ```

---

## 镜头 3：90°垂直俯视 (Pure 90° Zenith Flat-Lay)

- **戏剧功能**：手术解剖台感、绝对几何审判与上帝冷酷凝视。所有实体道具仿佛被无形力场压平在二维平面上，形成秩序与荒谬的绝妙讽刺。
- **物理光学参数**：
  - 焦距：`50mm` 标准定焦
  - 拍摄高度与夹角：`90°` 严格天顶正俯拍，光轴与水平桌面成绝对直角
  - 构图几何：同心圆或严格中轴对称
  - 阴影：硬接触阴影紧贴物体轮廓下方，无长投影
- **下游排版留白**：中心放射或四角对称，四周边缘预留完整的 30% 纯色安全环带，极易环绕排版。
- **结构化 Prompt 描述片段**：
  ```text
  pure 90-degree zenith flat-lay perspective directly perpendicular to the tabletop surface, surgical autopsy geometric precision, razor-sharp contact drop shadows dropped flush beneath object contours onto pristine solid seamless paper, zero perspective divergence, immaculate clean negative space around the perimeter
  ```

---

## 镜头 4：15°荷兰倾角 (15° Subtle Dutch Angle & Dynamic Tilt)

- **戏剧功能**：潜在失控、打破体面秩序、倾覆前一秒的悬念动态。利用微小的偏轴失衡撕开荒诞现实的裂缝，比大幅度倒吊更加克制与紧张。
- **物理光学参数**：
  - 焦距：`35mm - 50mm` 人文/标准定焦
  - 偏轴夹角：沿画面对角线微倾 `15°`
  - 动态：凝固瞬间（1/2000s 闪光同步），物体受剪切力静止
  - 阴影：硬接触投影随画面倾角自然滑出画面对角，贯穿纯色背景（倾角来自机位，不由打光角度决定）
- **下游排版留白**：倾斜形成的对角三角形负空间，为横版或竖版斜跨标题提供天然视线导引。
- **结构化 Prompt 描述片段**：
  ```text
  dynamic 15-degree Dutch angle tilt, diagonal horizon creating unstable off-axis kinetic tension, subject frozen in dynamic balance, harsh bare-bulb strobe flash casting sharp diagonal contact shadows across the solid vibrant backdrop, ample breathing room in the upper corner
  ```

---

## 镜头 5：广角贴脸微畸变 (Intrusive Wide-Angle Facial Confrontation)

- **戏剧功能**：打破社交安全距离的无理侵入、荒谬的死鱼眼对视。利用轻微的光学桶形畸变将面部或道具中心放大膨胀，制造滑稽与不安的双重心理反射。
- **物理光学参数**：
  - 焦距：`24mm` 广角镜头
  - 拍摄距离：仅 `20cm - 30cm` 贴脸距离
  - 畸变：中心微凸（Barrel Distortion），四周向边缘收缩
  - 打光：自镜头轴线直射的小发光面积裸灯直闪，鼻梁与额头出现锐利点状死白高光
- **下游排版留白**：头部居中，头顶上方与左右两侧留出平整无污渍的纯色背景纸空间。
- **结构化 Prompt 描述片段**：
  ```text
  intrusive 24mm wide-angle close-up shot only 25cm from subject, slight optical barrel perspective exaggeration bulging the frontal elements toward the lens, confronting deadpan direct stare, harsh direct bare-bulb flash from the lens axis highlighting facial skin texture and prop contours with crisp pinpoint specular highlights, solid seamless backdrop
  ```

---

## 镜头 6：边缘微窥视 (Edge Peeping & Occluded Voyeuristic Framing)

- **戏剧功能**：偷窥密谋感、不体面的观察视角。通过前景的不透明硬边缘强行遮挡部分视线，让观者仿佛躲在门缝、桌面或障碍物后窥视一场优雅的荒诞行径。
- **物理光学参数**：
  - 焦距：`50mm` 标准焦段
  - 前景遮挡：前景实物硬阴影剪影遮挡单侧 `30% ~ 40%` 画面
  - 景深：前景锐利或微虚，后方主体在狭窄开孔中极度清晰
  - 阴影：前景遮挡物投下的巨大几何暗区与背景亮区形成硬割裂
- **下游排版留白**：前景大面积暗部遮挡区域，是下游排版放置高对比度白色主标题或二维码的绝佳天然画板。
- **结构化 Prompt 描述片段**：
  ```text
  voyeuristic framing partially occluded by a massive sharp silhouette edge in the immediate foreground occupying 35% of the frame, the absurd interaction brightly illuminated through the aperture under direct hard studio strobe flash, razor-sharp shadow boundary division, clean solid background behind the subject
  ```
