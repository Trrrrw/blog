+++
title = 'Stack 主题美化'
date = '2025-06-30T00:59:59+08:00'
tags = ['Stack', 'Waline']
categories = ['建站记录']
image = 'cover.webp'
draft = true
+++

## 前言
这篇文章只是简单修改了下 Waline 的配色以及 a 标签的样式  
可以先参考 *「[建站技术 | 使博客更好地接入 Waline](./#参考文献)」* 配置好 Waline

## Waline
`assets\scss\custom.scss`
```scss
// Waline
:root {
    --waline-theme-color: #34495e !important;
    --waline-active-color: #34495e7b !important;
}

.wl-content a {
    text-decoration: none;
    box-shadow: 0 -2px rgba(var(--link-background-color), var(--link-background-opacity)) inset;
    transition: all .3s ease;

    &:hover {
        box-shadow: 0 calc(-1rem * 2.2) rgba(var(--link-background-color), var(--link-background-opacity-hover)) inset;
    }

    @media (prefers-color-scheme:light) {
        &:hover {
            color: var(--waline-theme-color) !important;
        }
    }
}

.wl-header-item input {
    font-size: .75em !important;
}
```

## 附录
### 参考文献
1. [建站技术 | 使博客更好地接入 Waline](https://blog.reincarnatey.net/2024/0719-better-waline)

### 文章封面
[遙@RSyaooooo](https://x.com/RSyaooooo/status/1836575756358459883)
