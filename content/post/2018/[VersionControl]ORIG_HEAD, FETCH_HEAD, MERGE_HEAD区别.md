+++
title= "[VersionControl]ORIG_HEAD, FETCH_HEAD, MERGE_HEAD区别"
date= "2018-06-28T17:08:02+08:00"
categories= ["VersionControl"]
tags= ["Git"]
+++

区别：

+ `HEAD`: The current ref that you’re looking at. In most cases it’s probably refs/heads/master

+ `FETCH_HEAD`: The SHAs of branch/remote heads that were updated during the last git fetch

+ `ORIG_HEAD`: When doing a merge, this is the SHA of the branch you’re merging into.

+ `MERGE_HEAD`: When doing a merge, this is the SHA of the branch you’re merging from.

+ `CHERRY_PICK_HEAD`: When doing a cherry-pick, this is the SHA of the commit which you are cherry-picking.

The complete list of these refs can be found by cloning git sources。

clone一个仓库后，可以在.git文件夹内找到 HEAD、FETCH_HEAD、MERGE_HEAD 等文件。


参考自：ORIG_HEAD, FETCH_HEAD, MERGE_HEAD etc  
https://stackoverflow.com/questions/17595524/orig-head-fetch-head-merge-head-etc/17596265	

***
`如果有来生，要做一只鸟，飞越永恒，没有迷途的苦恼。东方有火红的希望，南方有温暖的巢床，向西逐退残阳，向北唤醒芬芳。`