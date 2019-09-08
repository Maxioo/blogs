---
layout: article
title: 虚拟机内Spark平台的搭建
key: 100007
category: blog
tags: tools
date: 2019-09-08 14:41:00 +08:00
modify_date: 2019-09-08 14:41:00 +08:00
---

# 利用Vscode在WSL上进行C++调试

## 1. 安装WSL
这里网上有很多教程，[参考博客](https://www.cnblogs.com/skyshalo/p/7724072.html)

## 2. 安装Vscode

我选择Vscode的原因如下：

1. 相比于宇宙第一IDE(Visual Studio)更轻量级。
2. 界面好看，代码补全等一些功能比较齐全。
3. 不用怎么折腾，如果你爱折腾，可以选择Vim or emacs or 两者结合的spacemacs，一般不建议，学习成本高，建议把重点放在提升技术上。

Vscode的安装也非常简单，去官网下载安装包即可。

## 3. 安装C++编译器

我使用的编译器是mingw，具体安装细节可参考以下博客，[参考博客](https://www.cnblogs.com/TAMING/p/9945389.html)

## 4. Vscode的插件

Vscode上有各种方便的插件，但是我认为对C/C++的支持不算友好，官方的C/C++插件配置相比于原来还是提升了不少，配置界面都有图形界面了，但对于中大型项目建议转Visual Studio。

必装插件：Remote WSL，C/C++插件，Code Runner。

其中Code Runner是国内开发者所开发的插件，使用只需点击右上角三角形，即可运行（默认已经装了编译器，并添加到环境变量中）

## 5. 配置WSL

首先打开WSL，建立工作目录，例如```/home/xxx/workspace/project/helloworld```。

并输入```code .```此时会弹出vscode，那么在这里就可以编辑代码并运行啦。

## 6. Debug

但是，如果程序遇到错误，那么难免需要进行Debug，此时就需要使用C/C++插件啦。

首先按F5，选择```C++ (GDB/LLDB)```，然后会自动生成一个launch文件，不用修改，然后再按F5，还是会报错，此时选择创建Task，然后又会生成一个task.json文件。

最后打上断点后，按F5就能进行Debug啦。大功告成。