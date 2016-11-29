---
title: docker概念及基本用法2
date: 2016-11-23 22:44:34
tags: docker
---
## Docker概念
### 容器技术
特点：
 1. 比虚拟化技术更轻量级
 2. 资源消耗小
 3. 共享系统内核
 4. 基于LXC技术构建的容器引擎
 5. 核心理念就是 Build once, Run anywhere

### 镜像
类似于虚拟机里的镜像
通过Dockerfile创建，也可以通过DockerHub下载

### 容器
镜像的运行实例，容器之间隔离使用linux的CGroups和Namespaces技术实现，CGroups控制对硬件资源的访问，Namespaces提供环境的隔离。

### 仓库
类似于maven或者说像git仓库，可以push,pull

##安装
### ubuntu
```
$ sudo apt-get update
$ sudo apt-get install docker
```

### 基本命令
#### 查看Docker 命令
#### 命令帮助同其它linux 命令 --help

### Docker服务
docker服务启动选项：
/etc/default/docker
`DOCKER_OPTS`

#### 停止Docker服务
sudo service docker stop

#### 启动docker服务
sudo service docker start

#### 查看docker服务状态
sudo service docker status

#### docker镜像查找过程
docker run busybox echo "hello,Shi"
busybox:镜像名
1.首先本地查找
2.从Docker Hub或系统配置的默认Registry中下载

查看镜像
docker ps    不包括停止的镜像
docker ps -a 查看所有镜像

### 容器管理
#### docker run
创建容器
`$ docker run -t -i ubuntu /bin/bash`
-t：分配一个 pseudo-TTY
-i：--interactive参数缩写，表示交互模式，如果没有 attach 保持 STDIN 打开状态
ubuntu：运行的镜像名称，默认为latest 标签
/bin/bash：容器中运行的应用

退出
1. 直接 exit，这时候 bash 程序终止，容器进入到停止状态
2. 使用组合键退出，仍然保持容器运行，我们可以随时回来到这个bash中来，组合键是 **Ctrl-p Ctrl-q**，你没有看错，是两组组合键，先同时按下Ctrl和p，再按Ctrl和q。就可以退出到我们的宿主机了。

#### docker attach
进入正在运行的容器
`docker attach`

#### docker ps
查看正在运行的容器
- -a：查看所有容器，含停止运行的
- -l：查看刚启动的容器
- -q：只显示容器ID

#### docker start
启动容器

#### docker inspect
查看 Docker 容器或镜像的一些内部信息

#### docker rm
删除容器操作。不能删除运行的容器

### 镜像管理

#### docker images 命令我们可以列出当前系统上所有的镜像信息
#### 获取镜像docker pull busybox
#### 创建镜像
1. 创建Dockerfile文件
```
from ubuntu:latest
ENV HOSTNAME=shiyanlou
```
2. 执行docker build -t 镜像名 Dockerfile文件目录
3. 查看docker images

#### 清理镜像
```java
public static void main(){
	System.out.println("xxxxxx");
}
```
