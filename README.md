<div align="center">

**[English README →](README_EN.md)**

<img src="docs/screenshot-icon.png" width="170" alt="跟唱练习手册">

# 跟唱练习手册 · SingAlong

**一个跑在你自己电脑上的伴奏分离面板。**
上传 mp3，出来伴奏和人声 —— 全程本地 AI 推理，音频不离开你的机器。

做好的成品压缩包再推进手机 App，变成随时能翻开的跟唱练习册；电脑端直接点击跟唱页html文件就可以进行练习。

[![Release](https://img.shields.io/github/v/release/Non-sth/sing-along-handbook?style=flat-square&color=4a6fa5)](https://github.com/Non-sth/sing-along-handbook/releases)
[![Downloads](https://img.shields.io/github/downloads/Non-sth/sing-along-handbook/total?style=flat-square&color=2e8b57)](https://github.com/Non-sth/sing-along-handbook/releases)
[![Stars](https://img.shields.io/github/stars/Non-sth/sing-along-handbook?style=flat-square&color=e8b100)](https://github.com/Non-sth/sing-along-handbook/stargazers)
[![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10--3.12-3776ab?style=flat-square&logo=python&logoColor=white)](安装环境.md)
[![CUDA](https://img.shields.io/badge/CUDA-optional%20but%20recommended-76b900?style=flat-square&logo=nvidia&logoColor=white)](安装环境.md)
[![Android](https://img.shields.io/badge/Android-7.0%2B-3ddc84?style=flat-square&logo=android&logoColor=white)](player/README.md)
[![Agent Ready](https://img.shields.io/badge/AI%20agent-ready-8a2be2?style=flat-square)](AGENTS.md)

**能上网 → 只下这一个，双击，等它装完：**
**[⬇ `SingAlong-Setup.exe`（17 MB）](https://github.com/Non-sth/sing-along-handbook/releases/latest/download/SingAlong-Setup.exe)**

**断网 → 上面那个 exe + 下面 5 个全下（共 7.2 GB，6 个文件放同一文件夹）：**
[`part1`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part1.zip)
[`part2`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part2.zip)
[`part3`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part3.zip)
[`part4`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part4.zip)
[`part5`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part5.zip)

<img src="docs/screenshot-library.png" width="220" alt="曲库列表">
<img src="docs/screenshot-practice.png" width="220" alt="跟唱页">
<img src="docs/screenshot-home.png" width="220" alt="桌面图标">

</div>

---

## 🐣 完全不懂代码？从这里开始

**「面板」是什么？** 就是一个网页。你双击一个图标，浏览器自动打开一个页面，
往里面拖歌、点按钮，完事。它不联网上传任何东西，跑在你自己电脑上。

### Windows：只需要三件事——下对文件 → 双击 → 等它装完

> **一句话版**：
> 能上网 → 下 `SingAlong-Setup.exe` → 双击 → 等 25–50 分钟 → 桌面出现「跟唱练习器」→ 双击它开面板。
> 没网 → 再多下 5 个分卷，**6 个文件放同一个文件夹**、把 5 个 zip 都解压到当前文件夹 → 双击同一个 exe。

#### 第 0 步：我该下哪个文件？（只看这一张表）

| 你的情况 | 下哪些文件 | 要解压吗 |
|---|---|---|
| **能上网**（推荐） | 只下 **`SingAlong-Setup.exe`**（17 MB） | 不用 |
| **不能上网 / 网太慢** | 上面那个 exe + `part1`～`part5`（共 7.2 GB，链接都在本页最上面） | 5 个 zip 全部要解压 |

> 另有 `SingAlong-Panel-1.6.2.zip`（487 KB，只换界面）和 `SingAlong-Launcher.exe`（8.9 MB，
> 只要个双击入口）两个小文件，**新手用不到**，需要时看下面的折叠块。

<details>
<summary>❓ 点开看：发布页那 5 项分别是什么？为什么都只有几 MB？</summary>

**5 项逐项对照**（只有前 3 项是你上传的，后 2 项是 GitHub 自己塞进来的）：

| # | 页面上这一项 | 后缀 | 要下吗 | 是什么、给谁 |
|---|---|---|---|---|
| 1 | `SingAlong-Setup.exe`（17.5 MB） | `.exe` | **要**（大多数人只下这个） | 装机版：装环境、装模型、建桌面图标 |
| 2 | `SingAlong-Panel-1.6.2.zip`（487 KB） | `.zip` | 按需 | 面板补丁，21 个文件，只含界面与脚本 |
| 3 | `SingAlong-Launcher.exe`（8.9 MB） | `.exe` | 按需 | 纯启动器，只开面板、不装环境 |
| 4 | `Source code (zip)` | `.zip` | **不要** | GitHub 自动生成的**源码快照**：整个仓库的文字文件，没有 exe、没有模型、没有依赖包，解压出来双击没反应。删不掉，但对你装机零用处 |
| 5 | `Source code (tar.gz)` | `.tar.gz` | **不要** | 同上，只是打包格式不同（Linux 常用），内容一模一样 |

> 一句话记法：**名字里带 `Source code` 的两个 = GitHub 送的源码快照，永远不用下。**
> 多下了、放着不管，**不会影响安装**——安装器只认 exe 旁边有没有 `payload\` 文件夹，别的文件一概不看。

**为什么都只有几 MB？因为这一页放的全是「程序」，不是「资源」。**

| 层次 | 内容 | 在哪 | 多大 |
|---|---|---|---|
| 程序 | 安装器 / 启动器 / 面板 | **最新版页面的 3 个附件** | 共 26 MB |
| 资源（离线） | torch、60 个依赖包、Python 3.12、28 个模型 | **[v1.6.1 页面的 5 个分卷](https://github.com/Non-sth/sing-along-handbook/releases/tag/v1.6.1)** | 共 7.22 GB |
| 资源（在线） | 同上 | 双击 `SingAlong-Setup.exe` 后它自己上网取 | 约 3.6 GB |

- **资源为什么不跟新版本一起发**：① 模型跟面板版本无关，1.6.2 只修了一个 bug，没必要让所有人重下 7 GB；
  ② GitHub 单个附件上限 2 GB（torch 一个包 2.4 GB，所以切成两块），单版本容量也有限。
- 装完之后这 7 GB 会被搬到 `%LOCALAPPDATA%\SingAlong\envs\uvr\`（依赖约 3.6 GB + 模型约 4 GB），
  **解压出来的 `payload\` 就能删了**，等于白捡 7 GB 空间。

</details>

---

#### 方式 A · 在线装机版（1 个文件，最省事）

| 步骤 | 做什么 |
|---|---|
| 1️⃣ 下载 | 只下 **[`SingAlong-Setup.exe`](https://github.com/Non-sth/sing-along-handbook/releases/latest/download/SingAlong-Setup.exe)**（17 MB） |
| 2️⃣ 双击 | **不用解压**，放桌面、放下载文件夹都行。双击后它自己上网取约 3.6 GB 环境和模型 |
| 3️⃣ 等 | 25–50 分钟（看网速）。中途断了直接重跑，已下好的部分会续传 |

<details>
<summary>🐍 点开看：「我已经装过 Python 了，还要再装吗？」</summary>

**要，但不会动你自己的 Python。**

安装器只把你系统里的 Python 当**母版**，用它建一个独立环境
`%LOCALAPPDATA%\SingAlong\envs\uvr`。torch、audio-separator、onnxruntime 全都装进那个环境，
你自己 Python 里装的包一个都不会变，也不需要管理员权限。

- 唯一硬要求是 **3.12**：优先用系统里现成的 3.12，找不到就静默装一个（用户级）。
- 你装的是 3.13 / 3.14 也一样要装 3.12 —— AI 组件只有 3.12 的预编译包，别的版本装不上。
- 你本来就有别的 Python 时，安装器**不改你的 PATH，也不顶掉你的默认 `python` 命令**。
- 离线包 `part5` 里那个 Python 3.12 就是当母版用的，**不是让你拿它写代码**。

</details>

---

#### 方式 B · 离线安装包（6 个文件，断网也能装）

| 步骤 | 做什么 |
|---|---|
| 1️⃣ 下载 6 个 | **[`SingAlong-Setup.exe`](https://github.com/Non-sth/sing-along-handbook/releases/latest/download/SingAlong-Setup.exe)**（17 MB）+ [`part1`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part1.zip) · [`part2`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part2.zip) · [`part3`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part3.zip) · [`part4`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part4.zip) · [`part5`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part5.zip)（合计约 7.2 GB） |
| 2️⃣ 放一起 | 6 个文件**全放进同一个文件夹**，例：新建 `D://跟唱安装包//`。不能分开放 |
| 3️⃣ 解压 | 在**这个文件夹里**把 5 个 zip **全部**「解压到当前文件夹」。别解压成 `part1\` 这种子文件夹 |
| 4️⃣ 双击 | 双击 `SingAlong-Setup.exe`。它看到旁边有 `payload\` 就全程本地安装，**不联网** |

解压完，文件夹必须是这个样子（关键就一条：**`payload` 和 exe 挨在一起**）：

```
D:\跟唱安装包\
├─ SingAlong-Setup.exe                       ← 双击这个（5 个 zip 解压完，留着或删掉都行）
├─ SingAlong-Offline-part1.zip ～ part5.zip   （已解压，同上）
└─ payload\                                   ← 5 个 zip 解压出来的全部离线资源：4 个文件夹 / 93 个文件
   ├─ python\
   │   └─ python-3.12.10-amd64.exe           （Python 3.12 官方安装包，26 MB，当「母版」用）
   ├─ cuda_bootstrap\
   │   ├─ _cuda_dll_bootstrap.pth            （让显卡加速的 DLL 能被找到，缺了会静默退回 CPU）
   │   └─ _cuda_dll_bootstrap.py
   ├─ wheels\                                 （60 个依赖包 + torch 切成的 2 块，共 62 个文件）
   │   ├─ torch-2.14.1+cu126-…whl.chunk001    ← torch 一个包 2.4 GB，超 GitHub 单附件上限
   │   ├─ torch-2.14.1+cu126-…whl.chunk002    ← 被切成两块，安装器会拼回一个文件
   │   ├─ onnxruntime_gpu-1.22.0-…whl         （205 MB，显卡加速）
   │   ├─ audio_separator-0.47.0-…whl         （分离主程序）
   │   └─ …另 50 多个（scipy / numba / librosa / numpy / soundfile / imageio-ffmpeg …）
   └─ models\                                 （28 个模型文件，约 4 GB）
      ├─ bs_roformer_revive.ckpt              ← 默认分离模型（610 MB）+ 同名的 .yaml 配置
      ├─ config_bs_roformer_revive.yaml
      ├─ melband_roformer_inst_v2.ckpt        ← 最高质量档（1502 MB）+ 配套 yaml
      ├─ MelBandRoformer.ckpt                 ← 另一版 MelBand（871 MB）+ 配套 yaml
      ├─ BS-Roformer-Resurrection-Inst.ckpt   （195 MB）+ 配套 yaml
      ├─ …（其余 20 个模型与配置，逐个列在下面的折叠块里）
      └─ download_checks.json / mdx_model_data.json / vr_model_data.json  （模型清单，缺了模型页会空）
```

<details>
<summary>📂 点开看：解压完到底多出哪些文件（逐个写清）</summary>

5 个 zip 解压出来**不是 5 个文件夹，而是合并成同一个 `payload\`**——每个 zip 里的路径都从
`payload\` 开始，所以「解压到当前文件夹」才会自动拼到一起。

合起来一共 **93 个文件 = 1 个 Python 安装包 + 2 个显卡引导脚本 + 62 个 `wheels` 文件 + 28 个模型文件**。

**① `payload\python\`（1 个文件，26 MB）**

| 文件 | 干什么 |
|---|---|
| `python-3.12.10-amd64.exe` | Python 3.12 官方安装包。安装器拿它当**母版**建独立环境，不是让你拿来写代码 |

**② `payload\cuda_bootstrap\`（2 个文件）**

| 文件 | 干什么 |
|---|---|
| `_cuda_dll_bootstrap.pth` + `_cuda_dll_bootstrap.py` | 启动时把 torch 自带的 CUDA DLL 目录注册进搜索路径。**缺了不报错**，但会静默退回 CPU，分离慢十倍 |

**③ `payload\wheels\`（62 个文件 = 60 个依赖包 + torch 被切成的 2 块）**

安装器用 `pip --no-index` 只从这个目录装依赖，全程不联网。体积大的几个：

| 文件 | 大小 | 干什么 |
|---|---|---|
| `torch-2.14.1+cu126-cp312-cp312-win_amd64.whl.chunk001`<br>`torch-2.14.1+cu126-cp312-cp312-win_amd64.whl.chunk002` | 1.85 GB<br>0.66 GB | PyTorch（CUDA 12.6 构建）。整包 2.4 GB 超过 GitHub 单附件 2 GB 上限，只能切两块，安装器会先拼回一个完整 `.whl` |
| `onnxruntime_gpu-1.22.0-cp312-cp312-win_amd64.whl` | 205 MB | MDX-Net 与降噪那几个 onnx 模型靠它上显卡。**必须 1.22.0**，更高版本要 CUDA 13，本机驱动不支持 |
| `audio_separator-0.47.0-py3-none-any.whl` | 0.4 MB | 分离主程序 |
| `scipy` / `numpy` / `numba` / `llvmlite` / `librosa` / `scikit_learn` / `soundfile` / `imageio_ffmpeg` / `torchaudio` / `torchvision` … | 其余 | 剩下的运行依赖，共 50 多个 |

> 那两个 `chunk001` / `chunk002` 看着像「没下完的残文件」，其实**必须两个都在**：
> 只留一块时安装器会报 `is not a valid wheel filename` 直接失败。

**④ `payload\models\`（28 个 = 16 个权重 + 9 个 yaml 配置 + 3 个清单 json）**

| 分组 | 文件 | 说明 |
|---|---|---|
| 二轨 · 人声/伴奏 | `bs_roformer_revive.ckpt`（610 MB）+ `config_bs_roformer_revive.yaml` | **默认模型**，装完就用它 |
| | `melband_roformer_inst_v2.ckpt`（1502 MB）+ `config_melbandroformer_inst_v2.yaml` | 质量最高那一档，吃显存 |
| | `MelBandRoformer.ckpt`（871 MB）+ `config_melbandroformer_inst.yaml` | 另一版 MelBand，用来 A/B 对比 |
| | `BS-Roformer-Resurrection-Inst.ckpt`（195 MB）+ `config_bs_resurrection_inst.yaml` | 伴奏专用，体积小 |
| | `model_bs_roformer_ep_317_sdr_12.9755.yaml`、`model_bs_roformer_ep_368_sdr_12.9628.yaml` | 两版 BS-Roformer 的架构配置 |
| 多轨 · 拆乐器 | 6 个 `.th`：`955717e8-8726e21a.th`、`92cfc3b6-ef3bcb9c.th`、`04573f0d-f3cf25b2.th`、`5c90dfd2-34c22ccb.th`、`d12395a8-e57c48e6.th`、`f7e0c4bc-ba3fe64a.th`（各 80 MB） | Demucs 权重，文件名是哈希，**别改名** |
| | `htdemucs.yaml`、`htdemucs_6s.yaml`、`htdemucs_ft.yaml` | 上面 6 个的配置 |
| 轻量兜底 · MDX/VR | `Kim_Vocal_2.onnx`、`UVR-MDX-NET-Inst_HQ_3.onnx`、`UVR_MDXNET_KARA_2.onnx`（各 50–64 MB） | 老架构，显存紧张时用 |
| 降噪 · 去混响 | `UVR-DeNoise.pth`（121 MB）、`UVR-DeNoise-Lite.pth`（17 MB）、`Reverb_HQ_By_FoxJoy.onnx`（64 MB） | 「降噪」功能用 |
| 模型清单 | `download_checks.json`、`mdx_model_data.json`、`vr_model_data.json` | 每个模型的参数与下载地址表。缺了「⑥ 模型库」会空、分离会直接失败 |

> 这 28 个会被安装器原样复制到 `%LOCALAPPDATA%\SingAlong\envs\uvr\models\`，
> 之后想换模型，只要在那个目录里加减文件即可。

</details>

<details>
<summary>📦 点开看：5 个分卷分别装的是什么</summary>

| 分卷 | 下载体积（GitHub 显示值） | 里面装的东西 |
|---|---|---|
| `part1` | 1.94 GB | **torch 主程序包的前一半**（1850 MB 切块）。torch 整个 2.4 GB，超过 GitHub 单个附件 2 GB 上限，只能切成两块分开装 |
| `part2` | 1.57 GB | **MelBand Roformer v2 分离模型**（1502 MB）——分离质量最高的那一档 |
| `part3` | 1.58 GB | **MelBand Roformer 另一版权重**（871 MB）+ **torch 的后一半**（632 MB） |
| `part4` | 1.91 GB | **13 个模型 + onnxruntime-gpu**：默认模型 `bs_roformer_revive`（610 MB）、`BS-Roformer-Resurrection`（195 MB）、`UVR-DeNoise`（121 MB）、Demucs 五个（各 80 MB）、MDX-Net 与降噪音色四个 onnx；外加 onnxruntime-gpu 1.22（205 MB，显卡加速用） |
| `part5` | 223 MB | **Python 3.12 安装包**（26 MB）+ **其余 59 个依赖 wheel**（scipy、llvmlite、imageio-ffmpeg 等）+ **13 个模型小文件**（yaml 配置、下载清单 json） |
| **合计** | **7.2 GB** | 落在 `payload\` 里共 93 个文件（逐个清单见上面那个折叠块） |

> ⚠️ **分卷是按体积机械切的，不是按功能分的，不能只挑几个下。**
> `part1` 和 `part3` 里装的是**同一个 torch 包的两半**，缺任何一半 pip 都会报
> `is not a valid wheel filename` 直接失败；`part4` 缺了没模型可分离，`part5` 缺了连
> Python 和依赖都装不上。**5 个分卷 + 1 个 exe，六个文件一个都不能少**
> （可以分几次下完，最后凑齐放同一个文件夹就行）。

</details>

> ⚠️ **三种常见错法**（出现任一种，exe 就找不到离线资源，会退化成慢慢联网下载）：
> ① 6 个文件放在了不同文件夹；② 只解压了其中一部分 zip；③ 解压后多套了一层
> （变成 `...\SingAlong-Offline-part1\payload\`）。
>
> **自检一句话：打开文件夹，`payload` 和 `SingAlong-Setup.exe` 在同一层，就对了。**

> ⏳ **双击后先停半分钟、只打印一行「合并离线大包 torch…」——不是卡住。**
> torch 有 2.4 GB，超过 GitHub 单个附件 2 GB 上限，打包时被切成两块，安装器要先拼回一个完整文件。
> 看到这句就等它，别关窗口。

---

#### 装的过程中只会弹两个窗（两种方式都一样）

| 弹窗 | 怎么点 | 点错/不想选怎么办 |
|---|---|---|
| 「**选择安装文件夹**」 | 想换盘就挑一个空文件夹点「确定」；**不想折腾就直接点「取消」** | 取消 = 装到默认位置 `%LOCALAPPDATA%\SingAlong`，完全够用 |
| 「**是否在桌面创建快捷方式？**」 | 点「是」 | 点了「否」也不影响，去安装目录双击 `跟唱练习器.exe` 一样能开 |

**装完之后**：双击桌面**「跟唱练习器」** → 浏览器自动打开面板 → 点「① 工作流」把歌拖进去。

> 已经自己按 [安装环境.md](安装环境.md) 装好 Python 环境的人：不用再下 17MB 装机版，
> 直接用 [`SingAlong-Launcher.exe`](https://github.com/Non-sth/sing-along-handbook/releases/latest/download/SingAlong-Launcher.exe)（8.9 MB，纯启动器）即可。

<details>
<summary>⌨️ 习惯命令行？一条命令下载（PowerShell / cmd 均可）</summary>

```powershell
# 方式 A：在线装机版（17MB，永远指向最新版）
curl.exe -L -o SingAlong-Setup.exe https://github.com/Non-sth/sing-along-handbook/releases/latest/download/SingAlong-Setup.exe

# 方式 B：离线安装包（exe + 5 个分卷，约 6.7GB，请先建好文件夹并 cd 进去）
#   分卷体积大，固定指向 v1.6.1 那一份；以后面板/安装器更新不用重下这堆分卷
curl.exe -L -o SingAlong-Setup.exe https://github.com/Non-sth/sing-along-handbook/releases/latest/download/SingAlong-Setup.exe
for ($i=1; $i -le 5; $i++) {
  curl.exe -L -o "SingAlong-Offline-part$i.zip" "https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part$i.zip"
}

# 解压全部分卷到当前文件夹（Windows 11 自带 tar）
for ($i=1; $i -le 5; $i++) { tar -xf "SingAlong-Offline-part$i.zip" }

# 运行装机程序
.\SingAlong-Setup.exe
```

</details>

---

#### 已经装了旧版本？按「你现在是哪一版」对号入座

**先看一件事**：打开 `%LOCALAPPDATA%\SingAlong\panel\`，**有没有 `VERSION` 这个文件**。
有 → 你装的是 v1.6.1 或更新；没有 → 你装的是 v1.6.0 或更早。

| 你的情况 | 怎么做 |
|---|---|
| 面板右上角有徽章，显示 `v1.6.2` | 已是最新，什么都不用做 |
| 面板右上角有徽章，显示 `↑ v1.6.x` | **点一下那个徽章** → 下载 487 KB 补丁 → 面板自己重启完成升级 |
| **没有徽章**（`panel\VERSION` 不存在 = v1.6.0 或更早） | 这一版必须手动装**最后一次**：下 `SingAlong-Setup.exe` 双击覆盖安装（17 MB）；或把 `SingAlong-Panel-1.6.2.zip` 解压覆盖到 `%LOCALAPPDATA%\SingAlong\panel\`（487 KB）。装完这次之后，以后都能点一下升级 |

> 更新只替换 `panel` 这一个目录。**你做的歌、分离结果、模型都在 `envs\uvr\models\`，一个都不动。**
> 更新完在浏览器里按 **Ctrl+F5** 强刷一次，否则看到的还是旧界面。

<details>
<summary>📂 点开看：面板补丁 zip 解压出来是哪些文件（21 个，注意没有外层文件夹）</summary>

`SingAlong-Panel-1.6.2.zip` 里**没有 `panel\` 这一层**——解压出来就是下面这些，直接铺在根上。
所以**不能**「解压到 `SingAlong-Panel-1.6.2\`」，必须解压进目标目录本身。

| 解压出来的路径 | 是什么 |
|---|---|
| `VERSION` | 版本号，一行纯文本 `1.6.2`。面板新旧就靠它判断 |
| `assets\`（7 个） | `separator_panel.html`（界面本体，175 KB）、`capabilities.json`、`model_catalog.json`、`kanji_readings.json`、`karaoke_page_template.html`、`fat_fish.ico`、`panel.ico` |
| `scripts\`（9 个） | `serve_separator.py`（主程序，148 KB）、`separate_worker.py`、`studio.py`、`lyrics_io.py`、`lyrics_from_video.py`、`probe_lyric_box.py`、`romaji_engine.py`、`english_engine.py`、`llm_client.py` |
| `启动分离面板.bat`、`启动分离面板.sh`、`一键做跟唱页.bat` | 三个启动 / 出片脚本 |
| `README.md` | 面板自己的说明（23 KB） |

正确姿势（二选一）：

1. 右键 zip →「全部解压缩」→ 目标框填 `%LOCALAPPDATA%\SingAlong\panel` → 覆盖确认点「是」；
2. 或先解压到随便一个空文件夹 → 全选 21 项 → 复制 → 粘到 `...\SingAlong\panel\` → 「替换目标中的文件」。

**没解压对的样子**：桌面多出一个 `SingAlong-Panel-1.6.2\` 文件夹，而 `...\panel\VERSION` 还是旧值
→ 面板徽章照样显示 `↑ v1.6.2`，点它还是再下一个同样的补丁。

> 这个 zip **不含**模型、歌、分离结果、Python 环境（才 487 KB），所以覆盖它永远不会弄丢你的东西。

</details>

> 每个文件具体放在哪、放错会有什么症状，见 **[面板资源与升级指南.md](面板资源与升级指南.md)**。

> 手滑删了桌面图标 / 把 exe 挪了位置？去 `%LOCALAPPDATA%\SingAlong\跟唱练习器.exe` 双击照样能开。
> 那个 exe 也没了，就下一个 `SingAlong-Launcher.exe`（8.9 MB）放进同一个目录，再双击。

### macOS：能用，但没有一键安装包

mac 安装包（.app/.dmg）必须在 Mac 电脑上才能制作，作者暂时没有 Mac，
所以 macOS 用户走「5 条命令」路线（约 15 分钟，全可复制粘贴）：
👉 **[安装环境.md · macOS 章节](安装环境.md#macos)**，装完后每次用
`bash panel/启动分离面板.sh` 一条命令启动。

### 想看看软件长什么样？

双击打开 **[项目介绍.html](项目介绍.html)** —— 一份可以在浏览器里翻页的图文幻灯片。

---

## 这是什么

**主体是一个 Web 面板**，跑在你自己的电脑上，浏览器打开 `127.0.0.1:8848` 就能用。

它把原本要敲十几行命令行的本地 AI 人声分离，变成**拖个文件进去点一下**：

```
┌──────────────────────────────────────────────┐
│        伴奏分离面板  panel/                   │  ◄── 主页在这儿
│         http://127.0.0.1:8848                │
│                                              │
│  ① 工作流      全流程编成节点链，一键跑完      │
│  ② 音轨分离    上传 mp3 → 伴奏 / 人声          │
│  ③ 歌词+时间轴  没有歌词？从音频/视频识别      │
│  ④ 制作跟唱页  原唱+伴奏+歌词 → 跟唱页 HTML    │
│  ⑤ 音频降噪    专用降噪模型剥底噪/电流声       │
│  ⑥ 模型库      联网下载模型 · 按显卡分级推荐   │
│  ⑦ 语音台      打字 → 角色语音（可换声线模型） │
│                                              │
│  每页顶部 🚀 GPU 开关 · 环境自检 · 能力清单    │
└──────────────────────────────────────────────┘
          │
          │  做好的成品文件夹（跟唱页 + 音轨 + 字幕）
          ▼
┌──────────────────────────────────────────────┐
│      手机播放端  player/   （最后一环）        │
│      8 MB · 完全离线 · 零存储权限             │
└──────────────────────────────────────────────┘
```

**为什么值得自己搭一套**：现成的卡拉OK App 只能唱它曲库里的歌，
音质、歌词、时间轴都由平台决定。而这条路让你**把任何一首歌变成自己的练习材料** ——
逐字染色、单句循环、变速，而且**素材不出你的电脑**。

> 🛈 **完全不懂代码？** 直接双击打开 **[项目介绍.html](项目介绍.html)** ——
> 一份可以在浏览器里翻页的图文幻灯片，几分钟看懂整个流程。

---

## 🎛️ 主角：伴奏分离面板

### 它解决什么问题

命令行人声分离是这样的：

```bash
python -m audio_separator.separator.cli \
  --model_filename bs_roformer_revive.ckpt --output_dir ./out \
  --output_format mp3 --mp3_bitrate 320 --single_stem instrumental \
  --demucs_segment_size 256 ...（还有十几个参数）
```

参数要查文档、模型名要记、环境要激活、ffmpeg 要配 PATH。
**用完第一次，第二次就忘了上次怎么敲的。**

面板把这些**全部预先固化**：环境在哪、模型有哪些、ffmpeg 装没装、
显存够不够，打开页面就知道；上传文件点一下就跑。
顺带把**能做什么、做不到什么**直接摆在界面上，省掉"试了才发现不行"的反复。

### 能做什么

| | |
|---|---|
| 🔗 **工作流一键全流程** | 把「降噪 → 分离 → 歌词 →（可选 AI 翻译）→ 出片」编成节点链，每个节点可开关、可选模型；**启动前自动预检**，缺什么文件/模型逐项列出，不会白跑 |
| 🎯 **提取伴奏轨** | 去掉人声只留伴奏 —— 跟唱练习的主产物 |
| 🎤 **提取人声轨** | 剥出干声，扒唱法、对音、验证分离质量 |
| 🧹 **音频降噪** | 专用降噪模型（UVR DeNoise 系）剥底噪/电流声/环境轰鸣；可作分离前置工序 |
| 📝 **歌词识别** | 没有歌词文件？从音频/视频里识别：内嵌字幕 → 酷狗 KRC → 画面 OCR → ASR 的优先链 |
| 🔀 **12+ 模型** | RoFormer（质量最高）/ Demucs 四轨六轨 / MDX-Net 轻量 / 卡拉OK 专用 |
| 🌐 **模型库联网下载** | 24 个主流模型一键下载（国内镜像可达）；按你的显卡标注 🟢充裕/🟡偏紧/🔴超出，超出的直接推荐「缩水版」 |
| 🧩 **个人模型识别** | 自己下载的模型丢进文件夹即可：自动识别架构、估算显存、预判能否加载 |
| 📁 **统一文件浏览器** | 所有「选择文件」都打开同一个网页内文件夹浏览器，从盘符逐层进入、随时返回上级 |
| ⚖️ **多模型 A/B** | 同一段音频跑多个模型，产出可同步切换的试听页，切换时保留播放位置 |
| ✂️ **选段处理** | 只分离第 X 秒到第 Y 秒 —— **先跑 30 秒试效果**，别跑完整曲才发现不行 |
| 📚 **排队批处理** | 一次提交多个文件，串行执行（单卡 GPU 串行反而更快） |
| ⚙️ **参数可控** | 格式 MP3/WAV、码率 192–320、只要伴奏/只要人声、segment 尺寸、混合精度 |
| 🔍 **环境体检** | CUDA / 显存 / torch / onnxruntime / ffmpeg 实时状态，缺什么当场告诉你 |
| 🖥️ **桌面快捷方式** | `bash run.sh shortcut` 一键建图标（不依赖 COM）；`--inspect` 可查任意快捷方式真实指向 |
| 📋 **能力清单** | 按「已就绪 / 需下载」两态标注，**不夸大** |
| 🎬 **一键出跟唱页** | 提交原唱+伴奏+歌词 → 跟唱页 HTML + ASS 字幕 + 打印版。**切轨不重置进度**，位置原样保留 |
| 🧩 **任意自定义层** | 罗马音 / 译文 / 粤拼 / 生词注释都能自己传时间轴接进来，页面还能现场「+ 添加层」并命名 |
| 🔌 **用户自带时间轴** | 已经有罗马音或译文轴的，直接上传即用 —— **不跑本地引擎**，再算一遍反倒是降级 |
| 🪶 **制作开关** | 不想生成的层直接不生成：页面、ASS 都更轻，也能适配低配设备 |
| 🎙️ **语音台（文字→语音）** | 打字就能出声：edge-tts 在线基底音 + 本地 DDSP-SVC 声线转换；8 种语气预设、AI 情感理解（先理解再说话）、一句多抽卡挑最好的、可换自己下载的声线模型，也能选「Edge 裸声线」秒出不加载模型 |
| 🚀 **每页独立 GPU 开关** | 分离/歌词/降噪/语音台各自可切 GPU/CPU；工作流等页有全流程总开关；显卡型号实时探测，换台电脑显示它的卡 |
| 🤖 **大模型设置（可选）** | 语音台的情感理解、歌词 AI 翻译都走它：DeepSeek 出厂内置只填 key，其他厂商（OpenAI 兼容）可自定义；**key 只存你电脑的用户目录，不进仓库** |
| 🈂️ **AI 翻译歌词 + 罗马音校检** | 工作流里的节点：大模型翻译外语歌词，顺手校检本地罗马音引擎的误拆并标红；产出双语 LRC 直接喂给出片 |

### 能力边界

诚实比夸大有用。这些是**已知边界**，不是 bug：

| 限制 | 原因 |
|---|---|
| **无法零残留** | 镲片、军鼓与人声齿音同占 4–8 kHz，伴奏高频必有"水声"样伪影；男声中低频与吉他贝斯重叠在 100–400 Hz，伴奏低频可能发闷。这是频域分离的相位不确定性所致，换模型只能减轻 |
| **不适合直接发布翻唱作品** | 伪影一进混音就露馅。要发布只能买官方 off vocal 轨。**自己练习则完全够用** |
| **不能破解 DRM 容器** | 酷狗 `.kgm` / `.mgg` 用流密码，非简单循环 XOR。正确做法是在客户端先导出明文，再拖进面板 |
| **不能实时、不能分任意乐器** | 离线推理，2:51 曲目约 50 秒；除模型支持的轨道外，无法凭空拆出"小提琴""合成器"等任意声部 |
| **系统内存是真瓶颈** | 权重在显存，但音频缓冲需 1.5–2 GB 系统内存。跑之前先关浏览器/通讯软件/播放器 |

### 快速开始

```bash
# ① 装环境（首次，约 15–30 分钟）—— 详见 安装环境.md
# ② 启动
panel\启动分离面板.bat          # Windows：双击
bash panel/启动分离面板.sh      # macOS / Linux
```

浏览器自动打开 `http://127.0.0.1:8848/`，看到顶部一排**绿色**状态条就成了。

> **没有 NVIDIA 显卡也能用**，只是慢 —— 同样一首 2:51 的曲子，
> GPU 约 50 秒，CPU 要 15–40 分钟。选路线的方法见
> [安装环境.md 第零节](安装环境.md#零先想清楚一件事你要用-cpu-还是-gpu)。

### 本机实测性能

| | |
|---|---|
| 硬件 | RTX 4060 Laptop (8 GB) + Ryzen 7 8845H |
| 30 秒片段 | 加载 3.7 s + 分离 7.1 s |
| 2:51 整曲 | 约 50 秒 |
| 显存峰值 | 3225 MB |
| 模型加载 | 3–30 秒（Demucs 更久） |

**面板不写死任何路径** —— 环境探测按
`环境变量 → 仓库内 .venv → 常见位置` 逐级找，找不到也不崩，
而是在页面上给出「缺什么 + 怎么补 + 找过哪些位置」。

---

## 📱 最后一环：手机播放端

面板做出来的成品是**一个文件夹**，里面是跟唱页 HTML 和几条音轨。
手机 App 负责把它搬进口袋。

### 为什么不能直接把 HTML 丢进手机

在电脑上做跟唱页很容易，**但手机上不行**。无论你把 HTML 传进手机、丢进网盘、
还是用某笔记 App 打开，都会撞上同一堵墙：

- 页面里的相对路径全部失效（`file://` 是不透明源）
- **音频进度条拖不动**（`file://` 的 HTTP Range 支持不可靠）
- 字体、样式悄悄降级成系统默认

App 的做法是**在 App 里跑一个只监听 `127.0.0.1` 的本地 HTTP 服务**来伺服你的歌曲文件夹：

> **曲目文件夹的目录结构和页面里的相对路径原样可用 —— 跟唱页一行都不用改。**

### 特性

| | |
|---|---|
| 🎤 原曲 / 伴奏 / 人声切换 | 跟唱、清唱、听人声 |
| 🎨 罗马音 · 逐音节染色 | 假名对齐到音节 |
| 📜 歌词跟随滚动 | 行级滚动 + 单句高亮 |
| ⏩ 变速播放 · 🔁 单句循环 | 慢下来磨那卡住的一句 |
| ⏱️ 打轴模式 | 时间轴微调 ±0.1s |
| 📦 批量导入 | 一个 zip 放多首歌，支持多选 |
| 📶 完全离线 · 🔐 零存储权限 | 字体在包里；导入走系统文件选择器 |

去 [Releases](https://github.com/Non-sth/sing-along-handbook/releases) 下载 `SingAlong-Player-Android-vX.X.apk`，
或直接取仓库里 [`player/assets/跟唱练习手册-播放端-vX.X.apk`](player/assets/)（同一个文件，仓库内保留中文名），传到手机，
文件管理器点开安装即可。Android 7.0+，不联网，不装别的。

> 首次安装提示红字是正常的 —— APK 用自签名证书，不是 Google Play 分发。

详见 **[player/README.md](player/README.md)** 与 **[用户手册](用户手册.md)**。

---

## 🔧 可选：完整制作链路

面板已经覆盖了日常使用。不过面板背后还有一套更完整的流水线，
适合**从零开始**处理一首歌（比如从 B 站链接开始、歌词要 OCR 抠）。

### 九个阶段

| 阶段 | 做什么 | 判定门 |
|---|---|---|
| **S0** 定界 | 一句话任务卡 | 说得清输入/输出/语言 |
| **S1** 取源 | 拿到本地音频轨 | `ffmpeg -i` 读得出时长 |
| **S1.5** 素材体检 | （可选）降噪 / 修削波 | 问题清单为空 |
| **S2** 歌词获取 | 拿到歌词文本 | 过「歌词性校验」 |
| **S3** 时间轴 | 行级或逐字轴 | 首行时间不是 `16:34` |
| **S4** 分离 | `_伴奏` / `_人声` | 两轨存在且**不是同一个文件** |
| **S5** 出片 | 跟唱页 + ASS + 报告 | **报告已读**，待办为 0 |
| **S6** 校验 | 断言 + 截图 | 断言全过 + 视觉不错位 |
| **S7** 打包 | 独立目录 | 不依赖仓库目录 |
| **S8** 归档 | 干净的作品目录 | 中间文件已清理 |

### 歌词从哪来：7 级优先链

**从"免费且精确"往"昂贵且易错"找，找到就停。**

| 优先级 | 来源 | 精度 | 成本 |
|---|---|---|---|
| 1 | 用户直接给的歌词文件 | 最高（常带逐字轴） | 0 |
| 2 | 视频容器里的内嵌字幕轨 | 高 | 极低 |
| 3 | **本地酷狗 `.krc`** | **逐字轴 + 官方罗马音 + 官方译文 三合一** | 极低 |
| 4 | B站 CC 字幕 API | 中高 | 低 |
| 5 | 视频简介 / 置顶评论 | 低（无时间轴） | 低 |
| 6 | **画面 OCR**（硬字幕） | 文本准、时间粗 | 中 |
| 7 | **ASR**（faster-whisper） | 时间准、文本有幻觉 | 中高 |

**第 3 级是性价比之王** —— 一条 KRC 让取词、对轴、翻译**三道工序全部免做**。
但它不在音频旁边，文件名带 32 位哈希，**得按歌名关键词模糊搜**。

### 两条最有价值的实战经验

**① OCR 定文本，ASR 定边界 —— 不要二选一**

硬字幕场景下，OCR 的文本几乎无错（画面上就摆着）但时间粗；ASR 时间准但文本会幻觉。
正确做法是**每行起点用 OCR 帧级时间，末行终点用 ASR 段终点**。
（试过"按字数均分"和"用 ASR 段终点"，都会整段前移。）

**② 混音上 ASR 全灭，不代表没人声**

整轨混音 + VAD 过滤会让 Whisper 只吐一句「感谢观看」幻觉。
**正确顺序是先分离出人声轨再重跑 ASR** —— 同一模型立刻给出 42 句完整歌词。
别在混音上反复换模型/语言/VAD 参数，那三条路都试过，全部失败。

### 命令行入口

`run.sh` 会自动找到正确的 Python 环境与 ffmpeg：

```bash
bash run.sh check     # 环境自检：三个环境 + 包 + ffmpeg + CUDA 引导
bash run.sh demo      # 出三音轨跟唱页（混音 / 伴奏 / 人声 可切换）
bash run.sh doctor    # 素材体检：采样率/位深/削波/静音段
bash run.sh fetch     # 取源（yt-dlp）
bash run.sh lyrics    # 从视频抠歌词（OCR + ASR）
```

出片后打开 `examples/out/Demo Song_跟唱页.html` 即可看到成品。

---

## 🚀 完整工作流

最省事的方式是面板的**「① 工作流」页签**：选好源音频，把「降噪 → 分离 → 歌词 →
（外语歌可插「AI 翻译歌词」）→ 出片」编成一条节点链一键跑完；启动前会自动预检，
缺歌词、缺模型会逐项告诉你，不会白跑。

想分步精细控制也行：

```bash
# 1. 电脑上：打开面板，「② 音轨分离」上传歌曲，分离出伴奏
#    （或走上面的完整链路，从视频/链接开始）

# 2. 「④ 制作跟唱页」：提交 原唱+伴奏+歌词 → 出跟唱页
#    （出片时勾选「打包手机端 zip」可跳过第 3 步）

# 3. 把整个文件夹压成 zip

# 4. 传到手机（微信文件传输助手 / 数据线 / 网盘都行）

# 5. 手机上：导入 → 练
```

**App 认的锚点是「文件名以 `_跟唱页.html` 结尾」的文件** —— 文件夹名不算数，会递归找，
中文文件名没问题，一个 zip 放多首歌也行。

---

## 📁 项目结构

> **关于源码**：下表里带 ★ 的程序部分（`panel/` `player/` `tools/` `run.sh`）在**私有源码仓** `sing-along-handbook-dev` 里，
> 公开仓只放**文档 + 安装包**。想参与开发见下面的 [🤝 参与](#-参与)。

```
sing-along-handbook/
├── panel/                            ★ 主角：伴奏分离面板
│   ├── README.md                     功能全览 + API + 环境变量
│   ├── scripts/
│   │   ├── serve_separator.py        服务端（标准库 http.server，零框架依赖）
│   │   ├── studio.py                 出片引擎（跟唱页 + ASS + 打印版）
│   │   ├── romaji_engine.py          日语 → 罗马音，逐音节切分
│   │   ├── english_engine.py         英语音节切分 + 中文译文
│   │   └── lyrics_io.py              歌词读写（krc/lrc/ass/srt/txt）
│   ├── assets/
│   │   ├── separator_panel.html      前端界面（单文件、零依赖、离线可用）
│   │   ├── capabilities.json         能力清单与模型元数据
│   │   ├── model_catalog.json        模型库下载目录（24 个主流模型，镜像源）
│   │   └── karaoke_page_template.html
│   ├── 启动分离面板.bat / .sh        一键启动（自动探测环境）
│   └── 一键做跟唱页.bat              拖两个文件上去即出片
│
├── player/                           ◄── 最后一环：手机播放端
│   ├── README.md
│   ├── app/                          源码（Java + 单文件 HTML 界面）
│   ├── build-tools/                  手工构建链（不用 Gradle）
│   ├── tools/                        图标生成脚本
│   └── assets/                       预编译 APK
│
├── tools/                            辅助脚本（可选，面板没覆盖的场景）
│   ├── scripts/                      fetch_source / lyrics_from_video / audio_doctor …
│   └── references/                   各环节的详细规则文档
│
├── examples/                         无版权演示素材（克隆后即可跑通）
├── run.sh                            ★ 命令行一键入口
├── 项目介绍.html                   ★ 不懂代码也能看：HTML 幻灯片讲清整个过程（双击即用）
├── 项目介绍_EN.html                英文版项目介绍（English intro slideshow）
├── 安装环境.md                     ★ 从零装环境（含排错对照表）
├── 用户手册.md                     手机端使用
├── 仓库文件说明书.html              每个文件干什么
├── 演示素材与版权.md
├── 发布到GitHub.md
├── docs/                           README 用的界面截图
├── AGENTS.md                         ★ 给 AI 智能体的自动化指南
└── CHANGELOG.md / CONTRIBUTING.md / LICENSE
```

---

## 🤖 这个项目为 AI 智能体做好了准备

仓库包含一份 **[AGENTS.md](AGENTS.md)** —— 写给 AI 编程智能体（Claude Code / CodeBuddy / Cursor 等）看的操作手册。

把它连同仓库丢给智能体，它能读懂项目结构、知道构建命令、知道 30+ 个不能踩的坑，
从而**自动完成**：

```
「帮我给这首歌做个跟唱页」
  → 判断输入形态 → 走歌词优先链 → 选时间轴策略 → 分离 → 出片 → 读报告回填 → 校验

「帮我换个 App 图标」
  → 判断素材类型（特写 vs 插画）→ 选对脚本 → 生成五密度图标 → 构建 → 模拟机验证
```

---

## 🤝 参与

**这个项目用「公开仓 + 私有源码仓」两个仓库运作**，既不把全部代码摊开，也保证想一起做的人有路可走：

| 仓库 | 可见性 | 放什么 |
|---|---|---|
| [`sing-along-handbook`](https://github.com/Non-sth/sing-along-handbook) | 公开 | 文档、安装包（Release）、Issue、讨论 —— **所有人**都能看和下载 |
| `sing-along-handbook-dev` | 私有 | 完整源码、构建链 —— 邀请制，成为协作者后才能看和提交 |

### 三条参与路径

**① 任何人都能做（不用源码权限）**

- 报 bug、提需求：开 [Issue](../../issues)，附上你的系统、报错截图、复现步骤
- 改文档 / 翻译 / 写教程：文档就在公开仓，直接提 PR
- 推荐好用的分离模型：开 Issue 附上模型下载页与文件名，维护者会加进模型库

**② 想长期一起开发**

在 [Issue](../../issues) 或 Discussion 里说明**你想做什么、大概怎么做**，维护者看到后会把你的
GitHub 账号加进私有源码仓（Settings → Collaborators，个人账号不额外收费），之后你就能正常提 PR。

**③ 只想要功能不想要代码**

直接开 Issue 描述场景就行，需求描述得越具体越容易被实现。

### 特别欢迎

新的分离模型接入、非日语/英语的语言支持（韩语罗马音、粤语拼音…）、
界面主题、更好的歌词来源。

**两个硬约束**（提 PR 前请确认不违反）：
面板保持**零 Web 框架依赖**（只用标准库）；手机端保持**完全离线**。

---

## 📄 许可与版权

代码 [MIT](LICENSE)，随便用（含商用）。APK 里的字体（Noto Serif JP、Inter）为 SIL Open Font License。

**⚠️ 关于内容版权**：取词、分离、翻译三条链路**全部受版权约束**。

- 仓库里**不包含任何受版权保护的歌词或音频**
- `examples/` 与 `testdata/` 里都是程序合成的音轨 + 自写歌词，可自由使用
- 自己做、自己练属于个人使用；**公开分享成品页 / 音频 / 歌词属于复制与传播**
- 生成页面的页脚自带免责声明，请不要删掉

详见 [演示素材与版权.md](演示素材与版权.md)。

**🔐 关于签名密钥**：仓库里**不含签名密钥**（`.gitignore` 已排除 `keystore/`）。
公开密钥等于让任何人能签出**同签名** APK 冒充发布，所以每个构建者用自己的。
`build.sh` 检测到没有密钥会**自动生成一个** —— 记得备份。

---

<div align="center">

**如果这个项目帮你把练习搬到了自己手里，点个 ⭐ 就是最好的支持。**

</div>
