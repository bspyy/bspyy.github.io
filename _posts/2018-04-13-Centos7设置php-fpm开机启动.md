本来是想通过

	systemctl enable php-fpm

来实现，但是因为php7编译安装，所以不行，只好用脚本来实现

<!-- more -->

1 创建启动php-fpm的脚本文件
	
	vim /etc/init.d/php-fpm.sh

在文件中写入如下内容

	# /bin/bash

	/usr/local/php7/sbin/php-fpm #php-fmp路径

2 赋予该脚本可执行权限

	chmod a+x /etc/init.d/php-fpm.sh

3 打开/etc/rc.d/rc.local文件，在末尾增加如下内容

	/etc/init.d/php-fpm.sh

4.在centos7中，/etc/rc.d/rc.local的权限被降低了，所以需要执行如下命令赋予其可执行权限

	chmod +x /etc/rc.d/rc.local

设置完成。重启即可查看效果

参考资料

Centos7开机启动自己的脚本的方法 ：www.jb51.net/os/RedHat/513981.html
