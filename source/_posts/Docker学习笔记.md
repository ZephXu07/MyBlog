---
title: Docker学习笔记
date: 2020-08-02 17:34:30
tags: [笔记, docker]
---
[学习视频](https://www.bilibili.com/video/BV1og4y1q7M4?spm_id_from=333.788.b_765f64657363.1)

[笔记来源](https://blog.csdn.net/xiaozecheng/article/details/106145593)

> Docker 学习

- Docker 概述
- Docker安装
- Docker命令
  - 镜像命令
  - 容器命令
  - 操作命令
  - 。。。
- Docker镜像
- 容器数据卷
- DockerFile
- Docker网络原理
- IDEA整合Docker（单机Docker)
- Docker Compose
- Docker Swarm
- CI\CD Jenkins

<!-- more -->

# Docker概述

## Docker为什么出现？

一款产品： 开发–上线 两套环境！应用环境，应用配置！

开发 — 运维。 问题：我在我的电脑上可以允许！版本更新，导致服务不可用！对于运维来说考验十分大？

环境配置是十分的麻烦，每一个及其都要部署环境(集群Redis、ES、Hadoop…) !费事费力。

发布一个项目( jar + (Redis MySQL JDK ES) ),项目能不能带上环境安装打包！

之前在服务器配置一个应用的环境 Redis MySQL JDK ES Hadoop 配置超麻烦了，不能够跨平台。

开发环境Windows，最后发布到Linux！

传统：开发jar，运维来做！

现在：开发打包部署上线，一套流程做完！

安卓流程：java — apk —发布（应用商店）一 张三使用apk一安装即可用！

docker流程： java-jar（环境） — 打包项目帯上环境（镜像） — ( Docker仓库：商店）-----

Docker给以上的问题，提出了解决方案！

![image-20200514192040435](https://github.com/ZephXu07/IMG/raw/master/docker1.png)

Docker的思想就来自于集装箱！

JRE – 多个应用(端口冲突) – 原来都是交叉的！
隔离：Docker核心思想！打包装箱！每个箱子是互相隔离的。

Docker通过隔离机制，可以将服务器利用到极致！

本质：所有的技术都是因为出现了一些问题，我们需要去解决，才去学习！

## Docker历史

2010年，几个的年轻人，就在美国成立了一家公司 `dotcloud`

做一些pass的云计算服务！LXC（Linux Container容器）有关的容器技术！

> Linux Container容器是一种内核虚拟化技术，可以提供轻量级的虚拟化，以便隔离进程和资源。

他们将自己的技术（容器化技术）命名就是 Docker
Docker刚刚延生的时候，没有引起行业的注意！`dotCloud`，就活不下去！

==开源==

2013年，Docker开源！

越来越多的人发现docker的优点！火了。Docker每个月都会更新一个版本！

2014年4月9日，Docker1.0发布！

docker为什么这么火？十分的轻巧！

在容器技术出来之前，我们都是使用虚拟机技术！

虚拟机：在window中装一个VMware，通过这个软件我们可以虚拟出来一台或者多台电脑！笨重！

虚拟机也属于虚拟化技术，Docker容器技术，也是一种虚拟化技术！

==vm : linux centos 原生镜像（一个电脑！） 隔离、需要开启多个虚拟机！ 几个G 几分钟==
==docker: 隔离，镜像（最核心的环境 4m + jdk + mysql）十分的小巧，运行镜像就可以了！小巧！ 几个M 秒级启动！==
==12==

> 聊聊Docker

Docker基于Go语言开发的！开源项目！

[docker官网](https://www.docker.com/)

[文档](https://docs.docker.com/)： Docker的文档是超级详细的！

[仓库](https://hub.docker.com/)：

## Docker能干嘛

> 之前的虚拟机技术！

![image-20200515153852954](https://github.com/ZephXu07/IMG/raw/master/docker2.png)

**虚拟机技术缺点**：

1、 资源占用十分多

2、 冗余步骤多

3、 启动很慢！

> 容器化技术

==容器化技术不是模拟一个完整的操作系统==

![image-20200515094336846](https://github.com/ZephXu07/IMG/raw/master/docker3.png)

比较Docker和虚拟机技术的不同：

- 传统虚拟机，虚拟出一条硬件，运行一个完整的操作系统，然后在这个系统上安装和运行软件
- 容器内的应用直接运行在宿主机的内容，容器是没有自己的内核的，也没有虚拟我们的硬件，所以就轻便了
- 每个容器间是互相隔离，每个容器内都有一个属于自己的文件系统，互不影响

> DevOps（开发、运维）

**应用更快速的交付和部署**

传统：一堆帮助文档，安装程序。

Docker：打包镜像发布测试，一键运行。

**更便捷的升级和扩缩容**

使用了 Docker之后，我们部署应用就和搭积木一样
项目打包为一个镜像，扩展服务器A！服务器B

**更简单的系统运维**
在容器化之后，我们的开发，测试环境都是高度一致的

**更高效的计算资源利用**

Docker是内核级别的虚拟化，可以在一个物理机上可以运行很多的容器实例！服务器的性能可以被压榨到极致。

# Docker安装

## Docker的基本组成

![image-20200514195805400](https://github.com/ZephXu07/IMG/raw/master/docker4.png)

**镜像（image)：**

docker镜像就好比是一个目标，可以通过这个目标来创建容器服务，tomcat镜像\=\=>run\=\=>容器（提供服务器），通过这个镜像可以创建多个容器（最终服务运行或者项目运行就是在容器中的）。

**容器(container)：**

Docker利用容器技术，独立运行一个或者一组应用，通过镜像来创建的。
启动，停止，删除，基本命令
目前就可以把这个容器理解为就是一个简易的 Linux系统。

**仓库(repository)：**

仓库就是存放镜像的地方！
仓库分为公有仓库和私有仓库。(很类似git)
Docker Hub是国外的。
阿里云…都有容器服务器(配置镜像加速!)

## 安装Docker

> 环境准备

Linux要求内核3.0以上

```shell
➜  ~ uname -r    
4.15.0-96-generic # 要求3.0以上
➜  ~ cat /etc/os-release 
NAME="Ubuntu"
VERSION="18.04.4 LTS (Bionic Beaver)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 18.04.4 LTS"
VERSION_ID="18.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"VERSION_CODENAME=bionic
UBUNTU_CODENAME=bionic
1234567891011121314
```

> 安装

帮助文档：https://docs.docker.com/engine/install/

```bash
#1.卸载旧版本
yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
#2.需要的安装包
yum install -y yum-utils
#3.设置镜像的仓库
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
#默认是从国外的，不推荐
#推荐使用国内的
yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
#更新yum软件包索引
yum makecache fast
#4.安装docker相关的 docker-ce 社区版 而ee是企业版
yum install docker-ce docker-ce-cli containerd.io
#5、启动docker
docker systemctl start docker
#6. 使用docker version查看是否按照成功
docker version
#7. 测试
docker run hello-world
123456789101112131415161718192021222324252627282930
#7. 测试
➜  ~ docker run hello-world
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
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
12345678910111213141516171819202122
#8.查看一下下载的镜像
➜  ~ docker images         
REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
hello-world           latest              bf756fb1ae65        4 months ago        13.3kB
1234
```

了解：卸载docker

```shell
#1. 卸载依赖
yum remove docker-ce docker-ce-cli containerd.io
#2. 删除资源
rm -rf /var/lib/docker
# /var/lib/docker 是docker的默认工作路径！
12345
```

[Ubuntu19.10安装docker](https://www.cnblogs.com/Chaser-Eagle/p/12232382.html)

[在Ubuntu 18.04安装Docker](https://blog.csdn.net/b9567/article/details/105027440/)

## 阿里云镜像加速

1、登录阿里云找到容器服务

![image-20200515102112851](https://github.com/ZephXu07/IMG/raw/master/docker5.png)

2、找到镜像加速器

![image-20200515102009470](https://github.com/ZephXu07/IMG/raw/master/docker6.png)

3、配置使用

![image-20200515102216898](https://github.com/ZephXu07/IMG/raw/master/docker7.png)

```
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://8bbku6za.mirror.aliyuncs.com"]
}
EOF
systemctl daemon-reload
systemctl restart docker
```



## 回顾HelloWorld流程

![image-20200515102503722](https://github.com/ZephXu07/IMG/raw/master/docker8.png)

**docker run 流程图**

![image-20200515102637246](https://github.com/ZephXu07/IMG/raw/master/docker9.png)

## 底层原理

Docker**是怎么工作的**？

Docker是一个Client-Server结构的系统，Docker的守护进程运行在主机上。通过Socket从客户端访问！

Docker-Server接收到Docker-Client的指令，就会执行这个命令！

![image-20200515102949558](https://github.com/ZephXu07/IMG/raw/master/docker10.png)

**为什么Docker比Vm快**
1、docker有着比虚拟机更少的抽象层。由于docker不需要Hypervisor实现**硬件资源虚拟化**,运行在docker容器上的程序直接使用的都是实际物理机的硬件资源。因此在CPU、内存利用率上docker将会在效率上有明显优势。
2、docker利用的是宿主机的内核,而不需要Guest OS。

> GuestOS： VM（虚拟机）里的的系统（OS）;
>
> HostOS：物理机里的系统（OS）；

![image-20200515104117329](https://github.com/ZephXu07/IMG/raw/master/docker11.png)

因此,当新建一个 容器时,docker不需要和虚拟机一样重新加载一个操作系统内核。仍而避免引导、加载操作系统内核返个比较费时费资源的过程,当新建一个虚拟机时,虚拟机软件需要加载GuestOS,返个新建过程是**分钟级别**的。而docker由于直接利用宿主机的操作系统,则省略了这个复杂的过程,因此新建一个docker容器只需要**几秒钟**。

---

[Docker"Got permission denied while trying to connect to the Docker daemon socket"问题](https://blog.csdn.net/liangllhahaha/article/details/92077065)

---

# Docker的常用命令

## 帮助命令

```shell
docker version    #显示docker的版本信息。
docker info       #显示docker的系统信息，包括镜像和容器的数量
docker 命令 --help #帮助命令
123
```

[帮助文档的地址](https://docs.docker.com/engine/reference/commandline/build/)

## 镜像命令

> docker images #查看所有本地主机上的镜像 可以使用docker image ls代替
>
> docker search 搜索镜像
>
> docker pull 下载镜像 docker image pull
>
> docker rmi 删除镜像 docker image rm

**docker images** 查看所有本地的主机上的镜像

```shell
➜  ~ docker images
REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
mysql                 5.7                 e73346bdf465        24 hours ago        448MB

# 解释
#REPOSITORY			# 镜像的仓库源
#TAG				# 镜像的标签
#IMAGE ID			# 镜像的id
#CREATED			# 镜像的创建时间
#SIZE				# 镜像的大小
# 可选项
Options:
  -a, --all             Show all images (default hides intermediate images) #列出所有镜像
  -q, --quiet           Only show numeric IDs # 只显示镜像的id
  
➜  ~ docker images -aq ＃显示所有镜像的id
e73346bdf465
d03312117bb0
d03312117bb0
602e111c06b6
2869fc110bf7
470671670cac
bf756fb1ae65
5acf0e8da90b
```

**docker search 搜索镜像**

```shell
➜  ~ docker search mysql
NAME                              DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
mysql                             MySQL is a widely used, open-source relation…   9500                [OK]                
mariadb                           MariaDB is a community-developed fork of MyS…   3444                [OK]  
# --filter=STARS=3000 #搜索出来的镜像就是STARS大于3000的
Options:
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print search using a Go template
      --limit int       Max number of search results (default 25)
      --no-trunc        Don't truncate output
      
➜  ~ docker search mysql --filter=STARS=3000
NAME                DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
mysql               MySQL is a widely used, open-source relation…   9500                [OK]             
mariadb             MariaDB is a community-developed fork of MyS…   3444                [OK]
123456789101112131415
```

**docker pull** 下载镜像

```shell
# 下载镜像 docker pull 镜像名[:tag]
➜  ~ docker pull tomcat:8
8: Pulling from library/tomcat #如果不写tag，默认就是latest
90fe46dd8199: Already exists   #分层下载： docker image 的核心 联合文件系统
35a4f1977689: Already exists 
bbc37f14aded: Already exists 
74e27dc593d4: Already exists 
93a01fbfad7f: Already exists 
1478df405869: Pull complete 
64f0dd11682b: Pull complete 
68ff4e050d11: Pull complete 
f576086003cf: Pull complete 
3b72593ce10e: Pull complete 
Digest: sha256:0c6234e7ec9d10ab32c06423ab829b32e3183ba5bf2620ee66de866df640a027  # 签名 防伪
Status: Downloaded newer image for tomcat:8
docker.io/library/tomcat:8 #真实地址

#等价于
docker pull tomcat:8
docker pull docker.io/library/tomcat:8
```

**docker rmi 删除镜像**

```shell
➜  ~ docker rmi -f 镜像id #删除指定的镜像
➜  ~ docker rmi -f 镜像id 镜像id 镜像id 镜像id#删除指定的镜像
➜  ~ docker rmi -f $(docker images -aq) #删除全部的镜像
```

## 容器命令

> docker run 镜像id 新建容器并启动
>
> docker ps 列出所有运行的容器 docker container list
>
> docker rm 容器id 删除指定容器
>
> docker start 容器id #启动容器
> docker restart 容器id #重启容器
> docker stop 容器id #停止当前正在运行的容器
> docker kill 容器id #强制停止当前容器

说明：我们有了镜像才可以创建容器，Linux，下载centos镜像来学习

```bash
➜  ~ docker container     
Usage:  docker container COMMAND
Manage containers
Commands:
  attach      Attach local standard input, output, and error streams to a running container
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  inspect     Display detailed information on one or more containers
  kill        Kill one or more running containers
  logs        Fetch the logs of a container
  ls          List containers
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  prune       Remove all stopped containers
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  run         Run a command in a new container
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  wait        Block until one or more containers stop, then print their exit codes
Run 'docker container COMMAND --help' for more information on a command.
123456789101112131415161718192021222324252627282930
```

**新建容器并启动**

```shell
docker run [可选参数] image | docker container run [可选参数] image 
#参书说明
--name="Name"		容器名字 tomcat01 tomcat02 用来区分容器
-d					后台方式运行
-it 				使用交互方式运行，进入容器查看内容
-p					指定容器的端口 -p 8080(宿主机):8080(容器)
		-p ip:主机端口:容器端口
		-p 主机端口:容器端口(常用)
		-p 容器端口
		容器端口
-P(大写) 				随机指定端口
# 测试、启动并进入容器
➜  ~ docker run -it centos /bin/bash
[root@95039813da8d /]# ls  #查看容器内的centos
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@95039813da8d /]# exit #从容器退回主机
exit
➜  ~ ls
shell  user.txt
123456789101112131415161718192021222324
```

**列出所有运行的容器**

```shell
#docker ps命令 #列出当前正在运行的容器
  -a, --all       #运行及停止      Show all containers (default shows just running)
  -n, --last int        Show n last created containers (includes all states) (default -1)
  -q, --quiet           Only display numeric IDs
  
  ➜  ~ docker ps   
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                    NAMES
68729e9654d4        portainer/portainer   "/portainer"             14 hours ago        Up About a minute   0.0.0.0:8088->9000/tcp   funny_curie
d506a017e951        nginx                 "nginx -g 'daemon of…"   15 hours ago        Up 15 hours         0.0.0.0:3344->80/tcp     nginx01
➜  ~ docker ps -a
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS                       PORTS                    NAMES
95039813da8d        centos                "/bin/bash"              3 minutes ago       Exited (0) 2 minutes ago                              condescending_pike
1e46a426a5ba        tomcat                "catalina.sh run"        11 minutes ago      Exited (130) 9 minutes ago                            sweet_gould
14bc9334d1b2        bf756fb1ae65          "/hello"                 3 hours ago         Exited (0) 3 hours ago                                amazing_stonebraker
f10d60f473f5        bf756fb1ae65          "/hello"                 3 hours ago         Exited (0) 3 hours ago                                dreamy_germain
68729e9654d4        portainer/portainer   "/portainer"             14 hours ago        Up About a minute            0.0.0.0:8088->9000/tcp   funny_curie
677cde5e4f1d        elasticsearch         "/docker-entrypoint.…"   15 hours ago        Exited (143) 8 minutes ago                            elasticsearch
33eb3f70b4db        tomcat                "catalina.sh run"        15 hours ago        Exited (143) 8 minutes ago                            tomcat01
d506a017e951        nginx                 "nginx -g 'daemon of…"   15 hours ago        Up 15 hours                  0.0.0.0:3344->80/tcp     nginx01
24ce2db02e45        centos                "/bin/bash"              16 hours ago        Exited (0) 15 hours ago                               hopeful_faraday
42267d1ad80b        bf756fb1ae65          "/hello"                 16 hours ago        Exited (0) 16 hours ago                               ecstatic_sutherland
➜  ~ docker ps -aq
95039813da8d
1e46a426a5ba
14bc9334d1b2
f10d60f473f5
68729e9654d4
677cde5e4f1d
33eb3f70b4db
d506a017e951
24ce2db02e45
42267d1ad80b
```

**退出容器**

```shell
exit #容器直接退出
ctrl +P +Q #容器不停止退出
```

**删除容器**

```shell
docker rm 容器id   #删除指定的容器，不能删除正在运行的容器，如果要强制删除 rm -rf
docker rm -f $(docker ps -aq)  #删除指定的容器
docker ps -a -q|xargs docker rm  #删除所有的容器
```

**启动和停止容器的操作**

```shell
docker start 容器id	#启动容器
docker restart 容器id	#重启容器
docker stop 容器id	#停止当前正在运行的容器
docker kill 容器id	#强制停止当前容器
```

## 常用其他命令

**后台启动命令**

```shell
# 命令 docker run -d 镜像名
➜  ~ docker run -d centos
a8f922c255859622ac45ce3a535b7a0e8253329be4756ed6e32265d2dd2fac6c
➜  ~ docker ps           
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
# 问题docker ps. 发现centos 停止了
# 常见的坑，docker容器使用后台运行，就必须要有要一个前台进程，docker发现没有应用，就会自动停止
# nginx，容器启动后，发现自己没有提供服务，就会立刻停止，就是没有程序了
```

**查看日志**

```shell
docker logs --help
Options:
      --details        Show extra details provided to logs 
*  -f, --follow         Follow log output
      --since string   Show logs since timestamp (e.g. 2013-01-02T13:23:37) or relative (e.g. 42m for 42 minutes)
*      --tail string    Number of lines to show from the end of the logs (default "all")
*  -t, --timestamps     Show timestamps
      --until string   Show logs before a timestamp (e.g. 2013-01-02T13:23:37) or relative (e.g. 42m for 42 minutes)
➜  ~ docker run -d centos /bin/sh -c "while true;do echo 6666;sleep 1;done" #模拟日志      
#显示日志
-tf		#显示日志信息（一直更新）
--tail number #需要显示日志条数
docker logs -t --tail n 容器id #查看n行日志
docker logs -ft 容器id #跟着日志
```

**查看容器中进程信息** ps

```shell
# 命令 docker top 容器id
```

![image-20200515132913888](https://github.com/ZephXu07/IMG/raw/master/docker12.png)

**查看镜像的元数据**

```shell
# 命令
docker inspect 容器id

#测试
➜  ~ docker inspect 55321bcae33d
[
    {
        "Id": "55321bcae33d15da8280bcac1d2bc1141d213bcc8f8e792edfd832ff61ae5066",
        "Created": "2020-05-15T05:22:05.515909071Z",
        "Path": "/bin/sh",
        "Args": [
            "-c",
            "while true;do echo 6666;sleep 1;done"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 22973,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2020-05-15T05:22:06.165904633Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:470671670cac686c7cf0081e0b37da2e9f4f768ddc5f6a26102ccd1c6954c1ee",
        "ResolvConfPath": "/var/lib/docker/containers/55321bcae33d15da8280bcac1d2bc1141d213bcc8f8e792edfd832ff61ae5066/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/55321bcae33d15da8280bcac1d2bc1141d213bcc8f8e792edfd832ff61ae5066/hostname",
        "HostsPath": "/var/lib/docker/containers/55321bcae33d15da8280bcac1d2bc1141d213bcc8f8e792edfd832ff61ae5066/hosts",
        "LogPath": "/var/lib/docker/containers/55321bcae33d15da8280bcac1d2bc1141d213bcc8f8e792edfd832ff61ae5066/55321bcae33d15da8280bcac1d2bc1141d213bcc8f8e792edfd832ff61ae5066-json.log",
        "Name": "/bold_bell",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Capabilities": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/1f347949ba49c4dbee70cea9ff3af39a14e602bc8fac8331c46347bf6708757a-init/diff:/var/lib/docker/overlay2/5afcd8220c51854a847a36f52775b4ed0acb16fe6cfaec3bd2e5df59863835ba/diff",
                "MergedDir": "/var/lib/docker/overlay2/1f347949ba49c4dbee70cea9ff3af39a14e602bc8fac8331c46347bf6708757a/merged",
                "UpperDir": "/var/lib/docker/overlay2/1f347949ba49c4dbee70cea9ff3af39a14e602bc8fac8331c46347bf6708757a/diff",
                "WorkDir": "/var/lib/docker/overlay2/1f347949ba49c4dbee70cea9ff3af39a14e602bc8fac8331c46347bf6708757a/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "55321bcae33d",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "while true;do echo 6666;sleep 1;done"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20200114",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS",
                "org.opencontainers.image.created": "2020-01-14 00:00:00-08:00",
                "org.opencontainers.image.licenses": "GPL-2.0-only",
                "org.opencontainers.image.title": "CentOS Base Image",
                "org.opencontainers.image.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "63ed0c837f35c12453bae9661859f37a08541a0749afb86e881869bf6fd9031b",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/63ed0c837f35",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "b129d9a5a2cbb92722a2101244bd81a9e3d8af034e83f338c13790a1a94552a1",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.4",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:04",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "ad5ada6a106f5ba3dda9ce4bc1475a4bb593bf5f7fbead72196e66515e8ac36a",
                    "EndpointID": "b129d9a5a2cbb92722a2101244bd81a9e3d8af034e83f338c13790a1a94552a1",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.4",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:04",
                    "DriverOpts": null
                }
            }
        }
    }
]
➜  ~
```

**进入当前正在运行的容器**

```shell
# 我们通常容器都是使用后台方式运行的，需要进入容器，修改一些配置

# 命令 
docker exec -it 容器id bashshell

#测试
➜  ~ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
55321bcae33d        centos              "/bin/sh -c 'while t…"   10 minutes ago      Up 10 minutes                           bold_bell
a7215824a4db        centos              "/bin/sh -c 'while t…"   13 minutes ago      Up 13 minutes                           zen_kepler
55a31b3f8613        centos              "/bin/bash"              15 minutes ago      Up 15 minutes                           lucid_clarke
➜  ~ docker exec -it 55321bcae33d /bin/bash
[root@55321bcae33d /]# 

1234567891011121314
```

![image-20200515133433372](https://github.com/ZephXu07/IMG/raw/master/docker13.png)

```shell
# 方式二
docker attach 容器id
#测试
docker attach 55321bcae33d 
正在执行当前的代码...
区别
#docker exec #进入当前容器后开启一个新的终端，可以在里面操作。（常用）
#docker attach # 进入容器正在执行的终端
12345678
```

![image-20200515133907134](https://github.com/ZephXu07/IMG/raw/master/docker14.png)

**从容器内拷贝到主机上**

```shell
docker cp 容器id:容器内路径   主机目的路径
#进入docker容器内部
➜  ~ docker exec -it  55321bcae33d /bin/bash 
[root@55321bcae33d /]# ls
bin  etc   lib    lost+found  mnt  proc  run   srv  tmp  var
dev  home  lib64  media       opt  root  sbin  sys  usr
#新建一个文件
[root@55321bcae33d /]# echo "hello" > java.java
[root@55321bcae33d /]# cat java.java 
hello
[root@55321bcae33d /]# exit
exit
➜  ~ docker cp 55321bcae33d:/java.java /    #拷贝
➜  ~ cd /              
➜  / ls  #可以看见java.java存在
bin   home            lib         mnt   run       sys  vmlinuz
boot  initrd.img      lib64       opt   sbin      tmp  vmlinuz.old
dev   initrd.img.old  lost+found  proc  srv       usr  wget-log
etc   java.java       media       root  swapfile  var  
```

学习方式：将我的所有笔记敲一遍，自己记录笔记！

**小结：**

![image-20200514214313962](https://github.com/ZephXu07/IMG/raw/master/docker15.png)

```shell
  attach      Attach local standard input, output, and error streams to a running container
  #当前shell下 attach连接指定运行的镜像
  build       Build an image from a Dockerfile # 通过Dockerfile定制镜像
  commit      Create a new image from a container's changes #提交当前容器为新的镜像
  cp          Copy files/folders between a container and the local filesystem #拷贝文件
  create      Create a new container #创建一个新的容器
  diff        Inspect changes to files or directories on a container's filesystem #查看docker容器的变化
  events      Get real time events from the server # 从服务获取容器实时时间
  exec        Run a command in a running container # 在运行中的容器上运行命令
  export      Export a container's filesystem as a tar archive #导出容器文件系统作为一个tar归档文件[对应import]
  history     Show the history of an image # 展示一个镜像形成历史
  images      List images #列出系统当前的镜像
  import      Import the contents from a tarball to create a filesystem image #从tar包中导入内容创建一个文件系统镜像
  info        Display system-wide information # 显示全系统信息
  inspect     Return low-level information on Docker objects #查看容器详细信息
  kill        Kill one or more running containers # kill指定docker容器
  load        Load an image from a tar archive or STDIN #从一个tar包或标准输入中加载一个镜像[对应save]
  login       Log in to a Docker registry #
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes
```

# docker命令小结

```shell
systemctl start docker #启动docker命令
docker version  #查看docker是否启动
docker images  #查看docker 下载 镜像
docker search  名称  #搜索镜像
docker pull  镜像名：[:tag] #下载镜像
docker rmi -f 9cfcce23593a (通过 IMAGE ID 删除，删除单个容器) #删除单个容器镜像
docker rmi -f 容器id 容器id 容器id (通过 IMAGE ID 删除，删除多个容器) # 删除多个容器镜像
docker rmi -f $（docker images -qa） #删除全部容器镜像 
 # docker ps 命令
 # docker ps 查看当前运行的容器
   -a #列出当前运行的容器和历史
   -n # 列出最近运行的容器
exit #退出容器并且停止
Ctrl +P+Q #容器不停止退出
docker rm 容器id #删除指定容器（不能删除正在运行的容器 如果强制的话  rm -f）
docker rm -f $(docker ps -aq) #删除所有的容器
docker ps -a -q|xargs docker rm #删除所有容器
docker start 容器id        #启动容器
docker restart 容器id      #重启容器
docker stop 容器id		#停止当前正在运行的容器
docker kill 容器id		#强制停止当前容器
docker Logs -tf --tail 10 CONTAINER ID（值） #查看容器日志命令
docker top 8523b51dc9d4 #查看容器中的进程信息 ps
docker inspect 容器id #查看镜像的元数据
docker exec -it 容器id bashShell  #命令 docker exec 进入容器后开启新的（正常）
docker attach 容器id # docker attach 进入容器正在执行的终端，不会启动新的进程
docker cp 容器id:/容器文件夹/文件 /主机目录 #从容器内拷贝文件到主机上
docker stats # 查看内存状态
```

## 作业练习

> Docker 安装Nginx

```shell
docker pull nginx
#1. 搜索镜像 search 建议大家去docker搜索，可以看到帮助文档
#2. 拉取镜像 pull
#3、运行测试
# -d 后台运行
# --name 给容器命名
# -p 宿主机端口：容器内部端口
docker search nginx
docker pull nginx
docker run -d --name nginx01 -p 3344:80 nginx
docker ps
curl localhost:3344

#进入容器
docker exec -it nginx01 /bin/bash
whereis nginx
cd etc/nginx
ls

```

---

[物理机访问虚拟机中docker的nginx服务](https://www.cnblogs.com/dnoir/p/11719812.html)

虚拟机地址：192.168.195.129 docker 172.17.0.1

---



思考问题：我们每次改动nginx配置文件，都需要进入容器内部？十分的麻烦，要是可以在容器外部提供一个映射路径，达到在容器修改文件名，容器内部就可以自动修改？√数据卷！

![image-20200514215915650](https://github.com/ZephXu07/IMG/raw/master/docker16.png)

> 作用：docker 来装一个tomcat

```shell
# 官方的使用
docker run -it --rm tomcat:9.0
# 之前的启动都是后台，停止了容器，容器还是可以查到， docker run -it --rm image 一般是用来测试，用完就删除
--rm       Automatically remove the container when it exits
#下载
docker pull tomcat
#启动运行
docker run -d -p 3355:8080 --name tomcat01 tomcat
#测试访问有没有问题
curl localhost:8080

#进入容器
docker exec -it tomcat01 /bin/bash           
# 发现问题：1、linux命令少了。 2.没有webapps，阿里云镜像，默认最小
```

思考问题：我们以后要部署项目，如果每次都要进入容器是不是十分麻烦？要是可以在容器外部提供一个映射路径，webapps，我们在外部放置项目，就自动同步内部就好了！

> 作业：部署es+kibana

```shell
# es 暴露的端口很多！耗内存！
# es 的数据一般需要放置到安全目录！挂载
# --net somenetwork ? 网络配置

# 启动elasticsearch
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.6.2
# 测试一下es是否成功启动
➜  ~ curl localhost:9200
{
  "name" : "d73ad2f22dd3",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "atFKgANxS8CzgIyCB8PGxA",
  "version" : {
    "number" : "7.6.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
➜  ~ docker stats # 查看docker容器使用内存情况
```

![image-20200515152552722](https://github.com/ZephXu07/IMG/raw/master/docker17.png)

```shell
#关闭，添加内存的限制，修改配置文件 -e 环境配置修改
➜  ~ docker rm -f d73ad2f22dd3                                                  
➜  ~ docker run -d --name elasticsearch02 -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e ES_JAVA_OPTS="-Xms64m -Xmx512m" elasticsearch:7.6.2
```

![image-20200515153511695](https://github.com/ZephXu07/IMG/raw/master/docker18.png)

```shell
➜  ~ curl localhost:9200
{
  "name" : "b72c9847ec48",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "yNAK0EORSvq3Wtaqe2QqAg",
  "version" : {
    "number" : "7.6.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

作业：使用kibana连接es？思考网络如何才能连接

![image-20200515153725991](https://github.com/ZephXu07/IMG/raw/master/docker19.png)

## 可视化

- portainer(先用这个)

```shell
docker run -d -p 8088:9000 \
--restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
```

- Rancher(CI/CD再用)

**什么是portainer？**

Docker图形化界面管理工具！提供一个后台面板供我们操作！

```shell
docker run -d -p 8080:9000 \
--restart=always -v /var/run/docker.sock:/var/run/docker.sock --privileged=true portainer/portainer
12
```

测试访问： 外网：8080

![image-20200515155006079](https://github.com/ZephXu07/IMG/raw/master/docker20.png)

进入之后的面板

![image-20200515155113693](https://github.com/ZephXu07/IMG/raw/master/docker21.png)

# Docker镜像讲解

## **镜像是什么**

镜像是一种轻量级、可执行的独立软件保，用来打包软件运行环境和基于运行环境开发的软件，他包含运行某个软件所需的所有内容，包括代码、运行时库、环境变量和配置文件

## **Docker镜像加载原理**

> UnionFs （联合文件系统）

UnionFs（联合文件系统）：Union文件系统（UnionFs）是一种分层、轻量级并且高性能的文件系统，他支持对文件系统的修改作为一次提交来一层层的叠加，同时可以将不同目录挂载到同一个虚拟文件系统下（ unite several directories into a single virtual filesystem)。Union文件系统是 Docker镜像的基础。镜像可以通过分层来进行继承，基于基础镜像（没有父镜像），可以制作各种具体的应用镜像
特性：一次同时加载多个文件系统，但从外面看起来，只能看到一个文件系统，联合加载会把各层文件系统叠加起来，这样最终的文件系统会包含所有底层的文件和目录

> Docker镜像加载原理

docker的镜像实际上由一层一层的文件系统组成，这种层级的文件系统UnionFS。
boots(boot file system）主要包含 bootloader和 Kernel, bootloader主要是引导加 kernel, Linux刚启动时会加bootfs文件系统，在 Docker镜像的最底层是 boots。这一层与我们典型的Linux/Unix系统是一样的，包含boot加載器和内核。当boot加载完成之后整个内核就都在内存中了，此时内存的使用权已由 bootfs转交给内核，此时系统也会卸载bootfs。
rootfs（root file system),在 bootfs之上。包含的就是典型 Linux系统中的/dev,/proc,/bin,/etc等标准目录和文件。 rootfs就是各种不同的操作系统发行版，比如 Ubuntu, Centos等等。

![image-20200515163049959](https://github.com/ZephXu07/IMG/raw/master/docker22.png)

平时我们安装进虚拟机的CentOS都是好几个G，为什么Docker这里才200M？

![image-20200515163140559](https://github.com/ZephXu07/IMG/raw/master/docker23.png)

对于个精简的OS,rootfs可以很小，只需要包合最基本的命令，工具和程序库就可以了，因为底层直接用Host的kernel，自己只需要提供rootfs就可以了。由此可见对于不同的Linux发行版， boots基本是一致的， rootfs会有差別，因此不同的发行版可以公用bootfs.

虚拟机是分钟级别，容器是秒级！

## 分层理解

> 分层的镜像

我们可以去下载一个镜像，注意观察下载的日志输出，可以看到是一层层的在下载

![image-20200515163839180](https://github.com/ZephXu07/IMG/raw/master/docker24.png)

思考：为什么Docker镜像要采用这种分层的结构呢？

最大的好处，我觉得莫过于资源共享了！比如有多个镜像都从相同的Base镜像构建而来，那么宿主机只需在磁盘上保留一份base镜像，同时内存中也只需要加载一份base镜像，这样就可以为所有的容器服务了，而且镜像的每一层都可以被共享。

查看镜像分层的方式可以通过docker image inspect 命令

```shell
➜  / docker image inspect redis          
[
    {
        "Id": "sha256:f9b9909726890b00d2098081642edf32e5211b7ab53563929a47f250bcdc1d7c",
        "RepoTags": [
            "redis:latest"
        ],
        "RepoDigests": [
            "redis@sha256:399a9b17b8522e24fbe2fd3b42474d4bb668d3994153c4b5d38c3dafd5903e32"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2020-05-02T01:40:19.112130797Z",
        "Container": "d30c0bcea88561bc5139821227d2199bb027eeba9083f90c701891b4affce3bc",
        "ContainerConfig": {
            "Hostname": "d30c0bcea885",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "6379/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "GOSU_VERSION=1.12",
                "REDIS_VERSION=6.0.1",
                "REDIS_DOWNLOAD_URL=http://download.redis.io/releases/redis-6.0.1.tar.gz",
                "REDIS_DOWNLOAD_SHA=b8756e430479edc162ba9c44dc89ac394316cd482f2dc6b91bcd5fe12593f273"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "CMD [\"redis-server\"]"
            ],
            "ArgsEscaped": true,
            "Image": "sha256:704c602fa36f41a6d2d08e49bd2319ccd6915418f545c838416318b3c29811e0",
            "Volumes": {
                "/data": {}
            },
            "WorkingDir": "/data",
            "Entrypoint": [
                "docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {}
        },
        "DockerVersion": "18.09.7",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "6379/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "GOSU_VERSION=1.12",
                "REDIS_VERSION=6.0.1",
                "REDIS_DOWNLOAD_URL=http://download.redis.io/releases/redis-6.0.1.tar.gz",
                "REDIS_DOWNLOAD_SHA=b8756e430479edc162ba9c44dc89ac394316cd482f2dc6b91bcd5fe12593f273"
            ],
            "Cmd": [
                "redis-server"
            ],
            "ArgsEscaped": true,
            "Image": "sha256:704c602fa36f41a6d2d08e49bd2319ccd6915418f545c838416318b3c29811e0",
            "Volumes": {
                "/data": {}
            },
            "WorkingDir": "/data",
            "Entrypoint": [
                "docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": null
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 104101893,
        "VirtualSize": 104101893,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/adea96bbe6518657dc2d4c6331a807eea70567144abda686588ef6c3bb0d778a/diff:/var/lib/docker/overlay2/66abd822d34dc6446e6bebe73721dfd1dc497c2c8063c43ffb8cf8140e2caeb6/diff:/var/lib/docker/overlay2/d19d24fb6a24801c5fa639c1d979d19f3f17196b3c6dde96d3b69cd2ad07ba8a/diff:/var/lib/docker/overlay2/a1e95aae5e09ca6df4f71b542c86c677b884f5280c1d3e3a1111b13644b221f9/diff:/var/lib/docker/overlay2/cd90f7a9cd0227c1db29ea992e889e4e6af057d9ab2835dd18a67a019c18bab4/diff",
                "MergedDir": "/var/lib/docker/overlay2/afa1de233453b60686a3847854624ef191d7bc317fb01e015b4f06671139fb11/merged",
                "UpperDir": "/var/lib/docker/overlay2/afa1de233453b60686a3847854624ef191d7bc317fb01e015b4f06671139fb11/diff",
                "WorkDir": "/var/lib/docker/overlay2/afa1de233453b60686a3847854624ef191d7bc317fb01e015b4f06671139fb11/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:c2adabaecedbda0af72b153c6499a0555f3a769d52370469d8f6bd6328af9b13",
                "sha256:744315296a49be711c312dfa1b3a80516116f78c437367ff0bc678da1123e990",
                "sha256:379ef5d5cb402a5538413d7285b21aa58a560882d15f1f553f7868dc4b66afa8",
                "sha256:d00fd460effb7b066760f97447c071492d471c5176d05b8af1751806a1f905f8",
                "sha256:4d0c196331523cfed7bf5bafd616ecb3855256838d850b6f3d5fba911f6c4123",
                "sha256:98b4a6242af2536383425ba2d6de033a510e049d9ca07ff501b95052da76e894"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]
```

**理解：**

所有的 Docker镜像都起始于一个基础镜像层，当进行修改或培加新的内容时，就会在当前镜像层之上，创建新的镜像层。

举一个简单的例子，假如基于 Ubuntu Linux16.04创建一个新的镜像，这就是新镜像的第一层；如果在该镜像中添加 Python包，
就会在基础镜像层之上创建第二个镜像层；如果继续添加一个安全补丁，就会创健第三个镜像层该像当前已经包含3个镜像层，如下图所示（这只是一个用于演示的很简单的例子）。

![image-20200515165234274](https://github.com/ZephXu07/IMG/raw/master/docker25.png)

在添加额外的镜像层的同时，镜像始终保持是当前所有镜像的组合，理解这一点非常重要。下图中举了一个简单的例子，每个镜像层包含3个文件，而镜像包含了来自两个镜像层的6个文件。

![image-20200515164958932](https://github.com/ZephXu07/IMG/raw/master/docker26.png)

上图中的镜像层跟之前图中的略有区別，主要目的是便于展示文件
下图中展示了一个稍微复杂的三层镜像，在外部看来整个镜像只有6个文件，这是因为最上层中的文件7是文件5的一个更新版

![image-20200515165148002](https://github.com/ZephXu07/IMG/raw/master/docker27.png)

文种情況下，上层镜像层中的文件覆盖了底层镜像层中的文件。这样就使得文件的更新版本作为一个新镜像层添加到镜像当中

Docker通过存储引擎（新版本采用快照机制）的方式来实现镜像层堆栈，并保证多镜像层对外展示为统一的文件系统

Linux上可用的存储引撃有AUFS、 Overlay2、 Device Mapper、Btrfs以及ZFS。顾名思义，每种存储引擎都基于 Linux中对应的
件系统或者块设备技术，井且每种存储引擎都有其独有的性能特点。

Docker在 Windows上仅支持 windowsfilter 一种存储引擎，该引擎基于NTFS文件系统之上实现了分层和CoW [1]。

下图展示了与系统显示相同的三层镜像。所有镜像层堆并合井，对外提供统一的视图

![image-20200515165557807](https://github.com/ZephXu07/IMG/raw/master/docker28.png)

> 特点

Docker 镜像都是只读的，当容器启动时，一个新的可写层加载到镜像的顶部！

这一层就是我们通常说的容器层，容器之下的都叫镜像层！

![image-20200515161505897](https://github.com/ZephXu07/IMG/raw/master/docker29.png)

**commit镜像**

```shell
docker commit 提交容器成为一个新的副本

# 命令和git原理类似
docker commit -m="描述信息" -a="作者" 容器id 目标镜像名:[TAG]
1234
```

实战测试

```shell
# 1、启动一个默认的tomcat
docker run -d -p 8080:8080 tomcat
# 2、发现这个默认的tomcat 是没有webapps应用，官方的镜像默认webapps下面是没有文件的！
docker exec -it 容器id
# 3、拷贝文件进去
cp -r webapps.dist/* webapps
# 4、将操作过的容器通过commit调教为一个镜像！我们以后就使用我们修改过的镜像即可，这就是我们自己的一个修改的镜像。
docker commit -m="描述信息" -a="作者" 容器id 目标镜像名:[TAG]
docker commit -a="zeph" -m="add webapps app" cf23f6ff3f4b tomcat02:1.0
```

如果你想要保存当前容器的状态，就可以通过commit来提交，获得一个镜像，就好比我们我们使用虚拟机的快照。

****

==入门！！！！==

-----

[笔记docker 进阶 之容器数据卷 DockerFile Docker网络](https://blog.csdn.net/xiaozecheng/article/details/106165491)

# 容器数据卷

## 什么是容器数据卷

**docker的理念回顾**

将应用和环境打包成一个镜像！

数据？如果数据都在容器中，那么我们容器删除，数据就会丢失！==需求：数据可以持久化==

MySQL，容器删除了，删库跑路！==需求：MySQL数据可以存储在本地！==

容器之间可以有一个数据共享的技术！Docker容器中产生的数据，同步到本地！

这就是卷技术！目录的挂载，将我们容器内的目录，挂载到Linux上面！

![image-20200516105258456](https://github.com/ZephXu07/IMG/raw/master/docker30.png)

==**总结一句话：容器的持久化和同步操作！容器间也是可以数据共享的！**==

## 使用数据卷

> 方式一 ：直接使用命令挂载 -v

```shell
-v, --volume list                    Bind mount a volume

docker run -it -v 主机目录:容器内目录  -p 主机端口:容器内端口
➜ ~ docker run -it -v /home/ceshi:/home centos /bin/bash
#通过 docker inspect 容器id 查看
12345
```

![image-20200515191647970](https://github.com/ZephXu07/IMG/raw/master/docker31.png)

测试文件的同步

![image-20200515191718470](https://github.com/ZephXu07/IMG/raw/master/docker32.png)

再来测试！

1、停止容器

2、宿主机修改文件

3、启动容器

4、容器内的数据依旧是同步的

![image-20200516110850431](https://github.com/ZephXu07/IMG/raw/master/docker33.png)

好处：我们以后修改只需要在本地修改即可，容器内会自动同步！

## 实战：安装MySQL

思考：MySQL的数据持久化的问题

```shell
# 获取mysql镜像
➜  ~ docker pull mysql:5.7
# 运行容器,需要做数据挂载 #安装启动mysql，需要配置密码的，这是要注意点！
# 参考官网hub 
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag

#启动我们得
-d 后台运行
-p 端口映射
-v 卷挂载
-e 环境配置
-- name 容器名字
➜  ~ docker run -d -p 3310:3306 -v /home/zeph/Desktop/mysql/conf:/etc/mysql/conf.d -v /home/zeph/Desktop/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=10709991 --name mysql01 mysql:5.7

# 启动成功之后，我们在本地使用sqlyog来测试一下
# sqlyog-连接到服务器的3310--和容器内的3306映射 

# 在本地测试创建一个数据库，查看一下我们映射的路径是否ok！
```

假设我们将容器删除

![image-20200516112532950](https://github.com/ZephXu07/IMG/raw/master/docker34.png)

发现，我们挂载到本地的数据卷依旧没有丢失，这就实现了容器数据持久化功能。

## 具名和匿名挂载

```shell
# 匿名挂载
-v 容器内路径!
docker run -d -P --name nginx01 -v /etc/nginx nginx

# 查看所有的volume的情况
➜  ~ docker volume ls    
DRIVER              VOLUME NAME
local               33ae588fae6d34f511a769948f0d3d123c9d45c442ac7728cb85599c2657e50d
local            
# 这里发现，这种就是匿名挂载，我们在 -v只写了容器内的路径，没有写容器外的路劲！

# 具名挂载
➜  ~ docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx nginx
➜  ~ docker volume ls                  
DRIVER              VOLUME NAME
local               juming-nginx

# 通过 -v 卷名：容器内路径
# 查看一下这个卷
```

![image-20200516113545746](https://github.com/ZephXu07/IMG/raw/master/docker35.png)

所有的docker容器内的卷，没有指定目录的情况下都是在`/var/lib/docker/volumes/xxxx/_data`下
如果指定了目录，docker volume ls 是查看不到的

![image-20200516114231435](https://github.com/ZephXu07/IMG/raw/master/docker36.png)

```shell
# 三种挂载： 匿名挂载、具名挂载、指定路径挂载
-v 容器内路径			#匿名挂载
-v 卷名：容器内路径		#具名挂载
-v /宿主机路径：容器内路径 #指定路径挂载 docker volume ls 是查看不到的
1234
```

拓展：

```shell
# 通过 -v 容器内路径： ro rw 改变读写权限
ro #readonly 只读
rw #readwrite 可读可写
docker run -d -P --name nginx05 -v juming:/etc/nginx:ro nginx
docker run -d -P --name nginx05 -v juming:/etc/nginx:rw nginx

# ro 只要看到ro就说明这个路径只能通过宿主机来操作，容器内部是无法操作！
1234567
```

## 初始Dockerfile

Dockerfile 就是用来构建docker镜像的构建文件！命令脚本！先体验一下！

通过这个脚本可以生成镜像，镜像

```shell
# 创建一个dockerfile文件，名字可以随便 建议Dockerfile
# 文件中的内容 指令(大写) 参数
FROM centos

VOLUME ["volume01","volume02"]

CMD echo "----end----"
CMD /bin/bash
#这里的每个命令，就是镜像的一层！
```

`docker build -f /home/docker-test-volume/dockerfile1 -t zeph/centos:1.0 .`

![image-20200516121221066](https://github.com/ZephXu07/IMG/raw/master/docker37.png)

```shell
# 启动自己写的镜像
```

![image-20200516121459026](https://github.com/ZephXu07/IMG/raw/master/docker38.png)

这个卷和外部一定有一个同步的目录

![image-20200516121531626](https://github.com/ZephXu07/IMG/raw/master/docker39.png)

查看一下卷挂载

```
docker inspect 容器id
```

![image-20200516121630295](https://github.com/ZephXu07/IMG/raw/master/docker40.png)

测试一下刚才的文件是否同步出去了！

这种方式使用的十分多，因为我们通常会构建自己的镜像！

假设构建镜像时候没有挂载卷，要手动镜像挂载 -v 卷名：容器内路径！

## 数据卷容器

多个MySQL同步数据！

命名的容器挂载数据卷！

![image-20200516122047440](https://github.com/ZephXu07/IMG/raw/master/docker41.png)

```shell
--volumes-from list              Mount volumes from the specified container(s)
# 测试，我们通过刚才启动的
12
```

![image-20200516123020050](https://github.com/ZephXu07/IMG/raw/master/docker42.png)

![image-20200516123128475](https://github.com/ZephXu07/IMG/raw/master/docker43.png)

```shell
# 测试：可以删除docker01，查看一下docker02和docker03是否可以访问这个文件
# 测试依旧可以访问
```

![image-20200516123355034](https://github.com/ZephXu07/IMG/raw/master/docker44.png)

**==3个容器共享卷映射到宿主机相同地址。==**

多个mysql实现数据共享

```shell
➜  ~ docker run -d -p 3307:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7
➜  ~ docker run -d -p 3308:3306 -e MYSQL_ROOT_PASSWORD=123456 --name mysql02 --volumes-from mysql01  mysql:5.7
# 这个时候，可以实现两个容器数据同步！
123
```

结论：

容器之间的配置信息的传递，数据卷容器的生命周期一直持续到没有容器使用为止。

但是一旦你持久化到了本地，这个时候，本地的数据是不会删除的！

# DockerFile

## DockerFile介绍

`dockerfile`是用来构建docker镜像的文件！命令参数脚本！

构建步骤：

1、 编写一个dockerfile文件

2、 docker build 构建称为一个镜像

3、 docker run运行镜像

4、 docker push发布镜像（DockerHub 、阿里云仓库)

![image-20200516131400456](https://github.com/ZephXu07/IMG/raw/master/docker45.png)

点击后跳到一个Dockerfile

![image-20200516131441750](https://github.com/ZephXu07/IMG/raw/master/docker46.png)

很多官方镜像都是基础包，很多功能没有，我们通常会自己搭建自己的镜像！

官方既然可以制作镜像，那我们也可以！

## DockerFile构建过程

**基础知识：**

1、每个保留关键字(指令）都是必须是大写字母

2、执行从上到下顺序

3、#表示注释

4、每一个指令都会创建提交一个新的镜像层，并提交！

![image-20200516131756997](https://github.com/ZephXu07/IMG/raw/master/docker47.png)

Dockerfile是面向开发的，我们以后要发布项目，做镜像，就需要编写dockerfile文件，这个文件十分简单！

Docker镜像逐渐成企业交付的标准，必须要掌握！

DockerFile：构建文件，定义了一切的步骤，源代码

DockerImages：通过DockerFile构建生成的镜像，最终发布和运行产品。

Docker容器：容器就是镜像运行起来提供服务。

## DockerFile的指令

```shell
FROM				# 基础镜像，一切从这里开始构建
MAINTAINER			# 镜像是谁写的， 姓名+邮箱
RUN					# 镜像构建的时候需要运行的命令
ADD					# 步骤，tomcat镜像，这个tomcat压缩包！添加内容 添加同目录
WORKDIR				# 镜像的工作目录
VOLUME				# 挂载的目录
EXPOSE				# 保留端口配置
CMD					# 指定这个容器启动的时候要运行的命令，只有最后一个会生效，可被替代。
ENTRYPOINT			# 指定这个容器启动的时候要运行的命令，可以追加命令
ONBUILD				# 当构建一个被继承 DockerFile 这个时候就会运行ONBUILD的指令，触发指令。
COPY				# 类似ADD，将我们文件拷贝到镜像中，不会自动解压
ENV					# 构建的时候设置环境变量！
```

![1](https://github.com/ZephXu07/IMG/raw/master/docker48.png)

## 实战测试

> 创建一个自己的centos

```shell
# 1.编写Dockerfile文件
vim mydockerfile-centos
FROM centos
MAINTAINER zeph<1300928574@qq.com>

ENV MYPATH /usr/local
WORKDIR $MYPATH

RUN yum -y install vim
RUN yum -y install net-tools

EXPOSE 80

CMD echo $MYPATH
CMD echo "-----end----"
CMD /bin/bash
# 2、通过这个文件构建镜像
# 命令 docker build -f 文件路径 -t 镜像名:[tag] .
docker build -f mydockerfile-centos -t mycentos:0.1 .
```

![image-20200516140831464](https://github.com/ZephXu07/IMG/raw/master/docker49.png)

**测试运行**

![image-20200516141629583](https://github.com/ZephXu07/IMG/raw/master/docker50.png)

我们可以列出本地进行的变更历史

`docker history`

![image-20200516141840706](https://github.com/ZephXu07/IMG/raw/master/docker51.png)

我们平时拿到一个镜像，可以研究一下是什么做的

> CMD 和 ENTRYPOINT区别

```shell
CMD					# 指定这个容器启动的时候要运行的命令，只有最后一个会生效，可被替代。
ENTRYPOINT			# 指定这个容器启动的时候要运行的命令，可以追加命令
```

**测试cmd**

```shell
# 编写dockerfile文件
$ vim dockerfile-cmd-test
FROM centos
CMD ["ls","-a"]
# 构建镜像
$ docker build -f dockerfile-cmd-test -t cmd-test:0.1 .
# 运行镜像
$ docker run cmd-test:0.1
.
..
.dockerenv
bin
dev

# 想追加一个命令  -l 成为ls -al
$ docker run cmd-test:0.1 -l
docker: Error response from daemon: OCI runtime create failed: container_linux.go:349: starting container process caused "exec: \"-l\":
 executable file not found in $PATH": unknown.
ERRO[0000] error waiting for container: context canceled 
# cmd的情况下 -l 替换了CMD["ls","-l"]。 -l  不是命令所有报错
```

测试ENTRYPOINT

```shell
# 编写dockerfile文件
$ vim dockerfile-test-entrypoint
FROM centos
ENTRYPOINT ["ls","-a"]
docker build -f dockerfile-test-entrypoint -t test-entrypoint .
$ docker run test-entrypoint
.
..
.dockerenv
bin
dev
etc
home
lib
lib64
lost+found ...
# 我们的命令，是直接拼接在我们得ENTRYPOINT命令后面的
$ docker run test-entrypoint -l
total 56
drwxr-xr-x   1 root root 4096 May 16 06:32 .
drwxr-xr-x   1 root root 4096 May 16 06:32 ..
-rwxr-xr-x   1 root root    0 May 16 06:32 .dockerenv
lrwxrwxrwx   1 root root    7 May 11  2019 bin -> usr/bin
drwxr-xr-x   5 root root  340 May 16 06:32 dev
drwxr-xr-x   1 root root 4096 May 16 06:32 etc
drwxr-xr-x   2 root root 4096 May 11  2019 home
lrwxrwxrwx   1 root root    7 May 11  2019 lib -> usr/lib
lrwxrwxrwx   1 root root    9 May 11  2019 lib64 -> usr/lib64 ....
123456789101112131415161718192021222324252627
```

Dockerfile中很多命令都十分的相似，我们需要了解它们的区别，我们最好的学习就是对比他们然后测试效果！

## 实战：Tomcat镜像

1、准备镜像文件

 准备tomcat 和 jdk到当前目录，编写好README（百度）

![image-20200516162443652](https://github.com/ZephXu07/IMG/raw/master/docker52.png)

2、编写dokerfile

```shell
FROM centos 
MAINTAINER zeph<1300928574@qq.com>

COPY readme.txt /usr/local/readme.txt 
#复制文件
ADD jdk-8u261-linux-x64.tar.gz /usr/local/ 
#复制解压
ADD apache-tomcat-9.0.37.tar.gz /usr/local/ 
#复制解压

RUN yum -y install vim

ENV MYPATH /usr/local 
#设置环境变量
WORKDIR $MYPATH 
#设置工作目录

ENV JAVA_HOME /usr/local/jdk1.8.0_261 
#设置环境变量
ENV CLASSPATH $AJAVA_HOME/lib/dt.jar:%JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /usr/local/apache-tomcat-9.0.37 
#设置环境变量
ENV CATALINA_BASH /usr/local/apache-tomcat-9.0.37
ENV PATH $PATH:$JAVA_HOME/bin:$CATALINA_HOME/lib:$CATALINA_HOME/bin 
#设置环境变量 分隔符是：

EXPOSE 8080 
#设置暴露的端口
CMD /usr/local/apache-tomcat-9.0.37/bin/startup.sh && tail -F /usr/local/apache-tomcat-9.0.37/logs/catalina.out 
# 设置默认命令
```

3、构建镜像

```shell
# 因为dockerfile命名使用默认命名 因此不用使用-f 指定文件
$ docker build -t diytomcat:0.1 .
12
```

4、run镜像

```shell
docker run -d -p 9090:8080 --name zephtomcat -v /root/Desktop/tomcat/test:/usr/local/apache-tomcat-9.0.37/webapps/test -v /root/Desktop/tomcat/tomcatlogs/:/usr/local/apache-tomcat-9.0.37/logs diytomcat:0.1
```

5、访问测试

6、发布项目(由于做了卷挂载，我们直接在本地编写项目就可以发布了！)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd" id="WebApp_ID" version="3.0">
</web-app>
```

```jsp
<%@ page language="java" contentType="text/html; charset=utf-8"
         pageEncoding="utf-8" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <meta charset=utf-8">
    <title>zeph</title>
</head>
<body>
hello world<br/>
<%
	System.out.println("----test web logs----");
%>
</body>
</html>
```



发现：项目部署成功，可以直接访问！

我们以后开发的步骤：需要掌握Dockerfile的编写！我们之后的一切都是使用docker镜像来发布运行！

## 发布自己的镜像

> Dockerhub

1、地址 https://hub.docker.com/

2、确定这个账号可以登录

3、登录

```shell
$ docker login --help
Usage:  docker login [OPTIONS] [SERVER]

Log in to a Docker registry.
If no server is specified, the default is defined by the daemon.

Options:
  -p, --password string   Password
      --password-stdin    Take the password from stdin
  -u, --username string   Username
docker login -u zephxu
```

4、提交 push镜像

![image-20200516164434042](https://github.com/ZephXu07/IMG/raw/master/docker53.png)

```shell

# 会发现push不上去，因为如果没有前缀的话默认是push到 官方的library
# 解决方法
# 第一种 build的时候添加你的dockerhub用户名，然后在push就可以放到自己的仓库了
$ docker build -t zephxu/diytomcat:0.1 .
docker push zephxu/test-entrypoint:1.0
#docker push 用户名/镜像名:版本号
# 第二种 使用docker tag #然后再次push
$ docker tag 容器id chengcoder/mytomcat:1.0 #然后再次push
```

> 阿里云镜像服务上

[阿里云-->容器镜像-->命名空间-->容器镜像](https://cr.console.aliyun.com/repository/)

```
$ sudo docker push registry-vpc.cn-hangzhou.aliyuncs.com/acs/agent:0.7-dfb6816
```

```shell
$ sudo docker login --username=zchengx registry.cn-shenzhen.aliyuncs.com
$ sudo docker tag [ImageId] registry.cn-shenzhen.aliyuncs.com/dsadxzc/cheng:[镜像版本号]
# 修改id 和 版本
sudo docker tag a5ef1f32aaae registry.cn-shenzhen.aliyuncs.com/dsadxzc/cheng:1.0
# 修改版本
$ sudo docker push registry.cn-shenzhen.aliyuncs.com/dsadxzc/cheng:[镜像版本号]
```

![image-20200516171012186](https://github.com/ZephXu07/IMG/raw/master/docker54.png)

## 小结

![image-20200516171155667](https://github.com/ZephXu07/IMG/raw/master/docker55.png)

# Docker 网络

## 理解Docker 0

清空所有环境

> 测试

![image-20200515223236772](https://github.com/ZephXu07/IMG/raw/master/docker56.png)

三个网络

```shell
 # 问题： docker 是如果处理容器网络访问的？
1
```

![image-20200516172041985](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL2NoZW5nY29kZXgvY2xvdWRpbWcvbWFzdGVyL2ltZy9pbWFnZS0yMDIwMDUxNjE3MjA0MTk4NS5wbmc?x-oss-process=image/format,png)

```shell
# 测试  运行一个tomcat
$ docker run -d --name tomcat01 tomcat

$ ip addr       
# 查看容器内部网络地址 发现容器启动的时候会得到一个 eth0@if5 ip地址，docker分配！
4: eth0@if5: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever
       
# 思考？ linux能不能ping通容器内部！ 可以 容器内部可以ping通外界吗？ 可以！
$ ping 172.17.0.2
PING 172.17.0.2 (172.17.0.2) 56(84) bytes of data.
64 bytes from 172.17.0.2: icmp_seq=1 ttl=64 time=0.069 ms
64 bytes from 172.17.0.2: icmp_seq=2 ttl=64 time=0.074 ms
```

> 原理

1、我们每启动一个docker容器，docker就会给docker容器分配一个ip，我们只要按照了docker，就会有一个docker0桥接模式，使用的技术是[veth-pair技术](https://www.cnblogs.com/bakari/p/10613710.html)

再次测试ip add

![image-20200515224036883](https://github.com/ZephXu07/IMG/raw/master/docker57.png)

2 、在启动一个容器测试，发现又多了一对网络

![image-20200516173259458](https://github.com/ZephXu07/IMG/raw/master/docker58.png)

```shell
# 我们发现这个容器带来网卡，都是一对对的
# veth-pair 就是一对的虚拟设备接口，他们都是成对出现的，一端连着协议，一端彼此相连
# 正因为有这个特性 veth-pair 充当一个桥梁，连接各种虚拟网络设备的
# OpenStac,Docker容器之间的连接，OVS的连接，都是使用veth-pair技术
1234
```

3、我们来测试下tomcat01和tomcat02是否可以ping通

```shell
$ docker-tomcat docker exec -it tomcat01 ip addr  #获取tomcat01的ip 172.17.0.2   
550: eth0@if551: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever
$ docker-tomcat docker exec -it tomcat02 ping 172.17.0.2#让tomcat02ping tomcat01 
PING 172.17.0.2 (172.17.0.2) 56(84) bytes of data.
64 bytes from 172.17.0.2: icmp_seq=1 ttl=64 time=0.098 ms
64 bytes from 172.17.0.2: icmp_seq=2 ttl=64 time=0.071 ms
# 可以ping通
```

![image-20200516174248626](https://github.com/ZephXu07/IMG/raw/master/docker59.png)

结论：tomcat01和tomcat02公用一个路由器，docker0。

所有的容器不指定网络的情况下，都是docker0路由的，docker会给我们的容器分配一个默认的可用ip。

> 小结：

Docker使用的是Linux的桥接，宿主机是一个Docker容器的网桥 docker0

![image-20200516174701063](https://github.com/ZephXu07/IMG/raw/master/docker60.png)

Docker中所有网络接口都是虚拟的，虚拟的转发效率高（内网传递文件）

只要容器删除，对应的网桥一对就没了！

> 思考一个场景：我们编写了一个微服务，database url=ip: 项目不重启，数据ip换了，我们希望可以处理这个问题，可以通过名字来进行访问容器？

## –link

```shell
$ docker exec -it tomcat02 ping tomca01   # ping不通
ping: tomca01: Name or service not known
# 运行一个tomcat03 --link tomcat02 
$ docker run -d -P --name tomcat03 --link tomcat02 tomcat
5f9331566980a9e92bc54681caaac14e9fc993f14ad13d98534026c08c0a9aef
# 用tomcat03 ping tomcat02 可以ping通
$ docker exec -it tomcat03 ping tomcat02
PING tomcat02 (172.17.0.3) 56(84) bytes of data.
64 bytes from tomcat02 (172.17.0.3): icmp_seq=1 ttl=64 time=0.115 ms
64 bytes from tomcat02 (172.17.0.3): icmp_seq=2 ttl=64 time=0.080 ms

# 用tomcat02 ping tomcat03 ping不通
```

**探究：**

docker network inspect 网络id 网段相同

![image-20200516175904551](https://github.com/ZephXu07/IMG/raw/master/docker61.png)

docker inspect tomcat03

![image-20200516180308530](https://github.com/ZephXu07/IMG/raw/master/docker62.png)

查看tomcat03里面的/etc/hosts发现有tomcat02的配置

![image-20200516180629012](https://github.com/ZephXu07/IMG/raw/master/docker63.png)

–link 本质就是在hosts配置中添加映射

现在使用Docker已经不建议使用–link了！

自定义网络，不适用docker0！

docker0问题：不支持容器名连接访问！

## 自定义网络

```shell
docker network
connect     -- Connect a container to a network
create      -- Creates a new network with a name specified by the
disconnect  -- Disconnects a container from a network
inspect     -- Displays detailed information on a network
ls          -- Lists all the networks created by the user
prune       -- Remove all unused networks
rm          -- Deletes one or more networks
```

> 查看所有的docker网络

![image-20200516190316073](https://github.com/ZephXu07/IMG/raw/master/docker64.png)

**网络模式**

bridge ：桥接 docker（默认，自己创建也是用bridge模式）

none ：不配置网络，一般不用

host ：和所主机共享网络

container ：容器网络连通（用得少！局限很大）

测试

```shell
# 我们直接启动的命令 --net bridge,而这个就是我们得docker0
# bridge就是docker0
$ docker run -d -P --name tomcat01 tomcat
等价于 => docker run -d -P --name tomcat01 --net bridge tomcat

# docker0，特点：默认，域名不能访问。 --link可以打通连接，但是很麻烦！
# 我们可以 自定义一个网络
$ docker network create --driver bridge --subnet 192.168.0.0/16 --gateway 192.168.0.1 mynet
```

![image-20200516191139944](https://github.com/ZephXu07/IMG/raw/master/docker65.png)

```shell
$ docker network inspect mynet;
```

![image-20200516191407065](https://github.com/ZephXu07/IMG/raw/master/docker66.png)

启动两个tomcat,再次查看网络情况

```shell
docker run -d -P --name tomcat-net-01 --net mynet tomcat
docker run -d -P --name tomcat-net-02 --net mynet tomcat
```



![image-20200516191844240](https://github.com/ZephXu07/IMG/raw/master/docker67.png)

![image-20200516192007371](https://github.com/ZephXu07/IMG/raw/master/docker68.png)

在自定义的网络下，服务可以互相ping通，不用使用–link

![image-20200516192134673](https://github.com/ZephXu07/IMG/raw/master/docker69.png)

我们自定义的网络docker当我们维护好了对应的关系，推荐我们平时这样使用网络！

好处：

redis -不同的集群使用不同的网络，保证集群是安全和健康的

mysql-不同的集群使用不同的网络，保证集群是安全和健康的

![image-20200516192504367](https://github.com/ZephXu07/IMG/raw/master/docker70.png)

## 网络连通

![image-20200516193243146](https://github.com/ZephXu07/IMG/raw/master/docker71.png)

![image-20200516193259185](https://github.com/ZephXu07/IMG/raw/master/docker72.png)

```shell
# 测试两个不同的网络连通  再启动两个tomcat 使用默认网络，即docker0
docker network connect 容器 网络
$ docker run -d -P --name tomcat01 tomcat
$ docker run -d -P --name tomcat02 tomcat
# 此时ping不通
```

![image-20200516193554931](https://github.com/ZephXu07/IMG/raw/master/docker73.png)

```shell
# 要将tomcat01 连通 tomcat—net-01 ，连通就是将 tomcat01加到 mynet网络
# 一个容器两个ip（tomcat01）
```

![image-20200516193848337](https://github.com/ZephXu07/IMG/raw/master/docker74.png)

```shell
# 01连通 ，加入后此时，已经可以tomcat01 和 tomcat-01-net ping通了
# 02是依旧不通的
```

结论：假设要跨网络操作别人，就需要使用docker network connect 连通！

## 实战：部署Redis集群

![image-20200516194419471](https://github.com/ZephXu07/IMG/raw/master/docker75.png)

```shell
# 创建网卡
docker network create redis --subnet 172.38.0.0/16
# 通过脚本创建六个redis配置
for port in $(seq 1 6);\
do \
mkdir -p /mydata/redis/node-${port}/conf
touch /mydata/redis/node-${port}/conf/redis.conf
cat << EOF >> /mydata/redis/node-${port}/conf/redis.conf
port 6379
bind 0.0.0.0
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
cluster-announce-ip 172.38.0.1${port}
cluster-announce-port 6379
cluster-announce-bus-port 16379
appendonly yes
EOF
done

# 通过脚本运行六个redis
for port in $(seq 1 6);\
docker run -p 637${port}:6379 -p 1667${port}:16379 --name redis-${port} \
-v /mydata/redis/node-${port}/data:/data \
-v /mydata/redis/node-${port}/conf/redis.conf:/etc/redis/redis.conf \
-d --net redis --ip 172.38.0.1${port} redis:5.0.9-alpine3.11 redis-server /etc/redis/redis.conf
docker exec -it redis-1 /bin/sh #redis默认没有bash
redis-cli --cluster create 172.38.0.11:6379 172.38.0.12:6379 172.38.0.13:6379 172.38.0.14:6379 172.38.0.15:6379 172.38.0.16:6379  --cluster-replicas 1
```

![image-20200516202902241](https://github.com/ZephXu07/IMG/raw/master/docker76.png)

docker搭建redis集群完成！

![image-20200516203323971](https://github.com/ZephXu07/IMG/raw/master/docker77.png)



我们使用docker之后，所有的技术都会慢慢变得简单起来！

# SpringBoot微服务打包Docker镜像

1、构建SpringBoot项目

2、打包运行

```shell
mvn package
```

3、编写dockerfile

```shell
FROM java:8
COPY *.jar /app.jar
CMD ["--server.port=8080"]
EXPOSE 8080
ENTRYPOINT ["java","-jar","app.jar"]
```

4、构建镜像

```shell
# 1.复制jar和DockerFIle到服务器
# 2.构建镜像
$ docker build -t xxxxx:xx  .
```

5、发布运行

以后我们使用了Docker之后，给别人交付就是一个镜像即可！

# Docker Compose

## 简介

原先dockerfile build run，需要手动操作，单个容器！
Docker Compose 可以高效管理容器，定义运行多个容器。

==作用：批量容器编排。==

****

Compose是Docker官方的开源项目。需要安装！
web服务，redis，mysql，nginx……多个容器，通过compose可以快速启动。

Compose

```yml
version: '2.0'
services:
  web:
    build: .
    ports:
    - "5000:5000"
    volumes:
    - .:/code
    - logvolume01:/var/log
    links:
    - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```

docker-compose up 100个服务

Compose重要概念：

- 服务services，容器应用。(web,redis,mysql…)
- 项目project。一组关联的容器。 博客，web,mysql wp

## 安装Compose

1、下载

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# 备用地址，比较快
curl -L https://get.daocloud.io/docker/compose/releases/download/1.25.5/docker-compose-'uname -s'-'uname-m' > /usr/local/bin/docker-compose
```

2、授权

```bash
chmod +x /usr/local/bin/docker-compose
```

## getting start体验

官方地址：https://docs.docker.com/compose/gettingstarted/
python应用，计数器，redis

1、应用 app.py

```shell
mkdir composetest
cd composetest
vim app.py
```

```python
import time

import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)


def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)


@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)
```

`vim requirements.txt`

```
flask
redis
```

2、Dockerfile 应用打包为镜像

`vim Dockerfile `

```dockerfile
FROM python:3.7-alpine
WORKDIR /code
ENV FLASK_APP app.py
ENV FLASK_RUN_HOST 0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run"]
```

3、Docker-compose yml 文件（定义整个服务需要的环境：web, redis）

`vim docker-compose.yml `

```yml
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:alpine"
```

4、启动compose项目（docker-compose up）

`docker-compose up`

## 流程

1、创建网络

2、执行Docker-compose yaml

3、启动服务

Docker-compose yaml

Creating composetest_web_1   ... done
Creating composetest_redis_1 ... done

默认的服务名：==文件名_服务名\_num==
多个服务器 集群 A B _num，num代表副本数量
服务redis服务 => 4个副本
集群状态，服务都不可能只有一个运行实例。弹性

## 网络规则

NETWORK ID          NAME                  DRIVER              SCOPE
40b3600ac322        composetest_default   bridge              local

10个服务构成一个项目，项目中的内容都在同个网络下。

`docker inspect composetest_default`

```
"Containers": {
            "2381a01096bcce4feadef05194300cdbd309b0eb0aabacec676d4ff7d62920f4": {
                "Name": "composetest_redis_1",
                "EndpointID": "187fa1a26e568028ae1177a15aee73e35f7a2e7393115a52139649612678606d",
                "MacAddress": "02:42:ac:12:00:03",
                "IPv4Address": "172.18.0.3/16",
                "IPv6Address": ""
            },
            "767c5c85f88693f83ded0bf607b198efbfdb9317a1eacb0814b9190b52b19f72": {
                "Name": "composetest_web_1",
                "EndpointID": "065396cbe27beec58539302c359cc464ea3206189b4123e957ed30d2c5ae4b06",
                "MacAddress": "02:42:ac:12:00:02",
                "IPv4Address": "172.18.0.2/16",
                "IPv6Address": ""
            }
        },

```

在同一网络下，可通过名称访问，保证了高可用。

## 停止

docker-compose down 

ctrl+c

以前都是单个docker run启动容器，docker-compose通过yml配置文件，可以通过compose一键启动所有服务、停止

## Docker小结

1、docker镜像。run --> 容器

2、dockerFile构建镜像（服务打包）

3、docker-compose启动项目（编排、多个微服务或环境）

4、docker网络

## yaml规则

docker-compose.yaml核心

[官方文档](https://docs.docker.com/compose/compose-file/)

```yaml
#3层
version: ''
#版本
	服务1：web
	#服务配置
		images
		build
		network
		......
	服务2:
	......
#其他配置：网络、卷挂载、全局规则
volumes:
networks:
configs:

```

## 部署博客

[官方文档](https://docs.docker.com/compose/wordpress/)

下载程序、安装数据库、配置……

compose应用 ---> 一键启动

1、下载项目（docker-compose.yaml）

2、dockerfile

3、文件准备

4、启动`docker-compose up`

前台启动`docker-compose up -d`

## 实战

1、编写项目微服务

```java
@RestController
public class HelloController {
    @Autowired
    StringRedisTemplate redisTemplate;

    @GetMapping("/hello")
    public String hello() {
        Long views = redisTemplate.opsForValue().increment("views");
        return "hello world，views：" + views;
    }
}
```

2、Dockerfile构建镜像

```dockerfile
FROM java:8

COPY *.jar /app.jar

CMD ["--server.port=8080"]

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "/app.jar"]
```

3、docker-compose.yaml编排项目

```yaml
version: '3.8'
services:
  zephapp:
    build: .
    image: zephapp
    depends_on:
      - redis
    ports:
      - "8080:8080"
  redis:
    image: "library/redis:plpine"

```

4、加载到服务器，启动

`docker-compose up`

项目重新部署打包

```shell
docker-compose up --build
```

总结：

项目compose：三层

+ 工程Project
+ + 服务
  + + 容器：运行实例

# Docker Swarm

## 准备

+ 4台服务器，都安装docker

+ 技巧：xshell同步操作

## 工作模式

![image](https://github.com/ZephXu07/IMG/raw/master/swarm-diagram.png)

## 搭建集群

```shell
docker swarm --help

Usage:	docker swarm COMMAND

Manage Swarm

Commands:
  ca          Display and rotate the root CA
  init        Initialize a swarm
  join        Join a swarm as a node and/or manager
  join-token  Manage join tokens
  leave       Leave the swarm
  unlock      Unlock swarm
  unlock-key  Manage the unlock key
  update      Update the swarm

```

![images](https://github.com/ZephXu07/IMG/raw/master/docker78.png)

![images](https://github.com/ZephXu07/IMG/raw/master/docker79.png)

初始化节点：`docker swarm init --advertise-adr 172.24.82.149`

加入一个节点：`docker swarm join`

```shell
#获取令牌
docker swarm join-token mannager
docker swarm join-token worker
```

![images](https://github.com/ZephXu07/IMG/raw/master/docker80.png)

把后面的节点搭建进去：

![images](https://github.com/ZephXu07/IMG/raw/master/docker81.png)

==1、生成主节点 init==

==2、加入管理者、工作者==

==目标：双主双从==

## Raft协议

双主双从：假设一个节点失效，其他节点是否可以用？

Raft协议：保证大多数节点存活才可以用。集群至少需要==3==个管理节点，且需要==1==个管理节点存活才能保证集群可以使用！

### 实验：

1、将docker1机器停止，宕机！双主双从，另外一个主节点也不能使用。

![images](https://github.com/ZephXu07/IMG/raw/master/docker82.png)

2、可以让其他节点离开集群：

![images](https://github.com/ZephXu07/IMG/raw/master/docker83.png)

3、worker工作，manager管理，例如`docker node ls`，3台机器设置为manager。

==集群至少需要3个管理节点，且需要1个管理节点存活才能保证集群可以使用！==

**Raft协议：保证大多数节点存活才可以用，高可用！**

## 体会

弹性、扩缩容！集群！

告别`docker run`

单机：`docker-compose up`

集群：swarm，`docker service`

容器 --> 服务

容器 --> 服务 --> 副本

redis服务 --> 10个副本（同时开启10个redis容器）

体验：创建服务、动态扩展服务、动态更新服务。

![images](https://github.com/ZephXu07/IMG/raw/master/docker84.png)

灰度发布（金丝雀发布）

![images](https://github.com/ZephXu07/IMG/raw/master/docker85.png)

```shell
docker run
#容器启动，不具有扩缩容。
docker service
#服务，具有扩缩容，滚动更新。
```

查看服务 replicas

![images](https://github.com/ZephXu07/IMG/raw/master/docker86.png)

动态扩缩容

![images](https://github.com/ZephXu07/IMG/raw/master/docker87.png)

服务，集群中的任意的节点都可以访问。服务可以有多个副本动态扩缩容实现高可用。

![images](https://github.com/ZephXu07/IMG/raw/master/docker88.png)



## 概念总结

> swarm

集群的管理和编号。docker可以初始化一个swarm集群，其他节点可以加入（manager、worker）。

> Node

就是一个docker节点。多个节点就组成了一个网络集群。（manager、worker两种节点）

> Service

任务，可以在管理节点或者工作节点来运行。核心！用户访问！

> Tas

![images](https://github.com/ZephXu07/IMG/raw/master/docker89.png)

**逻辑是不变的。**

==命令 --> 管理 ---> api ---> 调度 --> 工作节点（创建Task容器维护）==

> 服务与全局服务

![images](https://github.com/ZephXu07/IMG/raw/master/docker90.png)

调整service以什么方式运行

```shell
--mode string
service mode (replicated or global)(default "relicated")

docker service create --mode replicated --name mytom tomcat:7

docker service create --mode global --name haha alpine baidu.com

#场景？日志收集
#每一个节点有自己的日志收集器，过滤。把所有日志最终再传给日志中心
#服务监控，状态性能
```

----

拓展：

​	网络模式：

​		"PublishMode":"ingress"

+ Swarm
+ Overlay
+ ingress：特殊的Overlay网络，具有负载均衡功能！IPVS、VIP



虽然docker在四台机器上，实际网络是同一个！ingress网络，是一个特殊的Overlay网络。

![images](https://github.com/ZephXu07/IMG/raw/master/docker91.png)

集群就是一个整体！

![images](https://github.com/ZephXu07/IMG/raw/master/docker92.png)

# Docker Stack

+ docker-compose 单机部署项目

+ docker stack 集群部署项目

```shell
#单机
docker-compose up -d wordpress.yaml

#集群
docker stack deploy wordpress.yaml

```

```
version: '3.4'
services:
  mongo:
    image: mongo
    restart: always
    networks: 
      - mongo_network
    deploy:
      restart_policy:
        condition: on-failure
      replicas: 2
  mongo-express: 
    image: mongo-express
    restart: always
    networks: 
      - mongo_network
    ports:
      - target: 8081
        published: 80
        protocol: tcp
        mode: ingress
    environment:
      ME_CONFIG_MONGODB_SERVER: mongo
      ME_CONFIG_MONGODB_PORT: 27017
    deploy:
      restart_policy:
        condition: on-failure
      replicas: 1
networks:
  mongo_network:
    external: true
```

![images](https://github.com/ZephXu07/IMG/raw/master/docker94.png)

# Docker Secret

安全，部署密码，证书！

![images](https://github.com/ZephXu07/IMG/raw/master/docker93.png)

# Docker Config

配置

![images](https://github.com/ZephXu07/IMG/raw/master/docker95.png)

# 拓展到K8S