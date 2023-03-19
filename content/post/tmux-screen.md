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

## 使用

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

tmux与screen功能相似，但是更易用，也更强大。

```bash
# 安装
sudo apt install tmux

# 启动
tmux

# 退出
# 按下ctrl+d或输入exit
exit
```

## 会话管理

```bash
# 新建
tmux new -s <会话名>

# 分离会话
tmux detach

ctrl+b d

# 查询所有会话
tmux ls

ctrl+b s

# 接入
tmux attach -t <会话名>

# 杀死
tmux kill-session -t <会话名>

# 切换
tmux switch -t <会话名>

# 重命名
tmux rename-session -t <会话名>

ctrl+b $

```

| 前缀   | 指令   | 描述                                   |
| ------ | ------ | -------------------------------------- |
| Ctrl+b | ?      | 显示快捷键帮助文档                     |
| Ctrl+b | d      | 断开当前会话                           |
| Ctrl+b | D      | 选择要断开的会话                       |
| Ctrl+b | Ctrl+z | 挂起当前会话                           |
| Ctrl+b | r      | 强制重载当前会话                       |
| Ctrl+b | s      | 显示会话列表用于选择并切换             |
| Ctrl+b | :      | 进入命令行模式，此时可直接输入ls等命令 |
| Ctrl+b | [      | 进入复制模式，按q退出                  |
| Ctrl+b | ]      | 粘贴复制模式中复制的文本               |
| Ctrl+b | ~      | 列出提示信息缓存                       |

## 窗格和面板

什么是窗格什么是面板?   
答：窗格可以简单理解为一个你自己分类的工作区域，如开发工程师使用的IDE，功能强大，但是功能都是十分内聚的，核心功能就是用于方便开发;  
面板则是这个界面上不同的组成部分，如代码编辑界面、文档结构目录、编译结果输出区域。  
不同的窗格负责不同的主要工作内容，面板则负责工作内容的细分。

![窗格和面板](https://raw.githubusercontent.com/Wu-Yanjiang/img-storage/master/tmux-winddowAndPanel.png)

## 窗格操作

| 前缀   | 指令 | 描述                                     |
| ------ | ---- | ---------------------------------------- |
| Ctrl+b | c    | 新建窗口                                 |
| Ctrl+b | &    | 关闭当前窗口（关闭前需输入y or n确认）   |
| Ctrl+b | 0~9  | 切换到指定窗口                           |
| Ctrl+b | p    | 切换到上一窗口                           |
| Ctrl+b | n    | 切换到下一窗口                           |
| Ctrl+b | w    | 打开窗口列表，用于且切换窗口             |
| Ctrl+b | ,    | 重命名当前窗口                           |
| Ctrl+b | .    | 修改当前窗口编号（适用于窗口重新排序）   |
| Ctrl+b | f    | 快速定位到窗口（输入关键字匹配窗口名称） |

## 面板操作

| 前缀   | 指令        | 描述                                                           |
| ------ | ----------- | -------------------------------------------------------------- |
| Ctrl+b | "           | 当前面板上下一分为二，下侧新建面板                             |
| Ctrl+b | %           | 当前面板左右一分为二，右侧新建面板                             |
| Ctrl+b | x           | 关闭当前面板（关闭前需输入y or n确认）                         |
| Ctrl+b | z           | 最大化当前面板，再重复一次按键后恢复正常（v1.8版本新增）       |
| Ctrl+b | !           | 将当前面板移动到新的窗口打开（原窗口中存在两个及以上面板有效） |
| Ctrl+b | ;           | 切换到最后一次使用的面板                                       |
| Ctrl+b | q           | 显示面板编号，在编号消失前输入对应的数字可切换到相应的面板     |
| Ctrl+b | {           | 向前置换当前面板                                               |
| Ctrl+b | }           | 向后置换当前面板                                               |
| Ctrl+b | Ctrl+o      | 顺时针旋转当前窗口中的所有面板                                 |
| Ctrl+b | 方向键      | 移动光标切换面板                                               |
| Ctrl+b | o           | 选择下一面板                                                   |
| Ctrl+b | 空格键      | 在自带的面板布局中循环切换                                     |
| Ctrl+b | Alt+方向键  | 以5个单元格为单位调整当前面板边缘                              |
| Ctrl+b | Ctrl+方向键 | 以1个单元格为单位调整当前面板边缘（Mac下被系统快捷键覆盖）     |
| Ctrl+b | t           | 显示时钟                                                       |

# 参考资料

- [阮一峰的网络日志](http://www.ruanyifeng.com/blog/2019/10/tmux.html)
- [A Quick and Easy Guide to tmux](https://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/)
- [Tmux使用手册](http://louiszhai.github.io/2017/09/30/tmux/)
