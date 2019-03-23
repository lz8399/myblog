+++
title= "[VersionControl]git push error - Out of memory loading unknown object"
date= "2019-03-01T20:00:02+08:00"
categories= ["VersionControl"]
tags= ["git"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-008.jpg"
+++

Keywords: git

<!--more-->

git push receive error:

	POST git-receive-pack (chunked)
	error: unpack failed: error Out of memory loading unknown object

Solution  
Increase heap size using `-Xmx` option.

Reference  
https://github.com/gitbucket/gitbucket/issues/1541

***
`一个人在他的信仰上站得越不牢固，他就越要用双臂紧紧抱住那些使之区分于其他信仰的教条不放；相反，一个人在他的信念上站得越牢固，他就越可以自由地把双手伸向那些与他信仰不同的人。——弗兰克` 
