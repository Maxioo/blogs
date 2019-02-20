---
layout: article
title: 实现Windows录屏功能的想法
key: 100001
category: blog
tags: 音视频技术
date: 2018-06-28 15:00:00 +08:00
modify_date: 2019-02-18 14:40:00 +08:00
---

# 关于实现Windows录屏功能的想法

开始 **Camstudio**的刨析任务不现实，现从底层开始仔细思考该做什么内容。

<!--more-->

## 关于实现录屏软件的步骤

- 音频数据的采集
- 视频数据的采集
- 音频和视频的解码
- 将解码后的文件以一定的形式保存下来
 -保证视频和音频的同步

## 基础知识的学习

有幸在网上找到了某位大佬的分享  
从零开始学习音视频技术的话可以看看这个[音视频技术分享博客](http://blog.yundiantech.com/)  
此人在FFmpeg源码分析与音视频技术方面留下了宝贵的资料[雷霄骅](https://blog.csdn.net/leixiaohua1020)
