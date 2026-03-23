# BitMemo (像素记) Monorepo 📝

这是一个基于 **pnpm workspaces** 的多平台单合集仓库。支持浏览器插件、官方网站，并为未来的移动端和桌面端开发预留了扩展空间。

## 目录结构

- **`apps/`** (终端应用)
  - `extension/`: 浏览器插件项目 (Vanilla JS / Manifest V3)
  - `web/`: 官方展示网站 (React + Vite)
  - `mobile/`: [待开发] 移动端应用 (React Native)
  - `desktop/`: [待开发] 桌面端应用 (Electron/Tauri)
- **`packages/`** (共用代码与资源)
  - `assets/`: 共享的像素风格字体、图片、图标资源
  - `core/`: 共享的业务逻辑、i18n 多语言数据、工具函数

## 快速开始

### 1. 环境准备

确保已安装 [pnpm](https://pnpm.io/):
```bash
npm install -g pnpm
```

### 2. 安装所有依赖

```bash
pnpm install
```

### 3. 开发与构建

在根目录下运行：

- **启动官网开发服务**: `pnpm dev:web`
- **构建官网**: `pnpm build:web`
- **测试插件打包**: `pnpm build:ext`

---

## 协同与同步指南 🛰️

本项目通过 **GitHub Actions** 实现了从 Monorepo 到独立小仓库的自动同步：

- **自动同步详情**: 详见 [SYNC_GUIDE.md](./SYNC_GUIDE.md)
- **提交规则**: 开发者只需推送代码至 `BitMemo-Monorepo` (本仓库) 的 `main` 分支，变动将自动分发至插件和官网的独立仓库。

---

## 路线图 (Roadmap)

- [x] 仓库 Monorepo 重构
- [x] 共享 i18n 数据提取
- [ ] 移动端 App 开发 (iOS/Android)
- [ ] 桌面端软件开发 (macOS/Windows)
- [ ] 共享 React UI 组件库提取

---

由 **LZ7** 倾情打造 | Crafted with ❤️ by **LZ7**.
