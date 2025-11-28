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

## ⚠️ 重要注意事项

### 1. 浏览器缓存问题

**问题**：推送更新后，浏览器仍显示旧内容

**原因**：浏览器会缓存静态文件（HTML、CSS、JS、图片等），提高加载速度

**解决方法**：
- **Windows/Linux**: `Ctrl + Shift + R` 或 `Ctrl + F5`
- **macOS**: `Cmd + Shift + R`
- **Chrome 开发者模式**:
  1. 打开开发者工具（F12）
  2. 右键点击刷新按钮
  3. 选择"清空缓存并硬性重新加载"
- **无痕模式测试**: 使用浏览器的隐私/无痕模式访问

### 2. Git 推送冲突

**问题**：推送时提示 `non-fast-forward` 错误

**原因**：本地分支落后于远程分支

**解决方法**：
```bash
# 方法1：先拉取再推送（推荐）
git pull origin main
git push origin main

# 方法2：变基后推送（保持线性历史）
git pull --rebase origin main
git push origin main

# 方法3：强制推送（⚠️ 会覆盖远程更改，谨慎使用）
git push --force-with-lease origin main
```

### 3. 合并提交不自动部署

**问题**：使用 `git merge` 产生的合并提交可能不会触发自动部署

**临时解决方法**：联系管理员手动触发部署

**预防方法**：
- 使用 `git pull --rebase` 代替 `git pull`
- 或者在推送后检查网站是否更新

### 4. 文件路径大小写敏感

**注意**：Linux 服务器的文件系统区分大小写

**示例**：
- `Logo.png` 和 `logo.png` 是**不同的文件**
- HTML 中引用 `<img src="logo.png">` 但文件名是 `Logo.png` 会导致 404

**建议**：
- 统一使用小写文件名
- 在 HTML/CSS 中引用时确保大小写匹配

### 5. 相对路径 vs 绝对路径

**相对路径**（推荐）：
```html
<!-- ✅ 推荐：相对路径 -->
<link rel="stylesheet" href="css/style.css">
<img src="images/logo.png">
<a href="about.html">关于</a>
```

**绝对路径**（需要调整）：
```html
<!-- ⚠️ 需要修改为你的域名 -->
<link rel="stylesheet" href="https://yourname.feibisi.net/css/style.css">
```

### 6. 特殊文件和文件夹

**隐藏文件**（以 `.` 开头）：
- `.gitignore` - Git 忽略规则
- `.nojekyll` - 禁用 Jekyll 处理
- `.domains` - 自定义域名配置（计划中）

**保留文件夹**：
- `.git/` - Git 仓库数据（不会部署）
- `node_modules/` - 建议添加到 `.gitignore`

---

## 🔍 故障排查

### 问题1：推送后看不到更新

**可能原因**：
1. 浏览器缓存（最常见）
2. 推送到了错误的分支
3. 合并提交未触发部署
4. 部署过程出错

**排查步骤**：

**步骤1**: 强制刷新浏览器
```
Windows/Linux: Ctrl + Shift + R
macOS: Cmd + Shift + R
```

**步骤2**: 确认推送到正确分支
```bash
git branch  # 查看当前分支，应该是 main 或 master
git log --oneline -3  # 查看最近的提交
```

**步骤3**: 检查部署日志（管理员）
```bash
ssh your-server "tail -30 /var/log/forgejo-pages-deploy.log"
```

**步骤4**: 使用无痕模式测试
- 打开浏览器无痕模式
- 访问你的网站
- 如果无痕模式能看到更新，说明是缓存问题

### 问题2：404 Not Found

**可能原因**：
1. 缺少 `index.html` 文件
2. 文件名大小写错误
3. 文件路径错误
4. 仓库名称不是 `pages`

**解决方法**：

**检查1**: 确认根目录有 `index.html`
```bash
ls -la pages/
# 应该看到 index.html 在根目录
```

**检查2**: 确认文件名大小写
```bash
# 错误示例
git add Index.html  # ❌ 大写 I
git add index.HTML  # ❌ 大写 HTML

# 正确示例
git add index.html  # ✅ 全小写
```

**检查3**: 确认仓库名称
- 仓库名称必须是 `pages`（全小写）
- 访问地址：`https://yourname.feibisi.net`

