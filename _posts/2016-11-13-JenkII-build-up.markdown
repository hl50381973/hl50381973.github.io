---
layout: post
title:  "github pages 的搭建"
date:   2016-11-13 16:03:59
categories: github pages
---

## github pages 搭建


#### 安装 RubyInstaller for Windows

	下载地址：http://rubyinstaller.org/downloads/
	安装过程中，点击添加环境变量,或者事后手动添加环境变量
	选择最新版本 Ruby 2.3.1 (x64)

#### 安装 DEVELOPMENT KIT
	
	下载地址：http://rubyinstaller.org/downloads/
	选择版本 For use with Ruby 2.0 and above (x64 - 64bits only)
	配置：
		Download it, run it to extract it somewhere (permanent). 
		Then cd to it, run 'ruby dk.rb init and ruby dk.rb install' to bind it to ruby installations in your path.
	详细说明 https://github.com/oneclick/rubyinstaller/wiki/Development-Kit

#### 配置gem

	gem sources --remove https://rubygems.org/  
	gem sources -a http://gems.ruby-china.org/--（注意这里是http协议，网上给的https协议，会有认证失败错误）

#### Install Bundler
	gem install bundler

#### 配置Gemfile
	source 'http://gems.ruby-china.org/'
	gem 'github-pages', group: :jekyll_plugins
	bundle install

#### 一步步根据官网

	https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/	

*****
#### 参考博客

	https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/
	http://www.ezlippi.com/blog/2015/03/github-pages-blog.html

***

#### 注意
	官网中使用了jekyll _3.3.0_ new your-new-empty-directory
	上面是强制制定了jekyll的版本，很有可能和下载来来的jekyll_plugins不兼容
	所以建议取消版本号，只是使用jekyll _3.3.0_ your-new-empty-directory


	
