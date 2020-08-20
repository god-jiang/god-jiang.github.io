---
title: hexo博客搭建gitalk
date: 2019-12-31 13:50:31
tags: 
categories: hexo优化
---

## 背景

> 2019年1月份的时候就开始搭建了我的第一个博客hexo，部署到了Github Page上，也陆陆续续更新了一些大学时期学习的数据结构和算法内容，然后加了阅读量和访问量，后面发现没有评论系统的博客有点low的感觉，看了很多的评论系统，这里就不一一列举了，最后使用的是Gittalk评论系统。接下来就来介绍hexo集成Gittalk评论系统的全部过程。

<!--more-->

## 关于Gitalk

> Gitalk是一个基于Github Issue和Preact开发的评论插件。使用Github账号登录，界面干净整洁，主要还是Gitalk支持MarkDown语法。（**写过博客的都知道MarkDown好用**）

------



## 集成Gitalk

### 建立评论仓库

1. 可以在你的个人Github上重新创建一个仓库来专门存放你的评论信息
2. 可以直接使用你的hexo在Github上的仓库地址来存放你的评论信息，信息会放进你仓库里面的issue

### 新建一个OAuth App

​	地址：[https://github.com/settings/applications/new](https://github.com/settings/applications/new)

![](/images/新建OAuth App.png)

![](/images/OAuth说明.png)

**填完以上的信息会生成一个Client ID和一个Client Secret，等下的配置会用到这两个信息**

![](/images/生成OAuth.png)

### 更改配置文件

1. 新建`/layout/_third-party/comments/gitalk.swig`文件，并添加内容：

```
    {% if page.comments && theme.gitalk.enable %}
      <link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
      <script src="https://unpkg.com/gitalk/dist/gitalk.min.js"></script>
       <script type="text/javascript">
            var gitalk = new Gitalk({
              clientID: '{{ theme.gitalk.ClientID }}',
              clientSecret: '{{ theme.gitalk.ClientSecret }}',
              repo: '{{ theme.gitalk.repo }}',
              owner: '{{ theme.gitalk.githubID }}',
              admin: ['{{ theme.gitalk.adminUser }}'],
              id: location.pathname,
              distractionFreeMode: '{{ theme.gitalk.distractionFreeMode }}'
            })
            gitalk.render('gitalk-container')           
           </script>
    {% endif %}
```

2. 修改`/layout/_partials/comments.swig`，添加内容如下，与前面的`elseif`同一级别上：

```
    {% elseif theme.gitalk.enable %}
     <div id="gitalk-container"></div>
```

3. 修改`layout/_third-party/comments/index.swig`，在最后一行添加内容：

```
    {% include 'gitalk.swig' %}
```

4. 新建`/source/css/_common/components/third-party/gitalk.styl`文件，添加内容：

```
    .gt-header a, .gt-comments a, .gt-popup a
      border-bottom: none;
    .gt-container .gt-popup .gt-action.is--active:before
      top: 0.7em;
```

5. 修改`/source/css/_common/components/third-party/third-party.styl`，在最后一行上添加内容，引入样式：

```
    @import "gitalk";
```

6. 在主题配置文件`next/_config.yml`中添加如下内容：

```
    gitalk:
      enable: true
      githubID: github帐号  # 例：god-jiang   
      repo: 仓库名称   # 例：god-jiang.github.io
      ClientID: Client ID
      ClientSecret: Client Secret
      adminUser: github帐号 #指定可初始化评论账户
      distractionFreeMode: true
```

**以上就是next主题中添加Gitalk评论的配置，博客上传到Github上后，打开某一篇文章就可以看到评论了。**

------



## 搭建完成效果

![](/images/评论效果图.png)



## 其他

> 到这里就已经是大功告成了，当你用github账号登录，第一次加载会比较慢，因为第一次加载会自动在你的仓库下创建相对应的issue。



## 参考文献

- https://segmentfault.com/a/1190000014085547
- https://blog.csdn.net/qq_35076330/article/details/99968291
- https://asdfv1929.github.io/2018/01/20/gitalk/