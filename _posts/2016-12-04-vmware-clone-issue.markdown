---
layout: post
title:  "vmware 克隆 issue "
date:   2016-12-04 18:05:00
categories: vmware
---

[解决：：vmware 克隆问题] 网卡 eth0被重命名为eth1--主要手段删除70-persistent-net.rules

## 问题描述
vmware不管是linked克隆还是full克隆，会出现网卡重命名，例如网卡 eth0被重命名为eth1。



## 解决步骤
解决这样的问题，只需要下面几个步骤

- 重新生成mac地址
  点击右键-->设置-->硬件-->网络适配器-->高级-->生成

- 修改网卡配置信息
	<pre><code>
		vi /etc/sysconfig/network-scripts/ifcfg-eth0 

		TYPE=Ethernet
		DEVICE=eth0
		ONBOOT=yes
		BOOTPROTO=static
		IPADDR=192.168.100.201
		NETMASK=255.255.255.0
		GATEWAY=192.168.100.2
		DNS1=192.168.100.2
	</pre></code>


- 删除文件/etc/udev/rules.d/70-persistent-net.rules
	<pre><code>
		# cd /etc/udev/rules.d
		# cp 70-persistent-net.rules /root/
		# rm 70-persistent-net.rules
		# reboot
	</pre></code>
