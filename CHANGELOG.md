# 更新记录

本项目遵循 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/) 与 [语义化版本](https://semver.org/lang/zh-CN/)。

> 下面的版本号指**应用**（APK）的版本，与仓库结构演进不是一回事。
> 仓库本身的工程改动见最末的「仓库工程记录」。

---

## [仓库] 中英双语：面板语言切换 + 英文 README（2026-10-03）

### 新增

- **面板右上角 🌐 中/EN 切换**：文本节点级替换机制（中文节点 ↔ 英文，切回时逐节点还原），
  覆盖约 170 条静态 UI 文案（页签/卡片标题/按钮/提示/弹窗）；模型卡片的适配分级徽标
  （适合本机/顶格可跑/超预算）走 `fitTxt()` 双语动态渲染；语言选择存 localStorage，
  重开面板保持。
- **README_EN.md**：完整英文版 README（含 exe 三步上手、macOS 说明、仓库结构、版权边界）；
  README.md 顶部加互链；安装环境.md / 用户手册.md 顶部加英文指引条。

---

## [仓库] 模型库：手动下载兜底 · 文件夹实时监测 · 高性能模型导览（2026-10-03）

### 新增

- **每个模型卡片自带「手动下载」兜底**：下载失败时点开展示该模型全部文件的镜像直链
  （全部走 hf-mirror，无需翻墙）、应放入的模型文件夹完整路径、文件名必须保持一致的提醒；
  配套 yaml 小配置支持页面内直接保存。
- **模型文件夹实时监测**：新增 `GET /api/models/sig` 轻量指纹接口（文件数+总字节+最大 mtime），
  前端每 6 秒轮询，指纹一变自动刷新模型库——手动丢模型进文件夹约 6 秒内出现在
  「个人模型」里，免点刷新、免重启（下载任务进行中不打扰）。
- **「想要更强的模型？」导览卡片**：MVSEP 质量榜单、hf-mirror 的 RoFormer 检索入口，
  面向显卡 ≥12 GB 的用户，附「保留原文件名 + 看个人模型体检结论」提示。

### 修复

- 排查出本会话 curl 502 根因：shell 注入了 `http_proxy=127.0.0.1:53891`，
  localhost 请求被代理拦截——本机调试面板 API 需加 `--noproxy "*"`。

---

## [仓库] Windows exe 分发 + macOS 安装文档（2026-10-03）

### 新增

- **Windows 一键装机 exe**（`tools/launcher/karaoke_installer.py` → `跟唱练习器-装机版.exe`，17 MB）：
  纯标准库实现——检测/静默安装 Python 3.12（用户级，免管理员）→ 建 venv 到
  `%LOCALAPPDATA%\SingAlong\envs\uvr` → 按 `nvidia-smi` 检测结果装 CUDA 12 或 CPU 版 PyTorch
  （依赖走清华镜像）  → 装 audio-separator 并钉住 `onnxruntime-gpu==1.22.0`（更高版本需 CUDA 13）
  → 装 ffmpeg（复制 imageio-ffmpeg 的静态二进制到 `<env>/bin`）
  → 自动下载默认分离模型 BS-Roformer-Revive（610MB，hf-mirror 源，进度条显示，
    已存在则跳过）→ 释放内嵌面板与启动器 → 桌面建「跟唱练习器」快捷方式。
  中断重跑会跳过已完成步骤；装完即开箱即用，无需再手动下模型。
- **`serve_separator.py` 环境候选目录补充** `%LOCALAPPDATA%\SingAlong\envs\uvr`
  （装机版固定位置）——否则 exe 装的环境面板自身探测不到，模型/ffmpeg 目录会落空。
- **Windows 启动器 exe**（`tools/launcher/karaoke_launcher.py` → `跟唱练习器.exe`，9 MB）：
  内嵌完整 panel/（仅 772 KB），首次运行释放到 `%LOCALAPPDATA%\SingAlong\panel`，
  按「环境变量 → 装机版固定位置 → 常见约定位置」顺序找环境，服务就绪后再开浏览器；
  exe 挪到任何位置都能跑（环境与面板都在固定目录，不跟 exe 走）。
- **安装环境.md · macOS 完整章节**：Apple Silicon（CoreML/CPU 加速）与 Intel 的实测速度预期、
  Homebrew + python@3.12 + venv 五条命令全流程、HF 镜像加速提示、Gatekeeper 弹窗说明。
- **README 顶部「🐣 完全不懂代码？」入口**：一句话解释「面板是什么」，
  Windows 三步表格 / macOS 指引 / exe 挪位置后的自救路径。

### 工程

- exe 构建产物目录 `release/` 加入 `.gitignore`（exe 只走 GitHub Release 分发）；
  PyInstaller 打包环境为独立 venv（`pack`），不污染分离环境。

---

## [仓库] 面板四大功能：模型库 · 音频降噪 · 工作流 · 统一文件浏览器（2026-10-02）

### 新增

- **「⑥ 模型库」页签**：24 个主流模型联网一键下载（全部走国内可达镜像，断点续传 + 装后校验）；
  每个模型标注体积/显存估算/适配分级（🟢充裕 🟡偏紧 🔴超出），超预算的直接给出「缩水版」替代；
  个人放入的模型自动识别架构与可加载性（ckpt 查支持清单、onnx/pth 查尾部 10 MB 的 MD5 参数库）。
- **「⑤ 音频降噪」页签**：专用降噪模型（参数库中 `primary_stem = Noise` 的 UVR DeNoise 系）；
  可选保留「噪声轨」试听被剥掉的部分；非降噪模型会被接口拒绝并提示。
- **「① 工作流」页签**（默认首页）：「源音频 → 降噪 → 分离 → 歌词 → 出片」节点链，
  节点可单独禁用、独立选模型；启动前自动预检，缺文件/缺模型逐项列出，存在阻断项时禁止运行。
- **统一文件浏览器**：所有「选择文件」入口合并为一个网页内文件夹浏览器
  （盘符 → 逐层进入 → 双击选中，弹窗内保留系统对话框兜底）。
- **新 API**：`GET /api/models`、`POST /api/models/download|delete|open_models_dir`、
  `POST /api/denoise`、`GET /api/probe`。

### 修复

- **「上级目录」点击无反应**：`/api/fs` 返回的 `data-up` 项前端从未写处理器。
- **只填「到第 N 秒」不裁剪**：分离管线 `-t` 参数挂在 `if e and s` 上，起点为 0 时整段失效。
- **Demucs 模型显示 0 MB**：入口 yaml 仅几十字节，真实体积改为聚合同目录 `<hash>-*.th` 权重。
- **降噪副轨归类错误**：audio-separator 的 `NO_STEM` 是 `"No "`，产物实为 `(No Noise)` 而非 `(NoNoise)`。

### 变更

- 页签顺序重排为 **① 工作流 → ② 音轨分离 → ③ 歌词+时间轴 → ④ 制作跟唱页 → ⑤ 音频降噪 → ⑥ 模型库**，
  全部交叉引用同步改写。
- 能力清单改为「已就绪 / 需下载」两态，模型介绍折叠显示。
- `.gitignore` 的 APK 例外从旧路径 `android/assets/` 修正为 `player/assets/`（此前预编译 APK 实际未入库）。

---

## [1.5] - 2026-10-02

### 变更

- 随面板四大功能（工作流/降噪/模型库/文件浏览器）重新构建，App 本体功能与 v1.4 一致。
- 签名密钥与 v1.4 相同，**可直接覆盖安装，曲库不丢**。

---

## [仓库] 桌面快捷方式指向仓库 · 手工构造 .lnk

### 修复

- **桌面「伴奏分离面板」图标指向的是旧副本**。

  用户怀疑「桌面的面板软件似乎是旧的，检查目录发现是在 workbuddy 的文件夹」—— 查下来确认了，
  而且比预想多一处：面板历史上被复制到**三个**地方，代码版本各不相同。

  | 位置 | 角色 | `serve_separator.py` |
  |---|---|---|
  | `ohwhale-github/panel/` | 正版，随仓库更新 | 46,060 B / 1102 行 |
  | `~/.workbuddy/skills/lyrics-karaoke-studio/` | 技能自带副本 | 39,132 B / 929 行 |
  | `C:\Users\<你>\伴奏分离面板\` | 早期手工部署副本 | 39,132 B / 929 行 |

  桌面 `.lnk` 解析出来的参数指向第三处（`...\伴奏分离面板\serve_separator.py`），
  比仓库版**少 173 行** —— 缺的正是环境自检（`_candidate_env_dirs` / `_find_ffmpeg` /
  `_pick_model_dir` / `env_report`），所以它启动时不打印
  「Python环境 / 模型目录 / ffmpeg」那几行，用户也就无从察觉版本不对。

  由于沙箱禁止 COM（`WScript.Shell`），新增 `tools/scripts/make_panel_shortcut.py`
  按 MS-SHLLINK 规范纯二进制构造 `.lnk`，并顺带提供 `--inspect` 用于排查任意快捷方式的真实指向。

### 新增

- **`bash run.sh shortcut`**：在桌面创建/刷新指向仓库 `panel/` 的快捷方式；
  `--inspect X.lnk` 则打印它解析出的目标、工作目录、图标与逐级 IDList 目录链。
- **`panel/assets/panel.ico`** 纳入仓库，快捷方式默认引用它（不再依赖旧副本目录存活）。
- **`docs/用户手册.md` 新增「四、桌面快捷方式」**：解释三个副本的区别、怎么建新的、怎么查旧的。

### 技术说明

手写 ShellItem 编码踩到一个**字节级**陷阱，已记入 `AGENTS.md` §4.27：

- Dir(0x31) / File(0x32) 项的 `[9..10]` 是 **name 长度（含结尾 NUL）**。
  漏写（置 0）会让 Windows 认为名字是空串，整条 IDList 失效。
- 症状极具迷惑性：**文件本身"能被解析"，自写的校验器也 PASS，但双击静默失败**
  —— `os.startfile` 抛 `WinError 1155 没有应用程序与此操作的指定文件有关联`。
- 对照组是关键：同目录下真实的 `Jupyter Notebook.lnk` 能正常启动，
  排除了"环境问题/关联损坏"。
- 技能 `windows-restricted-env-deploy` 的 `make_lnk.py` 用
  `shell32.ILCreateFromPathW` 拿权威 PIDL，但该 API **在本机沙箱返回 NULL**
  （`SHParseDisplayName` 亦返回 `E_INVALIDARG`），只能降级 —— 降级产物同样是坏快捷方式。
  故改为手写，短名用 `GetShortPathNameW`（不走 shell，可用）。
- **唯一有效的验收方式：`os.startfile(lnk)` 不抛异常。** 字节解析 PASS 不等于能用。

其它要点：Volume item 须补齐到 23 B；目录项只写本级叶子名（不是整条路径）；
StringData 顺序由 LinkFlags 位序决定（NAME→RELATIVE_PATH→WORKDIR→ARGS→ICON）。

### 验证

- `bash run.sh shortcut` → 生成 650 B，`flags=0x000000DF`（含 bit0 `HasTargetIDList`），
  IDList 链 `桌面 > C:\ > Users > Lenovo > OHWHAL~1 > panel > 启动分离面板.bat`。
- `os.startfile` 无异常；真实启动后面板监听 `127.0.0.1:8848`，
  `panel.log` 确认加载的是**仓库**文件（`...\ohwhale-github\panel\assets\separator_panel.html`
  / `...\panel\scripts\studio.py`）、27 个模型权重、ffmpeg 全部自动探测到位。
- `bash run.sh pagetest` 20/20 通过；`bash run.sh check` 全绿。

### 追加修复（同日）：快捷方式一启动就被改小

**现象**：手工建的 `.lnk` 能用（`ShellExecuteW=42`、双击能启动），但**只要启动过一次，
文件就被改小**（650 B → 429 B），IDList 从完整路径链退化成只剩一个 Root 项，
再解析显得"坏了" —— 一开始误判成"快捷方式没建对"。

**真相**：这是 **Explorer 在把文件规范化**，不是失败。它打开自己不完全认同的 `.lnk` 时
会按自己的惯例整份重写。字节变化 ≠ 功能损坏。

**根因**：`LinkInfo` 有三处不合 Explorer 惯例（已记入 `AGENTS.md` §4.28）：

| 字段 | 原值 | 改成 |
|---|---|---|
| `LinkInfoHeaderSize` | `20` | **`28`** |
| `LinkInfoFlags` | `0x01` | **`0x03`** |
| `VolumeID` 卷标 | 写死 `"Windows"` | **真实卷标**（`GetVolumeInformationW`，本机 `Windows-SSD`） |

同时把 `Dir`/`File` 项升级为 Explorer 惯用的**扩展形态**（带 FILETIME、属性、
`BE EF 00 04` 扩展块、UTF-16 原名），进一步降低被重写的概率。

**验证**：修正后连续启动两次，文件稳定在 **1252 B 不再变化**，`ShellExecuteW` 每次均为 42；
解析出的 `ICON` 为 `...\panel\assets\panel.ico,0`，与旧版图标 MD5 一致
（`4594d198ae2245ef2ae81b66d9470133`）。旧版快捷方式与其备份 `伴奏分离面板.lnk.bak` 均未删除。

---

## [仓库] 切轨不再重置进度条 · demo 附中文译文

### 修复

- **切换「混音 / 伴奏 / 人声」时进度条看起来被重置**（`panel/assets/karaoke_page_template.html`）。

  用户报的是「demo 会这样，担心实际也有」—— 查下来是**真 bug**，而且比表面更细：
  `audio.currentTime` 其实一直保住了，**坏的是显示**。
  主循环里进度条只在 `isFinite(audio.duration)` 成立时才更新，
  切轨瞬间 `duration` 变 `NaN`，循环直接跳过 → 进度条冻在旧值（页面刚打开时就是 `0%` / `0:00`）。
  用户看到「条回到 0」，自然理解成"进度被重置了"。

  三处一起修：

  1. **抽出 `paintProgress()`** 作为进度显示的唯一出口。`tNow` 不再依赖 `duration`，
     时长未知时也照常刷新读数。
  2. **`pendingSeek` 替代一次性匿名监听器**。原来的 `loadedmetadata` 只挂一次，
     而实测该事件并非总会触发（缓存命中、快速重设同一 `src` 等），
     恢复位置会被**静默跳过**。现在用模块级变量记待办，
     由 `loadedmetadata` / `durationchange` / `canplay` / `loadeddata` 四个事件
     加 50 ms 轮询共同兜底，谁都可能先到。
  3. **就绪判定用 `readyState >= 1`**（HAVE_METADATA）而不是 `duration > 0`。
     少数编解码组合下 `duration` 仍为 `NaN` 时其实已经可以 seek，
     死等 `duration` 会把恢复无限推迟。

  顺带处理一个真实的边界：**各音轨时长不一致**（本仓库 demo 里伴奏 5:24、人声 0:36.9）。
  进度超出新轨长度时夹到末尾而不是被浏览器弹回 0，
  并给一条会自动消失的中性提示「这条音轨只有 0:36，已跳到末尾」——
  静默跳到末尾最容易被误认为"坏了"。提示条用冷色 `.info` 样式，与载入失败告警区分。

- 载入失败时清空 `pendingSeek`，不再徒劳尝试恢复；错误提示优先于「位置被夹」提示。

### 新增

- **`bash run.sh pagetest`**：跟唱页行为回归。用**假 audio 对象**直测切轨保位置逻辑，
  覆盖 7 组场景 20 项断言：暂停态/播放中切轨保位置、连切不漂移、
  切到更短音轨夹到末尾并提示、元数据晚到时位置不丢也不归零、载入失败不再恢复。

  为什么不用真浏览器：无头 Chrome 里音频解码常不可用（`readyState` 恒为 0），
  根本测不出这层逻辑；而「元数据晚到」「时长更短」这些边界在真浏览器里也难以精确编排。
  测试**从产物 HTML 里 grab 真源码**执行，测的是产品实现而不是另写一份。

- **`examples/demo-translation.txt`**：demo 的逐行中文译文。
  `run.sh demo` 会自动带上（文件存在才带），产物里 9 行歌词全部有中文对译。
  这也顺带演示了「**译文从哪来**」—— 软件不翻译，是你给文件它读进来。

### 变更

- `run.sh` 新增 `pagetest` 子命令；`help` 与未知子命令提示同步更新。
- 修正 demo 中「Switch between original and instrumental.」的译文为
  「可以在「混音 / 伴奏 / 人声」之间切换。」，与页面按钮实际文案一致。

---

## [仓库] 自定义层与制作开关：上传自己的时间轴、页面自主命名添加

### 新增

- **`--layer "名称:文件[:mode]"` 任意自定义层**（可重复）。一次做好，罗马音 / 译文 / 粤拼 /
  生词注释都只是它的特例。三种形态自动判定，判定原则是**时间轴不能被猜**：

  | 输入形态 | 判定 | 行为 |
  |---|---|---|
  | `.lrc` 带 `[mm:ss.xx]` | `timed` | 按时间就近落到对应歌词行，**不要求行数一致** |
  | 多行纯文本 / `.ass` | `lines` | 按行序一一对应，行数不齐时截断/留空并报告 |
  | 单行无换行 | `static` | 整段文本，显示在页面底部，不参与逐行 |

  例：`--layer "粤拼:pinyin.lrc" --layer "注释:notes.txt" --layer "页脚:footer.txt:static"`

- **`--romaji-file` / `--trans-file`**：用户自带时间轴时**跳过本地引擎**，直接采用。
  `--trans-file` 优先级高于 `--trans` 与歌词内嵌译文。

  这两种情况在真实使用里很常见：用户手上已经有别人做好的罗马音/译文轴，
  再跑一遍本地引擎反而是降级。

- **制作开关（适配低配设备 / 产物瘦身）**：`--no-romaji` / `--no-trans` /
  `--no-color` / `--no-timestamps`。不想生成的层直接抽掉，页面不会出现对应内容，
  按钮也会自动隐藏。实测全关后页面 46.3 KB → 44.2 KB，ASS 2070 → 708 字节。

- **页面「+ 添加层」按钮**：制作时没给层，打开页面也能现场加。
  点「+」→ 起名 → 选「每行一段」或「整段文字」→ 立刻出现在工具栏（带自己的显示开关）。
  现场添加的层写 `localStorage`（按曲名分键），下次打开同一页仍在。
  重名会被拦下并提示。

### 修复

- **`initSwitches` 被定义两次**（`panel/assets/karaoke_page_template.html`）。
  上一轮改动时新旧两版都留在了文件里，后一版会覆盖前一版，导致
  「按钮存在但内容为空 → 隐藏按钮」这段逻辑被丢掉：`--no-romaji` / `--no-trans`
  出片后，工具栏会留下点了没反应的空按钮。现合为一版。

- **`--no-color` 导致 ASS 渲染崩溃**（`KeyError: 'jpc'`）。关染色会清空
  `L["jpc"]` / `kk["ct"]` / `L["syl"]` / `kk["st"]`，但 `render_ass()` 仍直接下标访问。
  现改用 `.get(...) or []` 兜底，关染色时 ASS 自动跳过逐字/逐音节行。
  同一问题也存在于 `render_report()` 的音节计数，一并修掉。

- **`timed` 模式时间轴无限沿用最后一条**。层只有 4 条时，
  9 行歌词会全被填成第 4 条的内容。根因是「最后一条没有下一条来界定终点」，
  于是被当成了无限长。修复分三次收敛，最终确定的原则是：
  **最后一条不猜持续时长**，只在 `tol=0.35s` 容差内认为对得上，超出就留空 ——
  宁可少填，也不要凭空造出一条不存在的内容。

- **页面「+」添加静态层与制作注入路径各写一份挂载逻辑**，重复调用会产生重复的
  静态块。现统一交给 `renderLayerRows()` 挂载，并用 `data-ly` 去重。

### 变更

- `META` 新增 `ui.showRo / showCn / color / timestamps` 与 `layers[]`，
  页面按**制作时的设置**初始化各开关，不再出现「明明没生成却显示开」。
- 「染色」总开关：关掉后原文、罗马音都不再逐字/逐音节染色，只保留当前行高亮。

---

## [仓库] 演示素材改为真实三音轨

### 新增

- **多音轨演示**：`examples/` 从「单轨合成音」改为**三条音轨** ——
  `demo-instrumental.mp3`（伴奏，完整 5:24）/ `demo-narration.mp3`（人声，AI 朗诵 37 秒）
  / `demo-mix.mp3`（混音，朗诵叠在伴奏开头）。
  跟唱页上因此出现**「混音 / 伴奏 / 人声」三个可切换按钮**，这是本仓库要演示的核心功能。
- **人声轨用 edge-tts 生成**：逐行合成 9 句英文（`en-US-AriaNeural`，rate `-8%`），
  行间插 700 ms 停顿 → 总长 36.98 秒。逐行合成是为了拿到**行级精确时间戳**，
  一次性合成整段只能拿到词级时间戳，对不上按行排的歌词。

### 修复

- **文件清单的说明文字不跟随 `--label-*`**（`panel/scripts/studio.py`）。
  此前页面按钮按 `--label-orig/inst/vocals` 渲染，但页内「本文件夹内容」清单里
  的说明是**写死的**「原曲（对拍 / 参考唱法）」「伴奏（跟唱用）」「纯人声（扒唱法 / 对音用）」，
  于是出现「按钮写着『混音』、清单写着『原曲』」的自相矛盾。现改为全部跟随参数。
- **页头副标题写死「原曲 / 伴奏」**。改为按实际传入的音轨动态拼接，
  输出如「跟唱页 ・ 卡拉OK 音节染色 ・ 混音 / 伴奏 / 人声」。
- **合成音轨响度过低**：此前的合成命令用了 `volume=0.06`，叠加 `amix` 默认按路数
  分摊增益，峰值只有 **-43.5 dB**，用户按正常音量播放会以为文件损坏。
  现改为 `amix normalize=0` + `volume` + `loudnorm=I=-16:TP=-1.5:LRA=11`，
  峰值回到 **-8.4 dB**。`docs/演示素材与版权.md` 补了两个增益陷阱与自检命令。

### 变更

- `run.sh demo` 改为出三音轨；**缺伴奏时自动降级为单轨**，陌生人 clone 后仍能跑通。
- 删除 `examples/demo-original.mp3`（合成测试音，已被真实素材取代）。
- `examples/README.md` 重写：讲清三条音轨各自是什么、时间轴怎么对齐、
  以及「伴奏是商业作品」的版权提示。

### 验证

- 音轨切换逻辑用假 DOM 实跑 **15 项断言全通过**：
  三个按钮渲染正确、默认高亮项正确、逐个切换后 `audio.src` 指向对应文件、
  切换时保留播放进度与播放态、三个 mp3 文件真实存在。
- `bash run.sh check` 全绿；`bash run.sh demo` 正常出片；
  播放端桌面自检 **47 项 0 失败**。

---

## [仓库] 重定位：伴奏分离面板是主体

### 重大变更

- **重新定位仓库主体**。此前把「电脑制作端 + 手机播放端」当成并列的两半部，
  实际上**主体是伴奏分离面板**（本地 Web 面板），手机 App 只是把做好的成品
  搬到手机上的**最后一环**，不含任何分离或出片能力。文档、结构、README 全部按此重写。
- **全局改名**：`哦鲸鲸` → **`跟唱练习手册`**（仓库名 `ohwhale` → `sing-along-handbook`）
  - 覆盖：所有文档、`AndroidManifest.xml` 应用名、`strings.xml`、App 界面标题与副标题、
    APK 文件名（`跟唱练习手册-播放端-vX.X.apk`）、示例产物
  - **APK 已重新构建**，`aapt2 dump badging` 确认 `application-label:'跟唱练习手册'`，
    包内旧名残留清零

### 目录重构

```
panel/     ★ 主体：伴奏分离面板
player/    ◄── 最后一环：手机播放端（原 android/）
tools/     辅助脚本（原 desktop/skills/ 下的四个技能脚本）
examples/  无版权演示素材（原 desktop/examples/）
```

- 面板核心提到顶层 `panel/`：`scripts/` + `assets/` + 启动脚本
- `android/` → `player/`，明确其「播放端」定位
- `desktop/skills/` 下的四个技能脚本整理进 `tools/scripts/` 与 `tools/references/`
  （原先按技能分目录，实际是流水线各环节的脚本，扁平化更好找）

### 新增

- **环境路径自动探测**（`serve_separator.py`）。原版把 venv 路径写死成作者本机的
  `~/.workbuddy/binaries/python/envs/uvr`，**别人克隆下来必然白屏**。改为五级探测：
  1. `$KARAOKE_UVr_ENV` / `$KARAOKE_UV_ENV` / `$KARAOKE_ENV`（显式指定，优先级最高）
  2. `$KARAOKE_PY_ROOT/envs/{uvr,vocal-separator,audio-separator}`
  3. `<panel>/.venv`、`<repo>/.venv`、`venv`、`env`
  4. `~/.venvs/uvr`、`~/.workbuddy/binaries/python/envs/uvr`
  5. 找不到**不崩** —— 面板照常启动，页面上给出「缺什么 + 怎么补 + 找过哪些位置」
- **ffmpeg 四路探测**：`$KARAOKE_FFMPEG` → `<环境>/bin` → `<环境>/Scripts` → 系统 PATH
- **环境缺失横幅**（面板顶部）：把缺失项与修复命令直接摆在最显眼处，不再白屏
- `docs/安装环境.md`：从零装环境的完整文档（GPU / CPU 两条路线、
  版本钉选理由、常见报错对照表、环境变量一览）
- `panel/README.md`：面板功能全览 + API 一览 + 环境变量 + 技术选择说明
- `panel/启动分离面板.sh`：macOS / Linux 启动脚本（同时兼容 Windows 布局的 `Scripts/`，
  以便在 Git Bash / WSL 下复用已装好的 Windows 环境）

### 修复

- **启动脚本硬编码绝对路径**（`启动分离面板.bat` / `一键做跟唱页.bat`）
  原为硬编码的本机绝对路径，改为相对定位 + 与面板同一套探测顺序，
  找不到时打印安装指引
- `.sh` 启动脚本原先只找 `bin/` 下的解释器，**在 Git Bash 下跑 Windows 环境会误报「找不到环境」**；
  改为 `bin/` 与 `Scripts/` 都找

### 验证

- 面板实测启动：`env_ok=True`、`ffmpeg_ok=True`、12 个可用模型、CUDA 可用
- 纯净机器模拟（清空 HOME 与 PATH）：正确降级，给出可执行的修复指引，不崩溃
- `run.sh check` / `run.sh demo` / 桌面自检 47 项 / APK 构建：全部通过

---

## [仓库] 首次开源准备

### 新增

- **仓库拆成双半部**：`desktop/`（电脑制作端）+ `android/`（手机播放端）
  - 根 `README.md` 重写为全链路门面（架构图 / 九阶段 / 歌词 7 级链 / 实战经验）
  - 新增 `desktop/README.md`：环境搭建、九个阶段、三个关键判断、环境分工、常见问题
  - 新增 `android/README.md`：为什么不能直接丢 HTML、三个关键设计、构建与测试
- **`run.sh` 一键入口**：自动定位三个隔离的 Python 环境与 ffmpeg
  - 子命令：`check` / `demo` / `studio` / `fetch` / `lyrics` / `doctor`
  - `check` 是诊断命令，不依赖任何环境就位即可运行
- **`desktop/skills/`**：收入四个技能（编排层 + 工具层 + KRC 解析 + 人声分离），供 AI 智能体直接加载
- **`desktop/examples/`**：无版权演示素材（ffmpeg 合成音轨 + 自写英文歌词），克隆后即可跑通
- **`AGENTS.md`**：给 AI 智能体的操作手册（结构树 / 任务流程 / 25 条陷阱 / 交付契约）
- `docs/演示素材与版权.md`：四条 demo 素材路线对比与推荐
- `docs/发布到GitHub.md`：六步发布手册
- `LICENSE`（MIT）、`CONTRIBUTING.md`、`.gitattributes`

### 安全

- **签名密钥移出版本控制**（`keystore/` 进 `.gitignore`）
  - 公开密钥 = 任何人可签出**同签名** APK 冒充发布（手机系统会当成同一个 App 的更新直接覆盖安装）
  - `build.sh` 本就支持「没有密钥就自动生成」，陌生人克隆后构建照常可用
  - 本地密钥保留在机器上，你自己的版本仍可覆盖升级
- **`testdata/` 换成程序合成素材**
  - 原先的样例含真实歌曲（mp3 + 歌词 + 官方译文），约 **43 MB 受版权内容**不宜公开
  - 新增 `testdata/make_testdata.py`：ffmpeg 合成正弦波音轨 + 自写英文歌词，以 MIT 分发
  - 一个包放 2 首，同时覆盖「单曲形态」与「批量导入」；**体积从 43 MB 降到 472 KB**
  - 顺带修掉「两个包内容重叠导致同一首被导入两次、断言数虚高」的问题

### 修复

- **构建链路径无关化**：`build.sh` / `run.sh` 原本硬编码绝对路径，换目录即失效
  - 改为 `SCRIPT_DIR → APP_ROOT → REPO` 三级自动定位 + 三级工具链查找
- **桌面自检不幂等**（断言数会自己长大：49 → 54 → 62 → 74）
  - 根因：自检尾部会真正往曲库写曲目，而脚本不清空库目录，残留被下一轮扫进来
  - 修复：每轮开始前重置库目录，留 `KEEP_LIBRARY=1` 逃生阀；现在稳定 47 项
- **自检日志是 GBK 乱码**，`grep` / `tail` 会把它当二进制文件
  - 根因：JDK 17 上 `-Dstdout.encoding` 不生效（要 JDK 18+），真正起作用的是 `-Dfile.encoding`
  - 修复：三个属性一起传；编译诊断单独接走，只在失败时转码输出
- **`DesktopMain.java` 依赖当前工作目录**找 `app/assets/app`，换目录后自检直接退出
  - 修复：新增 `-Drepo=` 参数
- **`.gitignore` 误伤可分发的成品**：`*.apk` 会忽略掉 `android/assets/` 里的正式包，
  `testdata/*.zip` 会忽略掉自检样例 —— 各自加了白名单
- 文档中 `docs/` 相对链接从 `desktop/examples/` 出发少了一层
- `CONTRIBUTING.md` 里的构建路径未跟上目录重整

### 说明

- **仓库内不含任何受版权保护的歌词或音频**；演示素材与自检样例均为程序合成
- 三个 Python 环境（`uvr` / `asr` / `dl`）**不可合并**，`run.sh` 就是为屏蔽这件事而存在

---

## [1.4] - 2026-09-29

### 变更

- **应用图标更换**为蓝发小鲸鱼特写（带「已思考（用时13秒）大烧货」气泡）
  - 图标沿用素材自身白底，内容内缩至安全区，让左上角的气泡完整落在圆形遮罩内
  - 新增特写专用图标生成器 `tools/make_icon_dsh.py`，与全身插画用的 `make_whale_icon.py` 分开
  - 关键修正：**压边（vignette）必须作用在合成之后**，否则会出现「灰相框套白照片」；自适应图标的两层需用同一函数各压一遍

### 说明

- 装完若桌面仍是旧图标，属启动器缓存。卸载重装或重启手机即可（同一签名的覆盖安装一般会自己刷新）
- 签名密钥与 v1.3 相同，**可直接覆盖安装，曲库不丢**

---

## [1.3] - 2026-09-28

在安卓模拟机（Pixel 6 / Android 14）上实测通过。本轮实测抓出并修掉了三个真实缺陷：

### 修复

- **曲库读不出来、界面一直转圈**（最关键）
  - 根因：`@JavascriptInterface` 方法跑在 WebView 的 **JavaBridge 线程** 上，而来源校验里调用了 `webView.getUrl()` —— 该方法强制要求主线程，于是每次调用都抛异常，被前端 `try/catch` 吞掉，表现为「卡在加载中、日志里却没有崩溃」
  - 修复：在主线程把地址缓存进字段，桥接只读字段
- **内置字体没生效**，静默回退成系统字体
  - 根因：拦截回来的字体响应属于跨源资源，缓存响应缺 `Access-Control-Allow-Origin`，被浏览器拦掉
  - 修复：给拦截响应补上跨源许可
- **导入进度条的文件名不显示**
  - 根因：拼 JS 字符串时引号套引号，整段脚本语法报错，进度标题永远停在第一句
  - 修复：改为由统一的参数转义方法组装
- **「删除这首」对某些压缩包一直失败**
  - 根因：把歌曲文件夹里的文件**直接**打包时，跟唱页会落在导入目录的第一层，而删除的安全检查原本要求至少两层深度，于是拒绝执行

### 新增

- `build-tools/desktop-test/` 桌面自检：**47 项断言**，覆盖解压 / 扫描 / Range / 路径穿越 / 删除 / 改名
- `build-tools/check_contract.py` JS ↔ Java 桥接契约静态校验（含两条防回归守卫），已接入构建流程第 4 步

---

## [1.2] - 2026-09-27

### 变更

- 应用更名为 **跟唱练习手册**
- 界面顶栏同步改名，副标题统一为「手机播放端」

---

## [1.1] - 2026-09-27

### 修复

- 启动时偶发显示「桥接未就绪」、点导入无反应
  - 修复：界面改为自己等待并重试，点击会排队等通信就绪，而不是被丢弃

---

## [1.0] - 2026-09-27

### 新增

- 首个版本
- WebView 壳 + 本地 HTTP 服务架构
- zip 批量导入（SAF 文件选择器，零存储权限）
- 曲库管理：列表 / 重命名 / 删除
- 跟唱页：原曲 · 伴奏 · 人声切换、罗马音染色、歌词跟随、变速、单句循环、打轴模式、时间轴微调、歌词搜索、打印页
- 内置字体拦截，完全离线可用

---

[1.5]: ../../releases/tag/v1.5
[1.4]: ../../releases/tag/v1.4
[1.3]: ../../releases/tag/v1.3
[1.2]: ../../releases/tag/v1.2
[1.1]: ../../releases/tag/v1.1
[1.0]: ../../releases/tag/v1.0
