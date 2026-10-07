---
title: github-page搭建
date: 2026-10-06
categories: Jekyll
tags:
  - github-page
  - Jekyll
  - 博客
render_with_liquid: false
---

## 怎么用GitHub挂个人网站 

GitHub 免费提供的**静态网站托管**，把你的网页代码放在 GitHub 仓库，就能直接上线个人网站。

> 只能放**静态网页**：纯 HTML/CSS/JS、Vue/React 打包后的静态产物、Hexo/Hugo 博客；**不能运行后端代码、数据库、登录接口**（没有服务器环境）GitHub Doc...

### 两种站点类型

1. **个人主页（推荐做简历 / 个人介绍站）**
    
    仓库名字必须严格是：`你的github用户名.github.io`
    
    上线后默认地址：`https://你的github用户名.github.io`
    
    一个账号只能建**1 个**这种个人站点。
    
2. **项目网站**
    
    任意仓库都可以开启 Pages，用来放项目文档，地址：`https://用户名.github.io/仓库名`
    

###  优点

1. **永久免费**：每月带宽上限 100GB，绝大多数个人简历、博客完全够用，仓库上限 1GB，单文件最大 100MB腾讯云
2. 自动 HTTPS，自带 SSL 证书
3. 可以绑定你自己买的自定义域名
4. 代码 push 上传之后，自动部署更新，版本由 Git 管理
5. 适合：程序员简历页、作品集、技术博客、项目文档

###  最简上手步骤 

注册 GitHub 账号，新建仓库，命名 username.github.io（username 替换成你的用户名） 

在仓库里写 index.html（网站首页） 

进入仓库 Settings → Pages，选择部署分支，保存 

等待几分钟，访问 https://username.github.io 就能打开网站

Jekyll 会自动忽略带 _下划线开头的文件夹（_posts、_layouts）Jekyll 博客文章，必须放在 _posts文件夹 内，md 文件名严格遵守格式：YYYY-MM-DD-文章标题.md 例如 2026-10-06-first-blog.md，放在仓库根目录_posts下面，Jekyll 才会识别为博客文章。

## 手把手添加 Jekyll 模板
（放到你的 Obsidian 库 `D:\beaver503.github.io`）

> 全部文件直接在这个文件夹新建，和 index.html 同级，写完 Obsidian Git 一键提交推送，GitHub Pages 自动编译。

### 1. 新建 `_config.yml`（Jekyll 核心配置文件，放在根目录）

新建文本文档，粘贴下面内容，保存，改名 `_config.yml`

```yaml
# 站点基础信息
title: Beaver 的博客
description: Obsidian + GitHub Pages 搭建的个人博客
author: beaver503

# 网页url，固定写这个
baseurl: ""
url: "https://beaver503.github.io"

# 主题（使用Jekyll默认 minima，开箱即用不用额外装东西）
theme: minima

# 文章目录
collections:
  posts:
    output: true

# 开启语法高亮
markdown: kramdown
highlighter: rouge
```

### 2. 新建文件夹 `_posts`（**必须下划线开头**）

在根目录新建文件夹，名字：`_posts`

> ✅ 所有博客文章都放这里 ✅ 文件命名强制格式：`年-月-日-文章标题.md` 示例：`2026-10-06-my-first-article.md`

新建第一篇文章，放到`_posts`里，内容示例：

```markdown
---
layout: post
title: "第一篇博客"
date: 2026-10-06
---

# Hello Blog
这是我用Obsidian写、推送到GitHub Pages的第一篇文章。

可以直接写markdown，**加粗、列表、链接都支持**。
```

### 3. 新建文件夹 `_layouts`（网页布局模板）

根目录新建文件夹：`_layouts` 在`_layouts`里面新建文件 `post.html`，用来定义博客文章页面样式：

```html

<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>{{ page.title }}</title>
</head>
<body>
  <h1>{{ page.title }}</h1>
  <p>发布时间：{{ page.date }}</p>
  {{ content }}
</body>
</html>
```

