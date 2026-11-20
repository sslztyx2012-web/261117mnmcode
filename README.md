# DEAD DAWN · 死者黎明

> **末日据点 · 第一人称生存射击**
> **Outpost Survival · First-Person Shooter**

**一款完全由 AI 编程助手从零写出来的浏览器第一人称射击游戏 —— 整个游戏就是一个 HTML 文件，下载下来双击就能玩，零安装、零素材、零构建。**

**A browser first-person shooter written end-to-end by an AI coding agent — the whole game is a single HTML file. Download it, double-click, play. No install, no assets, no build step.**

`game` `fps` `three.js` `webgl` `ai-generated` `single-file` `no-assets` `procedural`

---

## 中文

### 这是什么

你被丢在一座废弃的军事据点里，四周是成群涌来的感染者。守住阵地，收集弹药与废料，用木板加固门窗，活过一波又一波。

游戏内所有东西都是**程序化生成**的：没有一张外部贴图，没有一个模型文件。所有材质由 Canvas 2D 现场绘制，所有几何体由代码搭建，所有音效由 WebAudio 实时合成。

### 怎么玩

**在线直接玩：** <https://sslztyx2012-web.github.io/261117mnmcode/>

1. 下载（或克隆）本仓库，得到 `index.html`（这就是整个游戏，文件名是 `index.html` 是为了让 GitHub Pages 直接能打开）。
2. 用 Chrome / Edge / Firefox 打开它。
3. 点击「开始游戏」，鼠标会被指针锁定，`Esc` 退出。

> 首次加载需要联网一次：three.js r160 通过 CDN 的 import map 引入。除此之外全程离线可玩。

### 操作

| 操作 | 按键 |
| --- | --- |
| 移动 | `W` `A` `S` `D` |
| 疾跑 | `Shift` |
| 跳跃 | `Space` |
| 蹲下（按一次蹲下，再按一次站起） | `Q` |
| 开火 | 鼠标左键 |
| 瞄准（光学瞄镜） | 鼠标右键 |
| 换弹 | `R` |
| 切换武器 | `1` / `2`（或滚轮） |
| 互动 / 加固路障 | `E` |
| 手电筒 | `F` |
| 暂停 | `Esc` |

### 特色系统

**第一人称武器**
AK-74M 与 M870 两把枪都是完整建模的：机匣、皮卡汀尼导轨、觇孔机械瞄具、红点镜附件、导气箍、消焰器、弹匣井、枪托，以及一双真的握住武器的手 —— 手指是沿圆弧扫掠出来的独立几何体，食指会跟着扳机一起动。
换弹是分阶段编排的：倾斜 → 退匣 → 弹匣掉到地上 → 插新匣 → 左手回位 → 拉机柄，配套 `magOut` / `magIn` / `bolt` 等程序化音效。霰弹枪则是泵动前推＋抛真实红壳。
枪身运动用弹簧模拟：呼吸晃动、行走摆动、冲刺姿态、后坐的三路位移与俯仰偏航回弹，开火时还有枪口火焰、烟雾、抛壳。

**瞄准镜**
右键抬枪，镜筒叠加层淡入、枪身让位、世界视野从 76° 收到 42°（约 1.8 倍放大远处目标），屏幕中央是红点与刻线。枪身不会挡住视线。

**程序化美术**
混凝土、锈铁、木料、树皮、布料、橡胶、危险品标识等材质全部由噪声函数生成法线贴图与污渍贴花；墙体有墙裙、壁柱、压顶、破损露筋；营房有波纹屋顶、封檐、天沟、落水管、百叶与封窗木板；院子里有沙袋墙、弹药箱、油桶、水壶、路锥、警示牌、轮胎堆、格状桅杆、碎石与积水；外面是分叉树干与三层树冠的森林。

**敌人与玩法**
五种感染者（walker / runner / brute / spitter / crawler）各有独立的体型、速度、血量与 AI 行为。门有木板和耐久度，可以用废料加固；击杀掉落弹药与废料；难度、灵敏度、画质、泛光都在设置里。

