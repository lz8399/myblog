+++
title= "[MacOS]通过 U 盘启动重装 macOS 系统"
date= "2018-01-23T20:35:02+08:00"
categories= ["MacOS"]
tags= ["MacOS"]
keywords= ["Mac", "Install"]
+++


重装系统是工作和生活中经常需要做的事情，作为一名开发人员，学会该技能你才是一名合格的程序猿！以后再也不会遇到“程旭元你会装系统吗？”的尴尬了！本文主要介绍怎样通过U盘启动重新安装 macOS 系统，以安装当前最新的 macOS Sierra 10.12 为例。

##### 一、准备工作
1. 准备一个 8G 或以上的U盘，请备份U盘里面的数据，后面的操作会抹掉U盘中的数据；

2. 在 AppStore 中下载 macOS Sierra 安装包；或者通过其他途径下载，拖动至自己的应用程序（Applications）文件夹。

##### 二、格式化U盘
1. 插入U盘，前往「应用程序」->「实用工具」里面找到并打开「磁盘工具」； 

2. 在左方列表中找到 U 盘的名称并点击

3. 右边顶部选择「分区」，然后在「分区布局」选择「1个分区」 

4. 在分区信息中的 「名称」输入「myl」 (由于后面的命令中会用到此名称，如果你要修改成其它名称，请务必对应修改后面的命令) 

5. 在「格式」中选择 「Mac OS 扩展 (日志式)」 

6. 这时，先别急着点“应用”，还要先在 「选项」里面，选择「GUID 分区表」 

7. 开始格式化

##### 三、制作启动盘
1. 在「应用程序」->「实用工具」里面找到「终端」并打开； 

2. 复制下面的命令，并粘贴到「终端」里，按回车运行

	$ sudo /Applications/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/myl --applicationpath /Applications/Install\ macOS\ Sierra.app --nointeraction

回车后，系统会提示你输入管理员密码，接下来就是等待系统开始制作启动盘了。这时，命令执行中你会陆续看到类似以下的信息：

	WARNING: Improper use of the sudo command could lead to data loss
	or the deletion of important system files. Please double-check your
	typing when using sudo. Type "man sudo" for more information.

	To proceed, enter your password, or type Ctrl-C to abort.

	Password:
	Erasing Disk: 0%... 10%... 20%... 30%...100%...
	Copying installer files to disk...
	Copy complete.
	Making disk bootable...
	Copying boot files...
	Copy complete.
	Done.
	
等待命令运行完成并显示「Done.」，此时系统启动盘制作完毕！

##### 四、U盘启动安装 macOS Sierra
当你插入制作完成的 macOS Sierra U盘启动盘之后，桌面出现「Install macOS Sierra」的盘符那么就表示启动盘是正常的了。那么怎样通过 USB 启动进行全新的系统安装呢？

其实很简单，步骤如下

1. 重启 Mac，听到开机启动音之后按下 option 键，在磁盘选择界面选择 U 盘启动，按回车确认 

2. 这时选择 U 盘的图标回车，即可通过 U 盘来安装 macOS Sierra 了！你可以直接覆盖安装系统(升级)，也可以在磁盘工具里面格式化抹掉整个硬盘，或者重新分区等实现全新的干净的安装。

