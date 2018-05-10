docker有两个命令可以导出文件

	docker export containerId > filename

和

	docker save imageId > filename

其中 **export** 是对容器进项操作containerId为容器Id 通过 **docker ps -a** 可以查看已有的所有容器，
**save** 是对镜像进行操作imageId为镜像Id，通过 **docker images**可以查看所有镜像

通过**export**命令导出的文件要用

	docker import filename

命令进行导入

通过 **save** 命令导出的文件要用

	docker load < filename

命令进行导入

不然有可能会报错