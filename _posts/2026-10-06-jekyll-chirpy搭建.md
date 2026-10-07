---
title: chirpy模板搭建
date: 2026-10-06
categories: Jekyll
tags:
  - Chirpy
  - 博客
render_with_liquid: false
---

##  Chirpy 官方在线预览站点

👉 [https://chirpy.cotes.page/](https://chirpy.cotes.page/) 

这就是Chirpy作者本人的博客，也就是主题完整Demo，你可以直接浏览全部页面：首页文章列表、文章详情页、标签页、分类页、搜索、暗色模式、公式/Mermaid图表演示。

### 页面布局特点

- **左侧侧边栏**：头像、站点名称、导航（首页、分类、标签、归档、关于）
- **主内容区**：文章卡片列表，支持置顶文章
- **文章内页**：右侧自动生成文章目录（TOC），代码高亮、支持LaTeX数学公式、Mermaid流程图
- **一键明暗切换**：白底/深色模式
- **顶部搜索框**：全文站内搜索
- 移动端自动适配，侧边栏折叠成汉堡菜单

### 核心功能一览

1. 文章置顶、标签、两级分类、归档时间线
2. Markdown增强：提示块、图片排版、表格
3. RSS订阅、评论系统接入、访问统计
4. PWA，可以添加到手机桌面

### 使用chirpy模板搭建个人网站

####  模板仓库

 **官方推荐新手用 Chirpy Starter**： [https://github.com/cotes2020/chirpy-starter](https://github.com/cotes2020/chirpy-starter) 


 一键模板创建仓库，本地`bundle install`之后，**本地预览和线上Demo完全一致**。

#### 快速上手（Chirpy Starter）

1. 打开上面starter仓库，点 `Use this template`，新建仓库命名：`beaver503.github.io`

![[Pasted image 20261007141817.png]]

![](assets/img/Pasted image 20261007141817.png)

2. Clone到本地

```bash
git clone 你的仓库地址
```

3. `bundle install`，安装本地Ruby依赖

4. `bundle exec jekyll serve` 本地运行

5. 访问 [http://127.0.0.1:4000](http://127.0.0.1:4000/)

> 文章放在 `_posts`，文件名格式：`2026-10-06-my-note.md`

## 一些常见问题

### 要不想删原来的库？

#### 方案1：直接复用这个仓库（推荐，不用新建库）

1. 把当前仓库里**所有文件全部清空**（本地文件夹全部删掉，保留.git文件夹）
2. 把 Chirpy Starter 的全套文件复制进来
3. `git add`、`git commit`、`git push` 推送覆盖远端仓库
    
    > ✅ 好处：仓库名字还是 `beaver503.github.io`，域名不变，不用改任何Github Pages设置。 ⚠️ 风险：旧代码、旧提交记录全部还在，只是被新文件覆盖，历史提交不会消失。
    

#### 方案2：新建仓库，旧仓库保留（安全稳妥）

1. 先用 `Use this template` 从chirpy-starter生成**新仓库**
2. 旧仓库 `beaver503.github.io` 可以：
    - ① **保留不动**（存档，里面的笔记代码还在，以后可以查看），但Github Pages域名会失效；
    - ② **重命名**：改成别的名字，比如`old-blog-backup`，释放`beaver503.github.io`名字，再把新Starter仓库命名为`beaver503.github.io`；
    - ③ **彻底删除**（不推荐，一旦删除仓库，提交记录全部消失，不可恢复）。

####  我更推荐的操作流程（方案1，原地替换，域名不变）

1. 本地进入 `D:\beaver503.github.io`
2. **删除里面全部文件**，但是不要删掉 `.git` 隐藏文件夹（这个是仓库核心，删了就变成全新文件夹）
3. 下载/克隆 chirpy-starter 的文件，全部粘贴到这个目录
4. `bundle install` 本地测试跑通
5. git提交推送，直接覆盖线上博客

> 💡 注意：**重要文章笔记，先单独备份出来**，再清空仓库，避免误删写好的markdown。文章后续放到新仓库的`_posts`目录。
> 有相同的文件不要替换，保留自己的.git文件
> .obsidian 文件夹不要删！


## Chirpy Starter `_config.yml` 常用配置详细展开

> 文件路径：仓库根目录 `_config.yml` 只贴你大概率会用到的，注释写清楚，直接复制修改即可。

```
# --------------- 站点基础信息 ---------------
title: "Beaver 的笔记"          # 网站标题，浏览器标签、侧边栏显示
tagline: "技术阅读与随笔"       # 副标题，标题下方小字
description: >                  # 网站描述（SEO，搜索引擎抓取）
  个人知识库，记录技术、阅读思考。
author:
  name: Beaver                  # 作者名
  avatar: /assets/img/avatar.jpg # 头像路径，图片放到 assets/img/
  bio: 喜欢折腾笔记与技术        # 个人简介，头像下方
  email:                        # 邮箱（可选）
  social:                       # 社交链接，侧边栏图标
    - type: github
      icon: github
      url: " "

# --------------- 网站链接 ---------------
url: " "
baseurl: "" # 个人主页仓库保持空字符串，不要填东西

# --------------- 文章分页 ---------------
paginate: 10                    # 首页一页展示多少篇文章
paginate_path: "/page:num/"

# --------------- 语言与时区 ---------------
lang: zh-CN
timezone: Asia/Shanghai

# --------------- 主题功能开关 ---------------
theme_mode: dark                # 可选 dark / light / auto，auto跟随系统明暗
# 侧边栏是否展开
sidebar:
  nav: sidebar-main             # 导航菜单定义在 _data/sidebar-main.yml

# --------------- 文章相关 ---------------
post:
  # 是否在文章右侧生成目录TOC
  toc: true
  # TOC最多识别几级标题
  toc_level: [2,3]
  license: false                # 是否显示文章版权声明

# --------------- Markdown增强 ---------------
markdown: kramdown
kramdown:
  input: GFM
  syntax_highlighter: rouge

# 开启Mermaid流程图
mermaid: true

# LaTeX数学公式（KaTeX渲染）
katex: true

# --------------- 搜索 ---------------
search: true                    # 开启站内搜索

# --------------- RSS订阅 ---------------
rss: true

# --------------- 评论系统（Giscus，推荐）---------------
comments:
  provider: giscus
  giscus:
    repo: beaver503/beaver503.github.io
    repo_id:
    category: Announcements
    category_id:
    mapping: title
    input_position: bottom
    loading: lazy

# --------------- 插件 ---------------
plugins:
  - jekyll-paginate
  - jekyll-sitemap
  - jekyll-gist
  - jekyll-feed
  - jekyll-seo-tag
  - jekyll-archives
  - jekyll-include-cache

# 归档设置
jekyll-archives:
  enabled: [categories, tags, year]
  layouts:
    category: category
    tag: tag
    year: year
  permalinks:
    category: '/categories/:name/'
    tag: '/tags/:name/'
    year: '/:year/'
```

### 一、头像配置详细步骤

1. 准备图片，建议正方形，大小 200×200 左右，jpg/png
2. 放到路径：`assets/img/avatar.jpg`
3. 在 `_config.yml` 修改这一行：

```
avatar: /assets/img/avatar.jpg
```

> 注意：**开头必须带 `/`**，代表从网站根目录读取。 修改配置文件后，需要重启 jekyll serve 才生效。

### 二、侧边栏导航菜单

导航菜单文件：`_data/sidebar-main.yml` 默认自带首页、分类、标签、归档、关于。 你可以在这里增删菜单，示例：

```
- name: 首页
  link: /
- name: 分类
  link: /categories/
- name: 标签
  link: /tags/
- name: 归档
  link: /archives/
- name: 关于
  link: /about/
```

新建「关于」页面：在根目录新建 `about.md`

```
---
layout: page
title: 关于我
---
这里写自我介绍。
```

### 三、Giscus评论系统详细说明（可选）

> 给每篇文章加评论区。

1. 打开 [https://giscus.app/](https://giscus.app/)
2. 填入你的github仓库 `beaver503/beaver503.github.io`
3. 按页面指引，拿到 `repo_id` 和 `category_id`，回填到上面_config.yml的giscus区块。
4. 提交代码，线上页面就会出现评论框。本地预览看不到评论，只能线上生效。

### 四、Mermaid流程图 / LaTeX公式

- `mermaid: true`：直接在markdown写流程图，不需要额外插件

````
```mermaid
graph LR
A[笔记] --> B[Chirpy博客]
````

````
- `katex: true`：支持数学公式
```markdown
$$E=mc^2$$
````

### 五、写文章Front Matter模板（放在_post里的md头部）

```
---
title: "Jekyll + Chirpy 搭建博客记录"
date: 2026-10-06 14:30:00
categories: 技术
tags: [Jekyll, Chirpy, Obsidian]
toc: true # 单独控制这篇文章是否显示目录
---
正文……
```

文件名必须：`2026-10-06-jekyll-chirpy.md`

### 六、完整 `.gitignore`（Chirpy + Obsidian）

```
# Jekyll
_site/
.sass-cache/
.jekyll-cache/
.jekyll-metadata

# Ruby
Gemfile.lock
vendor/

# Obsidian
.obsidian/

# Windows
Thumbs.db

# Mac
.DS_Store
```

### 七、生效规则

1. 修改 `_config.yml` **必须重启jekyll服务**（Ctrl+C，再重新执行`bundle exec jekyll serve`）
2. 修改文章、普通md页面，保存自动刷新（livereload）

## 图片管理

博客图片统一放到 `assets/img/`，引用写法：

```
![图片描述](/assets/img/demo.png)
```

> Obsidian内部`[[wikilink]]`格式Chirpy**不识别**，图片链接要改成标准markdown格式。

## 截屏直接粘贴到Obsidian
###  图片在哪里

正常 `Win+Shift+S` 截图，`Ctrl+V` 粘贴进 Obsidian，**图片会被自动保存到你的Vault（库）里面**，`![[Pasted image xxx.png]]` 这个链接，指向的就是Vault里的图片文件。

> 你看到 `[[xxx.png]]` 这种链接，**前面少了感叹号 `!` 就不会预览图片，只显示成文本链接**。 正确嵌入写法：`![[Pasted image 20261007143000.png]]`

### 图片应该存在哪里？

打开 Obsidian 设置 → **文件与链接 → 新建附件的默认存放位置**，4个选项决定图片路径：

1. **Vault文件夹（默认）**：直接放在你的笔记库**根目录**，和md笔记放在同一层
2. **和当前文件在同一文件夹**：图片和你当前打开的`.md`笔记放在同一个文件夹
3. **当前文件夹下的子文件夹**：例如 `attachments/`，会在笔记所在目录自动新建这个文件夹放截图（推荐）
4. **在下方指定的文件夹**：统一放到库内固定目录，比如 `assets/`、`attachments/`

文件名一般是：`Pasted image 年月日时分秒.png`，在左侧文件管理器直接搜 `Pasted image` 就能找到。

## 删掉网站下标

![[Pasted image 20261007145418.png]]

![](assets/img/Pasted image 20261007145418.png)

### 找_includes文件夹

Chirpy Starter 用的是**gem主题**，`footer.html`、`sidebar.html` 这些源码**不在你的本地仓库文件夹里**，它们放在Ruby的gem包内部，所以你在本地`_includes`里找不到。

> 两种解决办法：① CSS直接隐藏（最简单，推荐，不用碰gem源码）；② 把主题文件复制到本地覆盖。

### 方案B：如果你想直接修改源码（永久删掉，不是隐藏）

1. 在PowerShell输入这条命令，查看gem主题所在路径

```
bundle info --path jekyll-theme-chirpy
```

会输出类似路径： `C:/Ruby34-x64/lib/ruby/gems/3.4.0/gems/jekyll-theme-chirpy-7.4.1`

2. 进入这个文件夹，里面有`_includes/footer.html`，复制这个文件，粘贴到你本地仓库的 `_includes/` 目录（本地没有`_includes`文件夹就新建）
    
    > 一旦放到本地仓库`_includes`，jekyll就优先读取你本地这个文件，不再读gem里的。
    
3. 打开本地`_includes/footer.html`，找到下面这段，删除：

```
<div class="powered">
  Powered by <a href="[https://jekyllrb.com](https://jekyllrb.com)" target="_blank" rel="noopener">Jekyll</a> & <a href="[https://github.com/cotes2020/jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy)" target="_blank" rel="noopener">Chirpy</a>
</div>
```

版权文字也在这个文件内，可以一起注释。

> 侧边栏左下角图标：同理，复制gem目录内的`_includes/sidebar.html`到本地`_includes`，删除`.sidebar-bottom`整个区块。

---

### 顺带补充

左下角图标（侧边栏底部），也可以直接在`_data/contact.yml`把所有条目注释掉，就不会渲染图标，这个文件**你本地仓库是有的**。 打开`_data/contact.yml`，全部加#注释：

```
# - type: github
#   icon: github
#   url: [https://github.com/beaver503](https://github.com/beaver503)
# - type: rss
#   icon: rss
#   url: /feed.xml
```

保存重启，左下角图标消失。

### 只复制**需要修改的那单个文件**

Jekyll 的规则：

> 本地仓库 `_includes/` 文件夹**只放你要改动的模板**；没放到本地的文件，会继续自动从gem主题包读取。 不需要把gem里`_includes`一整套全部拷过来。

### 需要复制这2个文件

1. `footer.html` → 修改底部版权、Chirpy署名文字
2. `sidebar.html` → 修改侧边栏（左下角社交图标）

> 其他所有文件（head.html、post.html、toc.html等等）**完全不用复制**，继续使用gem原版。

### 操作流程

1. 在你的仓库根目录新建文件夹 `_includes`（如果不存在）
2. 从gem目录的`_includes`里，**单独拷贝** `footer.html` 和 `sidebar.html` 放到你本地新建的`_includes`
3. 在本地修改这两个文件
4. 保存，重启 `bundle exec jekyll serve`

Jekyll会优先加载你本地这两个文件；剩下的模板依旧读取gem包，不会出问题。

### 补充说明

- 后续如果你想改别的部分（比如文章头部、页面head），**再单独复制对应的那一个文件**过来就行，一次性不用多拷。
- 好处：仓库干净，不会带一堆冗余模板；以后升级Chirpy主题版本也更简单（只需要对比你修改过的少量文件）。
- 坑提醒：不要一次性把全部`_includes`文件复制到本地。后续升级主题时，大量本地文件会覆盖新版主题文件，容易出现样式/功能错乱。

### 顺带回顾

侧边栏左下角图标，**优先用 `_data/contact.yml` 注释全部社交条目**，这个方法不用复制`sidebar.html`，最简单。 只有当你想彻底删掉渲染代码，才需要复制`sidebar.html`。

### 新版 Chirpy（7.x）的 `footer.html` 代码和旧版本不一样，

**没有直接写死 `footer-left / footer-right` 这两个class的标签**。

###  新版 Chirpy 7.x 的 footer.html 完整原版代码

```
<footer class="row">
  <div class="col-12 d-flex justify-content-between align-items-center text-muted">
    <div>
      <p class="mb-0">
        © {{ 'now' | date: "%Y" }} {{ site.author.name }}.
        {% assign copyright_text = site.data.locales[lang].copyright.brief %}
        {% if copyright_text %}
          <span data-bs-toggle="tooltip" data-bs-placement="top" title="{{ site.data.locales[lang].copyright.verbose }}">{{ copyright_text }}</span>
        {% endif %}
      </p>
    </div>
    <div>
      <p class="mb-0">
        {% capture platform_link %}<a href="[https://jekyllrb.com](https://jekyllrb.com)" target="_blank" rel="noopener">Jekyll</a>{% endcapture %}
        {% capture theme_link %}<a href="[https://github.com/cotes2020/jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy)" target="_blank" rel="noopener">Chirpy</a>{% endcapture %}
        {{ site.data.locales[lang].meta | replace: ":platform", platform_link | replace: ":theme", theme_link }}
      </p>
    </div>
  </div>
</footer>
```

> 左右两块是**两个`<div>`**，不是footer-left/footer-right。

### 方案1：直接注释掉页脚全部文字（推荐）

你把gem里的footer.html复制到本地`_includes/footer.html`之后： **把整个`<footer> ... </footer>`块注释掉**，如下：

```
{% comment %}
<footer class="row">
  <div class="col-12 d-flex justify-content-between align-items-center text-muted">
    <div>
      <p class="mb-0">
        © {{ 'now' | date: "%Y" }} {{ site.author.name }}.
        {% assign copyright_text = site.data.locales[lang].copyright.brief %}
        {% if copyright_text %}
          <span data-bs-toggle="tooltip" data-bs-placement="top" title="{{ site.data.locales[lang].copyright.verbose }}">{{ copyright_text }}</span>
        {% endif %}
      </p>
    </div>
    <div>
      <p class="mb-0">
        {% capture platform_link %}<a href="[https://jekyllrb.com](https://jekyllrb.com)" target="_blank" rel="noopener">Jekyll</a>{% endcapture %}
        {% capture theme_link %}<a href="[https://github.com/cotes2020/jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy)" target="_blank" rel="noopener">Chirpy</a>{% endcapture %}
        {{ site.data.locales[lang].meta | replace: ":platform", platform_link | replace: ":theme", theme_link }}
      </p>
    </div>
  </div>
</footer>
{% endcomment %}
```

保存，重启`bundle exec jekyll serve`，页面底部版权、Chirpy署名**全部消失**。

### 方案2：CSS 新版专用选择器（优先试这个，不用改html）

新建`assets/css/custom.css`，写入下面代码

```
/* 页脚整个区域隐藏 */
footer.row {
  display: none !important;
}
/* 侧边栏底部社交图标 */
.sidebar-bottom {
  display: none !important;
}
```

然后在`_includes/head.html`（也要从gem复制到本地），在主题css后面引入这个custom.css

```
<link rel="stylesheet" href="{{ '/assets/css/jekyll-theme-chirpy.css' | relative_url }}">
<link rel="stylesheet" href="{{ '/assets/css/custom.css' | relative_url }}">
```

> 浏览器一定要 `Ctrl+F5` 强制刷新清除缓存！普通刷新不会加载新css。

### 快速定位技巧（以后自己找元素）

1. 浏览器F12打开开发者工具
2. 点左上角**选择元素箭头**，点击页面上你要删除的文字
3. 直接看到对应的html标签和class，复制class写css

> 建议顺序：
> 
> 1. 先改`_data/contact.yml`去掉左下角图标
> 2. 然后用方案1，复制原版footer.html到本地，直接把footer整块注释掉，一次性删掉底部两行文字。

### 修改导航小图标

##  浏览器标签页小图标（Favicon）更换，Chirpy主题

> 就是你截图里「Beaver 的笔记」左边这个图标，术语叫 **favicon**

### 1. 目录位置

在你的项目根目录：

```
assets/img/favicons/
```

> 如果这个文件夹不存在，你手动新建：`assets/img/favicons` ⚠️ 注意：gem版Chirpy，**本地仓库这个文件夹是空的，需要你自己放图标文件进去，Jekyll会优先读取本地assets里的资源**

### 2. 制作多尺寸图标包（推荐）

1. 准备一张**正方形图片**，建议 512×512 以上PNG
2. 打开在线生成网站：[https://realfavicongenerator.net/](https://realfavicongenerator.net/)
3. 上传图片，全部默认选项，拉到底下载zip压缩包
4. 解压后，把里面的：`favicon.ico`、各种png图片、`site.webmanifest` 全部放到 `assets/img/favicons/`，覆盖（如果有旧文件）

> 这些文件包含浏览器标签、手机平板、桌面快捷方式等不同场景的图标。

### 3. 重启jekyll

```
bundle exec jekyll serve
```

浏览器按 `Ctrl+F5` **强制清除缓存刷新**，标签页图标就更新了。

### 简化版（临时快速测试，只改浏览器标签）

如果你不想生成整套图标包：

1. 准备一张正方形图片，命名 `favicon.ico`
2. 放到 `assets/img/favicons/`
3. 重启服务，强制刷新页面

### 补充区分两个图标，别搞混

1. ✅ **浏览器标签图标（你现在想改的）**：`assets/img/favicons/`
2. 侧边栏头像（左侧圆形头像）：`_config.yml` 里的 `author.avatar`，路径一般是`assets/img/avatar.jpg`

###  **新版Chirpy优先加载 `favicon.svg`**

Edge / Chrome 浏览器会**优先读取favicon.svg**，而不是ico。你目录里`favicon.svg`如果还是旧图标，标签页就永远显示旧图。

> `favicon.svg` ，**这个svg才是标签图标主文件**，ico只是备用兜底文件。

#### 步骤1：验证svg文件（关键）

1. 打开无痕窗口，直接访问：

```
[http://127.0.0.1:4000/assets/img/favicons/favicon.svg](http://127.0.0.1:4000/assets/img/favicons/favicon.svg)
```

👉 如果打开是**旧图标**：说明你的 `favicon.svg` 没有替换成新图，只换了ico。 👉 如果打开是**新图标**：说明文件没问题，浏览器缓存。

> realfavicongenerator 生成的包里的 favicon.svg，**一定要替换进去**！很多人只替换ico漏掉svg。

#### 步骤2：清理jekyll编译缓存

1. PowerShell里按`Ctrl+C`关闭jekyll服务
2. 删除项目里整个`_site`文件夹（全部删掉）
3. 确认`assets/img/favicons/`下：
    - favicon.svg（新图标！！）
    - favicon.ico（新图标）
    - 其他png、webmanifest
4. 重新启动：`bundle exec jekyll serve`

#### 步骤3：如果svg已经是新图，绕过浏览器缓存（终极方案）

复制gem里的 `_includes/favicons.html` 到本地`_includes/`

```
bundle info --path jekyll-theme-chirpy
```

打开本地的`favicons.html`，找到svg这一行，**加版本号**

```
<link rel="icon" type="image/svg+xml" href="{{ '/assets/img/favicons/favicon.svg' | relative_url }}?v=1">
```

> `?v=1` 告诉浏览器：这是全新文件，不要读取缓存。 每次改图标就把数字+1（v=2、v=3）

### 快速自检清单

1. assets/img/favicons/favicon.svg ✅ 是新图
2. assets/img/favicons/favicon.ico ✅ 是新图
3. 关闭jekyll → 删除_site → 重启jekyll
4. 无痕窗口访问 
 [http://127.0.0.1:4000/assets/img/favicons/favicon.svg](http://127.0.0.1:4000/assets/img/favicons/favicon.svg)
