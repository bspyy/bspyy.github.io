Linux安装：
	
	yum install docker

windows和mac安装：
在

	https://www.docker.com/community-edition

下载对应的安装包安装即可

测试运行情况

启动docker服务

	systemctl start docker

输出'hello world'

	[root@localhost ~]# docker run ubuntu echo hello docker
	hello docker

```
[root@localhost ~]# docker container run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://cloud.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/
```

错误处理：

```
[root@localhost ~]# docker run ubuntu echo hello docker
/usr/bin/docker-current: Error response from daemon: error creating overlay mount to /var/lib/docker/overlay2/47cc29e9472d073994ad56a64df4a590b1cba5c9da97a021d19174e28ee4b4dd-init/merged: invalid argument.
See '/usr/bin/docker-current run --help'.
```
这个是因为用的overlay2文件系统，而系统默认只能识别overlay文件系统

所以我们就要更新文件系统了	

https://blog.csdn.net/ysssssssssssssss/article/details/79596367