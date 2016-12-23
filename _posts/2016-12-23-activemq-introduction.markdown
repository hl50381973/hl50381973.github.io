---
layout: post
title:  "ActiveMQ入门 "
date:   2016-12-13 16:05:00
categories: ActiveMQ
---

# ActiveMQ

### 下载地址（ActiveMQ 5.11.1）：
http://activemq.apache.org/activemq-5111-release.html
	
### 有两个版本
1. Windows Distribution  -- apache-activemq-5.11.1-bin.zip
2. Unix/Linux/Cygwin Distribution -- apache-activemq-5.11.1-bin.tar.gz
3. 说明 windows版本可以方便测试用，linux搭建集群用
		
###	Maven dependency:
	<dependency>
		<groupId>org.apache.activemq</groupId>
		<artifactId>activemq-all</artifactId>
		<version>5.11.1</version>
	</dependency>

### windows 启动
	apache-activemq-5.11.1/bin/win64/activemq.bat

### 管控台 启动
	http://localhost:8161/admin
	用户名：admin
	密码：admin	

### 配置文件：
	conf/activemq.xml	-- 有activemq的默认连接地址，tcp://127.0.0.1:61616
	conf/jetty-realm.properties -- activemq管控台的用户账号密码admin: admin, admin
	conf/jetty.xml -- activemq管控台的端口

## hello world例子
我们首先写一个简单的hello world例子，让大家感受一下ActiveMQ，我们需要实现接受者和发送者两部分代码的编写.
	
	Sender/Receiver:
	第一步：建立ConnectionFactory工厂对象，需要填入用户名、密码、以及要连接的地址，均使用默认即可，默认连接地址为“tcp://localhost:61616”
	第二步: 通过ConnectionFactory工厂对象我们创建一个Connection连接，并且调用Connection的start方法开启连接，Conneciton默认是关闭的。
	第三步：通过Connection对象创建Session会话（上下文环境对象），用于发送/接收消息，参数配置1为是否启用事务，参数配置2为签收模式，一般我们设置自动签收。
	第四步：通过Session创建Destination对象，指的是一个客户端用来指定生产消息目标和消费信息来源的对象，在PTP模式中，Destination被称作Queue即是队列：在Pub/Sub模式，Destination被称作Topic即主题。
	第五步：我们需要通过Session对象创建消息的发送和接受对象（生产者和消费者）MessageProducer/MessageConsumer
	第六步：我们可以使用MessageProducer的setDeliveryMode方法为其设置持久化和非持久化特性（DeliveryMode）
	第七步：最后我们使用JMS规范的TextMessage形式创建数据（通过session对象），并用MessageProducer的send方法发送数据，同理客户端使用receive方法进行接受数据。最后不要忘记关闭Connection连接。

github code：

	https://github.com/hl50381973/activemq-sample/tree/master/helloworld

