---
title: Docker相关操作
top_img: transparent
tags: Docker
abbrlink: 32458
date: 2021-05-17 10:22:09
---

# `Docker`核心思想

`Docker`官网：`https://docs.docker.com/`

## 1.`Docker`简述

`Docker`利用虚拟化技术虚拟出应用程序的运行环境，使得应用程序得以运行。而主机仅需安装`docker`本身，并不需要再安装其他的环境。

优点：

> - 可以在同一个主机上运行多个应用程序，而应用程序的运行环境彼此隔离，互不干扰
> - 可以充分利用主机的计算和存储资源
> - 新机器只需要安装`docker`并导入构建好的镜像就可以完成程序部署，免去了繁琐的安装和配置工作，维护成本大大降低

## 2.`Docker`与虚拟机的不同

- 传统虚拟机，虚拟出一些硬件，运行一个完整的操作系统，然后在这个系统上安装和运行软件
- 容器内的应用直接运行在宿主机的内核，容器是没有自己的内核的，也没有虚拟硬件，所以更轻便
- 每个容器间是相互隔离的，每个容器内都有一个属于自己的文件系统，互不影响

## 3.`Docker`的基本组成

### 镜像（image）：

`docker`的镜像就好比一个模板，可以通过这个模板来创建容器服务。

`tomcat`镜像==>`run`==>`tomcat1`容器（提供服务），通过这个镜像可以创建多个容器，最终服务运行或者项目运行都是在容器中。

### 容器（container）：

`docker`利用容器技术，独立运行一个或一组应用，通过镜像来创建。

### 仓库（repository）：

仓库就是存放镜像的地方。仓库分为公有仓库和私有仓库。

## 3.`Docker`的常用命令

### docker服务命令

```shell
#显示docker的版本信息
docker version

#显示docker的系统信息，包括镜像和容器的数量
docker info

#帮助命令
docker <命令> --help

#启动docker
systemctl start docker

#停止docker
systemctl stop docker

#重启docker
systemctl restart docker

#查看docker服务状态
systemctl status docker

#开机启动docker
systemctl enable docker
```

### 镜像命令

```shell
#查看本地的镜像
[root@hui ~]# docker images
REPOSITORY                      TAG                 IMAGE ID            CREATED             SIZE
docker.io/hello-world           latest              d1165f221234        2 months ago        13.3 kB

#解释
REPOSITORY   镜像的仓库源
TAG			镜像的标签
IMAGE ID	镜像的id
CREATED		镜像的创建时间
SIZE		镜像的大小

#可选项
-a, --all    列出所有镜像
-q, --quiet  只显示镜像id
```

```shell
#搜索镜像
docker search <关键词>

#拉取镜像
docker pull <镜像名>:<版本号>

#删除镜像
docker rmi <镜像ID/镜像名>：<版本号>
```

### 容器命令

```shell
#查看容器
docker ps [参数]

#参数：
无参数    列出当前正在运行的容器
-a	     列出当前正在运行的容器和历史运行过的容器
-n=数字   显示最近创建的容器
-q		 只显示容器的编号
```

```shell
#创建容器
docker run [参数] <容器名>:<版本号>
#参数说明：
--name="Name" 容器名字
-d            后台方式运行
-it			 使用交互式运行，进入容器查看内容
-p			 指定容器的端口  -p 8080:8080

#测试，启动并进入容器
[root@hui ~]# docker run -it tomcat /bin/bash
root@97c13b95e960:/usr/local/tomcat# ls
BUILDING.txt  CONTRIBUTING.md  LICENSE  NOTICE  README.md  RELEASE-NOTES  RUNNING.txt  bin  conf  lib  logs  native-jni-lib  temp  webapps  webapps.dist  work
root@97c13b95e960:/usr/local/tomcat# exit  #从容器退回主机
exit
[root@hui ~]# 
```

```shell
#进入容器
docker attach 容器名/ID

#启动容器
docker start 容器名/ID

#停止容器
docker stop 容器名/ID

#强制停止当前容器
docker kill 容器名/ID

#删除容器
docker rm 容器名/ID



#查看容器信息
docker inspect 容器名/ID

#向容器发送命令
docker exec 容器名/ID 命令
```

```shell
#直接停止容器并退出
exit

#容器不停止退出
Ctrl + P + Q
```

