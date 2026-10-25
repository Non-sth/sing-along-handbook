# SingAlong · Karaoke Practice Handbook

[中文 README](README.md)

**A local AI vocal-separation panel that runs on your own computer.**
Drop in an mp3, get back the instrumental and the vocals — all inference happens locally,
your audio never leaves your machine. The finished song packs can be pushed into the
companion Android app as a karaoke practice book you can flip through anywhere.

[![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10--3.12-3776ab?style=flat-square&logo=python&logoColor=white)](安装环境.md)
[![CUDA](https://img.shields.io/badge/CUDA-optional%20but%20recommended-76b900?style=flat-square&logo=nvidia&logoColor=white)](安装环境.md)
[![Android](https://img.shields.io/badge/Android-7.0%2B-3ddc84?style=flat-square&logo=android&logoColor=white)](player/README.md)

**There is only one install path: download all 6 files below (7.2 GB) → same folder → unzip all 5 zips → double-click the exe.**
**[⬇ `SingAlong-Setup.exe` (17 MB)](https://github.com/Non-sth/sing-along-handbook/releases/latest/download/SingAlong-Setup.exe)**
**+ these 5:**
[`part1`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part1.zip)
[`part2`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part2.zip)
[`part3`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part3.zip)
[`part4`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part4.zip)
[`part5`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part5.zip)

> 🌐 The panel UI has a **Chinese/English toggle** (top-right 🌐 button).

---

## What this is

The core is a **web panel** running on your own machine — open `http://127.0.0.1:8848`
in your browser and use it:

```
┌────────────────────────────────────────────────┐
│        Separation panel   panel/               │  ◄── main interface
│         http://127.0.0.1:8848                  │
│                                                │
│  ① Workflow     chain the whole pipeline into  │
│                 nodes, run in one click        │
│  ② Separation   upload mp3 → instrumental /    │
│                 vocals                         │
│  ③ Lyrics+timing  no lyrics? recognize them    │
│                 from audio/video               │
│  ④ Karaoke page  original + instrumental +     │
│                 lyrics → karaoke HTML          │
│  ⑤ Denoise      dedicated models strip hiss/   │
│                 hum from recordings            │
│  ⑥ Models       download models online,        │
│                 ranked by your GPU             │
│  ⑦ Voice booth  type text → character voice,   │
│                 swappable voice models         │
│                                                │
│  per-tab 🚀 GPU toggle · env self-check ·      │
│  capability list · built-in ffmpeg             │
└────────────────────────────────────────────────┘
          │
          │  finished song folder (karaoke page + stems + subtitles)
          ▼
┌────────────────────────────────────────────────┐
│      Android player   player/   (final step)   │
│      8 MB · fully offline · zero storage       │
│      permissions                               │
└────────────────────────────────────────────────┘
```

**Why bother self-hosting**: karaoke apps only let you sing what's in their catalog,
with the platform deciding audio quality, lyrics and timing. This pipeline turns
**any song into your own practice material** — per-syllable highlighting, loop-one-line,
variable speed — and your files never leave your computer.

---

## Quick start

### Windows — the easy way (recommended for non-developers)

**Install path (only one): download 6 files → one folder → unzip all 5 zips → double-click the exe.**

**Step 0 — the 6 files you need**

| File | Size | What it is |
|---|---|---|
| `SingAlong-Setup.exe` | 17 MB | The installer itself (you double-click this) |
| `part1` – `part5` | 7.2 GB total | Wheels + all 28 models (offline assets — **download all five, no picking**) |

All 6 download links are **at the top of this page**.

> Two other small files — `SingAlong-Panel-1.6.2.zip` (487 KB, panel only) and
> `SingAlong-Launcher.exe` (8.9 MB, launcher only) — are **not needed for a first install**.
> See the collapsible section below when you need them.
>
> **Why isn't there a "just download the 17 MB exe and let it fetch everything" option?** Because that
> pulls ~3.6 GB live from GitHub, which in practice often stalls or fails. **Downloading the 6 files is
> simply more reliable**, so that route was removed from the docs.

<details>
<summary>❓ What are the 5 items on the release page? Why is everything only a few MB?</summary>

| # | Item on the page | Suffix | Download? | What it is |
|---|---|---|---|---|
| 1 | `SingAlong-Setup.exe` (17.5 MB) | `.exe` | **yes** | Full installer: sets up the environment, models and desktop icon (also used by the offline route) |
| 2 | `SingAlong-Panel-1.6.2.zip` (487 KB) | `.zip` | optional | Panel patch, 21 files: UI + scripts only |
| 3 | `SingAlong-Launcher.exe` (8.9 MB) | `.exe` | optional | Launcher only — opens the panel, installs nothing |
| 4 | `Source code (zip)` | `.zip` | **no** | **Source snapshot** GitHub generates automatically: plain text files of the whole repo. No exe, no models, no wheels — double-clicking does nothing. Cannot be deleted, and is useless for installing |
| 5 | `Source code (tar.gz)` | `.tar.gz` | **no** | Same thing, different packaging format (Linux-friendly) |

> Rule of thumb: **anything named `Source code` is an auto-generated snapshot — never download it.**
> Downloading it anyway and leaving it in the folder **does not affect installation** — the installer only
> looks for a `payload\` folder next to the exe and ignores everything else.

**Why so small? Because this page ships *programs*, not *assets*.**

| Layer | Content | Where | Size |
|---|---|---|---|
| Program | installer / launcher / panel | **the 3 assets on the latest release** | 26 MB |
| Assets | torch, 60 wheels, Python 3.12, 28 models | **the 5 `part` volumes** | 7.22 GB |

- **Why assets are not re-released every version**: ① models are independent of the panel version — v1.6.2
  fixes one bug, no reason to make everyone re-download 7 GB; ② GitHub caps a single asset at 2 GB
  (torch alone is 2.4 GB, hence the two chunks) and caps total release size.
- After installation that 7 GB is moved into `%LOCALAPPDATA%\SingAlong\envs\uvr\`
  (~3.6 GB dependencies + ~4 GB models), so **you can delete `payload\` afterwards** and reclaim 7 GB.

</details>

<details>
<summary>🐍 Before you start: "I already have Python — do I still need this one?"</summary>

> 🐍 **"I already have Python — do I still need this one?" Yes, but your own Python stays untouched**
>
> The installer only uses your system Python as a **template** to create a **private virtualenv**
> (`%LOCALAPPDATA%\SingAlong\envs\uvr`). torch, audio-separator and onnxruntime all go into that
> venv — nothing is installed into your own Python, and no admin rights are needed.
>
> The one hard requirement is **3.12**: it looks for a 3.12 first and silently installs one (per-user)
> if there is none. Having 3.13 / 3.14 does not help — the AI components only ship prebuilt wheels for
> 3.12. If you already have another Python, the installer **leaves your PATH and your default `python`
> command alone**. That is exactly what the Python 3.12 installer inside `part5` is for: **it is a
> template, not an interpreter you are meant to write code with.**
</details>

#### Install steps (4 steps — the only route)


| Step | Do this |
|---|---|
| 1️⃣ | Download all six: [`SingAlong-Setup.exe`](https://github.com/Non-sth/sing-along-handbook/releases/latest/download/SingAlong-Setup.exe) (17 MB) + [`SingAlong-Offline-part1.zip`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part1.zip) … [`part5.zip`](https://github.com/Non-sth/sing-along-handbook/releases/download/v1.6.1/SingAlong-Offline-part5.zip) (~7.2 GB total) |
| 2️⃣ | Put **all six in the same folder**, e.g. `D:\singalong-setup\` — do not split them up |
| 3️⃣ | Inside that folder, extract **all five** zips **into the current folder** (do **not** extract into a `SingAlong-Offline-part1\` subfolder) |
| 4️⃣ | **Double-click `SingAlong-Setup.exe`** → seeing `payload\` next to it, it installs entirely offline |

The folder must look like this — key point: **`payload` sits next to the exe**.

```
D:\singalong-setup\
├─ SingAlong-Setup.exe              ← double-click this one
├─ SingAlong-Offline-part1.zip … part5.zip   (already extracted; keep or delete)
└─ payload\                          ← everything the 5 zips produce: 4 folders / 93 files
   ├─ python\
   │   └─ python-3.12.10-amd64.exe   (official Python 3.12 installer, 26 MB — used as the "parent" runtime)
   ├─ cuda_bootstrap\
   │   ├─ _cuda_dll_bootstrap.pth    (makes torch's CUDA DLLs findable; missing ⇒ silently falls back to CPU)
   │   └─ _cuda_dll_bootstrap.py
   ├─ wheels\                         (60 dependency wheels + torch split in 2 chunks = 62 files)
   │   ├─ torch-2.14.1+cu126-…whl.chunk001   ← torch is 2.4 GB, above GitHub's 2 GB per-asset cap
   │   ├─ torch-2.14.1+cu126-…whl.chunk002   ← two halves, joined back by the installer
   │   ├─ onnxruntime_gpu-1.22.0-…whl        (205 MB, GPU acceleration)
   │   ├─ audio_separator-0.47.0-…whl        (the separation engine)
   │   └─ …50-odd more (scipy / numba / librosa / numpy / soundfile / imageio-ffmpeg …)
   └─ models\                         (28 files, ~4 GB)
      ├─ bs_roformer_revive.ckpt      ← default separation model (610 MB) + config_bs_roformer_revive.yaml
      ├─ melband_roformer_inst_v2.ckpt  ← highest quality tier (1502 MB) + its yaml
      ├─ MelBandRoformer.ckpt         ← the other MelBand checkpoint (871 MB) + its yaml
      ├─ BS-Roformer-Resurrection-Inst.ckpt  (195 MB) + its yaml
      ├─ …(the remaining 20 weights/configs are listed in the collapsible block below)
      └─ download_checks.json / mdx_model_data.json / vr_model_data.json  (model manifests)
```

<details>
<summary>📂 Click to see exactly which files the zips produce</summary>

The 5 zips do **not** create 5 folders — every entry inside them starts with `payload\`, so
"extract to the current folder" merges them into a single `payload\`.

Total: **93 files = 1 Python installer + 2 GPU bootstrap scripts + 62 `wheels` files + 28 model files**.

**① `payload\python\` (1 file, 26 MB)**

| File | Purpose |
|---|---|
| `python-3.12.10-amd64.exe` | Official Python 3.12 installer. The installer uses it as a **parent runtime** to build an isolated venv — it is not meant for writing your own code |

**② `payload\cuda_bootstrap\` (2 files)**

| File | Purpose |
|---|---|
| `_cuda_dll_bootstrap.pth` + `_cuda_dll_bootstrap.py` | Registers torch's bundled CUDA DLL folders at startup. **No error if missing**, but inference silently runs on CPU — about ten times slower |

**③ `payload\wheels\` (62 files = 60 dependency wheels + 2 torch chunks)**

Everything is installed with `pip --no-index` from this folder, fully offline. The big ones:

| File | Size | Purpose |
|---|---|---|
| `torch-2.14.1+cu126-cp312-cp312-win_amd64.whl.chunk001`<br>`…chunk002` | 1.85 GB<br>0.66 GB | PyTorch (CUDA 12.6 build). 2.4 GB total, split in two because of GitHub's 2 GB per-asset cap; the installer joins them first |
| `onnxruntime_gpu-1.22.0-cp312-cp312-win_amd64.whl` | 205 MB | Runs the MDX-Net / denoise onnx models on the GPU. **Must be 1.22.0** — newer builds need CUDA 13 |
| `audio_separator-0.47.0-py3-none-any.whl` | 0.4 MB | The separation engine |
| `scipy` / `numpy` / `numba` / `llvmlite` / `librosa` / `scikit_learn` / `soundfile` / `imageio_ffmpeg` / `torchaudio` / `torchvision` … | rest | The remaining runtime dependencies, 50-odd in total |

> The two `chunk001` / `chunk002` entries look like partial downloads, but **both are required** —
> with only one half the installer fails with `is not a valid wheel filename`.

**④ `payload\models\` (28 files = 16 weights + 9 yaml configs + 3 manifest json)**

| Group | Files | Notes |
|---|---|---|
| 2-stem · vocals/instrumental | `bs_roformer_revive.ckpt` (610 MB) + `config_bs_roformer_revive.yaml` | **Default model**, used right after install |
| | `melband_roformer_inst_v2.ckpt` (1502 MB) + `config_melbandroformer_inst_v2.yaml` | Highest-quality tier, heavy on VRAM |
| | `MelBandRoformer.ckpt` (871 MB) + `config_melbandroformer_inst.yaml` | The other MelBand variant, for A/B tests |
| | `BS-Roformer-Resurrection-Inst.ckpt` (195 MB) + `config_bs_resurrection_inst.yaml` | Instrumental-focused, small |
| | `model_bs_roformer_ep_317_sdr_12.9755.yaml`, `model_bs_roformer_ep_368_sdr_12.9628.yaml` | Architecture configs for the two BS-Roformer releases |
| Multi-stem · instrument split | 6 `.th` files: `955717e8-8726e21a.th`, `92cfc3b6-ef3bcb9c.th`, `04573f0d-f3cf25b2.th`, `5c90dfd2-34c22ccb.th`, `d12395a8-e57c48e6.th`, `f7e0c4bc-ba3fe64a.th` (80 MB each) | Demucs weights; the names are hashes, **do not rename** |
| | `htdemucs.yaml`, `htdemucs_6s.yaml`, `htdemucs_ft.yaml` | Configs for the six above |
| Lightweight fallback · MDX/VR | `Kim_Vocal_2.onnx`, `UVR-MDX-NET-Inst_HQ_3.onnx`, `UVR_MDXNET_KARA_2.onnx` (50–64 MB each) | Older architectures for low-VRAM machines |
| Denoise / dereverb | `UVR-DeNoise.pth` (121 MB), `UVR-DeNoise-Lite.pth` (17 MB), `Reverb_HQ_By_FoxJoy.onnx` (64 MB) | Used by the "denoise" feature |
| Manifests | `download_checks.json`, `mdx_model_data.json`, `vr_model_data.json` | Per-model parameters and download tables. Without them the model library tab is empty and separation fails |

> All 28 are copied verbatim into `%LOCALAPPDATA%\SingAlong\envs\uvr\models\`; swap models later by
> adding/removing files in that folder.

</details>

> 💡 **This bundle ships every model** — BS-Roformer (revive / resurrection / both MelBand variants),
> MDX-Net (Karaoke 2 / Inst HQ 3 / Kim Vocal 2), VR denoise (DeNoise / DeNoise-Lite / Reverb) and the
> Demucs set, 28 files in total. Switch between them in tab ⑥ without downloading anything else.
>
> ⏳ **If the exe pauses for ~30 s right after you double-click, printing “合并离线大包 torch…” — it is not stuck.**
> The torch wheel is 2.4 GB, above GitHub's 2 GB per-asset limit, so it ships as two chunks and the
> installer joins them back into one file first. Just wait; don't close the window.

##### 📦 What each of the 5 parts contains

| Part | Download size (as shown on GitHub) | What's inside |
|---|---|---|
| `part1` | 1.94 GB | **First half of the torch wheel** (1850 MB chunk). torch is 2.4 GB, above GitHub's 2 GB per-asset cap, so it ships as two halves |
| `part2` | 1.57 GB | **MelBand Roformer v2 separation model** (1502 MB) — the highest-quality tier |
| `part3` | 1.58 GB | **The other MelBand Roformer checkpoint** (871 MB) + **second half of the torch wheel** (632 MB) |
| `part4` | 1.91 GB | **13 models + onnxruntime-gpu**: the default `bs_roformer_revive` (610 MB), `BS-Roformer-Resurrection` (195 MB), `UVR-DeNoise` (121 MB), five Demucs checkpoints (80 MB each), four MDX-Net / denoise onnx models; plus onnxruntime-gpu 1.22 (205 MB, GPU acceleration) |
| `part5` | 223 MB | **Python 3.12 installer** (26 MB) + **the remaining 59 dependency wheels** (scipy, llvmlite, imageio-ffmpeg…) + **13 small model files** (yaml configs, download manifests) |
| **Total** | **7.2 GB** | 93 files land in `payload\` (full file list in the collapsible block above) |

> ⚠️ **The parts are split by size, not by feature — you cannot skip any of them.**
> `part1` and `part3` hold **the two halves of one torch wheel**; with either half missing pip fails
> outright with `is not a valid wheel filename`. Without `part4` there is no model to separate with,
> and without `part5` neither Python nor the dependencies can be installed.
> **All 5 parts + 1 exe — six files, none optional** (download them over several sessions if you like,
> just put the complete set in one folder).

> ⚠️ **Three common mistakes** (each makes the installer try to fetch everything from GitHub instead —
> which usually fails, so the install never finishes):
> ① the files are in different folders; ② only some of the zips were extracted; ③ extraction added an extra
> level (`...\SingAlong-Offline-part1\payload\`). Quick self-check: **`payload` and the exe are
> siblings**.

#### On v1.6.1 or later? One click upgrades it

Look at the version badge in the panel header:

| Badge | Meaning | What to do |
|---|---|---|
| `v1.6.2` | Up to date | nothing |
| `↑ v1.6.x` | Update available | click it → a few hundred KB patch downloads → the panel restarts itself |

> Only the panel files (`%LOCALAPPDATA%\SingAlong\panel`) are replaced —
> **your songs, separated stems and downloaded models are untouched**. Press Ctrl+F5 afterwards to
> refresh the page.

**Still on v1.6.0 or older?** That panel has no badge yet, so this version needs one manual step.
**Easiest:** close the panel window, then unzip `SingAlong-Panel-1.6.2.zip` over
`%LOCALAPPDATA%\SingAlong\panel\` (487 KB). Alternatively reinstall with the 6 files (4 steps above).
**After that you never have to do it again.**

<details>
<summary>📂 Which files does the panel patch zip contain? (21 files, no wrapper folder)</summary>

`SingAlong-Panel-1.6.2.zip` has **no `panel\` folder inside** — its entries sit at the archive root,
so you must extract it *into* the target folder, not into a `SingAlong-Panel-1.6.2\` folder.

| Path after extraction | What it is |
|---|---|
| `VERSION` | Version number, plain text `1.6.2`. This is how the panel detects its own age |
| `assets\` (7) | `separator_panel.html` (the UI, 175 KB), `capabilities.json`, `model_catalog.json`, `kanji_readings.json`, `karaoke_page_template.html`, `fat_fish.ico`, `panel.ico` |
| `scripts\` (9) | `serve_separator.py` (main program, 148 KB), `separate_worker.py`, `studio.py`, `lyrics_io.py`, `lyrics_from_video.py`, `probe_lyric_box.py`, `romaji_engine.py`, `english_engine.py`, `llm_client.py` |
| `启动分离面板.bat`, `启动分离面板.sh`, `一键做跟唱页.bat` | Launch / export scripts |
| `README.md` | The panel's own docs (23 KB) |

Correct way, either one:

1. Right-click the zip → "Extract All" → set the destination to `%LOCALAPPDATA%\SingAlong\panel` → confirm overwrite;
2. Or extract somewhere empty → select all 21 items → copy → paste into `...\SingAlong\panel\` → "Replace files".

**What it looks like when done wrong**: you end up with a `SingAlong-Panel-1.6.2\` folder on the desktop
while `...\panel\VERSION` still holds the old number → the badge keeps offering the same patch forever.

> This zip contains **no** models, songs, stems or Python environment (it is only 487 KB), so overwriting
> with it can never lose your data.

</details>

>
> Step-by-step guide (Chinese): **[面板资源与升级指南.md](面板资源与升级指南.md)** — where each file goes, the symptom table, and a post-upgrade checklist.

#### Two prompts you'll see either way

1. **Pick the install folder** at the start (OK = choose one; Cancel = default `%LOCALAPPDATA%\SingAlong`)
2. **"Create a desktop shortcut?"** at the end — choose Yes

Then double-click the desktop **「跟唱练习器」** icon → the panel opens in your browser →
open tab ① Workflow and drag a song in.

Already set up the Python environment yourself? Use the smaller `SingAlong-Launcher.exe`
(launcher only, 9 MB) instead.

> Moved the exe or lost the shortcut? No problem — everything lives in
> `%LOCALAPPDATA%\SingAlong`; run the launcher exe from there directly.

### macOS — works, but no one-click installer

macOS is fully supported (`panel/启动分离面板.sh` is a POSIX script), but .app/.dmg
installers can only be built on a Mac, which the author doesn't have. Follow the
**5-command setup** in [安装环境.md · macOS](安装环境.md) (~15 min, copy-paste),
then start the panel each time with:

```bash
bash panel/启动分离面板.sh
```

### From source (developers)

See [安装环境.md](安装环境.md) (Chinese; an English translation is welcome via PR).
Short version: Python 3.10–3.12 venv → `pip install torch torchaudio audio-separator
soundfile audioread requests` (CUDA 12 build of torch if you have an NVIDIA GPU;
pin `onnxruntime-gpu==1.22.0`) → run `panel/启动分离面板.bat` (Windows) or
`bash panel/启动分离面板.sh` (macOS/Linux).

---

## The mobile player (Android)

`player/` builds an 8 MB offline APK. Song folders produced by the panel are zipped
and imported into the app — per-syllable romaji highlighting, loop-one-line,
0.75–1.25× speed, no network, no storage permission. Requires Android 7.0+.

---

## Repository layout

> **About the source code**: this project uses **two repositories**. The public one
> (`sing-along-handbook`) ships docs + installers only; the full source lives in the
> **private** repo `sing-along-handbook-dev`. To develop with us, open an issue and ask
> for collaborator access.

| Path | What it is |
|---|---|
| `panel/` | The web panel: `scripts/serve_separator.py` (backend) + `assets/separator_panel.html` (single-file UI, with 中/EN toggle) |
| `player/` | Android player (manual build chain, no Gradle) |
| `tools/launcher/` | Source of the Windows exes (installer + launcher, PyInstaller) |
| `tools/scripts/` | Pipeline helpers (lyrics OCR/ASR, KRC parsing, self-checks) |
| `安装环境.md` | Environment setup (Windows / macOS / Linux) |
| `用户手册.md` | User manual |
| `项目介绍_EN.html` | A slideshow-style project intro in English (open in a browser); `项目介绍.html` is the Chinese original |
| `CHANGELOG.md` | Changelog |

## License & copyright

MIT for the code. The separated instrumentals are for **personal practice only** —
buy official off-vocal tracks for public release, and don't upload or share
separated stems or generated pages.
