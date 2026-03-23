# BitMemo Monorepo 提交与同步指南 🚀

为了支持未来多平台（插件、网页、移动端、桌面端）的开发，本项目已重构为 **Monorepo（单合集仓库）** 结构。本文档将指导你如何进行日常代码提交以及自动化同步。

---

## 1. 核心架构说明

项目采用 **"中心化开发，自动化镜像"** 的策略：

- **主仓库 (Monorepo)**: `BitMemo-Monorepo` (你是这里的管理员，所有开发都在这里进行)。
- **小仓库 (Sub-repos)**: `BitMemo` (插件独立仓库) 和 `BitMemo-Web` (官网独立仓库)。这些仓库的内容由主仓库通过 GitHub Actions **自动同步**，无需手动修改。

### 目录结构预览

```text
BitMemo/ (根目录)
├── apps/
│   ├── extension/   --> 对应独立的 BitMemo 仓库
│   └── web/         --> 对应独立的 BitMemo-Web 仓库
├── packages/
│   ├── assets/      --> 共享资源 (字体、图标)
│   └── core/        --> 共享逻辑 (i18n、工具函数)
└── .github/workflows/ --> 自动化同步脚本
```

---

## 2. 日常开发提交流程

你只需要记住：**所有提交只发送给主仓库 (`BitMemo-Monorepo`)**。

### 步骤 A：本地修改

在主仓库根目录下安装依赖并进行开发：

```bash
pnpm install
# 在 apps/extension 或 apps/web 下修改代码
```

### 步骤 B：提交到主仓库

```bash
git add .
git commit -m "feat: 你的功能描述"
git push origin main
```

---

## 3. 自动化同步机制 (GitHub Actions)

当你将代码推送到主仓库的 `main` 分支时，GitHub Actions 会自动触发 `.github/workflows/sync-subrepos.yml`：

1. **自动提取**: 它会自动提取 `apps/extension` 的变动并推送到 `LZ7TOP/BitMemo`。
2. **自动提取**: 它会自动提取 `apps/web` 的变动并推送到 `LZ7TOP/BitMemo-Web`。
3. **镜像提交**: 小仓库中会看到一条类似 `Update from BitMemo-Monorepo/commit/[hash]` 的提交记录。

---

## 4. 故障排查 (Troubleshooting)

如果发现同步失败（Actions 变红），请检查以下几点：

### 403 Forbidden 错误

- **原因**: `SYNC_PAT` (个人访问令牌) 权限过期或配置错误。
- **解决**: 

  1. 重新生成 PAT，确保勾选了 **`repo`** (Classic) 权限。
  2. 在主仓库的 `Settings -> Secrets -> Actions` 中更新 `SYNC_PAT` 的值。

### 邮件匹配问题

- 工作流已配置为使用你的 Git 邮箱 `garcia1004@163.com` 进行同步。如果更换了 Git 账号，请同步修改 `.github/workflows/sync-subrepos.yml` 中的 `user-email`。

---

## 5. 如何增加新的同步子仓库？

如果你未来增加了 `apps/mobile` (React Native) 并想同步到 `BitMemo-Mobile` 仓库：

1. 在 `.github/workflows/sync-subrepos.yml` 中复制一份 `job`。
2. 修改 `source-directory` 为 `apps/mobile`。
3. 修改 `destination-repository-name` 为 `BitMemo-Mobile`。

---

**享受 Monorepo 带来的高效开发体验吧！如有疑问随时召唤我。** 👾