### 问题3：403 Forbidden

**可能原因**：
1. 仓库设置为私有
2. 文件权限错误（服务器端）
3. 缺少必需文件

**解决方法**：

**检查1**: 确认仓库公开
1. 访问 https://feicode.com/你的用户名/pages
2. 检查右上角是否显示"公开"
3. 如果是"私有"，进入设置 → 修改为公开

**检查2**: 确认有 `index.html`
```bash
ls pages/index.html  # 确认文件存在
```

### 问题4：样式/图片不显示

**可能原因**：
1. 路径错误
2. 文件未提交
3. 大小写不匹配
4. 浏览器缓存

**解决方法**：

**检查1**: 验证文件是否提交
```bash
git status  # 查看未提交的文件
git add css/ images/  # 添加文件夹
git commit -m "Add assets"
git push
```

**检查2**: 检查路径引用
```html
<!-- ✅ 正确：相对路径 -->
<link rel="stylesheet" href="css/style.css">
<img src="images/logo.png">

<!-- ❌ 错误：绝对路径 -->
<link rel="stylesheet" href="/css/style.css">  <!-- 缺少域名 -->
<img src="C:/Users/你/Desktop/logo.png">  <!-- 本地路径 -->
```

**检查3**: 使用浏览器开发者工具
1. 打开开发者工具（F12）
2. 切换到"Network"（网络）标签
3. 刷新页面
4. 查看哪些资源加载失败（红色）
5. 点击失败的资源查看错误原因

### 问题5：推送失败 (non-fast-forward)

**错误信息**：
```
! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs
```

**原因**：本地分支落后于远程分支

**解决方法**：
```bash
# 查看状态
git status
git log --oneline -5

# 拉取并合并远程更改
git pull origin main

# 如果有冲突，解决后：
git add .
git commit -m "Resolve conflicts"

# 推送
git push origin main
```

### 问题6：网站访问很慢

**可能原因**：
1. 图片文件过大
2. 未压缩 CSS/JS
3. 网络问题

**优化建议**：

**优化1**: 压缩图片
- 使用工具：TinyPNG, ImageOptim
- 目标：单张图片 < 500KB
- 格式：优先使用 WebP、AVIF

**优化2**: 压缩代码
```bash
# CSS 压缩
npm install -g clean-css-cli
cleancss -o style.min.css style.css

# JS 压缩
npm install -g terser
terser script.js -o script.min.js
```

**优化3**: 使用 CDN 加载库
```html
<!-- ✅ 使用 CDN -->
<script src="https://cdn.jsdelivr.net/npm/vue@3/dist/vue.global.js"></script>

<!-- ❌ 不要提交 node_modules -->
<script src="node_modules/vue/dist/vue.js"></script>
```

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

**Hugo**:
```bash
# 生成静态文件到 public/
hugo

# 提交生成的文件
git add public/*
git commit -m "Update site"
git push
```

**Jekyll**:
```bash
# 生成静态文件到 _site/
jekyll build

# 提交生成的文件
git add _site/*
git commit -m "Update site"
git push
```

**Hexo**:
```bash
# 生成静态文件到 public/
hexo generate

# 提交生成的文件
git add public/*
git commit -m "Update site"
git push
```

**VitePress / VuePress**:
```bash
# 构建文档站点
npm run docs:build

# 提交 dist/ 或 .vuepress/dist/
git add dist/
git commit -m "Update docs"
git push
```

### 添加 Favicon（网站图标）

**方法1：使用 .ico 文件**
```html
<link rel="icon" href="favicon.ico" type="image/x-icon">
```

**方法2：使用 PNG/SVG（推荐）**
```html
<!-- PNG 格式 -->
<link rel="icon" type="image/png" sizes="32x32" href="favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="favicon-16x16.png">

<!-- SVG 格式（现代浏览器）-->
<link rel="icon" type="image/svg+xml" href="favicon.svg">

<!-- Apple Touch Icon（iOS 设备）-->
<link rel="apple-touch-icon" sizes="180x180" href="apple-touch-icon.png">
```

**生成 Favicon**：
- 在线工具：https://realfavicongenerator.net
- 或使用 https://favicon.io

