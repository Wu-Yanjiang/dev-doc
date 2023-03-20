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

.命令用于重复上次的修改操作   
u命令用于撤销上次的修改操作   
\>G 增加从当前行到文档末尾处的缩进层级   

# 不要自我重复

A命令在当前行尾添加内容,进入insert模式  
I命令在当前行首添加内容,进入insert模式  


# 移动与跳转

> 实际行: 在开启行号显示模式下，行号就对应实际行  
> 屏幕行：在一行太长被vim自动折叠的情况下，所显示的行


行首行尾移动：

|命令|光标动作|
|:--|--|
|$  |移动至实际行的行尾   |
|g$ |移动至屏幕行的行尾   |
|^  |移动至实际行第一个非空字符  |
|g^ |移动至屏幕行第一个非空字符  |
|0  |移动至实际行的行首  |
|g0 |移动至屏幕行的行首|

 
基于单词移动：
|命令|光标动作|
|:--|--|
|w  |正向移动至下一个单词|
|b  |反向移动到当前或上一个单词开头|
|e  |正向移动到当前或下一个单词结尾|
|ge |反向移动到上一个单词结尾|

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


# 复制粘贴

:copy命令简称:t，用于把一行或多行从文档的一部分复制到另外一部分。  
:move命令移动一行或多行至文档的另外一部分。  

```bash
$ cat ex_mode/shopping-list.todo
Line 1 Shopping list
2　Hardware Store
3　　Buy new hammer
4　　Beauty Parlor
5　　Buy nail polish remover
6　　Buy nails
```

copy命令格式如下：  
:[range]copy{address}  

```bash
:6t.	把第6行复制到当前行下方
:t6	把当前行复制到第6行下方
:t.	为当前行创建副本
:t$	把当前行复制到文本结尾
:'<,'>t0
```



# 参考资料

- [Vim实用技巧](https://book.douban.com/subject/25869486/)
 
