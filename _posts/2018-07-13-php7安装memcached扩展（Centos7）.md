
php安装地址：**/usr/local/php7/**

##### 安装 libmemcached-devel 包

	yum install libmemcached-devel

##### 安装 memcached扩展

下载memcached扩展


	wget http://pecl.php.net/get/memcached-3.0.4.tgz

解压

	tar -xvf memcached-3.0.4.tgz

生成 **configure** 文件

	cd memcached-3.0.4

	/usr/local/php7/bin/phpize

编译安装

	./configure --with-php-config=/usr/local/php7/bin/php-config --with-libmemcached-dir=/usr/ --disable-memcached-sasl

	make && make install

修改php.ini

	vi /usr/local/php7/etc/php.ini

添加

	extension=memcached.so;

查看结果
	
	[root@localhost ~]# php -m | grep memcached
	memcached

安装成功


	

