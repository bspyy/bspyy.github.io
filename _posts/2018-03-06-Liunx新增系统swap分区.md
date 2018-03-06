---
layout: post
title: Liunx新增swap分区
---

编译php7的时候系统报 make: *** [ext/fileinfo/libmagic/apprentice.lo] 错误，网上查了一下，说是 
因为服务器内存不足1G,只需要在配置命令中添加 --disable-fileinfo 即可,但是担心项目会用到用到该模块，
不便禁用，并查了一下其他的解决方法，结果就找到了可以通过增加swap分区来解决这个问题

步骤如下 

##### 增加 swap 大小, 1G 左右
> dd if=/dev/zero of=/var/swap bs=1M count=1024

##### 设置交换文件
> mkswap /var/swap 

##### 激活启用交换分区
> swapon /var/swap 

##### 添加系统引导时自启动运行
    
    vi /etc/fstab
    新增一行
    /var/swap               swap                    swap    defaults        0 0 

[在装完Linux系统之后自己去修改Swap分区的大小(两种方法) ](http://blog.itpub.net/29440247/viewspace-1445502/)
[Linux增加swap分区大小](http://blog.csdn.net/zhouzme/article/details/19578025)