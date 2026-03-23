# ✅ 立即行动清单

## 🎯 你现在需要做的 3 件事

### ① 打开 Codemagic 并注册（5 分钟）

**链接**: https://codemagic.io/

**步骤**:
1. 点击右上角 **Sign Up**
2. 选择 **Continue with GitHub**
3. 用你的 GitHub 账号（uvkwong）登录
4. 授权 Codemagic 访问你的仓库
5. 完成！

---

### ② 配置 Apple ID 签名（5 分钟）

**步骤**:
1. 登录 Codemagic 后台
2. 点击左侧菜单 **Teams**
3. 点击 **Credentials**
4. 点击 **+ Add New** 
5. 选择 **Apple Certificates**
6. 填写以下信息：

| 字段 | 内容 |
|------|------|
| Credential name | `Apple iOS Signing` |
| Apple ID | `uvkwong@163.com` |
| Password | `jvff-xwha-rfox-dgrh` |

7. 勾选 **"Automatically manage signing"** ✅
8. 点击 **Save**
9. 等待验证完成（会显示绿色 ✅）

---

### ③ 触发构建（点击即可，然后等待）

**步骤**:
1. 返回项目主页
2. 找到你的 **RunWin-APP** 项目
3. 点击 **Build** 或 **Start New Build** 按钮
4. 确认分支是 **main**
5. 点击 **Build** 按钮
6. **等待 15-20 分钟**，构建会自动完成

**期间你可以**:
- 查看实时构建日志
- 看到各个步骤的进度

**构建完成后**:
- 点击 **Artifacts** 下载 `瑞荣APP.ipa`
- 文件大约 50-100MB

---

## 🎉 然后你就可以分享给同学了！

### 最简单的方法（蒲公英）

1. 打开 https://www.pgyer.com/
2. 注册免费账号
3. 上传你下载的 `瑞荣APP.ipa`
4. 复制分享链接
5. 发送链接给同学

### 同学的安装步骤

1. 在 iPhone Safari 中打开你发的链接
2. 点击 **下载**
3. 系统会提示 "信任此企业级应用"
4. 同学需要进入：**设置 > 通用 > VPN 与设备管理**
5. 找到你的 Apple ID 名称，点击 **信任**
6. 返回浏览器，重新点击安装
7. 完成！ ✅ APP 现在在同学的 iPhone 上了

---

## ⏱️ 预计耗时

| 任务 | 耗时 |
|------|------|
| ① 注册 Codemagic | 5 分钟 |
| ② 配置签名 | 5 分钟 |
| ③ 等待构建 | 20 分钟 |
| ④ 下载 + 分享 | 5 分钟 |
| **总计** | **35 分钟** |

---

## ❓ 如果遇到问题

### 构建失败？
- 点击失败的构建任务
- 查看 **Build log** 末尾的错误信息
- 常见原因：
  - ❌ Apple ID 密码错误 → 检查应用专用密码是否正确
  - ❌ CocoaPods 依赖问题 → 重新构建通常能解决

### IPA 无法在 iPhone 上安装？
- 最常见原因：同学没有信任你的开发者证书
- 解决：进入 **设置 > 通用 > VPN 与设备管理** 并点击信任

### 其他问题？
- Codemagic 官方文档: https://docs.codemagic.io/
- Codemagic Discord 社区: https://discord.gg/codemagic

---

## 📌 关键信息速记

```
GitHub 账号: uvkwong
Apple ID: uvkwong@163.com
应用专用密码: jvff-xwha-rfox-dgrh
GitHub 仓库: https://github.com/uvkwong/RunWin-APP
Codemagic: https://codemagic.io/
```

---

## ✨ 现在就开始吧！

**第一步**: 打开 https://codemagic.io/

🚀 **祝你成功！** 🎉

---

**如有任何问题，随时问我！**
