---
title: "Github Pages搭建个人博客"
date: "2016-12-16T18:44:02+08:00"
categories:
- Web
tags:
- Github
- Blog
---


1，创建GitHub Pages的步骤：
https://pages.github.com/
创建好以后就可以将静态博客的文件提交到这个仓库的根目录下，比如hugo的public目录下的文件。
{{< figure src="/img/20161216-Github Pages搭建个人博客/Github Pages搭建个人博客-01.jpg">}}

2，打开刚刚创建的仓库，点击settings
{{< figure src="/img/20161216-Github Pages搭建个人博客/Github Pages搭建个人博客-02.jpg">}}
修改Custom domain，改成自己的域名即可：
{{< figure src="/img/20161216-Github Pages搭建个人博客/Github Pages搭建个人博客-03.jpg">}}
点击save之后，仓库根目录下就会多出一个CNAMe文件。里面内容就是刚刚设置的域名。

3，在自己购买的域名服务平台上设置后DNS。DNS的IP可以通过ping pages.github.com获得。
{{< figure src="/img/20161216-Github Pages搭建个人博客/Github Pages搭建个人博客-04.jpg">}}
{{< figure src="/img/20161216-Github Pages搭建个人博客/Github Pages搭建个人博客-05.jpg">}}