### 4. 根目录 `index.html`（博客首页，覆盖你现有的）

根目录的 index.html，作为博客首页，列出所有文章：

```html
---
---
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>{{ site.title }}</title>
</head>
<body>
<h1>{{ site.title }}</h1>
<p>{{ site.description }}</p>

<h2>文章列表</h2>
<ul>
{% for post in site.posts %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a> — {{ post.date | date:"%Y-%m-%d" }}
  </li>
{% endfor %}
</ul>
</body>
</html>
```

问题：Liquid 模板代码原样显示，**没有被 Jekyll 渲染**

页面直接打印出来，说明 Jekyll**没有把这个 index.html 当成模板去处理**。

原因

`index.html` **缺少 Front Matter（最顶部的`---`分隔块）**

👉 Jekyll 规则：HTML/markdown 文件**必须在文件最开头加上`---`**，才会解析 Liquid 模板；没有，就直接原样输出文本，不执行变量、循环。

修复方法

打开你的 `index.html`，**在文件最最顶部**，添加三横`---`，可以空配置：


1. 保存上面全部文件，你的 Obsidian 库里面就会出现这几个新文件 / 文件夹
    
2. 打开 Obsidian Git 插件面板
    
3. 点 **Commit-and-sync**
    
4. 等待 10~60 秒，GitHub Pages 自动重新构建
    
5. 访问 [https://beaver503.github.io](https://beaver503.github.io)，首页就会展示文章列表，点标题打开博文
    

## 安装Ruby

为什么安装Ruby，因为可以先本地预览然后提交到github

Windows 安装 Ruby + Jekyll（安装位置+完整步骤） 
> 重点：**Ruby 是独立程序，装在系统盘/你指定文件夹；Jekyll 是 Ruby 的插件(gem)，跟着Ruby目录走，不需要单独选位置** > 推荐下载：**Ruby+Devkit** 版本（必须带Devkit，否则装Jekyll会报错） 
### 1. 下载RubyInstaller 
官网：https://rubyinstaller.org/downloads/ 
选：`Ruby+Devkit 3.2.x-x64`（不要选不带Devkit的版本） 
### 2. 安装路径怎么填（重要） 
✅ 推荐：`C:\Ruby32-x64` 或者 `D:\Ruby32-x64` 
⚠️ 规则：**路径不能有中文、空格**  
❌ 不要：`C:\Program Files\Ruby`（有空格容易出问题） 
❌ 不要：`D:\软件\Ruby`（中文目录） 
安装向导里**勾选 Add Ruby executables to your PATH**，自动加入系统环境变量。 
安装到最后一步：勾选 `Run ridk install to set up MSYS2`，点Finish。 
弹出命令窗口，输入 `3` 回车，
安装MSYS2编译工具链，等待跑完。 
### 3. 验证Ruby是否装好 
**关闭所有旧PowerShell，新开一个终端**（环境变量才生效） ```
```
powershell ruby -v gem -v
``` 
输出版本号，代表Ruby安装成功。 
### 4. 安装 Jekyll + Bundler（Jekyll就装在Ruby目录下） 
```
powershell gem install jekyll bundler 
```

- Jekyll 实际存放位置：`C:\Ruby32-x64\lib\ruby\gems\3.2.0\gems\jekyll-xxx` 
- **不用手动选Jekyll安装目录，gem自动管理** 
- 验证： ```powershell jekyll -v ``` 
- 输出版本号，代表Jekyll安装完成。 
### 5. 在你的博客仓库 
D:\beaver503.github.io 使用 进入仓库文件夹： 
```powershell 
cd D:\beaver503.github.io 
bundle init 
bundle add jekyll 
```

本地启动预览 
```bash
bundle exec jekyll serve --livereload
```

访问：[http://127.0.0.1:4000](http://127.0.0.1:4000)
> 注意：Ruby是**全局环境**，本机所有Jekyll仓库共用这一套Ruby/Jekyll，**不用每个Obsidian库单独装一份**。 


