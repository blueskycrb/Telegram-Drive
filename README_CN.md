# Telegram Drive 中文说明

**Telegram Drive** 是一个开源、跨平台的桌面应用，可以把你的 Telegram 账号变成一个安全的云盘。它基于 **Tauri**、**Rust** 和 **React** 构建，支持 Windows、macOS、Linux，并提供 Android 侧载测试版。

> 说明：本文件是对原英文 README 的中文整理与翻译，方便中文用户快速了解、安装和使用。若与英文 README 或上游发布页面存在差异，请以上游英文文档和 Release 页面为准。

## 项目简介

Telegram Drive 通过 Telegram API 上传、整理和管理文件。它会把你的「Saved Messages（收藏消息）」以及创建的 Telegram 频道当作文件夹，并提供类似文件管理器的界面，方便你把 Telegram 云端空间作为个人文件仓库使用。

## 主要功能

- **近似无限云存储**：利用 Telegram 的云端基础设施保存文件。
- **高性能网格列表**：虚拟滚动可以流畅处理包含大量文件的目录。
- **自动更新**：Windows、macOS、Linux 桌面端支持自动更新。
- **媒体在线播放**：视频和音频文件无需完整下载即可播放。
- **PDF 查看器**：内置 PDF 阅读支持，适合查看文档。
- **拖拽上传**：支持直观的拖放上传和文件管理。
- **缩略图预览**：图片和媒体文件支持内联缩略图。
- **文件夹管理**：通过创建私有 Telegram 频道来组织文件。
- **分享链接**：可生成下载链接，支持密码、过期时间和撤销访问；公开频道内文件也可复制 Telegram 原生消息链接。
- **本地 REST API**：默认关闭，可配置端口和 API Key，适合 AI 工具或自动化脚本集成。
- **代理支持**：支持 SOCKS5 和 MTProto 代理，适合受网络环境限制的地区。
- **VPN 优化**：提供更激进的网络调优，包括带宽限制、传输分块大小和自适应保活，提高高延迟网络下的稳定性。
- **重视隐私**：API Key 和数据保存在本地，不依赖第三方服务器。
- **跨平台**：支持 macOS（Intel/Apple Silicon）、Windows 和 Linux。

## Android 版本（预构建、未签名 APK）

项目提供 Android 侧载测试版 APK，可在 Release 页面下载：

- [Android v2.1.0 beta release](https://github.com/caamer20/Telegram-Drive/releases/tag/Androidv2.1.0beta)

注意：该 APK **未签名**，也**不在 Google Play 商店上架**。安装时需要在 Android 系统中允许「安装未知来源应用」。该版本包含 Google AdMob 横幅广告以支持开发。

### Android 安装步骤

1. 从 Release 页面下载 `Telegram-Drive-v2.1.0-beta.apk`。
2. 在 Android 设备中进入：设置 → 应用 → 特殊应用权限 → 安装未知应用。
3. 允许浏览器或文件管理器安装未知来源应用。
4. 打开下载的 APK，点击安装。
5. 首次启动时输入你的 Telegram API 凭据，和桌面版相同。

补充说明：

- 需要 Android 7.0（API 24）或更高版本。
- 如果 Android 15+ 模拟器或设备阻止安装，可通过 ADB 绕过低目标 SDK 限制：

```bash
adb install --bypass-low-target-sdk-block Telegram-Drive-v2.1.0-beta.apk
```

- Android 版本属于社区/测试构建；Windows、macOS、Linux 桌面端仍是主要支持平台。

## 技术栈

- **前端**：React、TypeScript、TailwindCSS、Framer Motion
- **后端**：Rust（Tauri）、Grammers（Telegram Client）
- **构建工具**：Vite

## 开始使用

### 前置要求

1. **Node.js 18+**

   下载地址：[https://nodejs.org/](https://nodejs.org/)

2. **Rust 最新稳定版**

   macOS/Linux 可使用：

   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   ```

   Windows 用户可从 [rustup.rs](https://rustup.rs/) 下载并运行 `rustup-init.exe`。

   安装后可用以下命令检查：

   ```bash
   rustc --version
   cargo --version
   ```

3. **Tauri 所需系统构建工具**

   - macOS：安装 Xcode Command Line Tools：

     ```bash
     xcode-select --install
     ```

   - Ubuntu/Debian Linux：

     ```bash
     sudo apt update && sudo apt install libwebkit2gtk-4.1-dev build-essential curl wget file libxdo-dev libssl-dev libayatana-appindicator3-dev librsvg2-dev
     ```

   - Windows：必须安装 [Visual Studio Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)，并选择 **Desktop development with C++** 工作负载。否则可能出现 `linker 'link.exe' not found` 错误。
   - Windows WebView2：Windows 10/11 通常已预装；如果没有，请安装 [WebView2 Runtime](https://developer.microsoft.com/en-us/microsoft-edge/webview2/#download-section)。

4. **Telegram API 凭据**

   你需要自己的 `api_id` 和 `api_hash`：

   1. 登录 [my.telegram.org](https://my.telegram.org)。
   2. 进入 **API development tools**。
   3. 创建一个应用，获取 `api_id` 和 `api_hash`。

提示：首次运行 `npm run tauri dev` 或 `npm run tauri build` 时会下载并编译大量 Rust crate，可能需要 5～15 分钟，后续构建会快很多。

## 安装与运行

1. 克隆仓库：

```bash
git clone https://github.com/caamer20/Telegram-Drive.git
cd Telegram-Drive
```

如果使用的是本 fork：

```bash
git clone https://github.com/blueskycrb/Telegram-Drive.git
cd Telegram-Drive
```

2. 安装依赖：

```bash
cd app
npm install
```

3. 开发模式运行：

```bash
npm run tauri dev
```

4. 构建安装包：

```bash
npm run tauri build
```

## 使用注意事项

- 该应用不隶属于 Telegram FZ-LLC，请遵守 Telegram 服务条款并合理使用。
- Telegram 对单文件大小、账号风控、频道/消息频率等可能存在限制，请避免高频滥用。
- API 凭据和本地 API Key 请妥善保管，不要提交到公开仓库。
- 如需在网络受限环境使用，优先配置 SOCKS5 或 MTProto 代理。
- 本地 REST API 默认关闭，只有在确实需要自动化或 AI 工具调用时再开启，并设置强 API Key。

## 开源协议

本项目是自由开源软件，可自由使用、修改和分发。

许可证：**MIT License**。

## 相关链接

- 原项目仓库：[https://github.com/caamer20/Telegram-Drive](https://github.com/caamer20/Telegram-Drive)
- 本 fork 仓库：[https://github.com/blueskycrb/Telegram-Drive](https://github.com/blueskycrb/Telegram-Drive)
- VPN 优化版本：[https://github.com/caamer20/Telegram-Drive-ForVPNs](https://github.com/caamer20/Telegram-Drive-ForVPNs)