**围城：感染者会真的打进基地**
感染者不再只在门外干瞪眼。一张 0.5 米的导航网格每 0.2 秒从玩家位置重新泛洪一次，尸群会自动绕开障碍、找到大门的缺口、穿过营房与指挥部的门洞，一路追到你面前。围墙上有四处可以砸开的加固段：普通感染者要砸十几下，brute 只要几下就能把混凝土墙敲穿，碎石会留在原地。围墙东侧还有一段已经塌掉的破口，不用拆就能直接挤进来。
反过来，南墙有一处 1.2 米高的矮口：**只有蹲下的玩家钻得过去，感染者永远过不来** —— 那是给你留的逃生通道，不是给它们的。

**爆头：头会飞出去，脖子喷绿汁**
一枪打中脑袋，感染者当场倒地 —— 头颅沿着**被打中的那一侧**飞出去：打左边就往左飞，打右边就往右飞，飞得够远还会翻着跟头落下，落地弹一下、滚一段，最后静静躺在地上。飞行途中一路滴着**绿色浓汁**，脖子的断口同时在狂喷。打身体依然是原来的红色血浆效果。

**丧尸不会互相重叠**
感染者之间有体积：挤在一起会互相顶开，不会叠在同一个点上，也不会穿模重合。

**它们长了脑子**
会自己找路。卡住了、被堵住了、或者目标暂时够不着的时候，会先用导航网格评估四周，挑一条**真正能通向你的方向**绕过去 —— 往左、往右、贴着墙挪都行，绝不会卡在原地磨蹭。

**子弹能穿过软障碍**
你钉在门窗上的木板、感染者正在猛砸的可破坏墙段、地上的矮口与低矮杂物，都不再挡子弹 —— 你可以隔着路障把那只正在砸门的感染者一枪爆头。实心墙和高掩体仍然挡子弹，掩体该有的意义一点不少。

**其它**
中英双语界面、雷达小地图、受击方向指示、命中标记、程序化音效、照片模式（`?photo=1&shot=N`）、死亡统计。

### 技术

- 单文件：`index.html`，约 261 KB，自包含。
- 渲染：three.js r160（唯一外部依赖，CDN import map），WebGL2。
- 零外部素材：贴图 = Canvas 2D 噪声；模型 = 代码几何；音效 = WebAudio 合成。
- 性能：约 370–450 draw calls、约 350–410k 三角形，1080p 下 132–144 FPS（高档画质）。导航寻路每 0.2 秒重算一次，单次约 1.5 ms。
- 渲染分两遍：世界（layer 0）与第一人称武器（layer 3）分别用不同的镜头参数渲染，武器有独立的 52° 视角，避免近距离透视把枪身拉变形。

### 仓库结构

```
index.html        # 整个游戏（单文件，GitHub Pages 入口）
README.md
LICENSE
```

---

## English

### What is this

You are dropped into an abandoned military outpost with infected pouring in from every side. Hold the line, scavenge ammunition and scrap, board up the doors and windows, and survive wave after wave.

Everything in the game is **procedurally generated**: not a single external texture, not a single model file. Every material is painted on a 2D canvas at runtime, every mesh is built in code, every sound effect is synthesised with WebAudio.

### How to play

**Play it online:** <https://sslztyx2012-web.github.io/261117mnmcode/>

1. Download (or clone) this repo and get `index.html` — that file *is* the whole game (it is named `index.html` so GitHub Pages can serve it straight away).
2. Open it in Chrome / Edge / Firefox.
3. Click **Start Game**. The pointer locks, press `Esc` to release it.

> One online connection is needed on first load: three.js r160 is pulled from a CDN via an import map. After that it runs fully offline.

### Controls

| Action | Key |
| --- | --- |
| Move | `W` `A` `S` `D` |
| Sprint | `Shift` |
| Jump | `Space` |
| Crouch (press to toggle) | `Q` |
| Fire | Left mouse |
| Aim (optic) | Right mouse |
| Reload | `R` |
| Switch weapon | `1` / `2` (or scroll) |
| Interact / barricade | `E` |
| Flashlight | `F` |
| Pause | `Esc` |

### Highlights

