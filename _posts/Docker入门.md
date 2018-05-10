### Docker安装
Docker CE 的安装请参考官方文档。

[Mac](https://docs.docker.com/docker-for-mac/install/)
[Windows](https://docs.docker.com/docker-for-windows/install/)
[Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
[Debian](https://docs.docker.com/install/linux/docker-ce/debian/)
[CentOS](https://docs.docker.com/install/linux/docker-ce/centos/)
[Fedora](https://docs.docker.com/install/linux/docker-ce/fedora/)
[其他 Linux 发行版](https://docs.docker.com/install/linux/docker-ce/binaries/)

安装成功之后，启动docker服务

	systemctl start docker

将docker设置为开机启动

	systemctl enable docker

配置Docker中国区官方镜像

编辑 /etc/docker/daemon.json 文件并添加上"registry-mirrors":["https://registry.docker-cn.com"]，如下：
```
vim /etc/docker/daemon.json 

{
	"registry-mirrors":["https://registry.docker-cn.com"]
}

```
配置完之后执行下面的命令，以使docker的配置文件生效

	systemctl daemon-reload 
	systemctl restart docker


错误处理：


```
[root@localhost ~]# docker run ubuntu echo hello docker
/usr/bin/docker-current: Error response from daemon: error creating overlay mount to /var/lib/docker/overlay2/47cc29e9472d073994ad56a64df4a590b1cba5c9da97a021d19174e28ee4b4dd-init/merged: invalid argument.
See '/usr/bin/docker-current run --help'.
```
这个是因为用的overlay2文件系统，而系统默认只能识别overlay文件系统

所以我们就要更新文件系统了	

https://blog.csdn.net/ysssssssssssssss/article/details/79596367

### image 文件
Docker 把应用程序及其依赖，打包在 image 文件里面。只有通过这个文件，才能生成 Docker 容器。image 文件可以看作是容器的模板。Docker 根据 image 文件生成容器的实例。同一个 image 文件，可以生成多个同时运行的容器实例。
```
# 列出本机的所有 image 文件。
docker image ls
或 
docker images

# 删除 image 文件
docker image rm [imageName]
```
image 是二进制文件。实际开发中，一个 image 文件往往通过继承另一个 image 文件，加上一些个性化设置而生成。举例来说，你可以在 Ubuntu 的 image 基础上，往里面加入 Apache 服务器，形成你的 image。


# 列出本机的所有 image 文件。
$ docker image ls

# 删除 image 文件
$ docker image rm [imageName]
image 文件是通用的，一台机器的 image 文件拷贝到另一台机器，照样可以使用。一般来说，为了节省时间，我们应该尽量使用别人制作好的 image 文件，而不是自己制作。即使要定制，也应该基于别人的 image 文件进行加工，而不是从零开始制作。

为了方便共享，image 文件制作完成后，可以上传到网上的仓库。Docker 的官方仓库 Docker Hub 是最重要、最常用的 image 仓库。此外，出售自己制作的 image 文件也是可以的。


### 实例 hello world

首先，运行下面的命令，将 image 文件从仓库抓取到本地

>docker image pull library/hello-world

上面代码中，docker image pull是抓取 image 文件的命令。library/hello-world是 image 文件在仓库里面的位置，其中library是 image 文件所在的组，hello-world是 image 文件的名字。

由于 Docker 官方提供的 image 文件，都放在library组里面，所以它的是默认组，可以省略。因此，上面的命令可以写成下面这样。

>docker image pull hello-world

抓取成功以后，就可以在本机看到这个 image 文件了。

> docker image ls

现在，运行这个 image 文件。

>docker container run hello-world

docker container run命令会从 image 文件，生成一个正在运行的容器实例。

注意，docker container run命令具有自动抓取 image 文件的功能。如果发现本地没有指定的 image 文件，就会从仓库自动抓取。因此，前面的docker image pull命令并不是必需的步骤。

如果运行成功，你会在屏幕上读到下面的输出。
```
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

输出这段提示以后，hello world就会停止运行，容器自动终止。

有些容器不会自动终止，因为提供的是服务。比如，安装运行 Ubuntu 的 image，就可以在命令行体验 Ubuntu 系统。


> docker container run -it ubuntu bash

对于那些不会自动终止的容器，必须使用docker container kill 命令手动终止。

> docker container kill [containID]

### 容器文件
image 文件生成的容器实例，本身也是一个文件，称为容器文件。也就是说，一旦容器生成，就会同时存在两个文件： image 文件和容器文件。而且关闭容器并不会删除容器文件，只是容器停止运行而已。


列出本机正在运行的容器

> docker container ls

列出本机所有容器，包括终止运行的容器 

>docker container ls --all

上面命令的输出结果之中，包括容器的 ID。很多地方都需要提供这个 ID，比如上一节终止容器运行的docker container kill命令。

终止运行的容器文件，依然会占据硬盘空间，可以使用docker container rm命令删除。


> docker container rm [containerID]

运行上面的命令之后，再使用docker container ls --all命令，就会发现被删除的容器文件已经消失了。

删除所有容器

>docker rm $(docker ps -a -q)

![image](https://csdnimg.cn/passport/login-banner.png)