---
layout: post
title: "Windows安装Jekyll"
date: 2021-06-24 10:15:06
description: "Windows安装Jekyll"
tag: 个人博客搭建
---


### 1.首先下载Ruby
1.1 从[https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/) 选择需要安装的Ruby版本，点击链接下载，建议下载Ruby + Devkit安装程序
![](/images/posts/IntallJekyll/0.png)

### 2.安装Ruby
2.1 
![](/images/posts/IntallJekyll/1.png)


2.2 这三项可以都勾选，勾选”Add Ruby executables to your PATH“配置环境变量
![](/images/posts/IntallJekyll/2.png)
2.3 MSYS2 可以不勾选
![](/images/posts/IntallJekyll/3.png)
2.4 取消勾选，如需安装可以后续再装
![](/images/posts/IntallJekyll/4.png)

### 3.安装和配置Jekyll
3.1 首先确认gem是否安装，打开Powershell，输入gem -v 查看版本，如出现版本号，然后再输入  
gem install bundler jekyll 安装jekyll，这个安装过程有点慢，请耐心等待。
![](/images/posts/IntallJekyll/6.png)
3.2 安装完成后输入jekyll -v查看版本
![](/images/posts/IntallJekyll/7.png)
### 4.配置Jekyll
4.1 首先定位到要新建blog的文档地址，例如：E:\GitHub
![](/images/posts/IntallJekyll/11.png)
4.2 输入jekyll new myblog新建一个blog，新建需要等待一个比较长的时间
![](/images/posts/IntallJekyll/12.png)
4.3 如从别的地方拷贝过来的文件，例如从Github上拉取的源码，需要运行bundle install，  
这个过程是安装运行时的相关依赖及版本，具体可以打开Gemfile.lock文档查看安装项目，这个安装过程非常慢，请耐心等待。
![](/images/posts/IntallJekyll/13.png)
4.4 输入bundle exec jekyll serve启动jekyll，打开http://localhost:4000可以查看网页
![](/images/posts/IntallJekyll/10.png)
4.5 安装步骤如下图，如果是新建按照1->1.1->3步骤，如果是迁移或者是拷贝按照1->2->3步骤
![](/images/posts/IntallJekyll/5.png)
4.6 点<a href="{{site.baseUrl}}/files/install jekyll.7z">此处下载</a>批处理文件。用记事本打开批处理文件，根据自己情况更改文件的路径  
![](/images/posts/IntallJekyll/14.png)
### 5.Jekyll模板
5.1 从[http://jekyllthemes.org/](http://jekyllthemes.org/)选择模板。
### 6.错误排查
6.1 从github上拉取的模板，运行 bundle exec jekyll serve时报错，说明运行环境中有指定bundle的版本，文件夹中找到.gemspec文档，修改版本号和当前安装一致就行了。
![](/images/posts/IntallJekyll/15.png)
如上截图版本号1.12改为2.1.2，然后运行bundle exec jekyll serve正常。
![](/images/posts/IntallJekyll/16.png)


