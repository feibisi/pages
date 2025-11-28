# FeiCode Pages 用户指南

## 🎯 如何使用 FeiCode Pages

FeiCode Pages 是一个免费的静态网站托管服务，让你可以直接从 Git 仓库部署网站。

---

## 快速开始

### 1. 创建 Pages 仓库

1. 登录 [FeiCode](https://feicode.com)
2. 点击右上角 "+" → "新建仓库"
3. 仓库名称**必须**是 `pages`
4. 设置为**公开**仓库
5. 创建仓库

### 2. 推送你的网站

```bash
# 克隆你的 pages 仓库
git clone https://feicode.com/你的用户名/pages.git
cd pages

# 创建你的网站（必须有 index.html）
cat > index.html << "HTML"
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>我的网站</title>
</head>
<body>
    <h1>欢迎来到我的网站！</h1>
    <p>这是我在 FeiCode Pages 上的第一个网站。</p>
</body>
</html>
HTML

# 提交并推送
git add .
git commit -m "Initial commit"
git push origin main
```

### 3. 访问你的网站

推送成功后，你的网站会自动部署到：

**https://你的用户名.feibisi.net**

例如：
- 用户 `zhang3` → https://zhang3.feibisi.net
- 用户 `lisi` → https://lisi.feibisi.net

---

## 📁 支持的文件类型

- **HTML** (.html, .htm)
- **CSS** (.css)
- **JavaScript** (.js)
- **图片** (.jpg, .png, .gif, .svg, .webp)
- **字体** (.woff, .woff2, .ttf, .otf)
- **文档** (.pdf, .json, .xml)

---

## 📋 要求

### ✅ 必须满足

1. 仓库名称必须是 `pages`
2. 仓库必须是公开的
3. 必须有 `index.html` 文件在根目录
4. 推送到 `main` 或 `master` 分支

### ❌ 不支持

1. 服务器端代码（PHP、Python、Node.js 等）
2. 数据库
3. WebSocket
4. 私有仓库

---

## 🔄 部署流程

```
推送代码到 Git
    ↓
Git Hook 自动触发
    ↓
文件部署到服务器
    ↓
网站立即可访问
```

**部署时间**：通常 1-5 秒

---

## 📂 目录结构示例

```
pages/
├── index.html          # 首页（必需）
├── about.html          # 关于页面
├── css/
│   └── style.css      # 样式文件
├── js/
│   └── main.js        # JavaScript
└── images/
    └── logo.png       # 图片
```

---

## 🎨 完整示例

### 简单博客

```bash
cd pages

# 创建首页
cat > index.html << HTML
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我的博客</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>我的个人博客</h1>
        <nav>
            <a href="index.html">首页</a>
            <a href="about.html">关于</a>
        </nav>
    </header>
    <main>
        <article>
            <h2>第一篇文章</h2>
            <p>这是我在 FeiCode Pages 上的第一篇文章...</p>
        </article>
    </main>
</body>
</html>
HTML

# 创建样式
cat > style.css << CSS
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
}

header {
    border-bottom: 2px solid #333;
    padding-bottom: 20px;
    margin-bottom: 30px;
}

nav a {
    margin-right: 15px;
    text-decoration: none;
    color: #0066cc;
}
CSS

# 提交
git add .
git commit -m "Add blog design"
git push
```

---

## 🔍 故障排查

### 问题：推送后看不到更新

**解决方法：**

1. 确认推送到了 `main` 或 `master` 分支
2. 检查部署日志：
   ```bash
   ssh 你的服务器 "tail /var/log/forgejo-pages-deploy.log"
   ```
3. 清除浏览器缓存（Ctrl+F5）

### 问题：404 Not Found

**解决方法：**

1. 确认仓库根目录有 `index.html`
2. 确认文件名大小写正确
3. 确认仓库名称是 `pages`

### 问题：403 Forbidden

**解决方法：**

1. 确认仓库是公开的
2. 确认有 `index.html` 文件

---

## 💡 高级使用

### 自定义 404 页面

创建 `404.html` 文件：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>页面未找到</title>
</head>
<body>
    <h1>404 - 页面未找到</h1>
    <p><a href="/">返回首页</a></p>
</body>
</html>
```

### 使用静态站点生成器

FeiCode Pages 支持任何静态站点生成器：

- **Hugo**: `hugo && git add public/* && git commit -m "Update" && git push`
- **Jekyll**: `jekyll build && git add _site/* && git commit -m "Update" && git push`
- **Hexo**: `hexo generate && git add public/* && git commit -m "Update" && git push`

---

## 📞 支持

- **问题反馈**: [FeiCode Issues](https://feicode.com/feiCode/pages/issues)
- **电子邮件**: admin@feicode.com
- **查看部署日志**: 
  ```bash
  tail -f /var/log/forgejo-pages-deploy.log
  ```

---

## 📊 限制

- 单个仓库大小: 建议不超过 100MB
- 单个文件大小: 建议不超过 10MB
- 静态文件缓存: 30 天

---

**享受你的 FeiCode Pages 之旅！** 🚀
