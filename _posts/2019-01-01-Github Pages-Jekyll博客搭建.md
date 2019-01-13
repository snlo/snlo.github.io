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

> 记录一些踩过的坑

### 简介

##### 为什么选择Github Pages？

- 免费，而且空间不限。
- 习惯了Git版本管理，可以直接在Github网页版上编辑和发布博客。

##### 为什么选择Jekyll？

- 被Github Pages推荐和默认支持的静态博客框架。

- 只关心`.md`的内容即可。简单不花哨，看它的<a href= "http://jekyllthemes.org/" target="_blank">官方主题</a>就知道。

### 项目环境

|  Name  | Version |                             Link                             |
| :----: | :-----: | :----------------------------------------------------------: |
|  Gem   | 2.5.2.3 | <a href= "https://gems.ruby-china.com" target="_blank">Sources</a> |
|  Ruby  |  2.3.7  | <a href= "https://www.ruby-lang.org/zh_cn/community/" target="_blank">Ruby社区</a> |
| Jekyll |  3.8.5  | <a href= "https://jekyllrb.com" target="_blank">Jekyllrb.com</a> |
| Gitalk |  1.4.1  | <a href= "https://gitalk.github.io" target="_blank">Github-gitalk</a> |

### Github Pages

怎么创建？其实很简单，就像新建Repositories一样，不同之处在于`Repository name`须命名为`user_name.github.io`的格式。其中`user_name`是指你Github的账户名，当然也可以不用这种命名格式。

- 若不是这是种命名格式，创建的Github Pages的访问地址'https://user_name.github.io/custom_repository_name/'。
- 若是这是种命名格式，创建的Github Pages的访问地址是'https://user_name.github.io'。

创建好后，找到Repository的`settings`选项，在设置中选择一个Jekyll主题（Github Pages推荐和支持的博客是Jekyll，所以可以在这里选择Jekyll主题）。再回到设置界面，此时可以看见你博客访问域名了。

