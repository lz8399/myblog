+++
title= "[VersionControl]Install Windows Service for SVN"
date= "2019-01-20T23:58:02+08:00"
categories= ["VersionControl"]
tags= ["SVN"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-009.jpg"
+++

Keywords: SVN, Windows Services, CMD

<!--more-->

CMD

	sc create svnservice binpath= "E:\TortoiseSVN\bin\svnserve.exe --service -r E:\svn_repos\myrep" displayname= "SVNService" depend= Tcpip

***
`如果有来生，要做一棵树，站成永恒，没有悲伤的姿势：一半在尘土里安详，一半在空中飞扬；一半散落阴凉，一半沐浴阳光。非常沉默非常骄傲，从不依靠从不寻找。——三毛` 
