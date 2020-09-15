---
title: Nginx学习笔记
date: 2020-08-16 16:37:30
tags: [笔记, Nginx]
---
[b站学习视频](https://www.bilibili.com/video/BV1W54y1z7GM?from=search&seid=2798938044175624758)

# Nginx介绍

## 1.1引言

> 为什么要学习Nginx
> 问题1：客户端到底要将请求发送给哪台服务器
> 问题2：如果所有客户端的请求都发送给了服务器1
> 问题3：客户端发送的请求可能是申请动态资源的，也有申请静态资源的

<!-- more -->

**服务器搭建集群后：**

![0](https://github.com/ZephXu07/IMG/raw/master/Nginx0.png)

**在搭建集群后，使用Nginx做反向代理：**

![1](https://github.com/ZephXu07/IMG/raw/master/Nginx1.png)

## 1.2Nginx介绍

Nginx是由俄罗斯人研发的，应对Rambler的网站并发，并且2004年发布的第一个版本

**Nginx的特点**

+ 1.稳定性极强，7*24小时不间断运行(就是一直运行)
+ 2.Nginx提供了非常丰富的配置实例
+ 3.占用内存小，并发能力强(随便配置一下就是5w+，而tomcat的默认线程池是150

# Nginx的安装

## 2.1安装Nginx

使用docker-compose安装

```shell
#在/opt目录下创建docker_nginx目录
cd /opt
mkdir docker_nginx
#创建docker-compose.yml文件并编写下面的内容,保存退出
vim docker-compose.yml
version: '3.1'
services: 
  nginx:
    restart: always
    image: daocloud.io/library/nginx:latest
    container_name: nginx
    ports: 
      - 80:80
执行docker-compose up -d
```

访问80端口，看到下图说明安装成功（ncthz.top是我阿里云服务器的域名，大家输入自己服务器的Ip就可以访问80端口了）

![2](https://github.com/ZephXu07/IMG/raw/master/Nginx2.png)

## 2.2Nginx的配置文件

```shell
#查看当前nginx的配置需要进入docker容器中
docker exec -it 容器id bash
#进入容器后
cd /etc/nginx/
cat nginx.conf
```

nginx.conf文件内容如下

```json
user  nginx;
worker_processes  1;
error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;
# 以上同城为全局块
# worker_processes的数值越大，Nginx的并发能力就越强
# error_log代表Nginx错误日志存放的位置
# pid是Nginx运行的一个标识

events {
    worker_connections  1024;
}
# events块
# worker_connections的数值越大，Nginx的并发能力就越强

http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

   
    include /etc/nginx/conf.d/*.conf;
}

# http块
# include代表引入一个外部文件
# include       /etc/nginx/mime.types;	mime.types中存放着大量媒体类型
#include /etc/nginx/conf.d/*.conf;	引入了conf.d下以.conf为结尾的配置文件

```

conf.d目录下只有一个default.conf文件，内容如下

```json
server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

# server块
# listen代表Nginx监听的端口号
# server_name代表Nginx接受请求的IP

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }
# location块
# root:将接受到的请求根据/usr/share/nginx/html去查找静态资源
# index:默认去上述的路径中找到index.html或index.htm

   
}


```

## 2.3修改docker-compose文件

```shell
#退出容器
exit
#关闭容器
docker-compose down
#修改docker-compose.yml文件如下
version: '3.1'
services: 
  nginx:
    restart: always
    image: daocloud.io/library/nginx:latest
    container_name: nginx
    ports: 
      - 80:80
    volumes:
      - /home/opt/docker_nginx/conf.d/:/etc/nginx/conf.d
#重新构建容器
docker-compose bulid
#重新启动容器
docker-compose up -d
```

这时我们再次访问80端口是访问不到的，因为我们映射了数据卷之后还没有编写server块中的内容。

我们在/opt/docker_nginx/conf.d下新建default.conf，并插入如下内容

```json
server {
    listen       80;
    server_name  localhost;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }
}
#重启nginx
docker-compose restart
```

这时我们再访问80端口，可以看到是访问成功的

# Nginx的反向代理

## 3.1正向代理和反向代理介绍

正向代理：

+ 1.正向代理服务是由客户端设立的；
+ 2.客户端了解代理服务器和目标服务器都是谁；
+ 3.帮助咱们实现突破访问权限，提高访问的速度，对目标服务器隐藏客户端的ip地址。

![3](https://github.com/ZephXu07/IMG/raw/master/Nginx3.png)

反向代理：

+ 1.反向代理服务器是配置在服务端的；
+ 2.客户端不知道访问的到底是哪一台服务器；
+ 3.达到负载均衡，并且可以隐藏服务器真正的ip地址。

![4](https://github.com/ZephXu07/IMG/raw/master/Nginx4.png)

## 3.2基于Nginx实现反向代理

1、准备一个目标服务器
2、启动tomcat服务器
3、编写nginx的配置文件(/opt/docker_nginx/conf.d/default.conf)，通过Nginx访问到tomcat服务器

### 3.2.1准备tomcat服务器

[ERROR: yaml.scanner.ScannerError: while scanning for the next token
found character '\t' that cannot start any token
  in "./docker-compose.yml", line 4, column 1](https://blog.csdn.net/tianshuhao521/article/details/84592114)

```shell
#在/opt目录下创建docker_nginx目录
cd /opt
mkdir docker_mysql_tomcat
#创建docker-compose.yml文件并编写下面的内容,保存退出
vim docker-compose.yml
version: '3.1'
services:
  mysql:
  #服务的名称
    restart: always
    #docker启动，容器不自动启动
    image: daocloud.io/library/mysql:5.7.4
    #指定镜像路径
    container_name: mysql
    #容器名称
    ports: 
      - 3306:3306
    #指定端口映射
    environment:
      MYSQL_ROOT_PASSWORD: root
      #密码
      TZ: Asia/Shanghai
      #时区
    volumes:
      - /opt/docker_mysql_tomcat/mysql_data:/var/lib/mysql
  tomcat:
    restart: always
    #docker启动，容器不自动启动
    image: tomcat
    #指定镜像路径
    container_name: tomcat
    #容器名称
    ports: 
      - 8080:8080
      #指定端口映射
    environment:
      TZ: Asia/Shanghai
      #时区
    volumes:
      - /opt/docker_mysql_tomcat/tomcat_webapps:/usr/local/tomcat/webapps
      - opt/docker_mysql_tomcat/tomcat_logs:/usr/local/tomcat/logs

执行docker-compose up -d
```



### 3.2.2编写Nginx的配置文件，通过Nginx访问到tomcat服务器

opt/docker_nginx/conf.d下default.conf文件内容如下

```json
server {
  listen       80;
  listen  [::]:80;
  server_name  localhost;

  #基于反向代理访问到Tomcat服务器
  location / {
      proxy_pass http://192.168.145.128:8080/;
      #虚拟机或者服务器地址及端口
  }
	
#    location / {
#       proxy_pass http://ncthz.top:8080/;
#   }
}
```

### 3.2.3重启nginx

`docker-compose restart`

这时我们访问80端口可以看到8080端口tomcat的默认首页

## 3.3关于Nginx的location路径映射

### 3.3.1"="匹配

```json
location = / {
	#精准匹配，主机名后面不能带能和字符串
	#例如www.baidu.com不能是www.baidu.com/id=xxx
}
```

### 3.3.2 通用匹配


```json
location /xxx {
	#匹配所有以/xxx开头的路径
	#例如127.0.0.1:8080/xxx	xxx可以为空，为空则和=匹配一样
}
```

### 3.3.3正则匹配


```json
location ~ /xxx {
	#匹配所有以/xxx开头的路径
}
```

### 3.3.4匹配开头路径


```json
location ^~ /images {
	#匹配所有以/xxx开头的路径
}
```

### 3.3.5匹配结尾路径


```json
location ~* \.(gif|jpg|png)$ {
	#匹配以.gif、.jpg或者.png结尾的路径
}
```

**优先级关系：**
==(location = )  >  (location /xxx/yyy/zzz)  >  (location ^~/xxx)  >  (location \~/xxx , \~* \\. (gif | jpg | png))  >  (location /起始路径) > (location /)==



修改/opt/docker_nginx/conf.d/default.conf如下

```json
server {
    listen       80;
    server_name  localhost;

	location = /index {
        proxy_pass http://192.168.145.128:8081/;	#tomcat首页
    }

	location ^~ /ssm/ {
        proxy_pass http://192.168.145.128:8080/ssm/;	#SSM项目首页
    }

    location / {
        proxy_pass http://192.168.145.128:8080/;	#Hello Nginx
    }
}

#重启nginx
docker-compose restart
```



==访问192.168.145.128/index可以进入tomcat首页==
==访问192.168.145.128/ssm可以进入SSM项目首页==
==访问192.168.145.128/可以进入Hello Nginx==

# Nginx负载均衡

![10](https://github.com/ZephXu07/IMG/raw/master/Nginx10.png)

Nginx为我们默认提供了三种负载均衡的策略：
+ 1.轮询：
  + 将客户端发起的请求，平均分配给每一台服务器；
+ 2.权重：
  + 会将客户端的请求，根据服务器的权重值（处理速度、处理请求能力）不同，分配不同的数量；
+ 3.ip_hash:
  + 基于发起请求的客户端的ip地址不同，他始终会将请求发送到指定的服务器上
    就是说如果这个客户端的请求的ip地址不变，那么处理请求的服务器将一直是同一个。

## 4.1轮询

想实现Nginx轮询负载均衡机制只需要修改配置文件如下：
```
upstream my-server{
  server 192.168.145.128:8080;
  server 192.168.145.128:8081;
}
#名字不可带下划线
server {
  listen       80;
  server_name  localhost;
  location / {
    proxy_pass http://my-server/;
  }
	
####
upstream 名字{
    server ip:端口;
    server 域名:端口;
}
server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

	location / {
        proxy_pass http://upstream的名字/;	
    }
}
#####


```

重启nginx：

`docker-compose restart`

多次刷新http://192.168.145.128/页面，根据版本号我们可以发现我们进入的是不同的tomcat

![6](https://github.com/ZephXu07/IMG/raw/master/Nginx6.png)

![7](https://github.com/ZephXu07/IMG/raw/master/Nginx7.png)

## 4.2权重

实现权重的方式：在配置文件中upstream块中加上weight：

```
upstream my_server{
  server ncthz.top:8080 weight=10;
  server ncthz.top:8081 weight=2;
}
server {
  listen       80;
  server_name  localhost;

  location / {
    proxy_pass http://my_server/;
  }
}
```

## 4.3ip_hash

实现ip_hash方式：在配置文件upstream块中加上ip_hash：

```
upstream my_server{
	ip_hash;
    server ncthz.top:8080 weight=10;
    server ncthz.top:8081 weight=2;
}
server {
    listen       80;
    server_name  localhost;

	location / {
        proxy_pass http://my_server/;	#tomcat首页
    }
}
```

# Nginx动静分离

Nginx的并发能力公式：
 ==worker_processes * worker_connections / 4 （或者2）= Nginx最终的并发能力==
动态资源需要/4，静态资源需要/2
Nginx通过动静分离来提升Nginx的并发能力，更快的给用户响应

动态资源：

![11](https://github.com/ZephXu07/IMG/raw/master/Nginx11.png)

静态资源：

![12](https://github.com/ZephXu07/IMG/raw/master/Nginx12.png)

## 5.1动态资源代理

配置如下：

```json
location / {
  proxy_pass 路径;
}
1234
```

## 5.2静态资源代理

停掉nginx：`docker-compose down`

修改docker-compose.yml添加静态资源数据卷：

不同版本的静态资源位置可能不同，可以在2.2中查看默认的位置（location块中root后的路径）

启动nginx：`docker-compose up -d`

docker-compose.yml

```shell
version: '3.1'
services: 
  nginx:
    restart: always
    image: daocloud.io/library/nginx:latest
    container_name: nginx
    ports: 
      - 80:80
    volumes:
      - /opt/docker_nginx/conf.d/:/etc/nginx/conf.d
      - /opt/docker_nginx/img/:/data/img
      - /opt/docker_nginx/html/:/data/html
      
```



在/opt/docker_nginx/html下新建一个index.html（在index.html里面随便写点东西展示）与在/opt/docker_nginx/img下添加图片：
修改nginx的配置文件：

```json
#代理到html静态资源
location /html {
  root /data;
  index index.html;
}
#代理到img静态资源
location /img {
  root /data;
  autoindex on;
}
#配置如下
#location / {
#    root 静态资源路径;
#    index 默认访问路径下的什么资源;
#    autoindex on;#代表展示静态资源的全部内容，以列表的形式展开
#}
```

重启nginx：`docker-compose restart`
访问http://192.168.145.128/如下

html与img如下

![8](https://github.com/ZephXu07/IMG/raw/master/Nginx8.png)

![8](https://github.com/ZephXu07/IMG/raw/master/Nginx13.png)

## 5.3 403Forbidden

==**Docker安装Nginx访问html正常，访问jpg出现403，Forbidden，原因是图片权限不够，解决方法是`chmod 777 -R 1.jpg`**==

==[docker部署nginx访问文件报403](https://my.oschina.net/sprouting/blog/3269861/print)==

# Nginx集群

## 6.1引言

可能出现单点故障，避免nginx的宕机，导致整个程序的崩溃

+ 准备多台Nginx
+ 准备keepalived，监听nginx的健康情况
+ 准备haproxy，提供一个虚拟的路径，统一的去接收用户的请求

![9](https://github.com/ZephXu07/IMG/raw/master/Nginx9.png)

## 6.2搭建

```shell
#先准备好以下文件放入/opt/docker_nginx_cluster目录中
#然后启动容器	注意确保80、8081和8082端口未被占用(或者修改docker-compose.yml中的端口)
docker-compose up -d

然后我们访问8081端口可以看到master，访问8082端口可以看到slave
因为我们设置了81端口的master优先级未200比82端口的slave优先级100高，所以我们访问80端口看到的是master
现在我们模仿8081端口的nginx宕机了
docker stop 8081端口nginx容器的ID
这时我们再去访问80端口看到的就是slave了
```

Dockerfile

```dockerfile
FROM nginx:1.13.5-alpine

RUN apk update && apk upgrade

RUN apk add --no-cache bash curl ipvsadm iproute2 openrc keepalived

COPY entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

CMD ["/entrypoint.sh"]

```

entrypoint.sh

```sh
#!bin/bash

#/usr/sbin/keepalvined -n -l -D -f /etc/keepalived/keepalived.conf --dont-fork --log-console &
/usr/sbin/keepalived -D -f /etc/keepalived/keepalived.conf


nginx -g "daemon off;"

```

docker-compose.yml

```yml
version: "3.1"
services:
  nginx_master:
    build:
      context: ./
      dockerfile: ./Dockerfile
    ports:
      - 8081:80
    volumes:
      - ./index-master.html:/usr/share/nginx/html/index.html
      - ./favicon.ico:/usr/share/nginx/html/favicon.ico
      - ./keepalived-master.conf:/etc/keepalived/keepalived.conf
    networks:
      static-network:
        ipv4_address: 172.20.128.2
    cap_add:
      - NET_ADMIN
  nginx_slave:
    build:
      context: ./
      dockerfile: ./Dockerfile
    ports:
      - 8082:80
    volumes:
      - ./index-slave.html:/usr/share/nginx/html/index.html
      - ./favicon.ico:/usr/share/nginx/html/favicon.ico
      - ./keepalived-slave.conf:/etc/keepalived/keepalived.conf
    networks:
      static-network:
        ipv4_address: 172.20.128.3
    cap_add:
      - NET_ADMIN
  proxy:
    image: haproxy:1.7-alpine
    ports:
      - 80:6301
    volumes:
      - ./haproxy.cfg:/usr/local/etc/haproxy/haproxy.cfg
    networks:
      - static-network
networks:
  static-network:
    ipam:
      config:
        - subnet: 172.20.0.0/16
```

keepalived-master.conf

```json
vrrp_script chk_nginx {
    script "pidof nginx"
    interval 2
}

vrrp_instance VI_1 {
    state MASTER
    interface etch0	#容器内部的网卡名称
    virtual_router_id 33
    priority 200	#优先级
    advert_int 1
    
    autheentication {
    	auth_type PASS
    	auth_pass letmein
    }
    
    virtual_ipaddress {
        172.20.128.50	#虚拟路径
    }

    track_script {
        chk_nginx
    }
}

```

keepalived-slave.conf

```json
vrrp_script chk_nginx {
    script "pidof nginx"
    interval 2
}

vrrp_instance VI_1 {
    state BACKUP
    interface etch0	#容器内部的网卡名称
    virtual_router_id 33
    priority 100	#优先级
    advert_int 1
    
    autheentication {
      auth_type PASS
      auth_pass letmein
    }
    virtual_ipaddress {
      172.20.128.50	#虚拟路径
    }
    track_script {
      chk_nginx
    }
}

```

haproxy.cfg

```
global
    log 127.0.0.1 local0
    maxconn 4096
    daemon
    nbproc 4
	
defaults
    log 127.0.0.1 local3
    mode http
    option dontlognull
    option redispatch
    retries 2
    maxconn 2000
    balance roundrobin
    timeout connect 5000ms
    timeout client 5000ms
    timeout server 5000ms
	
frontend main
    bind *:6301
    default_backend webserver
	
backend webserver
    server nginx_master 172.20.128.50:80 check inter 2000 rise 2 fall 5

```

index-master.html

```html
<h1>master！</h1>
```

index-slave.html

```html
<h1>slave！</h1>
```

## 6.3bug：

+ services.nginx_master.ports contains an invalid type, it should be an array
  + [“-” 或者“:”需要有空格](https://blog.csdn.net/qq_28513801/article/details/93405315)

+ [ERROR: Pool overlaps with other one on this address space](https://blog.csdn.net/bjzhaoxiao/article/details/95622301)

+ [standard_init_linux.go:211: exec user process caused "exec format error"](https://blog.csdn.net/Min_Chander/article/details/105977963)