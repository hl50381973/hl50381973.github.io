---
layout: post
title:  "java spi 机制 "
date:   2016-11-27 16:05:00
categories: java spi
---
github code
https://github.com/hl50381973/spi-sample


目录结构：

└── src
├── com
│   └── ivanzhang
│       └── spi
│           ├── HelloInterface.java
│           ├── impl
│           │   ├── ImageHello.java
│           │   └── TextHello.java
│           └── SPIMain.java
└── META-INF
    └── services
        └── com.ivanzhang.spi.HelloInterface

重点：
在META-INF\services下创建一个文件，名叫com.ivanzhang.spi.HelloInterface
文件内容：
com.ivanzhang.spi.impl.TextHello
com.ivanzhang.spi.impl.ImageHello




 reference:
http://singleant.iteye.com/blog/1497259
http://ivanzhangwb.github.io/blog/2012/06/01/java-spi/