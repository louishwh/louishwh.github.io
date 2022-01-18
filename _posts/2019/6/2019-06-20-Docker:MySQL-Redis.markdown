---
layout: post
title:  Docker:MySQL、Redis
date: 2019-06-20 21:00:00 +0800
categories: 【工具使用】
tag: 【Docker】
---

## MySQL安装
[1](https://www.runoob.com/docker/docker-install-redis.html)
[2](https://www.jianshu.com/p/a21be1a99b49)
[3](https://www.cnblogs.com/2016024291-/p/9045548.html)

1. 镜像拉取
> docker pull mysql:5.6 

2. 启动容器
> docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 
>
> &emsp;&emsp;-v $PWD/conf:/etc/mysql/conf.d 
>
> &emsp;&emsp;-v $PWD/data:/var/lib/mysql 
>
> &emsp;&emsp;-v $PWD/logs:/logs 
>
> &emsp;&emsp;--name test_mysql mysql:5.6

3. 参数说明:
> -d 让容器在后台运行 
> 
> -p 3306:3306 将容器的 3306 端口映射到主机的 3306 端口
> 
> -e 设置环境变量，这里是设置mysql的root用户的初始密码，这个必须设置 
> 
> -v $PWD/conf:/etc/mysql/conf.d 将主机当前目录下的 conf/my.cnf 挂载到容器的 /etc/mysql/my.cnf
> 
> -v $PWD/data:/var/lib/mysql 
将主机当前目录下的data目录挂载到容器的 /var/lib/mysql 
> 
> -v $PWD/logs:/logs 将主机当前目录下的 logs 目录挂载到容器的 /logs
> 
> –name 容器的名字，随便取，但是必须唯一

4. 远程访问
> 阿里云需要添加安全组


## [Redis安装](https://www.runoob.com/docker/docker-install-redis.html)

1. 拉取镜像
> docker pull redis

2. 创建文件
> 新建文件夹: mkdir redis
>
> 文件夹下建redis.conf

3. 配置文件添加配置信息
> 以下两线之间为配置信息

4. 运行容器
> docker run -p 6379:6379 
>
> &emsp;&emsp;--name redis 
>
> &emsp;&emsp;-v $PWD/redis.conf:/root/redis/redis.conf 
>
> &emsp;&emsp;-v $PWD/data:/root/redis/data 
>
> &emsp;&emsp;-d redis redis-server

5. 远程访问
> 阿里云需要添加安全组

----

#修改为守护模式

daemonize yes

#设置进程锁文件

pidfile redis/redis.pid

#端口

port 6379

#客户端超时时间

timeout 300

#日志级别

loglevel debug

#日志文件位置

logfile redis/log-redis.log

#设置数据库的数量，默认数据库为0，可以使用SELECT <dbid>命令在连接上指定数据库id

databases 8

##指定在多长时间内，有多少次更新操作，就将数据同步到数据文件，可以多个条件配合

#save <seconds> <changes>

#Redis默认配置文件中提供了三个条件：

save 900 1

save 300 10

save 60 10000

#指定存储至本地数据库时是否压缩数据，默认为yes，Redis采用LZF压缩，如果为了节省CPU时间，

#可以关闭该#选项，但会导致数据库文件变的巨大

rdbcompression yes

#指定本地数据库文件名

dbfilename dump.rdb

#指定本地数据库路径

dir redis/db/

#指定是否在每次更新操作后进行日志记录，Redis在默认情况下是异步的把数据写入磁盘，如果不开启，可能

#会在断电时导致一段时间内的数据丢失。因为redis本身同步数据文件是按上面save条件来同步的，所以有

#的数据会在一段时间内只存在于内存中

appendonly no

#指定更新日志条件，共有3个可选值：

#no：表示等操作系统进行数据缓存同步到磁盘（快）

#always：表示每次更新操作后手动调用fsync()将数据写到磁盘（慢，安全）

#everysec：表示每秒同步一次（折衷，默认值）

appendfsync everysec

#redis配置外网访问：

protected-mode no

#配置密码
requirepass password


----



