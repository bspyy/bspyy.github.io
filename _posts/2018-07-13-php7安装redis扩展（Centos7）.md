
php安装地址：**/usr/local/php7/**


下载redis扩展

	wget http://pecl.php.net/get/redis-4.1.0.tgz

解压

	tar -xvf redis-4.1.0.tgz

生成 **configure** 文件

	cd redis-4.1.0

	/usr/local/php7/bin/phpize

编译安装

	./configure --with-php-config=/usr/local/php7/bin/php-config 

	make 

	make install
	
修改php.ini

	vi /usr/local/php7/etc/php.ini

添加

	extension=redis.so

查看结果
	
	[root@localhost ~]# php -m | grep redis
	redis

安装成功