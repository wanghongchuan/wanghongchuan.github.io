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
环境：Mac 10.9. ； Git ; Ruby 1.9.3 ; mou  

推荐参考[Octopress官方指南](http://octopress.org/docs/setup/)。
##安装Octopress
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
首先，下载Octopress：
 
    $ git clone git://github.com/imathis/octopress.git octopress
安装依赖项：

    $ gem install bundler
    $ bundle install
我在执行bundle install的时候遇到错误，提示libffi install失败，其实不是libffi的问题，而是找不到make命令，需要Mac 安装Command Line Tools，其中带有GNU make功能。  

安装默认主题（个人感觉特别丑）：

    $ rake install
##部署博客
###部署
完成上面的内容之后，只是把Octopress部署到了本地，并没有和Github连接。  

首先，你需要到[github]()创建一个个人repo，命名格式一般是`username.github.io`.  
创建之后，就可以完成Github与Octopress连接：

    $ rake setup_github_pages
过程中会要求你输入你的仓库地址，按照要求输入就可以了，比如我输入的是：

    git@github.com:wanghongchuan/wanghongchuan.github.io.git
###检查配置
完成部署之后，最好检查一下目前存在哪些remote repo:

    $ git remote -v
    
我的输出是：

    octopress   git://github.com/imathis/octopress.git (fetch)
    octopress   git://github.com/imathis/octopress.git (push)
    origin   git@github.com:wanghongchuan/wanghongchuan.github.io.git (fetch)
    origin   git@github.com:wanghongchuan/wanghongchuan.github.io.git (push)
如果你的输出结果没有origin，你需要把按照下面的格式添加：

    git remote add origin git@github.com:username/username.github.io.git
命名repo分支master为source：

    $ git branch
    * master
    $ git branch -m master source
    $ git branch 
    * source
刚开始，对于不了解git的同学，对于branch、master、source，以及后面的add、commit、push等摸不着头脑，最好网上搜一下资料，理解一下。  

我们可以姑且这样理解（了解git的同学就不要看这一部分了，仅供参考，易于理解）:

- master:可以理解为你得repo的根目录
- branch:一个repo的根目录可以有多个分支
- source:本地都会生成一个source文件存放你的文件，对应于repo上也由一个source文件
- git add:就是把自己更改的内容进行添加
- git commit:就是提交最新程序的意思，用过SVN的就很好理解了
- git push origin source:把source更新到origin
- git pull:将git端的内容拉去到本地，git fetch实现功能，区别在于是否merge

##创建博客
###生成博客
输入下面代码：  

    $ rake generate
执行生成，会生成相应的source文件在本地。这个时候你已经可以预览一下blog界面了：

    $ rake preview
然后，在浏览器里面输入localhost:4000就可以看到了。  
接下来需要把生成后的代码上传到Github：  

    $ git add .
    $ git commit -m "your message"
    $ git push origin source
最后，完成部署。  

    $ rake deploy
现在，你可以在浏览器里输入username.github.io来访问自己blog了，第一次打开可能会有点慢，需要等一等。
###博客配置
你可以根据自己的信息配置blog，包括标题、姓名等等。  

	$ vim ~/octopress/_coinfig.yml
修改里面的内容就OK。
我们会发现默认的主题非常丑，你可以到[这里](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes)寻找自己喜欢的主题。比如我的诗[cleanpress主题](https://github.com/macjasp/cleanpress)：  

    $ cd octopress
    $ git clone git://github.com/macjasp/ cleanpress.git .themes/cleanpress
    $ rake install['cleanpress']
    $ rake generate
    
然后，部署到git上：  

    $ git add .
    $ git commit -m "your message"
    $ git push origin source
    
    $rake deploy
这时，你可以到username.github.io上看一下最新的blog界面了。
##写博客
###创建博客
现在，你可以写自己的第一篇博客了，比如这就是我的第一篇博客[基于Github Pages和Octopress搭建自己的blog](http://wanghongchuan.github.io)。  

    $ rake new_post['基于Github Pages和Octopress搭建自己的blog']
你可以在`~/source/_posts`下看到新生成的markdown文件。  
这时候你的博文只有题目等少量信息，不过已经可以预览一下了。  

    $ rake generate
    $ rake preview
进入localhost：4000。
###编辑博客
编辑博客只要打开markdown文件直接编辑就可以了，非常简单。  

个人推荐使用Mac端使用[Mou](http://25.io/mou/)进行markdown文件编辑，可以一边编辑一边预览效果。学习markdown语法也非常简单，直接查看Mou的help文件，完成可以掌握markdown文件的基本语法了。  

可能有人想知道，怎样在terminal上直接打开markdown文件并编辑呢?  

    $ open -a mou your-markdown-file-name
最后，还是老套路：  

    $ rake generate
    $ git add .
    $ git commit -m "your message"
    $ git push origin source
    $ rake deploy
你可以欣赏自己的第一篇blog了。
##定制博客
定制自己的博客，主要是完成评论、分享、定制域名、排版等功能，目前我还没有对自己的博客动刀，想深入了解的可以参照[这里](http://biaobiaoqi.me/blog/2013/07/10/decorate-octopress/)。  

好了，我也要欣赏一下自己的第一篇blog去了。