---
title: "Hugo+Github Pasges建立个人博客"
date: 2020-05-05T22:50:18+08:00
lastmod: 2020-05-05T22:50:18+08:00
keywords: []
description: ""
tags: ["hugo","github","vscode"]
categories: ["IT技术"]
author: "桀木"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
toc: false
autoCollapseToc: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
reward: false
mathjax: false
---
#### 前言

此贴用于记录本站的建立过程。  
为了便于数据的集中化管理，所有的数据和程序尽量部署在云端（家庭私有云+All-in-one服务器）：

1. 数据存放于群晖DS215j（家庭私有云）
2. Hugo和Code-server(vscode)程序运行于Unraid（All-in-one服务器）虚拟的Debian 10

#### 1. Hugo安装  
通过SSH或者Unraid里的VNC Remote登录Debian 10  
下载并安装Go语言和最新版的Hugo：  
```bash
apt-get install golang
wget https://github.com/gohugoio/hugo/releases/download/v0.69.2/hugo_0.69.2_Linux-64bit.deb
dpkg -i hugo_0.69.2_Linux-64bit.deb
hugo version
```
如果正确返回版本信息，说明已经安装成功

具体hugo建站流程参见官网教程[Quick Start](https://gohugo.io/getting-started/quick-start/)

#### 2. Host on Github
官方教程：
* 在Github中创建一个代码仓库\<YOUR-PROJECT\>用于存放Hugo的相关文件；
* 在Github中创建\<USERNAME\>.github.io代码仓库，用于存放网页文件；
* git clone \<YOUR-PROJECT-URL\> && cd \<YOUR-PROJECT\>
* 将Hugo站点文件复制到本地仓库 \<YOUR-PROJECT\>  
* 删除public文件夹
```bash
rm -rf public
```

* 建立submodule，将本地public代码仓库关联到\<USERNAME\>.github.io
```bash
git submodule add -b master https://github.com/\<USERNAME\>/\<USERNAME\>.github.io.git public
```


#### 3. Code-server(vscode)作为Markdown编辑器  

Code-server 的官方描述“Code-server is VS Code running on a remote server, accessible through the browser.”，它是一个运行在远端服务器上的VS Code，可以通过浏览器进行访问和操作。
![](https://github.com/cdr/code-server/raw/master/doc/assets/code-server.gif)

未完待续


<!--more-->
