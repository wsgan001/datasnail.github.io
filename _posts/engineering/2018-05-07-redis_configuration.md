---
layout: post
categories: Engineering
title: Redis使用Tips
author: datasnail
comments: true
show: index
intro: Redis的相关配置和使用Tips。
paperTime:
tags:
- 技术学习
---

### 一、Redis安装
Redis安装一般有两种方式，一种是去[Redis官网](https://redis.io/)下载安装包，然后解压、make；第二种是直接apt-get安装。   
第一种：
```
$ wget http://download.redis.io/releases/redis-4.0.9.tar.gz
$ tar zxvf redis-4.0.9.tar.gz
$ cd redis-4.0.9.tar.gz
$ make
```
安装完成后直接进入src目录下```./redis-server```启动。  
第二种：
```
$ sudo apt-get update
$ sudo apt-get install redis-server
```
然后直接启动```sudo /etc/init.d/redis-server start```。  

通过以上方法是否安装成功呢？可以启动Redis客户端查看，```redis-cli```，如果显示以下界面：
```
127.0.0.1:6379>
```
然后输入命令```ping```，返回```PONG```说明Redis安装成功，下面就基本可以愉快的玩耍Redis了。

### 二、配置文件(redis.cnf)
这部分网络上有很多博文记录和详解了Redis配置文件，有兴趣可以Google以下"Redis 配置文件详解"即有大批博文。  
1. 如果想要在另一台机器上远程访问Redis服务器，你可能要把配置文件中的```# bind 127.0.0.1```注释掉，或者改成```bind 0.0.0.0```，使得服务监听所有连接，如果只监听某台机器，可以配置```bind [机器IP]```。
2. 在Redis作为数据库使用的时候，可能会提示Redis内存不足而导致磁盘写错误。此时<span style="color:red">**切记不可**</span>通过设置Redis的最大内存来解决。是因为如果设置了最大内存，Redis有一个键删除策略删除你保存的Key值。[官方配置文件说明](https://redis.io/topics/config)有这样一段：  

{:.center}
![](/postimg/redis/redis_maxmemory.png)   
图1. 官方说明截取
{:.center}

可以看到，是**如果仅仅是把redis作为一个缓存来用的话，可以设置maxmemory**！因为利用有限的空间去更新数据，从而会按照删除策略删掉部分数据。



