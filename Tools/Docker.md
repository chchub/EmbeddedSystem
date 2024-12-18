# Docker

## docker 镜像

- [official-images](https://github.com/docker-library/official-images)

- [python docker images](https://hub.docker.com/_/python)

## Docker 架构

Docker 包括三个基本概念:

- 镜像（Image）：Docker 镜像（Image），就相当于是一个 root 文件系统。比如官方镜像 ubuntu:16.04 就包含了完整的一套 Ubuntu16.04 最小系统的 root 文件系统。

- 容器（Container）：镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。

- 仓库（Repository）：仓库可看着一个代码控制中心，用来保存镜像。
Docker 使用客户端-服务器 (C/S) 架构模式，使用远程API来管理和创建Docker容器。

Docker 容器通过 Docker 镜像来创建。

容器与镜像的关系类似于面向对象编程中的对象与类。

## 常用命令

- 获取镜像

docker pull ubuntu

- 启动容器

docker run -it ubuntu /bin/bash

- 查看所有的容器

docker ps -a

- 启动已停止运行的容器

docker start b750bbbcfd88

- 后台运行

在大部分的场景下，我们希望 docker 的服务是在后台运行的，我们可以过 -d 指定容器的运行模式。

docker run -itd --name ubuntu-test ubuntu /bin/bash

- 停止一个容器

docker stop <容器 ID>

- 停止的容器可以通过 docker restart 重启

docker restart <容器 ID>

- 进入容器推荐使用 exec 命令

docker exec -it 243c32535da7 /bin/bash

- [docker 容器数据卷](https://www.cnblogs.com/kevingrace/p/6238195.html)

可以直接挂载宿主机文件或目录到容器里，可以理解为目录映射，这样就可以让所有的容器共享宿主机数据，从而只需要改变宿主机的数据源就能够影响到所有的容器数据。

-v 后面的映射关系是"宿主机文件/目录:容器里对应的文件/目录"，其中，宿主机上的文件/目录是要提前存在的，容器里对应的文件/目录会自动创建。

```
-v /opt/host_folder:/var/container_folder
```

