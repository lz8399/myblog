---
title: "[hugo]快速搭建步骤"
date: "2016-11-27T22:50:40+08:00"
categories:
- Web
tags:
- Hugo
- Blog
---

1，新建文章：

    hugo new 章节名称/文章名称.md

2，生成HTML、js等静态web文件：

    hugo -v
    
这里-v是--verbose的缩写，只是打印信息。

注意，文章有个属性draft=true，表示当前文章为草稿，默认构建是不会为草稿生成html文件发的。如果生成时希望把草稿也生成出来，需要使用参数：--buildDrafts，例如：

    hugo --buildDrafts

3，启动http服务器（测试用），3中方式：

    hugo server
    hugo server --buildDrafts
    hugo server --theme=hugo_theme_robust --buildDrafts

或者执行完第2步之后，将publish目录下的所有文件拷贝到web服务器的相应目录下，比如nginx/html/

