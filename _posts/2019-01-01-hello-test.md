---
layout:              post
title:               "Github Pages+Jekyll博客搭建"
subtitle:            " \"Github Pages+Jekyll独立技术博客搭建教程\""
description:         "Github Pages Jekyll独立技术博客搭建教程"
date:                2019-01-01 00:00:00 +0800
author:              "SNLO"
header-img:          "img/header_code.jpg"
catalog:             true
tags:
- server
---

> 记录一些踩过的坑，躺过的河

### 简介

##### 为什么选择Github Pages？

- 免费，而且空间不限。
- 习惯了Git版本管理，可以直接在Github网页版上编辑和发布博客。

##### 为什么选择Jekyll？

- 被Github Pages推荐和默认支持的静态博客框架。

- 只关心`.md`的类容即可。简单不花哨，看它的<a href= "http://jekyllthemes.org/" target="_blank">官方主题</a>就知道。

### 项目环境

|  Name  | Version |                             Link                             |
| :----: | :-----: | :----------------------------------------------------------: |
|  Gem   | 2.5.2.3 | <a href= "https://gems.ruby-china.com" target="_blank">Sources</a> |
|  Ruby  |  2.3.7  | <a href= "https://www.ruby-lang.org/zh_cn/community/" target="_blank">Ruby社区</a> |
| Jekyll |  3.8.5  | <a href= "https://jekyllrb.com" target="_blank">Jekyllrb.com</a> |
| Gitalk |  1.4.1  | <a href= "https://gitalk.github.io" target="_blank">Github-gitalk</a> |

### Jekyll

plugins：-- jekyll-paginate

theme：<a href= "http://jekyllthemes.org/themes/project-pages/" target="_blank">Project-pages</a>

### Github Pages

怎么创建？其实很简单，就像新建Repositories一样，不同之处在于`Repository name`须命名为`user_name.github.io`的格式。其中`user_name`是指你Github的账户名，当然也可以不用这种命名格式。

- 若不是这是种命名格式，创建的Github Pages的访问地址是'https://user_name.github.io/custom_repository_name/'。
- 若是这是种命名格式，创建的Github Pages的访问地址是'https://user_name.github.io'。

创建好后，找到Repository的`settings`选项，在设置中选择一个Jekyll主题（Github Pages推荐和支持的博客是Jekyll，所以可以在这里选择Jekyll主题）。再回到设置界面，此时可以看见你博客访问域名了。

![](https://snlo.app/img/blog_img/190101/1.png)

![](https://snlo.app/img/blog_img/190101/2.png)

![](https://snlo.app/img/blog_img/190101/3.png)

若需要为博客配置自己的域名，则需要再到设置界面修改`Custom domain`选项值。Github Pages会为你的域名自动分配SSL证书，以使得域名可以经`https://`进行访问，值得注意的是Github Pages不提供自定义上传SSL证书的服务，所以有三个选择：

- 要么严格按照<a href= "https://help.github.com/articles/securing-your-github-pages-site-with-https/" target="_blank">Github Help - Enforce HTTPS</a>的指南进行域名的解析。
- 要么找类似<a href= "https://dash.cloudflare.com/" target="_blank">Cloudflare</a>域名托管服务提供商进行网站的反向代理。
- 要么就这样，以`http://`方式访问。

对于无法选中`Enforce HTTPS`选项的问题，强烈建议查看一下域名解析中是否已增加了一条为`letsencrypt.org 0 issue`的CAA记录，若没有则需要添加，关于这个问题只是针对已经颁发了SSL证书的域名。以下是Github技术支持的回复：

![](https://snlo.app/img/blog_img/190101/5.png)

### Gitalk

安装Gitalk bla bla bla bla... ...