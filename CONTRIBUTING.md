# 参与开发

感谢你有兴趣参与。这个项目规模不大，流程也刻意保持轻量。

---

## 先决条件

| 需要 | 说明 |
|---|---|
| JDK 17 | 见 [player/README 工具链章节](player/README.md) |
| Android SDK build-tools 34.0.0 + platforms android-34 | 同上 |
| Python 3.11+ | 用于 `mk_apk.py` / 图标脚本 / 契约校验 |
| Android Emulator（可选） | 想在装机前验证 UI 就需要 |

**不需要 Gradle，也不需要 Android Studio。**

---

## 本地开发循环

```bash
# 1. 改代码
#    Java  → app/src/com/karaoke/practice/
#    界面  → player/app/assets/app/index.html
#    资源  → player/app/res/

# 2. 跑静态检查（构建流程里也会自动跑）
python player/build-tools/check_contract.py \
  --html player/app/assets/app/index.html \
  --java player/app/src/com/karaoke/practice/MainActivity.java

# 3. 跑桌面自检（47 项断言，不需要设备）
bash player/build-tools/desktop-test/run.sh

# 4. 构建
bash player/build-tools/build.sh --clean
# 产物：player/build-tools/build/app-release.apk
# 首次构建会自动生成签名密钥（keystore/karaoke.jks，已被 .gitignore 排除）

# 5. 模拟机验证（可选）
bash player/build-tools/emu.sh launch
bash player/build-tools/emu.sh install
```

> **签名密钥不入库**：公开密钥会让任何人能签出同签名 APK 冒充发布。
> 你自己构建时 `build.sh` 会自动生成一个 —— 记得备份，丢了就没法覆盖升级。
> 详见 [发布到GitHub.md](发布到GitHub.md#-签名密钥不入库已处理)。

---

## 提交前检查清单

- [ ] `check_contract.py` 通过（桥接方法名 / 签名两边一致）
- [ ] 桌面自检全绿（47 项断言）
- [ ] 若改了界面：模拟机上实际点一遍，确认没有白屏 / 点了没反应
- [ ] 若改了桥接方法：**同步更新契约校验**，防止再次漂移
- [ ] 版本号在 `app/AndroidManifest.xml` 与 `build-tools/build.sh` 两处都已提升
- [ ] `CHANGELOG.md` 已更新

> 版本号在**两个地方**（`AndroidManifest.xml` 的 `versionCode`/`versionName`，
> 以及 `build.sh` 里 `aapt2 link` 的 `--version-code`/`--version-name`）。
> 这是手工链路的代价 —— 没有 Gradle 帮你统一。

---

## 代码约定

### Java

- **纯 Java 8 语法**，只依赖 Android 框架 API。引入 androidx 或任何第三方库会破坏手工构建链
- 编译用 `--release 8`，**不要用 `-bootclasspath android.jar`** —— `android.jar` 里的 `LambdaMetafactory` 是残缺桩，lambda 会报「找不到符号 metafactory」
- 桥接方法必须标 `@JavascriptInterface`，且**只做非 UI 工作**，需要碰 UI 就 `runOnUiThread`

### `index.html`

- 单文件，内联 CSS / JS，不引外部资源（字体走拦截）
- 通过 `window.Shelf` 对象与原生通信，**调用前先 `awaitBridge()`**
- 拼 JS 字符串一律走统一的参数转义方法，不要手写引号

### 提交信息

用 [约定式提交](https://www.conventionalcommits.org/zh-hans/)：

```
feat: 跟唱页新增节拍器
fix: 修复导入时进度条文件名不显示
docs: 补充模拟机调试说明
refactor: 抽出参数转义方法
```

---

## 报告问题

用 [Issue 模板](../../issues/new/choose)。请务必附上：

1. **Android 版本 + 手机型号**（部分机型启动器缓存行为不同）
2. **复现步骤**，越具体越好
3. **日志**：`adb logcat | grep -i karaoke`
4. 若与导入相关：**zip 的目录结构**（`unzip -l xxx.zip`）

---

## 想加新功能？

先开 [Issue](../../issues/new) 聊一下方向，避免白写。

**特别欢迎的方向**：

- 和弦显示 / 节拍器 / 录音对比
- 非日语歌词支持（韩语罗马音、粤语拼音…）
- 界面主题（深色模式适配）

**不建议的方向**：

- 引入 androidx / 第三方依赖 —— 会破坏手工构建链
- 在线曲库 / 账号系统 —— 这是刻意的离线设计

---

## 关于 AGENTS.md

如果你用 AI 智能体（Claude Code / CodeBuddy / Cursor 等）辅助开发，**先让它读 [AGENTS.md](AGENTS.md)**。

那份文档写清了项目结构、构建命令、以及所有已知陷阱。智能体读完就能独立完成
「改代码 → 构建 → 模拟机验证 → 出包」，不需要你手动敲命令。

**改了构建流程或踩到新坑，请顺手更新 AGENTS.md** —— 它是这个项目的活文档。
