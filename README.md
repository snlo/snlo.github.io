# SNLO BIOG

#### <a href= "https://snlo.app" target="_blank">查看snlo`blog →</a>

## 以简单的方式添加资源

该网站使用名为Jekyll的模板系统生成的静态HTML文件，并且可以轻松的完成网站的部署工作。GitHub与Jekyll很好地配合，允许您使用Web界面添加和编辑文件。所以不需要下载任何东西，你可以直接在GitHub上的存储库中完成。

首先需要确定的是，网站导航栏上要展示什么内容，主页、关于、归档还是项目。

只需要担心的唯一的文件夹是：

- _posts

因为它是存放网站内容的地方。

## 怎么构建

如果现在本机上运行这个repo，需要设置Jekyll。

要安装Jekyll，请打开命令行并键入...

```sh
$ gem install jekyll
```

... 然后 ...

```sh
$ cd ~/repo
$ jekyll serve 
```

关于详细的构建请参考：<a href= "https://snlo.app/2018/12/31/Github-Pages-Jekyll%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA/" target="_blank">Github Pages+Jekyll博客搭建</a>。