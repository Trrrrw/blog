+++
date = '2025-05-15T14:41:00+08:00'
title = 'Hugo Stack主题配置'
tags = ['Hugo','Stack','GitHub','Waline']
categories = ['教程']
image = 'cover.webp'
+++

## 前言
在上一篇文章中我们成功搭建了一个使用Stack主题的博客，并将其部署在了Vercel上。但此时网站中只有刚刚新建的文章，非常简陋，甚至头像也没有。  
而Stack主题官网的文档不仅是英文的，而且给出的内容非常有限。  
所以这里单独开一篇来说一下Stack主题的配置。

> - 对于 **static** 和 **assets** 这两个文件夹，Hugo 在构建时会直接将 **static** 文件夹下的文件复制到网站的根目录下，而 **assets** 文件夹下的文件会被编译后得到一个链接。  
> - 例如，我的网站图标是 **static/favicon.webp**，在最终上线后，可以直接访问 [https://www.trrw.tech/favicon.webp](https://www.trrw.tech/favicon.webp) 来打开这个图片。
而我首页的头像图片则是 **assets/img/avatar.jpg**，他的链接是 [https://www.trrw.tech/img/avatar_hu_b50a61df1acbb930.jpg](https://www.trrw.tech/img/avatar_hu_b50a61df1acbb930.jpg)  
> - 但是在配置中，这两个文件夹下的文件使用方式是一样的，上个两个文件的使用方式分别是：`favicon.webp` 和 `img/avatar.jpg`。

## 网站基础信息
### 网站标题
打开 **config/_default/config.toml** (在新版中这个 **config.toml** 也可以重命名成 **hugo.toml** )  
```toml
# config/_default/config.toml

baseURL = 'https://www.trrw.tech/'
languageCode = 'zh-cn'
title = "Trrrrw's Blog"
```
- **baseURL**：就填你现在打开网站后在主页时的网址就行，如果是自定义域名就填你的域名。
- **languageCode**：语言代码，这里填中文。(具体的语言代码可以看[这里](https://stack.jimmycai.com/config/i18n))
- **title**：网站标题，显示在左侧栏头像下方以及浏览器标签栏中。

### 网站图标
将你要作为网站图标的图片重命名成 **favicon.png**，然后将其放在 **static** 文件夹中，覆盖掉原先的图片。
配置文件在 **config/_default/params.toml** 中的 **favicon** 项。
```toml
# config/_default/params.toml

favicon = "favicon.png"
```

## 左侧边栏
### 头像
以 **assets/img/avatar.jpg** 为例，其配置在 **config/_default/params.toml** 中：
```toml
# config/_default/params.toml

[sidebar.avatar]
enabled = true
local = true
src = "img/avatar.jpg"
```
- **enabled**：是否启用头像
- **local**：是否使用本地图片，为 **false** 时需 **src** 需要填写图片链接而非本地图片路径
- **src**：图片链接

### 副标题

```toml
# config/_default/params.toml

[sidebar]
emoji = "❤️"
subtitle = "Spending a lifetime to taste the love and pain."
```
- **emoji**：左侧栏头像右下角可以显示一个 **emoji**
- **subtitle**：副标题

### 社交图标

```toml
# config/_default/menu.toml

[[social]]
identifier = "github"
name = "GitHub"
url = "https://github.com/Trrrrw"
weight = 1

[social.params]
icon = "brand-github"
```
- **identifier**：应该是给Hugo区分不同图标用的，不同图标的 **identifier** 不能相同
- **name**：鼠标悬停在图标上时显示的文字
- **url**：跳转链接
- **weight**：显示顺序，数字越小越靠前
- **icon**：图标名称，可以在这个网站上查找 [https://tabler.io/icons](https://tabler.io/icons)

如果网站上没有你想要的图标，可以将svg文件放在 **assets/icons** 文件夹中，之后在 **icon** 中填写文件名即可：
```toml
# config/_default/menu.toml

[social.params]
icon = "brand-x"    # 对应 assets/icons/brand-x.svg
```

### 导航菜单
设置导航菜单只需要在你想要显示在左侧栏的页面(page)的 **Front Matter** 中添加 **menu** 项即可：
```markdown
<!-- content/page/archives/index.md -->

+++
# ... existing code ...

[menu.main]
weight = 2
[menu.main.params]
icon = "archives"
+++
```
- **weight**：显示顺序，数字越小越靠前

而首页则是 **content/_index.md**：
```markdown
<!-- content/_index.md -->

+++
[menu.main]
name = "主页"
weight = -1 # 将首页置顶
[menu.main.params]
icon = "home"
+++
```

## 页面 Page

一般一个 blog 的 page 会有 **首页 home**、**归档 archives**、**链接 links**、**关于 about**、**搜索 search** 

### 首页、归档
- 首页一般只需要配置上一节中提到的 **menu** 项即可  
- 归档页面创建这个文件即可：**content/page/archives/index.md**

### 链接
这一部分可以参考 *「[Stack主题友链页面美化]({{< ref "Stack主题友链页面美化" >}})」*  
下面是**Stack**默认的**links**页面实现方式

```markdown
<!-- content/page/links/index.md -->

+++
# 基本信息
title = "链接"
layout = 'links'
slug = 'links'
toc = false
readingTime = false
license = false

# 友链
[[links]]
title = "友链1名称"
description = "简介"
website = "https://www.trrw.tech/"
image = "https://www.trrw.tech/favicon.webp"

[[links]]
title = "友链2名称"
description = "简介"
website = "https://www.trrw.tech/"
image = "https://www.trrw.tech/favicon.webp"

# 菜单栏设置
[menu.main]
weight = 3
[menu.main.params]
icon = "link"
+++

<!-- 下面是正常的 Markdown 这部分会显示在友链页面的顶部 -->
在此页面留言，或者给我发邮件。

> 名称：Trrrrw's Blog
> 
> 简介：Spending a lifetime to taste the love and pain.
> 
> 地址：https://www.trrw.tech/
> 
> 头像：https://www.trrw.tech/favicon.webp
```

### 关于、搜索
- **关于**页面：**content/page/about/index.md**，就和文章一样写就行
- **搜索**页面：**content/page/search/index.md**，一般不需要特殊配置

## 页脚
### 版权声明
```toml
# config/_default/params.toml

[footer]
since = 2022    # 起始年份
```
此时页脚会自动生成 **© 起始年份 - 当前年份 网站标题**

### 自定义文本
```toml
# config/_default/params.toml

[footer]
since = 2022    # 起始年份
customText = '自定义内容'
```
可用于添加**ICP备案号**或自定义内容

## 分类
分类文件夹是 **content/categories**  
在这个文件夹下创建以分类名称命名的文件夹，然后在这个文件夹下创建一个 **_index.md** 文件，内容如下：
```markdown
+++
title = "教程"
image = "cover.webp"
+++
```
- **title**：分类名称
- **image**：分类页封面，非必须

## 标签
标签直接在每个文章的 **Front Matter** 中添加 **tags** 项即可：
```markdown
+++
# ... existing code...

tags = ["Hugo","Stack","GitHub","Vercel"]
+++
```

## 评论
在 **config/_default/params.toml** 的 **comments** 参数中配置(这里以 [waline](https://waline.js.org/) 为例)：
```toml
# config/_default/params.toml

[comments]
enabled = true
provider = "waline"

# ... existing code...

[comments.waline]
serverURL = "waline.trrw.tech"
lang = "zh-CN"
visitor = ""
avatar = "img/Akkarin.jpg"
emoji = ["https://cdn.jsdelivr.net/gh/walinejs/emojis/weibo"]
requiredMeta = ["name", "email", "url"]
placeholder = "欢迎留下宝贵的评论！请留下正确的邮箱以便有回复时进行邮箱提醒，请勿发布任何与本文章无关的内容。"

[comments.waline.locale]
admin = "站长"
```
- **comments**
  - **enabled**：是否启用评论
  - **provider**：评论提供商
- **comments.waline**
  - **serverURL**：评论服务器地址
  - **lang**：语言
  - **visitor**：访问者头像（这一项和下面一项暂时没确定有什么具体效果）
  - **avatar**：评论者头像
  - **emoji**：表情服务
  - **requiredMeta**：必填项
  - **placeholder**：评论框占位文本
- **comments.waline.locale**
  - **admin**：管理员在自己网站评论时在昵称旁显示的文本

> 具体 Waline 的配置可以看 [Waline 文档](https://waline.js.org/guide/get-started/)

## 附录
### 参考文献
1. [HUGO中文文档](https://hugo.opendocs.io/)
2. [Stack主题文档](https://stack.jimmycai.com/)
3. [失迹の博客 | 使用 Hugo + Stack 简单搭建一个博客](https://blog.reincarnatey.net/2023/build-hugo-blog-with-stack-mod/)

### 文章封面
[天才たちのてぇてぇ](https://www.pixiv.net/artworks/126090215)
