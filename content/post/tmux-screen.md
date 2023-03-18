---
title: "tmux和screen命令速览"
date: 2023-03-18T15:57:54+08:00
categories:
- linux
tags:
- tmux
- screen
- linux命令
keywords:
- tmux
- screen

# 原文作者
#author:
# 原文链接
#link:
# 图片链接，用在open graph和twitter卡片上
#imgs:
# 在首页展开内容
#expand: true
# 外部链接地址，访问时直接跳转
#extlink:
# 在当前页面关闭评论功能
#comment:
# enable: false
# 关闭当前页面目录功能
# 注意：正常情况下文章中有H2-H4标题会自动生成目录，无需额外配置
#toc: false
# 绝对访问路径
#url: "{{ lower .Name }}.html"
# 开启文章置顶，数字越小越靠前
#weight: 1
# 开启数学公式渲染，可选值： mathjax, katex
#math: mathjax
# 开启各种图渲染，如流程图、时序图、类图等
#mermaid: true
---

tmux和screen命令学习备忘录

<!--more-->


# screen
利用screen命令实现终端窗口的复用

```bash
# 查看已有终端
screen -ls

# 新建名为abc的终端并使用
screen -S abc

# 跳转到abc终端
screen -r abc


```

# tmux

# 使用


```bash
安装
sudo apt install tmux



```

