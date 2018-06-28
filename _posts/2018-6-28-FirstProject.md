---
layout: article
title: 实现Windows录屏功能
---
##关于实现Windows录屏功能的想法
开始**Camstudio**的刨析任务不现实，现从底层开始仔细思考该做什么内容。
###关于实现录屏软件的步骤
-音频数据的采集
-视频数据的采集
-音频和视频的解码
-将解码后的文件以一定的形式保存下来
-保证视频和音频的同步
###基础知识的学习
有幸在网上找到了某位大佬的分享>http://blog.yundiantech.com/?log=index。
