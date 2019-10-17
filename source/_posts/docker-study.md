---
title: 'docker学习记录'
date: 2018-12-06 20:44:37
categories:
- 服务器相关
---
## 目标任务

* 构建mongoDB环境
* 构建node环境
* 构建nginx环境
* 整合这三个环境,以搭建基于koa2+angular/vue+mongoDB的全栈环境

## docker是什么,为什么要使用docker

docker是简化版linux container(LXC)引擎(管理各种所需依赖的容器),通过cgroup等机制对不同的container内运行的应用程序进行隔离,权限管理和quota分配等每个container拥有自己独立的各种命名空间(亦即资源)包括:PID进程, MNT文件系统, NET网络, IPC, UTS主机名等。并不包含操作系统内核。
docker是一个容器,用于对环境的构建,解决开发环境和部署环境的不同,以及部署在各种操作系统上的差异,做到依赖集成,并且对环境与部署机器的隔离.(Build once，Run anywhere，Configure once，Run anything),

## docker的相关概念

* 镜像：类似虚拟机快照，大多都是在现有工具镜像上创建新镜像。
* 容器：从镜像中创建应用环境，以单进程的方式运行。对外公开服务。是一种短暂的和一次性的环境。
* 数据卷：完成数据持久化的功能，使得宿主系统和容器之间可以数据访问
* 链接：引用其他容器，进行容器间通讯。

## win10安装docker

* 开启Hyper-V,win10菜单右键->应用和功能->程序和功能->启用或关闭Windows功能->选中Hyper-V
* 去[docker官网](https://www.docker.com/get-started)注册并登陆下载相应的win10最新镜像安装.注:下载的不是最新版本的,有点问题,需要启动后右键check for updates,更新到最新版就能正常使用了,还可以下载kitematic镜像管理工具搭配使用.

## linux(ubuntu)下安装docker

* 使用 'sudo apt-get install docker.io' 命令安装 docker，然后通过 'docker version' 查看版本。这样docker就在本机上安装了。

## docker常用命令行,更多请参考[菜鸟教程](https://www.runoob.com/docker/docker-command-manual.html)

### 镜像仓库类 (login,pull,push,search)

* docker search mongo 查找镜像文件
* docker pull mongo:latest 拉取最新镜像文件,

### 容器操作 (run,start/stop/restart,kill,rm,pause/unpause,create,exec)

* docker run -v /my/own/datadir:/data/db --name mongo -d mongo mongod --smallfiles
(运行mongo容器。-v参数用来指明数据卷的位置，并以命名为/data/db。--name参数指明容器的名字，-d 表示以后台运行容器并返回容器ID。mongo mongod --smallfiles表示建立mongo镜像的容器并以smallfiles参数执行mongod。)
* docker ps 查看当前运行的容器 (加 -a查看当前所有容器)
* docker rm NAMES 删除容器 (可根据id或者name删除)
* docker restart NAMES 重启容器

### 容器rootfs命令 (commit,cp,diff)

### 本地镜像管理 (images,rmi,tag,build,history,save,load,import)

### 其他命令 (info,version)
