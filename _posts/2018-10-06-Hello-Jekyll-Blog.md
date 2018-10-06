---
layout:     post
title:      "Hello 2018"
subtitle:   "Hello World, Hello Jekyll Blog，Win 10下搭建 Jekyll 博客"
date:       2018-10-05 12:00:00
author:     "丢手圈啊"
header-img: "img/post-bg-hello-2018.jpg"
catalog: true
tags:
    - 生活
---

> *第一个博客终于搭建好了。*
>
> *本来计划在 8 月搭建完成的，中间一直有事，终于在这个国庆，把这个博客搭建好了。现在回想整个
> 搭建博客过程，其实不难，甚至一小时就能完成，但是由于第一次接触Git，第一次使用GitHub 
> ，中间遇到了好多坑，尤其是在浪费了好多时间在代码同步这个步骤，折腾了半天时间。*
>
> *下面开始对今天这次博客搭建做一个回顾，也希望可以帮助到大家。*



# 一、环境搭建

*首先安装  Jekyll 所需要的基础环境。分别安装 Ruby，RubyDevKit，Git*



## 1. 安装 Ruby

Jekyll是用ruby语言编写的，所以我们首先要在windows上装好ruby环境。

1. 下载 [RubyInstaller](http://rubyinstaller.org/downloads/)，选择合适版本，注意自己电脑是 64 位，还是 32 位。

2.  安装Ruby，记得要勾选  `Add Ruby executables to your PATH`，其作用是绑定ruby环境变量，另外安装目录不可以包含空格。

3. 下载 DevKit：与 RubyInstller 同一链接，页面稍下方有 “DEVELOPMENT KIT”，注意 DevKit 版本要与上面的ruby版本是匹配的，64 位或 32 位。

4. 安装DevKit：解压 DevKit 完成后打开 CMD 窗口，回到 Devkit 根目录，输入：
```
ruby dk.rb init
ruby dk.rb install
```



## 2. 安装 Git

> *如果之前已经安装过 Git，可以忽略这一步*

1. 下载 [Git](https://git-scm.com/) ,选择合适版本 64 或 32 位。

2. 安装 Git，可以自定义路径，但是路径名称不要有中文。



## 3. 安装 Jekyll

以下几个步骤都是在 CMD 窗口下。

1. 更换源
Win 10 打开 CMD 窗口
```
    无翻墙软件，可使用国内淘宝提供的源
            gem sources --remove https://rubygems.org/
            gem sources -a https://ruby.taobao.org/
            gem sources -l

    有翻墙软件，可以使用如下源
            gem sources --remove https://rubygems.org/
            gem sources -a  http://rubygems.org/
```

2. 安装 Jekyll
```
    gem install jekyll
```

因为是联网安装，所以可能时间比较常，耐心等待，直至 Jekyll 安装全部完成。

3. 安装 paginate
```
    gem install jekyll-paginate
```

并在 _config.yml 中加入一句 `gems: [jekyll-paginate]`



# 二、使用 Jekyll

> Jekyll 是一个免费的简单静态网页生成工具，可以配合第三方服务例如： Disqus（评论）、多说(评论) 以及分享 等等扩展功能，Jekyll 可以直接部署在 Github（国外） 或 Coding（国内） 上，可以绑定自己的域名。



## 1. clone Github 博客

```
方法一：https方法，通过直接输入账号密码的格式提交代码
    git clone https://github.com/[username]/[username].github.io.git

方法二：ssh的方法，需要提前配置SSH，之后可直接push代码。
    git clone git@github.com:[username]/[username].github.io.git

ps：username 是你的 GitHub 名称
```



## 2. 启动 Jekyll 服务

在 CMD 窗口下，输入以下代码
```
    cd xxxx.github.io.git
    jekyll serve --watch
```

然后浏览这个 [http://localhost:4000/index.html](http://localhost:4000/index.html)网址，就可以看到你的博客效果了。

**注意事项**：提交文章时时间非常重要的，提交文章的时间最好比当前时间早一段时间，时差问题，可能会导致文章提交失败。



# 三、提交文章

> 以下命令在 CMD 下面输入



## 1. 配置 Git 用户名和邮箱

```
$ git config --global user.name "{username}"     //用户名替换{username}
$ git config --global user.email "{email}"    //邮箱替换{email}
```



## 2. 配置 SSH

```
$ ssh-keygen -t rsa -C"{email}"    //邮箱替换{email}
```

一路回车到命令完成。Win 10系统默认在文件夹 `C:\Users\{你的用户名}\.ssh`，该文件夹有`id_rsa`（私钥） 和 `id_rsa.pub`（公钥） 两个文件。

将`id_rsa.pub`内容复制到自己的Github主页的`Settings -> SSH keys`，添加完毕即可。



## 3. 提交

```
$ cd {username.github.io}
$ git init
$ git add .
$ git commit -m "message"
$ git push origin master
```

最后一步如果遇到错误，可以尝试换成
```
$ git push origin master --force
```



# 参考的相关链接

1. [Windows下搭建本地Jekyll](http://gityuan.com/2015/06/07/build-jekyll/)
2. [Windows下使用Jekyll搭建个人博客](https://nilzzzz.github.io/2017/03/jekyll_tutorials1/)
3. [Hux Blog](https://github.com/Huxpro/huxpro.github.io)



---
欢迎关注微信公众号：**丢手圈啊**
---