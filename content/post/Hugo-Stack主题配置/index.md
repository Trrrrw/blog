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

## 网站基础信息
### 网站标题和图标
#### 标题
打开 `config/_default/config.toml` (在新版中这个 `config.toml` 也可以重命名成 `hugo.toml` )  
```toml
baseURL = 'https://www.trrw.tech/'
languageCode = 'zh-cn'
title = "Trrrrw's Blog"
```
- **baseURL**：就填你现在打开网站后在主页时的网址就行，如果是自定义域名就填你的域名。
- **languageCode**：语言代码，这里填中文。(具体的语言代码可以看[这里](https://stack.jimmycai.com/config/i18n))
- **title**：网站标题，显示在左侧栏头像下方以及浏览器标签栏中。

#### 图标
将你要作为网站图标的图片重命名成`favicon.png`，然后将其放在`static`文件夹中，覆盖掉原先的图片。


## 左侧边栏


