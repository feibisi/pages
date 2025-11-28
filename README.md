# feiCode Pages

feiCode Pages 是基于 Forgejo 构建的免费静态网站托管服务，类似于 GitHub Pages。

## 🌟 特点

- **专业** - 基于 Forgejo 开源平台，稳定可靠
- **开放** - 完全开源，透明可信
- **安全** - 完善的备案和安全保障

## 🌐 访问地址

- **中国区域**：`*.feibisi.net`（已备案）
- **国际区域**：`*.feibisi.org`

## 🚀 快速开始

### 1. 创建仓库

在 [feiCode](https://feicode.com) 上创建一个新的仓库，仓库名称格式：
- 用户页面：`<username>.pages`
- 项目页面：任意仓库名

### 2. 添加网站内容

将您的静态网站文件（HTML、CSS、JS 等）推送到仓库的 `main` 分支：

```bash
git add .
git commit -m "Initial commit"
git push origin main
```

### 3. 访问您的网站

推送成功后，您的网站将自动部署到：
- 中国区：`https://<username>.feibisi.net`
- 国际区：`https://<username>.feibisi.org`

## 📁 目录结构

```
.
├── index.html          # 默认首页
├── README.md          # 项目说明
└── user-guide.md      # 用户指南
```

## 🔧 配置说明

### 自定义域名

如需使用自定义域名，请：
1. 在仓库根目录创建 `CNAME` 文件
2. 文件内容为您的域名（如：`example.com`）
3. 在您的域名 DNS 设置中添加 CNAME 记录指向 Pages 服务

### 分支设置

默认使用 `main` 分支作为发布源，您也可以在仓库设置中修改。

## 📖 更多信息

- **仓库地址**：[https://feicode.com/feiCode/pages](https://feicode.com/feiCode/pages)
- **用户指南**：查看 [user-guide.md](./user-guide.md)
- **技术支持**：访问 [feiCode](https://feicode.com)

## 📝 许可证

本项目基于 Forgejo 构建，遵循开源协议。

---

**菲码源库** © 2025 汉中菲比斯网络技术有限公司

备案号：陕ICP备15002899号-4 | 陕公网安备 61070202000234 号 | 增值电信业务经营许可证：陕 B2-20210198