+++
title= "[hugo]集成Highlight.js"
date= "2018-01-31T15:29:40+08:00"
categories= ["Web"]
tags= ["Hugo", "Blog", "Highlight.js"]
+++

1，在config.toml中开启highlight.js

    [params]
        syntaxHighlighter = "highlight.js"
             
2，在theme的./layouts/partials或者./layouts/chrome/目录下，找到header.html或者header.includes.html文件，然后再在\<header>标签内添加cdn地址：

    <link rel="stylesheet"
      href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.12.0/styles/default.min.css">
    <script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.12.0/highlight.min.js"></script>
    <script>hljs.initHighlightingOnLoad();</script>
    
highlight.js的最新cdn地址获取  
https://highlightjs.org/download/

如果要修改style，直接修改default.min.css的名字，比如想使用vs风格，那么就将

    href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.12.0/styles/default.min.css"
    
修改为

    href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.12.0/styles/vs.min.css"
    
这样hugo文章模板中的所有代码都会统一替换为highlight.js风格，不用在修改原有的.md文件。
    
##### highlight.js style演示合集
https://highlightjs.org/static/demo/
  
##### Hugo highlight语法：Syntax Highlighting
https://bwaycer.github.io/hugo_tutorial.hugo/extras/highlighting/#highlight-js-example