---
layout: post
title: Linux新增swap分区
---

编译php7的时候系统报 make: *** [ext/fileinfo/libmagic/apprentice.lo] 错误，网上查了一下，说是 
因为服务器内存不足1G,只需要在配置命令中添加 --disable-fileinfo 即可,但是担心项目会用到用到该模块，
不便禁用，并查了一下其他的解决方法，结果就找到了可以通过增加swap分区来解决这个问题
<!-- more -->

步骤如下:

查看当前内存和内存缓冲区(swap分区)的使用情况
> free -lh 

	[root@localhost ~]# free -mh
	       total  used  free  shared  buff/cache  available
	Mem:   993M   91M   788M  6.5M      113M       781M
	Swap:  1.0G   0B    1.0G


创建一个1G大小的空文件
> dd if=/dev/zero of=/var/swap bs=1M count=1024

[Linux中dd命令详解](http://blog.csdn.net/xizaihui/article/details/53307578)

将创建的文件设置为交换文件

> mkswap /var/swap 

激活启用交换分区
> swapon /var/swap 

此时可以用 **free -mh ** 命令查看结果

添加系统引导时自启动运行
    
    vi /etc/fstab
    新增一行
    /var/swap  swap  swap  defaults  0  0 

参考资料：

[在装完Linux系统之后自己去修改Swap分区的大小(两种方法) ](http://blog.itpub.net/29440247/viewspace-1445502/)

[Linux增加swap分区大小](http://blog.csdn.net/zhouzme/article/details/19578025)