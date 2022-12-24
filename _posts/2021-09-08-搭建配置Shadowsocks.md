---
layout: post
title: "搭建配置Shadowsocks"
date: 2021-09-07
tag: 科学上网 
---

###  服务器端的安装，配置
1.>  系统要求 
* CentOS 7.*  

2.>  命令准备  
* vim：  
输入vim回车提示：

> -bash:vim:common not found  

输入命令：yum -y install vim-enhanced，开始下载安装作为依赖其他也会被安装进来（如果没有安装其他文件，则单独再进行安装）。  
安装完成后再次输入 vim 命令，有命令行的版本等信息显示，则安装成功。  
输入:q 回车退出。  
3.> 安装Shadowsocks，依次输入如下命令：

> [root@vps19163870 ~]# yum install -y epel-release  
> [root@vps19163870 ~]# yum install -y python-pip  
> [root@vps19163870 ~]# pip install shadowsocks  

***EPEL*** 的全称叫 Extra Packages for Enterprise Linux。EPEL 是由 Fedora 社区打造，为 RHEL 及衍生发行版如 CentOS、Scientific Linux 等提供高质量软件包的项目。装上了 EPEL 之后，就相当于添加了一个第三方源   
**pip** 是 Python 的包管理工具，这里我们用 pip 安装 shadowsocks。  
Shadowsocks安装成功画面  
![](/images/posts/Shadowsocks/2.png)  
4.> 配置Shadowsocks参数  
输入命令：vim /etc/shadowsocks.json  
> [root@vps19163870 ~]# vim /etc/shadowsocks.json  

> {  
  "server":"0.0.0.0",  
  "server_port":443,  
  "local_address": "127.0.0.1",  
  "local_port":1080,  
  "password":"1234567890",  
  "timeout":300,  
  "method":"aes-256-cfb",  
  "fast_open": false,  
  "workers": 1  
}  

其中参数解析如下：
* server：表示监听的地址，这里表示监听所有的地址；
* server_port： ss服务器端口
* local_address：本地地址
* local_port：本地端口
* password：连接ss密码。
* timeout：超时时间(秒)。
* method：通信加密方式。
* fast_open ：true或false。开启fast_open以降低延迟，但要求Linux内核在3.7+。
* workers：工作线程数    

5.> 为了方便启动和关闭 这里设置成自启动，命令如下

> [root@vps19163870 ~]# vim /etc/systemd/system/shadowsocks.service  

> [Unit]  
Description=Shadowsocks  
[Service]  

> TimeoutStartSec=0  
ExecStart=/usr/bin/sslocal -c /etc/shadowsocks.json  

> [Install]  
WantedBy=multi-user.target    

6.> 启动Shadowsocks服务
> [root@vps19163870 ~]# systemctl enable shadowsocks.service  
> [root@vps19163870 ~]# systemctl start  shadowsocks.service  
> [root@vps19163870 ~]# systemctl status shadowsocks.service  

启动成功如下图
![](/images/posts/Shadowsocks/6.png)  

至此Shadowsocks已经搭建完成。

###  客户端配置  
1.>  最新版Shadowsocks/SS windows客户端下载  
本地下载：[Shadowsocks-4.3.1.0.zip](https://netfiles.pw/download.php?filename=/ss/windows/Shadowsocks-4.3.1.128.zip)  
官网下载：[官网下载链接](https://github.com/shadowsocks/shadowsocks-windows/releases)  
使用教程：[Shadowsocks/SS windows客户端配置教程](https://v2raytech.com/shadowsocks-windows-client-config-tutorial/)

Windows平台下shadowsock官方版可能会出现大量“HTTP Auto Proxy Detection Worker Process”进程的bug，有大神进行了修复并提供修复版：[Shadowsocks-4.1.7.1修复版](https://netfiles.pw/download.php?filename=/ss/windows/Shadowsocks-win-4.1.7.1-tlanyan.zip)。如果你的系统没有这个问题，直接用最新官方版就可以。  
SS和SSR不是同一个东西，如果用的SSR，请到这个页面下载：[ShadowsocksR/SSR windows客户端下载](https://v2raytech.com/shadowsockr-shadowsocksr-ssr-windows-client-download/)











