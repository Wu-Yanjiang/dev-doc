---
title: "Vim快速入门"
date: 2023-03-19T15:32:21+08:00
categories:
- vim 
tags:
- vim
keywords:
- vim
#thumbnailImage: //example.com/image.jpg
---

<!--more-->

# .命令

.命令用于重复上次的操作   
u命令用于回退上次的操作   
\>G 增加从当前行到文档末尾处的缩进层级   

# 不要自我重复

A命令在当前行尾添加内容,进入insert模式  
I命令在当前行首添加内容,进入insert模式  

$命令移动至行尾   
^命令移动至行首  
0命令也是移动至行首  

# .vimrc配置参数

| 设置参数   | 含 义                                                                                                                                                                                      |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| :set nu        | :set nu                                                                                                                                                                                      |
| :set nonu      | 设置与取消行号。                                                                                                                                                                     |
| :syn on        | :syn on                                                                                                                                                                                      |
| :syn off       | 是否依据语法显示相关的颜色帮助。在Vim中修改相关的配置文件或Shell脚本文件 时（如前面示例的脚本/etc/init.d/sshd)，默认会显示相应的颜色，用来帮助排错。如果觉得颜色产生了干扰，则可以取消此设置 |
| set hlsearch   | set hlsearch                                                                                                                                                                                 |
| set nohlsearch | 设置是否将査找的字符串高亮显示。默认是hlsearch高亮显示                                                                                                                |
| set nobackup   | set nobackup                                                                                                                                                                                 |
| set backup     | 是否保存自动备份文件。默认是nobackup不自动备份。如果设定了:set backup，则会产生“文件名〜”作为备份文件                                            |
| set ruler      | set ruler                                                                                                                                                                                    |
| set noruler    | 设置是否显示右下角的状态栏。默认是ruler显示                                                                                                                               |
| set showmode   | set showmode                                                                                                                                                                                 |
| set noshowmode | 设置是否在左下角显示如“一INSERT--”之类的状态栏。默认是showmode显示                                                                                               |

# 参考资料

- [Vim实用技巧](https://book.douban.com/subject/25869486/)
 
