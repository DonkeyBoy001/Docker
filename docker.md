

# Docker

## 简介

打包下面内容：

配置文件、

启动命令应用程序、

环境变量第三方软件库和依赖包

运行时环境

操作系统(OS)

# dock作用

![image-20230621142015530](/Users/zhouzhenzhou/Desktop/docker/docker.assets/image-20230621142015530.png)

dock可以打包上面环境，然后不用配置环境



## dock 和 虚拟机区别

虚拟机： 通过 Hypervisor 实现

![image-20230621142131767](/Users/zhouzhenzhou/Desktop/docker/docker.assets/image-20230621142131767.png)

将一个物理服务器 虚拟 分配 给多个逻辑服务器。

启动速度慢，占用内存多

![image-20230621142235693](/Users/zhouzhenzhou/Desktop/docker/docker.assets/image-20230621142235693.png)

dock不是容器，只是容器化的 一种解决方案

![image-20230621142326875](/Users/zhouzhenzhou/Desktop/docker/docker.assets/image-20230621142326875.png)

# Docker基本原理和概念

# Docker Ecosystem

Docker is a platform or ecosystem around creating and running containers

![image-20230621223410540](/Users/zhouzhenzhou/Desktop/docker/docker.assets/image-20230621223410540.png)

## Docker structure

![image-20230621224407705](/Users/zhouzhenzhou/Desktop/docker/docker.assets/image-20230621224407705.png)

## 镜像 images

镜像是一个只读的模板，它可以用来创建容器。

![image-20230621223818310](/Users/zhouzhenzhou/Desktop/docker/docker.assets/image-20230621223818310.png)

## 容器 containers

run a very specific program

容器是Docker的运行实例， 它提供了一个独立的可移植的环境。

可以在这个环境中，运行 应用程序实例。

镜像： 只读模版 

容器： 运行实例

镜像可以比作 类

容器可以比作 实例

## 仓库 Registry

用来存储images的地方

最流行仓库 dock hub

images共享 和 复用

![image-20230621143343489](/Users/zhouzhenzhou/Desktop/docker/docker.assets/image-20230621143343489.png)

 

## Docker 安装

https://www.docker.com/

https://docs.docker.com/desktop/install/mac-install/

```
docker -v
```

查看docker版本

Docker是使用Client-Server架构模式

Docker Client 和 Docker Daemon 之间 通过 socket 进行通信

Docker Daemon 服务端 守护进程： 负责管理docker各种资源

Docker Client 负责向 Docker Daemon 发送请求

Docker Daemon 接受到请求之后进行处理，将结果返回给 Docker Client

Docker Daemon 是一个后端进程，用来接收并处理来自Docker客户端的请求，然后将结果返回给客户端。

 ![image-20230621145244359](/Users/zhouzhenzhou/Desktop/docker/docker.assets/image-20230621145244359.png)



## 容器化 和 Dockerfile

容器化： 将应用程序打包成容器，然后在容器中 运行应用程序的过程。

分为三步走：

创建一个Dockerfile： 告诉 docker 构建应用程序镜像 所需要的步骤和配置。

使用Dockerfile构建镜像

使用镜像创建和运行容器



### Dockerfile:

里面是 docker指令

告诉docker 如何构建镜像

包括：应用程序执行的所有命令。

# 实际用例子：

创建Dockerfile文件

名字不可以修改，一定得是 Dockerfile

镜像是按层次结构来构建的

每一层都是基于上一层的

所以我们需要先指定一个基础镜像,然后在这个镜像的基础上 添加我们的应用程序

从一个最基础的Linux镜像开始,

 然后在这个镜像基础上,安装NodeJS和我们的应用程序

或者

直接使用node.js镜像，因为这个镜像已经是基于Linux来构建的了



```
FROM node:14-alpine
Copy index.js /index.js
CMD ["node", "/index.js"]
```

14表示 版本

基于Alpine这个Linux发行版来构建的，还可以选RedHat Centos都是linux发行版

copy命令 复制文件

​		第一个参： 原路径（相对于dockerFile的路径）

​		第二个参： 目标路径（相对镜像的路径）

CMD  ：

​		第一个参数：表示可执行程序的名字

​		第二个参数：这个可执行程序接收到的参数

```
docker build -t hello-docker .
```

hello-docker是 自己给images 起的名字

.表示 当前路径上

下面构建完，查看image

```
docker image ls
```

```
docker run hello-docker
```

docker运行命令

Hello-docker为image名字

如果你想要在另一个环境中，运行这个应用程序

那么就只需要把这个镜像文件复制过去

然后执行一下刚刚的命令就可以了。

可以把这个镜像文件上传到 DockerHubs上。



#### DockerHub仓库

https://hub.docker.com/r/blackdonkey001/hellodocker

#### Play with Docker

https://labs.play-with-docker.com/p/ci9nqs4snmng00f9i6dg

```
docker pull geekhour/hello-docker
```

geekhour表示用户名

Hello-docker表示image名

```
 docker run geekhour/hello-docker
```

启动docker



## Docker Compose

docker官方开源项目

用于定义和运行多容器Docker 应用程序的工具

使用YAML 文件来配置应用程序的服务

一条命令即可创建并启动所有服务



### docker compose

它通过一个单独的docker-compose.yaml的配置文件

![image-20230621191558759](/Users/zhouzhenzhou/Desktop/docker/docker.assets/image-20230621191558759.png)

```
docker compose up
```

一键安装环境



# 	Quick Rview of Operating System



Has a kernel

It governs access between all the programs.

And  all the physical hardware that is connected to your computer.

![image-20230621232214957](/Users/zhouzhenzhou/Desktop/docker/docker.assets/image-20230621232214957.png)



对比理解 Container

![image-20230621232729418](/Users/zhouzhenzhou/Desktop/docker/docker.assets/image-20230621232729418.png)

![image-20230621233103272](/Users/zhouzhenzhou/Desktop/docker/docker.assets/image-20230621233103272.png)
