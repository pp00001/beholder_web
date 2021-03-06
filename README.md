# beholder 

## 介绍

**beholder**是一款简洁而小巧的系统，主要作用是通过监控端口变化来发现企业内部的信息孤岛。例如：运维或开发新部署了一台机器未通知安全。没有采用masscan+nmap的组合进行检测，原因是在实际的使用中发现，虽然masscan可以提高扫描速度，但是漏报的情况太严重了。最终还是只使用nmap来进行探测。

系统由 `beholder_scanner`、 `beholder_web`  两个部分组成。这两个部分可以部署在一台机器上，也可以分开部署在不同的机器上。**当前项目为 `beholder_web`部分**。

* **beholder_scanner**：对IP进行端口扫描、比较端口变化，可部署多个beholder_scanner来组成集群加快扫描速度。
* **beholder_web**：提供前端界面展示。

## 支持任务

* 常规扫描：一次性的普通端口扫描任务
* 比较端口变化：用于比较两次扫描结果的端口变化
* 监控端口开放情况：一般用于监控IP是否开放高危端口，如开放则告警

## 支持平台

* Linux
* Windows

## 安装指南

[![Python 2.7](https://img.shields.io/badge/python-2.7-yellow.svg)](https://www.python.org/) 
[![Mongodb 3.x](https://img.shields.io/badge/mongodb-3.x-red.svg)](https://www.mongodb.com/download-center?jmp=nav)
[![Redis 3.x](https://img.shields.io/badge/redis-3.x-green)](https://redis.io/)

**依赖：项目运行依赖于mongodb和redis，所以需准备好mongodb和redis。mongodb和redis安装请参考：**

* [mongodb安装](./docs/mongodb.md)
* [redis安装](./docs/redis.md)

*** 
web端和scanner端的整体部署步骤都集中在[scanner的README](https://github.com/zj1244/beholder_scanner#%E5%AE%89%E8%A3%85%E6%8C%87%E5%8D%97)，这里不再重复。


## 使用手册

### 1. 配置
登陆平台后，需要在【配置】中设置扫描并发数。如果需要把比较结果发送邮箱，请配置邮件相关信息。

![](docs/pic/1.png)

### 2. 新增扫描任务
点击【添加任务】平台可以添加三种不同用途的扫描任务，分别是：

* 常规扫描：一次性的普通端口扫描任务
* 比较端口变化：用于比较两次扫描结果的端口变化
* 监控端口开放情况：一般用于监控高危端口的开放情况

![](docs/pic/5.png)

这里以比较端口变化任务为例，演示下使用方法。添加需要监控的IP段和端口后确定。注意：
* 任务名称不能重复
* 如果一个循环周期内扫描没有完成，下个循环周期开始时不会添加任务

![](docs/pic/2.png)

### 3. 查看端口变化
**当任务循环扫描两次（不含两次）以上时，才会进行端口比较。**

点击【任务列表】->【扫描详情】

![](docs/pic/3.png)

在【扫描详情】页面，点击【扫描次数】，可以查看每次扫描的IP变化。

![](docs/pic/4.png)