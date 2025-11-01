+++
title = 'Stack 主题下 Waline 美化'
date = '2025-10-22T17:24:14+08:00'
tags = ['Stack', 'Waline']
categories = ['建站记录']
image = 'cover.webp'
+++

## 前言
这篇文章只是简单修改了下 Waline 的配色以及 a 标签的样式  
可以先参考 *「[建站技术 | 使博客更好地接入 Waline](./#参考文献)」* 配置好 Waline

## Waline 美化
`assets\scss\custom.scss`
```scss
// Waline
:root {
    --waline-theme-color: var(--accent-color) !important;
    --waline-active-color: var(--accent-color-darker) !important;
}

.wl-panel {
    border-radius: var(--card-border-radius) !important;
}

.wl-action:first-child {
    display: none;
}

.wl-content a {
    text-decoration: none;
    box-shadow: 0 -2px rgba(var(--link-background-color), var(--link-background-opacity)) inset;
    transition: all .3s ease;

    &:hover {
        color: var(--waline-theme-color) !important;
        box-shadow: 0 calc(-1rem * 2.2) rgba(var(--link-background-color), var(--link-background-opacity-hover)) inset;
    }
}

.wl-header-item input {
    color: var(--card-text-color-secondary);
    font-size: .75em !important;
}
```
比较难绷的是如果你的标题只是 **waline** 的话，会因为 **id="waline"** 而把评论显示在标题位置

## 附录
### 参考文献
1. [建站技术 | 使博客更好地接入 Waline](https://blog.reincarnatey.net/2024/0719-better-waline)

### 文章封面
[遙@RSyaooooo](https://x.com/RSyaooooo/status/1836575756358459883)
