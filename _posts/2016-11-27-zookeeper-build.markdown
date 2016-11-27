---
layout: post
title:  "zookeeper 搭建 "
date:   2016-11-27 16:05:00
categories: zookeeper
---

zookeeper 搭建

- 下载jdk1.7
	解压到/usr/local/jdk1.7路径
- 下载zookeeper
http://zookeeper.apache.org/ --> Getting Started --> Download -->Download-->Releases may be downloaded from Apache mirrors: Download
-->下载当前最稳定版本zookeeper-3.4.9

- 使用xftp上传至centos 6的三个节点，地址/usr/local/software
- 解压 tar -zxvf zookeeper-3.4.5.tar.gz -C /usr/local
- mv zookeeper-3.4.5 zookeeper
- 配置环境变量
    vim /etc/profile
	export JAVA_HOME=/usr/local/jdk1.7
	export ZOOKEEPER_HOME=/usr/local/zookeeper
	export PATH=.:$JAVA_HOME/bin:$ZOOKEEPER_HOME/bin:$PATH
	source /etc/profile
	
- cd /usr/local/zookeeper/conf
- mv zoo_sample.cfg zoo.cfg
- vim zoo.cfg
	dataDir=/usr/local/zookeeper/data
	server.0=192.168.100.201:2888:38888
	server.1=192.168.100.202:2888:38888
	server.2=192.168.100.203:2888:38888
- mkdir -p /usr/local/zookeeper/data
- cd /usr/local/zookeeper/data
- 创建/usr/local/zookeeper/data/myid
	201机器上 vim myid，然后填写数字0
	202机器上 vim myid，然后填写数字1
	203机器上 vim myid，然后填写数字2
	
- 启动	
	在三台机器上都敲打指令 zkServer.sh start	
	
- 查看状态
	 zkServer.sh status
	 有的是follower 有的是 leader

- 进入客户端
	随便挑选一台节点，zkCli.sh
- ls / 	查看zooker上的znode