**First-person weapons**
The AK-74M and the M870 are fully modelled: receiver, Picatinny rail, aperture sights, a red-dot optic attachment, gas block, muzzle brake, magazine well, stock — and a pair of hands that actually hold it, with fingers swept along real arcs and a separate trigger finger that moves with the trigger.
Reloading is choreographed in stages: tilt → drop the magazine → the magazine falls to the ground → insert a fresh one → the support hand returns → cycle the charging handle, with matching `magOut` / `magIn` / `bolt` sounds. The shotgun racks its pump and throws real red shells.
Weapon motion is spring-driven: breathing, walk bob, sprint pose, three-axis recoil with settle oscillation, plus muzzle flash, smoke and ejected brass.

**Optics**
Right mouse raises the weapon: an optic overlay fades in, the body of the gun steps aside, and the world zooms from 76° to 42° (~1.8× magnification on distant targets) with a red dot and reticle in the centre. The weapon never blocks your view.

**Procedural art**
Concrete, rusted metal, wood, bark, cloth, rubber and hazard-stripe materials are all generated from noise functions, complete with derived normal maps and grime decals. Walls get skirts, pilasters, coping, cracks and exposed rebar. Barracks get corrugated roofs, fascia, gutters, downpipes, shutters and boarded windows. The yard fills with HESCO sandbag walls, ammo crates, barrels, canteens, traffic cones, warning signs, tyre stacks, lattice masts, rubble and puddles. Beyond the fence stands a forest of forked trunks with three layered canopies.

**Enemies and gameplay**
Five infected types (walker / runner / brute / spitter / crawler), each with its own size, speed, health and behaviour. Doors have boards and durability that you can reinforce with scrap. Kills drop ammunition and scrap. Difficulty, sensitivity, quality and bloom all live in the settings menu.

**Siege: the infected actually break into the base**
They no longer mill about outside. A 0.5 m navigation grid is flood-filled from your position a few times a second, so the horde paths around obstacles, finds the gap in the main gate, slips through the building doorways and reaches you. Four sections of the perimeter wall can be knocked down: a regular walker needs a dozen swings, a brute punches through the concrete in a few, and the rubble is left behind. A collapsed section on the east wall needs no demolition at all — they simply squeeze through it.
The other way round: there is a 1.2 m crawl-through in the south wall that **only a crouching player fits through — the infected never can**. That one is your escape route, not theirs.

**Headshots: the head flies off, the neck sprays green**
One round to the head puts the infected down instantly — and the head **flies off towards the side you hit**: shoot it on the left and it goes left, shoot it on the right and it goes right, tumbling through the air before it bounces, rolls and finally lies still on the ground. It drips **green goo** the whole way down while the torn neck keeps pumping. Body shots are unchanged — still the old red blood.

**The infected never overlap**
They have volume: shoulder each other apart instead of stacking into one point or clipping through each other.

**They have a brain now**
They find their own way. When they are pinned, blocked or the target is momentarily unreachable, they score the surroundings against the navigation grid and pick a direction that **actually leads to you** — left, right, sliding along a wall — instead of grinding away in one spot.

**Bullets pass through soft cover**
The boards you nail over a door, the wall sections the infected are busy smashing, the crawl gap and low clutter no longer stop a round — you can put a headshot through the barricade into the thing breaking it. Solid walls and real cover still stop bullets, so cover still means something.

**Extras**
Chinese / English UI, radar minimap, directional damage indicators, hit markers, procedural audio, a photo mode (`?photo=1&shot=N`) and an end-of-run scorecard.

### Tech

- One file: `index.html`, ~261 KB, fully self-contained.
- Rendering: three.js r160 (the only external dependency, via CDN import map), WebGL2.
- Zero external assets: textures = Canvas 2D noise, meshes = code geometry, audio = WebAudio synthesis.
- Performance: ~370–450 draw calls, ~350–410k triangles, 132–144 FPS at 1080p on high quality. The navigation field is recomputed every 0.2 s at roughly 1.5 ms per pass.
- Two-pass rendering: the world (layer 0) and the first-person weapon (layer 3) are rendered with different lens parameters — the weapon gets its own 52° lens so close-range perspective doesn't smear the gun into unreadable wedges.

### Repository layout

```
index.html        # the entire game (single file, GitHub Pages entry point)
README.md
LICENSE
```

---

## License

MIT — see [LICENSE](LICENSE).

Built with [three.js](https://threejs.org/) (r160) and an AI coding agent. All artwork, geometry and audio are generated procedurally at runtime; no third-party assets are bundled.