### 添加 SEO 元标签

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- 基本 SEO -->
    <title>你的网站标题 - 描述</title>
    <meta name="description" content="网站描述，140字以内">
    <meta name="keywords" content="关键词1, 关键词2, 关键词3">
    <meta name="author" content="你的名字">

    <!-- Open Graph (社交媒体分享) -->
    <meta property="og:title" content="你的网站标题">
    <meta property="og:description" content="网站描述">
    <meta property="og:image" content="https://yourname.feibisi.net/og-image.jpg">
    <meta property="og:url" content="https://yourname.feibisi.net">
    <meta property="og:type" content="website">

    <!-- Twitter Card -->
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:title" content="你的网站标题">
    <meta name="twitter:description" content="网站描述">
    <meta name="twitter:image" content="https://yourname.feibisi.net/twitter-image.jpg">
</head>
<body>
    <!-- 你的内容 -->
</body>
</html>
```

### 添加 Google Analytics（网站统计）

```html
<!-- 在 </head> 前添加 -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

**国内替代方案**：
- 百度统计：https://tongji.baidu.com
- 51.la：https://www.51.la

### 使用 .gitignore

创建 `.gitignore` 文件，避免提交不必要的文件：

```gitignore
# 操作系统文件
.DS_Store
Thumbs.db

# 编辑器配置
.vscode/
.idea/
*.swp
*.swo

# 依赖文件（不要提交）
node_modules/
vendor/

# 构建产物（如果从源码构建，不要提交这些）
dist/
build/
.cache/

# 本地环境配置
.env
.env.local

# 日志文件
*.log
npm-debug.log*
```

### 响应式设计最佳实践

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>响应式网站</title>
    <style>
        /* 移动优先设计 */
        body {
            font-size: 16px;
            padding: 10px;
        }

        .container {
            max-width: 100%;
        }

        /* 平板设备 */
        @media (min-width: 768px) {
            body {
                font-size: 18px;
                padding: 20px;
            }
            .container {
                max-width: 720px;
                margin: 0 auto;
            }
        }

        /* 桌面设备 */
        @media (min-width: 1024px) {
            .container {
                max-width: 960px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 你的内容 -->
    </div>
</body>
</html>
```

### 添加暗色模式支持

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>支持暗色模式的网站</title>
    <style>
        /* 默认（亮色）模式 */
        :root {
            --bg-color: #ffffff;
            --text-color: #333333;
            --link-color: #0066cc;
        }

        /* 暗色模式 */
        @media (prefers-color-scheme: dark) {
            :root {
                --bg-color: #1a1a1a;
                --text-color: #e0e0e0;
                --link-color: #66b3ff;
            }
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            transition: background-color 0.3s, color 0.3s;
        }

        a {
            color: var(--link-color);
        }
    </style>
</head>
<body>
    <h1>支持暗色模式</h1>
    <p>这个网站会根据系统设置自动切换亮色/暗色模式。</p>
</body>
</html>
```

### 性能优化技巧

**1. 懒加载图片**
```html
<!-- 使用 loading="lazy" 属性 -->
<img src="image.jpg" alt="描述" loading="lazy">
```

**2. 预加载关键资源**
```html
<!-- 在 <head> 中预加载 -->
<link rel="preload" href="style.css" as="style">
<link rel="preload" href="main.js" as="script">
```

**3. 使用 WebP 图片格式**
```html
<picture>
    <!-- 支持 WebP 的浏览器加载 WebP -->
    <source srcset="image.webp" type="image/webp">
    <!-- 不支持的浏览器回退到 JPG -->
    <img src="image.jpg" alt="描述">
</picture>
```

**4. 内联关键 CSS**
```html
<head>
    <!-- 内联首屏 CSS，加快首次渲染 -->
    <style>
        /* 关键的首屏样式 */
        body { margin: 0; font-family: Arial; }
        .header { background: #333; color: white; }
    </style>

    <!-- 其他 CSS 异步加载 -->
    <link rel="preload" href="full-styles.css" as="style" onload="this.onload=null;this.rel='stylesheet'">
    <noscript><link rel="stylesheet" href="full-styles.css"></noscript>
</head>
```

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
