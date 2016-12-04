---
layout: post
title:  "zookeeper 搭建 "
date:   2016-11-27 16:05:00
categories: zookeeper
---

## zookeeper集群搭建

- 下载jdk1.7
	解压到/usr/local/jdk1.7路径
- 下载zookeeper

	http://zookeeper.apache.org/ 
	--> Getting Started 
	--> Download 
	-->Download
	-->Releases may be downloaded from Apache mirrors: Download
	-->下载当前最稳定版本zookeeper-3.4.9

- 使用xftp上传至centos 6的三个节点，上传地址/usr/local/software
- 解压 tar -zxvf zookeeper-3.4.5.tar.gz -C /usr/local
- mv zookeeper-3.4.5 zookeeper
- 配置环境变量
	<pre><code>
		vim /etc/profile
		export JAVA_HOME=/usr/local/jdk1.7
		export ZOOKEEPER_HOME=/usr/local/zookeeper
		export PATH=.:$JAVA_HOME/bin:$ZOOKEEPER_HOME/bin:$PATH
		source /etc/profile
	</code></pre>	
- cd /usr/local/zookeeper/conf
- mv zoo_sample.cfg zoo.cfg
- vim zoo.cfg
	<pre><code>
		dataDir=/usr/local/zookeeper/data
		server.0=192.168.100.201:2888:38888
		server.1=192.168.100.202:2888:38888
		server.2=192.168.100.203:2888:38888
	</code></pre>	
- mkdir -p /usr/local/zookeeper/data
- cd /usr/local/zookeeper/data
- 创建/usr/local/zookeeper/data/myid
	<pre><code>
		201机器上 vim myid，然后填写数字0
		202机器上 vim myid，然后填写数字1
		203机器上 vim myid，然后填写数字2
	</code></pre>	
- 启动	
	在三台机器上都敲打指令 zkServer.sh start	
	
- 查看状态
	 zkServer.sh status
	 有的是follower 有的是 leader

- 进入客户端
	随便挑选一台节点，zkCli.sh
- ls / 	查看zooker上的znode

---


## zookeeper单节点搭建
1. 修改操作系统的/etc/hosts文件添加：
	```192.168.3.71 edu-provider-01```
2. 到http://apache.fayea.com/zookeeper/下载zookeeper-3.4.6:
	- wget http://apache.fayea.com/zookeeper/zookeeper-3.4.6/zookeeper-3.4.6.tar.gz
3. 解压zookeeper安装包
	- tar -zxvf zookeeper-3.4.6.tar.gz
4. 在/home/wu/sc/zookeeper-3.4.6目录下创建以下目录:
	- mkdir data
	- mkdir logs
5. 将zookeeper-3.4.6/conf目录下的zoo_sample.cfg文件拷贝一份，命名为zoo.cfg文件拷贝一份，命名为zoo.cfg
	- cp zoo_sample.cfg zoo.cfg
6. 修改zoo.cfg配置文件
	<pre><code>
		vi zoo.cfg
		
		tickTime=2000
		initLimit=10
		syncLimit=5
		dataDir=/home/wusc/zookeeper-3.4.6/data
		dataLogDir=/home/wusc/zookeeper-3.4.6/logs
		clientPort=2181
		server.1=edu-provider-01:2888:3888
	</pre></code>	

7. 在dataDir=/home/wusc/zookeeper-3.4.6/data下创建myid文件
	编辑myid文件，并在对应的ip的机器上输入对应的编号。如在zookeeper上，myid文件内容就是1。
	如果只在单点上惊醒安装配置，那么只有一个server.1
8. wusc用户下修改vi /home/wusc/.bash_profile，增加zookeeper配置：
	<pre><code>
		export ZOOKEEPER_HOME=/home/wusc/zookeeper-3.4.6
		export PATH=.:$ZOOKEEPER_HOME/bin:$PATH
		使配置文件生效
		source .bash_profile
	</pre></code>
9. 启动并测试zookeeper
	(1)zkServer.sh start
	(2)jps
	(3)zkServer.sh status
	