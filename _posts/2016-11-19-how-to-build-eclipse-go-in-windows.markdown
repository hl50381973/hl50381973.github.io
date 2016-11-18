---
layout: post
title:  "windows下用eclipse+goclipse插件+gdb搭建go语言开发调试环境!"
date:   2016-11-18 10:03:59
categories: go
---

## 安装goclipse
点击help-->eclipse marketplace->搜索goclipse-->安装

## 配置go解释器
preference -> 点击go -> 在directory下配置 go解释器的路径

## 下载GoCode源码
下载GoCode源码，从 https://github.com/nsf/gocode,下载源码后，在命令行进入文件夹目录执行`go build`编译生成`gocode.exe`

## 配置gocode
eclipse配置gocode，
preference -> 点击go -> tools --> gocode: executable:
选择生产的gocode.exe文件,apply接受并单击OK保持，敲入代码出现提示：

## 下载GDB
可以下载mingw 或者下载ruby的DevKit，就会有C:\DevKit\mingw\bin\gdb.exe
下载地址：http://rubyinstaller.org/downloads/
点击DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe

## 配置GDB
eclipse preferences--> 搜索debug --> 在c/c++ 的debug下的GDB里GDB debugger 中配置刚刚的gdb的路径