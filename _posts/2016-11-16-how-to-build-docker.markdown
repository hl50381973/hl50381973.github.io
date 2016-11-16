---
layout: post
title:  "docker搭建l!"
date:   2016-11-13 16:03:59
categories: docker
---

# 一步步搭建docker（虚拟机中的Ubuntu环境下）

#### 下载virtualbox
如果windows上装了docker，那么会带有virtualbox

#### 下载Ubuntu镜像
[下载Ubuntu](http://www.ubuntu.org.cn/download/alternative-downloads) 点击Ubuntu 14.04.4 Desktop (64-bit) 

### 安装ubuntu
打开virtualbox-->
- 点击新建
	- 选择类型linux，版本Ubuntu
	- 4G内存
	- 现在创建虚拟硬盘
	- VDI
	- 动态分配
	- 32GB
- 点击设置
	- 点击存储
	- 分配光驱-->
- 点击启动
- ...keybord 选择chinese

- 安装增强功能
	设备--》安装增强功能

- 共享粘贴版
设备--》剪切板双向功能

- 共享文件夹
	设备--》 共享文件夹

- 配置163 apt源
	http://mirrors.163.com/.help/ubuntu.html 
	

-------------------------------------------------------------------
## 安装docker

### 参考installtion centos
https://docs.docker.com/engine/installation/linux/centos/	
	
```	
	Install with the script
		
	1.Log into your machine as a user with sudo or root privileges.
	2. Make sure your existing packages are up-to-date.
		(centos)$ sudo yum update 
		(ubuntu)$ sudo apt-get update
	3. Run the Docker installation script.
	 	（使用daocloud脚本）curl -sSL https://get.daocloud.io/docker | sudo sh
		(不建议使用官网的脚本，因为国内网络)$ curl -fsSL https://get.docker.com/ | sudo sh
```		
	
### 配置加速器
	https://www.daocloud.io/mirror#accelerator-doc
	curl -sSL https://get.daocloud.io/daotools/set_mirror.sh | sh -s http://xxx.m.daocloud.io
	

参考资料 chinese_docker
https://github.com/widuu/chinese_docker	
