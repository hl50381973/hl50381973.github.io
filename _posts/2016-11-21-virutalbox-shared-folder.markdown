---
layout: post
title:  "VirtualBox 共享文件夹设置 "
date:   2016-11-21 22:47:00
categories: VirtualBox
---

# VirtualBox 共享文件夹设置 

- 安装VirtualBox增强功能包(VBoxGuestAdditions)
- 安装完成后,会重启系统
- 点击 `设备` ,然后点击`共享文件夹`
- 点击共享文件夹设置框，右上角的添加按钮
- 选择共享文件夹
- 选择固定分配，自动挂载

	共享文件夹的配置，注意：下面是举例

	- 共享文件夹：D:\jdk   --> 这个是与linux共享的windows文件夹
	- 共享文件夹名称：jdk  --> 这个是共享文件夹的别名，在下面敲打sudo mount -t vboxsf `jdk` /home/liang/jdk命令中对应的`jdk`

---

- 接下来的步骤有两种方法	

	- 方法一

		命令 ：`sudo usermod -aG vboxsf <your username>`
		举例：比如说你的用户名是liang
		那么使用 `sudo usermod -aG vboxsf liang` -->意思就是把你的当前的用户添加到vboxsf 用户组里
		查看位置：Linux下的`/media/sf_jdk` 目录 查看
 
	- 方法二
	
		命令 ：`sudo mount -t vboxsf <sharename> <mountpoint>`
		步骤如下：

		- 在linux里创建一个挂载点, mkdir -p /home/liang/jdk
		- 然后 sudo mount -t vboxsf jdk /home/liang/jdk,这里jdk是上面共享文件夹名称，/home/liang/jdk是刚刚创建的挂载点