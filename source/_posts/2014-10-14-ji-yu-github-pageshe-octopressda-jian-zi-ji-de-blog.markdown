---
layout: post
title: "基于Github Pages和Octopress搭建自己的blog"
date: 2014-10-14 19:57:04 +0800
comments: true
categories:入门 
---

#基于Github Pages和Octopress搭建自己的blog
___
##前言
___
环境：Mac 10.9. ； Git ; Ruby 1.9.3 ; mou  

推荐参考[Octopress官方指南](http://octopress.org/docs/setup/)。
##安装Octopress
___
###安装rvm
由于Octopress需要Ruby，而Octopress要求的版本是1.9.3,像Mac自带的Ruby版本过高，这里安装的是Ruby1.9.3-p125。  
安装Ruby需要先安装rvm或者rbenv，这里以rvm为例说明(本人使用rbenv安装Ruby过程中出现了错误，因此转投rvm)。  
下载RVM：

    curl -L https://get.rvm.io | bash -s stable --ruby
    
###安装Ruby
安装Ruby 1.9.3：

    rvm install 1.9.3
	rvm use 1.9.3
	rvm rubygems latest
	
安装之后，需要指定使用1.9.3版本。
###安装Octopress

##部署博客
___

##写博客
___