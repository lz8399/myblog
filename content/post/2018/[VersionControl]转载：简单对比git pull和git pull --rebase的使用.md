+++
title= "[VersionControl]转载：简单对比git pull和git pull --rebase的使用"
date= "2018-11-06T21:13:02+08:00"
categories= ["VersionControl"]
tags= ["Git"]
+++

原文：https://www.cnblogs.com/kevingrace/p/5896706.html

使用下面的关系区别这两个操作：  
{{< hl-text green >}}git pull = git fetch + git merge{{< /hl-text >}}  
{{< hl-text green >}}git pull --rebase = git fetch + git rebase{{< /hl-text >}}


现在来看看git merge和git rebase的区别。

假设有3次提交A,B,C。
{{< figure src="/img/20181106-[VersionControl]转载：简单对比git pull和git pull --rebase的使用/[VersionControl]转载：简单对比git pull和git pull --rebase的使用-01.png">}}


在远程分支origin的基础上创建一个名为"mywork"的分支并提交了，同时有其他人在"origin"上做了一些修改并提交了。
{{< figure src="/img/20181106-[VersionControl]转载：简单对比git pull和git pull --rebase的使用/[VersionControl]转载：简单对比git pull和git pull --rebase的使用-02.png">}}

其实这个时候E不应该提交，因为提交后会发生冲突。如何解决这些冲突呢？有以下两种方法：

1. **git merge**  
用git pull命令把"origin"分支上的修改pull下来与本地提交合并（merge）成版本M，但这样会形成图中的菱形，让人很困惑。
{{< figure src="/img/20181106-[VersionControl]转载：简单对比git pull和git pull --rebase的使用/[VersionControl]转载：简单对比git pull和git pull --rebase的使用-03.png">}}
2. **git rebase**  
创建一个新的提交R，R的文件内容和上面M的一样，但我们将E提交废除，当它不存在（图中用虚线表示）。由于这种删除，小李不应该push其他的repository.rebase的好处是避免了菱形的产生，保持提交曲线为直线，让大家易于理解。
{{< figure src="/img/20181106-[VersionControl]转载：简单对比git pull和git pull --rebase的使用/[VersionControl]转载：简单对比git pull和git pull --rebase的使用-04.png">}}

在rebase的过程中，有时也会有conflict，这时Git会停止rebase并让用户去解决冲突，解决完冲突后，用git add命令去更新这些内容，然后不用执行git-commit,直接执行git rebase --continue,这样git会继续apply余下的补丁。
在任何时候，都可以用git rebase --abort参数来终止rebase的行动，并且mywork分支会回到rebase开始前的状态。

***
`不能忍受无聊的一代人，将是平庸的一代人。不能忍耐无聊，生活就会变成持续的对无聊的逃离。`──罗素（Rusell）