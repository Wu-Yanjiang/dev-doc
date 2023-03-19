---
title: "Shell脚本"
date: 2023-03-19T17:21:53+08:00
categories:
- linux
- shell
tags:
- linux
- shell
keywords:
- shell
- linux
- sed
- gawk

#thumbnailImage: //example.com/image.jpg
---

<!--more-->

# sed命令

sed编辑器即流编辑器(stream editor),用于根据事先设计好的一组规则编辑数据流。  
 
sed编辑器可执行的操作：
- 从输入中读取一行数据
- 根据所提供的编辑器命令匹配数据
- 按照命令修改数据流中的数据
- 将新的数据输出到STDOUT
在流编辑器匹配并针对一行数据执行所有命令之后，读下一行并重复该过程至所有行处理完毕。

使用
```bash

sed options script file

```

options参数允许修改sed命令的行为，一下为可选项
|选项		|描述|
|:-------------:|:--:|
|-e commands	|在处理输入时，加入额外的sed命令|
|-f file	|在处理输入时，将file中的指定命令添加到已有的命令中|
|-n		|不产生命令输出|

script参数指定应用于流数据中的单个命令。


## 在命令行中定义编辑器命令

```bash
$ echo "This is a test" | sed 's/test/big test/'
This is a big test
$
```
使用替换（s）命令，用斜线间指定的第二个字符串替换第一个字符串。

```bash
$ cat data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
$

$ sed 's/dog/cat/' data1.txt
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
The quick brown fox jumps over the lazy cat.
$

$ cat data1.txt
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
The quick brown fox jumps over the lazy dog.
$
```

sed编辑器并不会修改文本文件的数据，他只处理数据并将其发送到STDOUT。如果，要修改数据，可以用重定向到原文本文件。  


## 命令行中使用多个编辑器命令

-e选项

```bash
$ sed -e 's/brown/red/; s/dog/cat/' data1.txt
The quick red fox jumps over the lazy cat.
The quick red fox jumps over the lazy cat.
The quick red fox jumps over the lazy cat.
The quick red fox jumps over the lazy cat.
$
```

命令间以分号（;）分割，并且命令末尾和分号之间不能出现空格。  

或者用bash shell的提示符来分隔命令。只需要输入第一个单引号一直回车就行。  
实例：

```bash
$ sed -e '
> s/brown/green/
> s/fox/toad/
> s/dog/cat/' data1.txt
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
$
```

切记要在闭合单引号所在行结束命令。  

## 从文件中读取编辑器命令

```bash
$ cat script1.sed
s/brown/green/
s/fox/toad/
s/dog/cat/
$
$ sed -f script1.sed data1.txt
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
The quick green toad jumps over the lazy cat.
$
```
为了避免和shell脚本弄混，这里常以.sed作为后缀名称，以示区分。  


# gawk命令