![](https://snlo.app/img/blog_img/190101/1.jpg)

![](https://snlo.app/img/blog_img/190101/2.jpg)

![](https://snlo.app/img/blog_img/190101/3.jpg)

若需要为博客配置自己的域名，则需要再到设置界面修改`Custom domain`选项值。Github Pages会为你的域名自动分配SSL证书，以使得域名可以经`https://`进行访问，值得注意的是Github Pages不提供自定义上传SSL证书的服务，所以有三个选择：

- 要么严格按照<a href= "https://help.github.com/articles/securing-your-github-pages-site-with-https/" target="_blank">Github Help - Enforce HTTPS</a>的指南进行域名的解析。
- 要么找类似<a href= "https://dash.cloudflare.com/" target="_blank">Cloudflare</a>域名托管服务提供商进行网站的反向代理。
- 要么就这样子，以`http://`方式访问。

对于无法选中`Enforce HTTPS`选项的问题，强烈建议查看一下域名解析中是否已增加了一条为`letsencrypt.org 0 issue`的CAA记录，若没有则需要添加，关于这个问题只是针对已经颁发了SSL证书的域名。以下是Github技术支持的回复：

![](https://snlo.app/img/blog_img/190101/5.jpg)

### Jekyll

- plugins：-- jekyll-paginate
- theme：<a href= "http://jekyllthemes.org/themes/project-pages/" target="_blank">Project-pages</a>

我用的是macOS High Sierra，它自带ruby-gems。注意10以后的版本在更新Gem的时候，由于系统的保护机制，即使在root权限下也没有系统根目录的写入权限，需要重启进入恢复模式，在terminal终端中键入csrutil disable命令才能有权限。但我不建议这么做，我们不应该去随意更改系统的目录结构，只需要修改更新的路径就可以了，也就是在另外一个地方去做更新处理，比如`sudo gem install -n/usr/local/bin cocoapods`

具体的安装：

```shell
$ gem --version		#查看版本
$ gem source -l		#查看源
*** CURRENT SOURCES ***

https://gems.ruby-china.com
#若url不是'https://gems.ruby-china.com'，则需要修改source的url为'https://gems.ruby-china.com'
$ gem sources -r url		#移除
$ gem sources -a new_url	#添加
$ gem sources -u			#更新源缓存

$ sudo gem install bundler		#安装'bundler'，一个很好的管理ruby项目gems的工具
#Password:
#Fetching: bundler-2.0.1.gem (100%)
#ERROR:  While executing gem ... (Gem::FilePermissionError)
#    You don't have write permissions for the /usr/bin directory.
#哦不，它报错了，没有写入权限，即使使用的是sudo,上面已经阐述了原因和解决方法
$ sudo gem install -n/usr/local/bin bundler 	#重新安装'bundler'

$ sudo gem instll -n/usr/local/bin jekyll 	#安装Jekyll
$ jekyll new user_blog		#新建名为'user_blog'的Jekyll博客项目
$ cd /users/mac_name/user_blog 	#cd到你刚刚新建的'user_blog'项目
$ bundle bundle exec jekyll serve	#本地启动Jekyll博客项目，也可以使用'jekyll serve'命令
#    Server address: http://127.0.0.1:4000/
#  Server running... press ctrl-c to stop.
#浏览器打开'http://127.0.0.1:4000/'便可实时预览博客效果
```

新版本的Jekyll在新建博客项目后，项目目录中没有`_includes/`、`_layouts/`... …。多了`Gemfile`，官方的解释是减掉了不必要的功能，让其更加的精简。如果需要的话需要在`Gemfile`添加，比如我的项目中需要用到分页的功能，它不再被Jekyll支持，而是以插件`jekyll-paginate`的形式存在。所以需要在`Gemfile`中添加：

```yaml
group :jekyll_plugins do
  gem 'jekyll-paginate'
  gem 'jekyll-sitemap'
end
```

然后在终端中输入以下命令更新：

```shell
$ bundle install
```

百度上的关于Jekyll目录的展示已经不再是`jekyll new ...`生成的了，像我这种非WEB前端人（我只是APP工程师）就只好到Github上寻找优秀的开源博客项目，然后Fork下来自己修改修改，然后感谢感谢贡献者，然后你也可以这样。并且我觉得Jekyll博客就像他们说的那样，应该简单纯粹一点，不需要太华丽，毕竟我们还是要多点花心思在写有高质量的文章这件事情上。

最后把本地修改好的博客项目push到你的Github Pages上就OK。

### Gitalk

要在你博客项目中集成Gitalk这么优秀的评论系统，首先需要到Github注册OAuth Apps。路径为Settings -> Developer settings -> OAuth Apps -> Register a new application:

![](https://snlo.app/img/blog_img/190101/6.jpg)

![](https://snlo.app/img/blog_img/190101/7.jpg)

要特别注意的是`Homepage URL`与`Authorization callback URL`需要与你的博客域名地址保持一致，否则无法与Gitalk进行回调

![](https://snlo.app/img/blog_img/190101/8.jpg)

以下是注册OAuth Apps生成的`clientID`、 `clientSecret`

![](https://snlo.app/img/blog_img/190101/9.jpg)

然后在博客目录下的`_config.yml`中配置：

```yaml
# Gitalk
gitalk: 
  enable: true    #是否开启Gitalk评论
  clientID: db0469bd2e8a5c7de54                            #生成的clientID
  clientSecret: 62b65779044955f7d44eac6022fd5b9b8a92f8c7    #生成的clientSecret
  repo: user_name-issues    #仓库名称
  owner: user_name    #github用户名
  admin: user_name
  distractionFreeMode: false #是否启用类似FB的阴影遮罩

```

此时只剩最后一步，就可以在每篇博客中自动生成Issues了。在你的博客目录`_layouts/post.html`中加入以下代码：

```html
<!--Gitalk评论start  -->
{% if site.gitalk.enable %}
<!-- 引入Gitalk评论插件  -->
<link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
    <script src="https://unpkg.com/gitalk@latest/dist/gitalk.min.js"></script>
    <div id="gitalk-container"></div>
    <!-- 引入一个生产md5的js，用于对id值进行处理，防止其过长 -->
    <!-- Thank DF:https://github.com/NSDingFan/NSDingFan.github.io/issues/3#issuecomment-407496538 -->
    <script src="{{ site.baseurl }}/js/md5.min.js"></script>
    <script type="text/javascript">
        var gitalk = new Gitalk({
        clientID: '{{site.gitalk.clientID}}',
        clientSecret: '{{site.gitalk.clientSecret}}',
        repo: '{{site.gitalk.repo}}',
        owner: '{{site.gitalk.owner}}',
        admin: ['{{site.gitalk.admin}}'],
        distractionFreeMode: {{site.gitalk.distractionFreeMode}},
        id: md5(location.pathname),
        });
        gitalk.render('gitalk-container');
    </script>
{% endif %}
<!-- Gitalk end -->
```

注意是自动生成Issues的，相对来说比较麻烦的是在首次生成的时候，需要博主的Github账号在该博客文章中去登录Gitalk，以此才能到达自动生成Issues的效果。有朋友说写个脚本去自动遍历生成Issues，就不用每次去登录账号了，这样当然是非常不错的做法，只是我觉得在每次写完每篇博客的时候都需要去审查刚刚写的文章，这时候顺便登录一下又何妨呢？不至于自己写的自己都不看吧？当然，要是Gitalk评论功能是在你博客项目后续才集成的，那就宁当别论了。

### 参考

<a href= "http://www.bootcss.com" target="_blank">Bootstrap</a> 、<a href= "https://github.com/ahmetcecen" target="_blank">Ahmet Cecen</a>

