---
layout: post
title: Linux系统访问FTP连接时出现“227 Entering Passive Mode“的解决方法
---

ftp分为主动和被动两种工作模式，详细介绍如下：
    
    主动 FTP ：　　　　
    命令连接：客户端 >1024 端口 → 服务器 21 端口
    数据连接：客户端 >1024 端口 ← 服务器 20 端口
<!-- more -->

    被动 FTP ：
    命令连接：客户端 >1024 端口 → 服务器 21 端口
    数据连接：客户端 >1024 端口 ← 服务器 >1024 端口

出现此错误的原因是因为当前动作模式为被动模式，而被动模式需要的端口尚未开放，因此
通过 *passive* 切换为主动工作模式即可

    ftp> passive
    Passive mode off. (被动模式关闭)

    ftp> passive (再次运行命令可打开）
    Passive mode on.

相关链接：

<a href="https://www.linuxidc.com/Linux/2013-05/83742.htm" target="_blank">Linux系统访问Windows 2003 FTP连接时出现“227 Entering Passive Mode” 的解决方法</a>