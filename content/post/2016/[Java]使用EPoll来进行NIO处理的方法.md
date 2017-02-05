---
title: "[Java]使用EPoll来进行NIO处理的方法"
date: "2012-01-05T23:20:41+08:00"
categories:
- Java
tags:
- JNI
- Epoll
- JVM
---

JDK 6.0 以及JDK 5.0 update 9 的 nio支持epoll （仅限 Linux 系统 ），对并发idle connection会有大幅度的性能提升，这就是很多网络服务器应用程序需要的。

启用的方法如下：

    -Djava.nio.channels.spi.SelectorProvider=sun.nio.ch.EPollSelectorProvider


例如在 Linux 下运行的 Tomcat 使用 NIO Connector ，那么启用 epoll 对性能的提升会有帮助。

而 Tomcat 要启用这个选项的做法是在 catalina.sh 的开头加入下面这一行

    CATALINA_OPTS='-Djava.nio.channels.spi.SelectorProvider=sun.nio.ch.EPollSelectorProvider'