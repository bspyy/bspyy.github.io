
错误信息：
```
/usr/bin/docker-current: Error response from daemon: error creating overlay mount to /var/lib/docker/overlay2/55a2d445b4be831e78288386f1c2c5c1bf7116d51dc62efbb93a6dc8414ac855/merged: invalid argument.
See '/usr/bin/docker-current run --help'.
```

原因：这个是因为用的overlay2文件系统，而当前系统不能识别

解决方式：将docker当前文件系统改为 overlay

#####1.停掉docker服务

	systemctl stop docker
#####2.删除当前docker images的镜像

	rm -rf /var/lib/docker

#####3.修改文件系统

	vi /etc/sysconfig/docker-storage

将
	
	DOCKER_STORAGE_OPTIONS="--storage-driver overlay2 "
改为

	DOCKER_STORAGE_OPTIONS="--storage-driver overlay "

启动docker服务 
	
	systemctl start docker

即可

