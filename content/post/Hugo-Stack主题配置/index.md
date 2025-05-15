+++
date = '2025-03-15T11:17:25+08:00'
draft = true
title = 'Hugo Stack主题配置'
tags = ['Hugo','Stack','GitHub','Vercel']
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
### 网站标题和图标
#### 标题
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

#### 图标
将你要作为网站图标的图片重命名成 **favicon.png**，然后将其放在 **static** 文件夹中，覆盖掉原先的图片。
配置文件在 **config/_default/params.toml** 中的 **favicon** 项。
```toml
# config/_default/params.toml

favicon = "favicon.png"
```

## 左侧边栏
### 头像
以 **assets\img\avatar.jpg** 为例，其配置在 **config/_default/params.toml** 中：
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
# config\_default\menu.toml

[[social]]
identifier = "github"
name = "GitHub"
url = "https://github.com/Trrrrw"
weight = 1

[social.params]
icon = "brand-github"
```
- **identifier**：社交图标名称，在 **config\_default\menu.toml** 中也可以找到
- **name**：显示在左侧栏的名称
- **url**：链接
- **weight**：显示顺序
- **icon**：图标名称，[https://tabler.io/icons](https://tabler.io/icons)