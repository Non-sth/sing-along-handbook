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

Both paths below end with **double-clicking the same installer exe**; they differ only in where the
~3.6 GB of resources come from. Pick one on the [Releases](https://github.com/Non-sth/sing-along-handbook/releases) page.

#### Option A — Online installer (1 file only)

| Step | Do this |
|---|---|
| 1️⃣ | Download **`SingAlong-Setup.exe`** (17 MB) only |
| 2️⃣ | Put it **anywhere** (Desktop, Downloads…) — **nothing to unzip** |
| 3️⃣ | **Double-click `SingAlong-Setup.exe`** → it downloads the Python env + AI components + ffmpeg + default model (~3.6 GB, 25–50 min, resumable) |

#### Option B — Offline bundle (6 files, installs with no internet)

| Step | Do this |
|---|---|
| 1️⃣ | Download all six: `SingAlong-Setup.exe` (17 MB) + `SingAlong-Offline-part1.zip` … `part5.zip` (~6.7 GB total) |
| 2️⃣ | Put **all six in the same folder**, e.g. `D:\singalong-setup\` — do not split them up |
| 3️⃣ | Inside that folder, extract **all five** zips **into the current folder** (do **not** extract into a `SingAlong-Offline-part1\` subfolder) |
| 4️⃣ | **Double-click `SingAlong-Setup.exe`** → seeing `payload\` next to it, it installs entirely offline |

The folder must look like this — key point: **`payload` sits next to the exe**.

```
D:\singalong-setup\
├─ SingAlong-Setup.exe              ← double-click this one
├─ SingAlong-Offline-part1.zip      (already extracted; keep or delete)
├─ SingAlong-Offline-part2.zip      (same)
├─ SingAlong-Offline-part3.zip      (same)
├─ SingAlong-Offline-part4.zip      (same)
├─ SingAlong-Offline-part5.zip      (same)
└─ payload\                          ← extracted offline resources
   ├─ python\   (Python installer)
   ├─ wheels\   (all deps, incl. the chunked torch wheel)
   └─ models\   (all 28 models, ~4 GB)
```

> 💡 **This bundle ships every model** — BS-Roformer (revive / resurrection / both MelBand variants),
> MDX-Net (Karaoke 2 / Inst HQ 3 / Kim Vocal 2), VR denoise (DeNoise / DeNoise-Lite / Reverb) and the
> Demucs set, 28 files in total. Switch between them in tab ⑥ without downloading anything else.

> ⚠️ **Three common mistakes** (each makes the installer fall back to a slow online download):
> ① the files are in different folders; ② only some of the zips were extracted; ③ extraction added an extra
> level (`...\SingAlong-Offline-part1\payload\`). Quick self-check: **`payload` and the exe are
> siblings**.

#### On v1.6.1 or later? One click upgrades it

Look at the version badge in the panel header:

| Badge | Meaning | What to do |
|---|---|---|
| `v1.6.1` | Up to date | nothing |
| `↑ v1.6.x` | Update available | click it → a few hundred KB patch downloads → the panel restarts itself |

> Only the panel files (`%LOCALAPPDATA%\SingAlong\panel`) are replaced —
> **your songs, separated stems and downloaded models are untouched**. Press Ctrl+F5 afterwards to
> refresh the page.

**Still on v1.6.0 or older?** That panel has no badge yet, so this version needs one manual install:
run `SingAlong-Setup.exe` again (17 MB), or unzip `SingAlong-Panel-1.6.1.zip` over
`%LOCALAPPDATA%\SingAlong\panel\` (484 KB). **After that you never have to do it again.**

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
