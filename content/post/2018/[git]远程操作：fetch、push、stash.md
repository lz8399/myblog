+++
title= "[git]远程操作：fetch、push、stash"
date= "2018-06-15T19:39:40+08:00"
categories= ["VersionControl"]
tags= ["Git"]
+++

相关参考：  
https://www.jianshu.com/p/e78b28081a44  
https://stackoverflow.com/questions/9237348/what-does-fetch-head-in-git-mean  
https://ruby-china.org/topics/4768  

##### git clone

git clone支持多种协议，除了HTTP(s)以外，还支持SSH、Git、本地文件协议等，通常来说，Git协议下载速度最快，SSH协议用于需要用户认证的场合。在clone完成之后，Git 会自动为你将此远程仓库命名为origin（origin只相当于一个别名，运行git remote –v或者查看.git/config可以看到origin的含义），并下载其中所有的数据，建立一个指向它的master 分支的指针，我们用(远程仓库名)/(分支名) 这样的形式表示远程分支，所以origin/master指向的是一个remote branch（从那个branch我们clone数据到本地），但你无法在本地更改其数据。同时，Git 会建立一个属于你自己的本地master 分支，它指向的是你刚刚从remote server传到你本地的副本。随着你不断的改动文件，git add, git commit，master的指向会自动移动，你也可以通过merge（fast forward）来移动master的指向。

    git clone + 远程仓库项目网址

克隆远程仓库项目到本地仓库，也就是俗称的拉代码，本地仓库生成的项目与远程仓库的项目结构一致。git clone + 远程仓库项目网址 + 本地仓库项目目录：克隆远程仓库项目到本地仓库，本地仓库生成的项目放在第二个参数【本地仓库项目目录】中

##### git fetch

真正理解 git fetch, git pull，要讲清楚git fetch，git pull,必须要附加讲清楚git remote，git merge 、远程repo， branch 、 commit-id 以及 FETCH_HEAD。

+ `git remote`  
首先， git是一个分布式的结构，这意味着本地和远程是一个相对的名称。  
本地的repo仓库要与远程的repo配合完成版本对应必须要有 git remote子命令，通过git remote add来添加当前本地长度的远程repo， 有了这个动作本地的repo就知道了当遇到git push 的时候应该往哪里提交代码。

+ `git branch`  
其次，git天生就是为了多版本分支管理而创造的，因此分支一说，不得不提， 分支就相当于是为了单独记录软件的某一个发布版本而存在的，既然git是分布式的，便有了本地分支和远程分支一说，git branch 可以查看本地分支， git branch -r  可以用来查看远程分支。 本地分支和远程分支在git push 的时候可以随意指定，交错对应，只要不出现版本从图即可。

+ `git merge`  
再者，git的分布式结构也非常适合多人合作开发不同的功能模块，此时如果每个人都在其各自的分支上开发一个相对独立的模块的话，在每次release制作时都需先将各成员的模块做一个合并操作，用于合并各成员的工作成果，完成集成。 此时需要的就是git merge.

+ `git push`和`commit-id`  
在每次本地工作完成后，都会做一个git commit 操作来保存当前工作到本地的repo， 此时会产生一个commit-id，这是一个能唯一标识一个版本的序列号。 在使用git push后，这个序列号还会同步到远程repo。

在理解了以上git要素之后，分析git fetch 和 git pull 就不再困难了。 

 

首先，git fetch 有四种基本用法：

+ `git fetch`  
这将更新git remote 中所有的远程repo 所包含分支的最新commit-id, 将其记录到.git/FETCH_HEAD文件中。今天从数据库git fetch 下（本地和远程版本库只有master分支），本地切换到master分支，然后git merge 不了，使用git merge FETCH_HEAD ,ok了

+ `git fetch remote_repo`  
这将更新名称为remote_repo 的远程repo上的所有branch的最新commit-id，将其记录。 

+ `git fetch remote_repo remote_branch_name`  
这将这将更新名称为remote_repo 的远程repo上的分支： remote_branch_name

+ `git fetch remote_repo remote_branch_name:local_branch_name`  
这将这将更新名称为remote_repo 的远程repo上的分支： remote_branch_name ，并在本地创建local_branch_name 本地分支保存远端分支的所有数据。

##### git pull 的运行过程

`git pull`等价与：`git fetch`当前指向的远程分支的数据，然后再将其与本地的当前分支合并。

##### git push

    git push origin 本地分支A : 远程分支B 

push 本地分支A到远程库origin的分支B HEAD指向当前工作的branch，master不一定指向当前工作的branch可以发现，master就是local branch，origin/master是remote branch$git diff origin/master master （show me the changes between the remote master branch and my master branch).需要注意的是，remotes/origin/master和origin/master的指向是相同的$git diff origin/master remotes/origin/master git push origin masterorigin指定了你要push到哪个remotemaster其实是一个“refspec”，正常的“refspec”的形式为”+:”，冒号前表示local branch的名字，冒号后表示remote repository下 branch的名字。注意，如果你省略了，git就认为你想push到remote repository下和local branch相同名字的branch。听起来有点拗口，再解释下，push是怎么个push法，就是把本地branch指向的commit push到remote repository下的branchgit push origin master:master (在local repository中找到名字为master的branch，使用它去更新remote repository下名字为master的branch，如果remote repository下不存在名字是master的branch，那么新建一个，如果存在则报错)git push origin master：（省略了，等价于“git push origin master:master”）

    git push origin master:refs/for/mybranch ：

(在local repository中找到名字为master的branch，用他去更新remote repository下面名字为mybranch的branch)

    git push origin HEAD:refs/for/mybranch ：

（HEAD指向当前工作的branch，master不一定指向当前工作的branch，所以我觉得用HEAD还比master好些）

    git push origin:mybranch ：

（再origin repository里面查找mybranch，删除它。用一个空的去更新它，就相当于删除了）


##### git stash

git栈，在切换分支的时候，当前分支有未完成提交的代码，但又不想提交，一方面是因为代码没有完成，一方面是因为这样会在log中打印许多无用的日志信息。但是不提交就无法切换分支，于是git便开辟出来一个临时的仓库，这个仓库可以暂时存放最新修改过的代码。git栈，可以存放多次修改，切换分支后这些存放的修改还在。

    git stash

保存当前的工作进度,会分别对暂存区和工作区的状态进行保存。保存后工作区恢复到之前最后一次提交的状态

    git stash list

显示进度列表。此命令显然显示了git stash 可以多次保存工作进度，并在恢复时候选择。

    git stash pop [--index] []

如果不使用任何参数，会恢复最新保存的工作进度，并将恢复的工作进度从存储的git栈列表中清除。

如果提供参数（来自git stash list显示的列表），则将工作进度恢复。恢复完毕也将从git栈删除工作进度。

    git stash [save [--patch] [-k|--[no]keep-index] [-q|--quiet] []]

这条命令实际上是第一条git stash命令的完整版。

使用参数--patch会显示工作区和HEAD的差异，通过对差异文件的编辑决定在进度中最终要保存的工作区的内容，通过编辑差异文件可以在进度中排除无关内容。

使用-k或者--keep-index参数，在保存进度后不会将暂存区重置。默认会将暂存区和工作区强制重置。

    git stash apply [--index] []

除了不删除恢复的进度之外，其余和git stash pop 命令一样。

    git stash drop []

删除一个存储的进度。默认删除最新的进度。

    git stash clear

删除所有存储的进度。
