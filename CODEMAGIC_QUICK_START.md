# Codemagic 快速配置指南（图文步骤）

## 📍 你现在拥有的信息

- ✅ Apple ID: `uvkwong@163.com`
- ✅ 应用专用密码: `jvff-xwha-rfox-dgrh`
- ✅ GitHub 仓库: `https://github.com/uvkwong/RunWin-APP`
- ✅ Codemagic 配置文件已在仓库中

---

## 🚀 5 分钟快速配置流程

### 步骤 1: 打开 Codemagic 并用 GitHub 登录

1. 访问 https://codemagic.io/
2. 点击 **Sign Up** 或 **Sign In**
3. 选择 **GitHub** 登录选项
4. 授权 GitHub 账号（允许访问你的仓库）

### 步骤 2: 创建新项目

1. 登录后，你会看到 **Dashboard**
2. 点击 **Create new app** 或 **+ New app**
3. 在仓库列表中找到 **RunWin-APP**（可能需要搜索）
4. 点击 **Select**
5. Codemagic 会自动检测 `codemagic.yaml` 文件

✨ **Codemagic 会自动读取你的构建配置！**

### 步骤 3: 配置 iOS 签名凭证（关键步骤！）

1. 在 Codemagic 左侧菜单，点击 **Teams**
2. 在 Teams 下方找到 **Credentials** 并点击
3. 点击 **+ Add New** 按钮
4. 在下拉菜单中选择 **Apple Certificates**

你会看到一个表单，需要填写：

| 字段 | 值 |
|------|-----|
| **Credential name** | `Apple iOS Signing` (或任意名称) |
| **Apple ID** | `uvkwong@163.com` |
| **Password** | `jvff-xwha-rfox-dgrh` ⚠️ 这是你的应用专用密码，不是 Apple ID 密码！ |

5. 勾选 **"Automatically manage signing"** ✅
6. 点击 **Save**

⏳ **Codemagic 会验证你的账号，通常需要 1-2 分钟**

验证成功后，你会看到一个绿色的勾号 ✅

### 步骤 4: 配置构建工作流

1. 回到你的 **RunWin-APP** 项目页面
2. 点击 **Workflow settings** 或 **Configure workflow**
3. 在 **iOS Signing** 部分，选择你刚才添加的凭证：`Apple iOS Signing`
4. 确保以下选项已勾选：
   - ☑️ **Build for testing**
   - ☑️ **Export Ad Hoc IPA**（用于测试分发）
5. 其他默认设置保持不变
6. 点击 **Save** 或 **Save workflow**

### 步骤 5: 手动触发第一次构建

1. 回到项目首页
2. 点击 **Build** 或 **Start New Build** 按钮
3. 选择分支：**main**
4. 点击 **Build** 按钮开始构建

📊 **构建过程通常需要 15-25 分钟**

实时日志会显示进度：
```
✅ Installing dependencies...
✅ Running Codemagic pre-build scripts...
✅ Building for iOS...
✅ Exporting IPA...
✅ Build completed successfully!
```

### 步骤 6: 下载 IPA 文件

1. 构建完成后，点击 **Artifacts** 或 **Download artifacts**
2. 你会看到 `瑞荣APP.ipa` 文件（大约 50-100MB）
3. 点击下载
4. 等待下载完成

---

## 📱 现在你可以分发给同学了！

### 方案 A: 使用蒲公英（推荐，最简单）

1. 访问 https://www.pgyer.com/
2. 注册账号（免费）
3. 点击 **上传应用** 或 **Create New App**
4. 选择你下载的 `瑞荣APP.ipa` 文件
5. 上传完成后，你会得到一个二维码和分享链接
6. 发送链接给你的同学

**同学的操作步骤：**
1. 在 iPhone Safari 中打开链接
2. 系统会显示"信任此企业级应用"
3. 同学需要进入 **设置 > 通用 > VPN 与设备管理**
4. 找到你的 Apple ID（或开发者账号）
5. 点击"信任"
6. 返回蒲公英页面，重新下载和安装

✅ 完成！APP 现在在同学的 iPhone 上了。

### 方案 B: 直接发送 IPA 文件

1. 把 IPA 文件上传到网盘（百度云、OneDrive 等）
2. 发送分享链接给同学
3. 同学下载后，需要用 Mac 的 Finder 或 Windows 的 iTunes 来安装

> 这种方式比较麻烦，因为同学需要连接电脑。

### 方案 C: 自动上传到蒲公英

如果你想每次构建完自动上传到蒲公英：

1. 在蒲公英获取你的 API Key
2. 在 Codemagic 的环境变量中添加：
   ```
   PGYER_API_KEY = 你的蒲公英 API Key
   ```
3. 修改 `codemagic.yaml` 中的上传部分（已经有模板）
4. 之后每次构建完成都会自动上传！

---

## ⚙️ 之后的自动化流程

从现在开始，你的开发流程变得非常简单：

### 更新代码的流程

```
1. 在本地修改代码
   ↓
2. git add . && git commit -m "更新信息" && git push
   ↓
3. GitHub 接收到推送
   ↓
4. ⚡ Codemagic 自动开始构建（不需要你手动操作）
   ↓
5. 构建完成后发邮件通知你
   ↓
6. 你可以从 Codemagic 或蒲公英下载最新的 IPA
   ↓
7. 分享给同学测试
```

**完全自动化，无需人工干预！** 🎉

---

## 🐛 如果构建失败了怎么办？

1. 点击失败的构建任务
2. 向下滚动查看 **Build log**
3. 查找错误信息（通常在末尾）
4. 常见错误：
   - ❌ "CocoaPods dependency not found" → 重新运行构建
   - ❌ "Code signing failed" → 检查 Apple ID 和密码
   - ❌ "Scheme not found" → 检查 `codemagic.yaml` 中的 Scheme 名称

---

## 📞 需要帮助？

- **Codemagic 官方文档**: https://docs.codemagic.io/
- **iOS 构建文档**: https://docs.codemagic.io/flutter-ios/building-ios-apps/
- **问题排查**: https://docs.codemagic.io/troubleshooting/

---

## ✅ 下一步

1. 📍 **立即**: 访问 https://codemagic.io/ 注册
2. 📍 **接下来**: 按照上面的 5 个步骤配置
3. 📍 **然后**: 触发第一次构建
4. 📍 **最后**: 分享 IPA 给同学

**你已经准备好了！开始吧！** 🚀
