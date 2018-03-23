
安装firewalld 防火墙

	yum install firewalld

开启服务

	systemctl start firewalld.service

关闭防火墙

	systemctl stop firewalld.service

开机自动启动

	systemctl enable firewalld.service

关闭开机制动启动

	systemctl disable firewalld.service

<!--more-->
firewalld中常用的区域名称及策略规则

| 	区域  	| 	默认规则策略 		
| 	:-:   	| 	:- 			
| trusted	|允许所有的数据包	
| home	    |拒绝流入的流量，除非与流出的流量相关；而如果流量与ssh、mdns、ipp-client、amba-client与dhcpv6-client服务相关，则允许流量
|internal   |等同于home区域
|work		|拒绝流入的流量，除非与流出的流量数相关；而如果流量与ssh、ipp-client与dhcpv6-client服务相关，则允许流量
|**public** |拒绝流入的流量，除非与流出的流量相关；而如果流量与ssh、dhcpv6-client服务相关，则允许流量
|external	|拒绝流入的流量，除非与流出的流量相关；而如果流量与ssh服务相关，则允许流量
|dmz		|拒绝流入的流量，除非与流出的流量相关；而如果流量与ssh服务相关，则允许流量
|block		|拒绝流入的流量，除非与流出的流量相关
|drop		|拒绝流入的流量，除非与流出的流量相关

#### 使用firewall-cmd 命令

**firewall-cmd**命令中使用的参数以及作用

| 			参数					|	作用
| 	 		:-:					|	:-
|--get-default-zone				|查询默认的区域名称
|--set-default-zone=<区域名称>	|设置默认的区域，使其永久生效
|--get-zones					|显示可用的区域
|--get-services					|显示预先定义的服务
|--get-active-zones				|显示当前正在使用的区域与网卡名称
|--remove-source=				|将源自此IP或子网的流量导向指定的区域
|--remove-source=				|不再将源自此IP或子网的流量导向某个指定区域
|--add-interface=<网卡名称>		|将源自该网卡的所有流量都导向某个指定区域
|--change-interface=<网卡名称>	|将某个网卡与区域进行关联
|--list-all						|显示当前区域的网卡配置参数、资源、端口以及服务等信息
|--list-all-zones				|显示所有区域的网卡配置参数、资源、端口以及服务等信息
|--add-service=<服务名>			|设置默认区域允许该**服务**的流量
|--remove-service=<服务名>		|设置默认区域不再允许该**服务**的流量
|--add-port=<端口号/协议>			|设置默认区域允许该**端口**的流量
|--remove-port=<端口号/协议>		|设置默认区域不再允许该**端口**的流量
|--reload						|让“永久生效”的配置规则立即生效，并覆盖当前的配置规则
|--panic-on						|开启应急状况模式
|--panic-off					|关闭应急状况模式

要使定义的协议永久生效，需要加一句 **--permanent**；--zone不写则使用默认区域

获取 firewalld 状态

	[root@localhost ~]# firewall-cmd --state
	running

查看所有可用区域

	[root@localhost ~]# firewall-cmd --get-zones
	block dmz drop external home internal public trusted work

查看当前区域

	[root@localhost ~]# firewall-cmd --get-default-zone
	public

设置默认区域为public
	
	[root@localhost ~]# firewall-cmd --set-default-zone=public
	Warning: ZONE_ALREADY_SET: public #出现此警告是因为当前的区域已经是public了
	success


查询public区域是否允许请求SSH和HTTP协议的流量：

	[root@localhost ~]# firewall-cmd --zone=public --query-service=ssh
	yes
	[root@localhost ~]# firewall-cmd --zone=public --query-service=http
	no

设置public区域为永久允许http流量并立即生效

	[root@localhost ~]# firewall-cmd --zone=public --add-service=http --permanent
	success
	[root@localhost ~]# firewall-cmd --reload
	success
	[root@localhost ~]# firewall-cmd --zone=public --query-service=http
	yes

允许外部连接接入，端口6666，TCP协议：

	[root@localhost ~]# firewall-cmd --zone=public --add-port=6666/tcp
	success

查询端口是否启用：
	
	[root@localhost ~]# firewall-cmd --zone=public --query-port=6666/tcp
	yes


移除端口

	[root@localhost ~]# firewall-cmd --zone=public --remove-port=6666/tcp
	success

重新加载防火墙规则：

	[root@localhost ~]# firewall-cmd --reload
	success


参考资料

[CentOS7 firewall-cmd 基础使用](https://blog.csdn.net/dybb8999/article/details/52216893)

[Iptables与Firewalld防火墙](https://www.linuxprobe.com/chapter-08.html#83_Firewalld)