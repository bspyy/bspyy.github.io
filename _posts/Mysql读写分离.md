### Mysql中间件

##### mysql-proxy

操作系统：Centos7(64位)		

Mysql:5.7

下载 通用版

	wget https://downloads.mysql.com/archives/get/file/mysql-proxy-0.8.5-linux-glibc2.3-x86-64bit.tar.gz

解压

	tar -xvf mysql-proxy-0.8.5-linux-glibc2.3-x86-64bit.tar.gz

移动文件位置

	mv mysql-proxy-0.8.5-linux-glibc2.3-x86-64bit.tar.gz /usr/local/mysql-proxy

配置mysql-proxy，创建主配置文件

```	
cd /usr/local/mysql-proxy

mkdir lua #创建脚本存放目录

mkdir logs #创建日志目录

cp share/doc/mysql-proxy/rw-splitting.lua ./lua #复制读写分离配置文件

cp share/doc/mysql-proxy/admin-sql.lua ./lua #复制管理脚本
```

```
vi /etc/mysql-proxy.cnf   #创建配置文件

[mysql-proxy]
user=root #运行mysql-proxy用户

admin-username=user #主从mysql共有的用户
admin-password=password #用户的密码

proxy-address=ip:port #mysql-proxy运行ip和端口，不加端口，默认4040

proxy-read-only-backend-addresses=ip:port #指定后端从slave读取数据
proxy-backend-addresses=ip:port #指定后端主master写入数据

proxy-lua-script=/usr/local/mysql-proxy/lua/rw-splitting.lua #指定读写分离配置文件位置
admin-lua-script=/usr/local/mysql-proxy/lua/admin-sql.lua #指定管理脚本

log-file=/usr/local/mysql-proxy/logs/mysql-proxy.log #日志位置
log-level=info #定义log日志级别，由高到低分别有(error|warning|info|message|debug)

daemon=true    #以守护进程方式运行
keepalive=true #mysql-proxy崩溃时，尝试重启

```

授权
	
	chmod 660 /etc/mysql-porxy.cnf

启动mysql-proxy

	/usr/local/mysql-proxy/bin/mysql-proxy --defaults-file=/etc/mysql-proxy.cnf


mysql-proxy实现读写分离
	
	https://www.cnblogs.com/lin3615/p/5684891.html

##### amoeba

##### atlas

##### mycat

##### kingshard

