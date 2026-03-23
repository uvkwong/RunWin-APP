# Codemagic 配置指南 - 瑞荣APP iOS 打包

## 🎯 目标
使用 Codemagic 云平台自动打包 iOS APP，生成 .ipa 文件供同学测试。

---

## 📋 前置准备

### 1️⃣ 生成 Apple ID 应用专用密码

**这个步骤必须先做！**

访问：https://appleid.apple.com

1. 使用 `uvkwong@163.com` 登录
2. 进入 **安全** 标签
3. 向下滚动找到 **应用专用密码** 部分
4. 点击 **生成密码**
5. 输入应用名称：`Codemagic` （或其他名称）
6. 系统会生成一个 16 位密码，格式如：`xxxx-xxxx-xxxx-xxxx`
7. ⚠️ **复制这个密码，稍后需要**

> **为什么需要这个？**
> - Apple 要求第三方应用通过专用密码认证，而不是直接使用你的 Apple ID 密码
> - 这个密码只能用于 Codemagic，安全性更高

### 2️⃣ 拥有 GitHub 账号
✅ 已完成（uvkwong）

### 3️⃣ 代码已推送到 GitHub
✅ 已完成（https://github.com/uvkwong/RunWin-APP）

---

## 🚀 Codemagic 配置步骤

### 步骤 1: 访问 Codemagic 并注册

1. 打开 https://codemagic.io/
2. 点击 **Sign Up** 
3. 选择 **Sign up with GitHub**
4. 授权 GitHub 账号（会要求允许访问你的仓库）
5. 完成注册

### 步骤 2: 连接 GitHub 仓库

1. 登录 Codemagic 后台
2. 点击 **Create new app** 或 **+ New app**
3. 在仓库列表中找到 **RunWin-APP**
4. 点击 **Select**
5. Codemagic 会自动检测 `codemagic.yaml` 配置文件

### 步骤 3: 配置 iOS 签名凭证

这是关键步骤！

1. 在 Codemagic 左侧菜单，点击 **Teams** > **Credentials** 
2. 点击 **+ Add New** > **Apple Certificates**
3. 填写以下信息：
   - **Credential name**: `Apple iOS Signing`
   - **Apple ID**: `uvkwong@163.com`
   - **Password**: 粘贴之前生成的 **应用专用密码**（16 位那个）
   - 勾选 **"Automatically manage signing"**
4. 点击 **Add**
5. Codemagic 会验证你的账号，大约需要 1-2 分钟

### 步骤 4: 配置构建设置

1. 进入 **RunWin-APP** 项目
2. 点击 **Build settings** 或 **Workflow editor**
3. 确认以下配置（应该已经自动读取）：
   - **iOS Signing**: 选择你刚才添加的 `Apple iOS Signing`
   - **Provisioning Profile**: 自动管理（Ad Hoc）
   - **Build for testing**: ✅ 勾选
   - **Export Ad Hoc IPA**: ✅ 勾选

### 步骤 5: 手动触发第一次构建

1. 点击 **Build** 或 **Start New Build**
2. 选择分支：`main`
3. 点击 **Build** 按钮
4. 等待构建完成（通常 15-20 分钟）

**构建过程会显示：**
```
✅ Installing CocoaPods dependencies
✅ Building iOS app
✅ Creating Ad Hoc IPA
✅ Artifacts ready
```

### 步骤 6: 下载 IPA 文件

1. 构建完成后，点击 **Artifacts**
2. 下载 `瑞荣APP.ipa`（大约 50-100MB）

---

## 📤 分发给同学

### 方案 A: 使用蒲公英（推荐）

1. 访问 https://www.pgyer.com/
2. 注册账号
3. 新建应用，上传 IPA
4. 获得下载链接，分享给同学
5. 同学用 Safari 打开链接 → 下载 → 信任证书 → 安装

### 方案 B: 直接分享 IPA 文件

1. Codemagic 下载的 IPA 上传到网盘（百度云、OneDrive 等）
2. 同学下载后用 iTunes/Finder 安装（需要 USB 连接 Mac）

### 方案 C: 自动上传蒲公英

如果你有蒲公英账号的 API Key：

1. 在 Codemagic 环境变量中添加：
   ```
   PGYER_API_KEY = 你的蒲公英 API Key
   ```
2. 每次构建完成后会自动上传到蒲公英
3. 获得分享链接，发给同学

---

## ⚙️ 后续操作

### 自动构建
- 每次你 `git push` 到 `main` 分支时，Codemagic 会自动构建
- 构建完成会发邮件通知

### 手动构建
- 在 Codemagic 后台点击 **Build** 随时手动触发

### 修改代码后更新 APP
1. 在本地修改代码
2. `git add .` → `git commit -m "更新信息"` → `git push`
3. Codemagic 自动开始构建
4. 构建完成后从 Artifacts 下载最新的 IPA

---

## 🐛 常见问题

### Q: 应用专用密码在哪里生成？
A: https://appleid.apple.com → 登录 → 安全 → 应用专用密码 → 生成密码

### Q: 构建失败了怎么办？
A: 
- 点击 **Build log** 查看详细错误
- 常见原因：CocoaPods 依赖问题、代码签名问题
- 联系 Codemagic 支持或 Discord 社区

### Q: 如何跳过自动构建？
A: 在提交信息中加入 `[skip ci]`，比如：
```
git commit -m "更新文档 [skip ci]"
```

### Q: IPA 文件很大，同学下载慢怎么办？
A: 使用 蒲公英/fir.im，它们会压缩文件

---

## 📞 需要帮助？

- Codemagic 官方文档：https://docs.codemagic.io/
- Codemagic Discord 社区：https://discord.gg/codemagic
- Apple ID 帮助：https://support.apple.com/

---

## ✨ 一切就绪！

现在你可以：
1. ✅ 自动构建 iOS APP
2. ✅ 生成 .ipa 文件
3. ✅ 分享给同学测试
4. ✅ 完全免费（Codemagic 每月 500 分钟免费额度）

**祝你成功！** 🎉
