---
layout: post
title:  CentOS:Docker:Nginx-Web
date: 2019-06-15 21:50:00 +0800
categories: 【运维】
tag: 【Docker】
---

### 问题定位

#### 问题描述：
1. 最近部门部门各个系统的URL又更新了，原本浏览器就已经存的地址废除了。
2. 所有人的地址都要更新地址：产品、前端、后端。

#### 解决方案：
1. 搭建一个小网站：包含需要的网址(URL资源中心)
2. 配置简单的域名
3. 更新部署方便

#### 需要资源：
1. 前端小伙一枚（自己不想写前端界面）
2. 服务器一台（可以要一台云主机）
3. 域名一枚（内网的DNS）

### 流程解析

#### 整体流程
1. 给前端小伙说了目的（他也很支持）
2. 大致画了简单的草图（简单草稿那种）
3. 他搞定了界面：大概20分钟：主要是找URL花了较多时间
4. 自己上传到公开的gitee仓库
5. 我找李子要服务器：10分钟
6. 安装Docker
7. 拉Nginx镜像
8. 启动容器：挂载文件
9. 排查Server 500的错误(docker装vim)
10. 愉快的成功了，小伙伴们分享😊

<br/> 
#### 前端界面（Vue.js）
这个没学过，估计不难，最近优先学后端架构。

<br/> 
#### 安装Docker（CentOS）
网上找到了这个[教程很不错👍](https://www.cnblogs.com/yufeng218/p/8370670.html)

1. 查看内核版本（内核版本>3.10）：
> uname -r 

2. 更新yum包(root权限)：
> sudo yum update

3. 卸载旧版本（可选）：
> sudo yum remove docker  docker-common docker-selinux docker-engine

4. 安装需要的软件包（yum-util提供yum-config-manager功能，另外两个是devicemapper驱动依赖的）
> sudo yum install -y yum-utils device-mapper-persistent-data lvm2

5. 设置yum源
> sudo yum-config-manager -&zwnj;-add-repo https://download.docker.com/linux/centos/docker-ce.repo

6. 查看所有仓库中所有docker版本，并选择特定版本安装
> yum list docker-ce -&zwnj;-showduplicates 

7. 安装docker
> sudo yum install docker-ce  # repo中默认只开启stable仓库，故这里安装的是最新稳定版17.12.0
>
> sudo yum install <FQPN>  # 例如：sudo yum install docker-ce-17.12.0.ce

8. 启动并加入开机启动
> sudo systemctl start docker
>
> sudo systemctl enable docker

9. 验证安装是否成功(有client和service两部分表示docker安装启动都成功了)
> docker version

<br/> 
#### Docker拉取Nginx镜像，配置Nginx
找的教程，一步一步来就能解决[教程很全，不过有坑](https://www.cnblogs.combingo1024/p/9022890.html)

1. 拉取镜像
> docker pull nginx

2. 创建挂载目录
> mkdir -p /data/nginx/{conf,conf.d,html,logs}

3. 安装vim
> yum install vim

4. 配置文件

> ###### vim /data/conf/nginx.conf
>
> user  nginx;
>
> worker_processes  1;
>
> error_log  /var/log/nginx/error.log warn;
>
> pid        /var/run/nginx.pid;
>
> events {
>
> &emsp;&emsp; worker_connections  1024;
>
>}
>
>http {
>
> &emsp;&emsp;include       /etc/nginx/mime.types;
>
> &emsp;&emsp;default_type  application/octet-stream;
>
> &emsp;&emsp;log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
>
> &emsp;&emsp;&emsp;&emsp; '$status $body_bytes_sent "$http_referer" '
>
> &emsp;&emsp;&emsp;&emsp;  '"$http_user_agent" "$http_x_forwarded_for"';
>
> &emsp;&emsp; access_log  /var/log/nginx/access.log  main;
>
> &emsp;&emsp; sendfile        on;
>
> &emsp;&emsp; #tcp_nopush     on;
>
> &emsp;&emsp; keepalive_timeout  65;
>
> &emsp;&emsp; #gzip  on;
>
> &emsp;&emsp; include /etc/nginx/conf.d/*.conf;
>
> }

> ###### vim /data/conf/nginx.conf

> server {  
>
> listen       80;  
>
> server_name  localhost;  
>
> location / {  
> 
> &emsp;&emsp; root   /usr/share/nginx/html;  
>
> &emsp;&emsp; index  index.html index.htm;  
>
> &emsp;&emsp; autoindex  on;  
>
> &emsp;&emsp;}  
>
> error_page   500 502 503 504  /50x.html;  
> 
> location = /50x.html { 
>
> &emsp;&emsp; root /usr/share/nginx/html; 
>
> &emsp;&emsp; }
> 
> }

#### 整体流程
将容器中nginx的80端口映射到本地的80端口

> docker run --name nginx81 -d -p 80:80 
> 
> &emsp;&emsp; -v /data/nginx/html:/usr/share/nginx/html 
>
> &emsp;&emsp; -v /data/nginx/conf/nginx.conf:/etc/nginx/nginx.conf  
>
> &emsp;&emsp; -v /data/nginx/logs:/var/log/nginx 
> 
> &emsp;&emsp; -v /data/nginx/conf.d:/etc/nginx/conf.d 
> 
> &emsp;&emsp; -d nginx:latest
> 

<br/> 
#### 问题解析 

1. nginx配置注意事项：
> nginx配置的资源地址必须是容器内部的地址，即映射的内部地址

2. nginx错误定位：
> 在容器内查看错误日志：
> 
> tail -f  error.log

3. docker命令：
> docker -p 宿主机端口：容器内端口 -v 宿主机文件路径：容器文件路径 -d 启动的镜像

4. 整个过程大致花了一个小时：
> 主要耗时在：nginx的配置错误导致一直报500的错误(重定向错误)
> 
> 问题定位不清楚，一直在纠结在挂载文件上(实际上是nginx的配置问题)































