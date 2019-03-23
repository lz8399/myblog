+++
title= "[VersionControl]git push error-Java heap space"
date= "2019-03-23T17:53:02+08:00"
categories= ["VersionControl"]
tags= ["Git"]
thumbnailImage= "/thumbnail/cover-Tso Moriri Lake.jpg"
autoThumbnailImage= "true"
thumbnailImagePosition= "top"
+++

Keywords: Git

<!--more-->

git push receive error:

	Counting objects: 108, done.
	Delta compression using up to 8 threads.
	Compressing objects: 100% (93/93), done.
	POST git-receive-pack (chunked)
	Writing objects: 100% (108/108), 561.41 MiB | 4.91 MiB/s, done.
	Total 108 (delta 51), reused 0 (delta 0)
	error: unpack failed: error Java heap space
	To https://repo_address
	! [remote rejected] dev -> dev (n/a (unpacker error))
	error: failed to push some refs to 'https://repo_address'

Solution  
modify JVM arguments:

	-Dsun.io.useCanonCaches=false -Djava.awt.headless=true -Djna.nosys=true -Dsvnkit.http.methods=Digest,Basic,NTLM,Negotiate -Xmx512m

Reference  
https://stackoverflow.com/questions/52821194/subgit-java-heap-space

***
`真正有血性的人，绝不曲意求得别人重视，也不怕别人忽视。──乔治·戈登·拜伦（George Gordon Byron)` 
