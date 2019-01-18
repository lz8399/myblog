+++
title= "Steamworks后台配置相关"
date= "2018-09-04T18:24:02+08:00"
categories= ["Steam"]
tags= ["Steamworks"]
keywords= ["Steamworks"]
+++

### 如何修改SteamWorks中游戏名称

改名需要改两个地方：一个是Application Name，一个是Package Name。

##### 修改Application Name
先打开SteamWork首页，点击App名称，进入App Admin页面
{{< figure src="/img/20180904-Steamworks后台配置相关/Steamworks后台配置相关-01.jpg">}}

然后点击“Edit Steamworks Settings”
{{< figure src="/img/20180904-Steamworks后台配置相关/Steamworks后台配置相关-02.jpg">}}

然后修改Application Name，并点击Save
{{< figure src="/img/20180904-Steamworks后台配置相关/Steamworks后台配置相关-03.jpg">}}

##### 修改Package Name
先打开SteamWork首页，点击App名称，进入App Admin页面
{{< figure src="/img/20180904-Steamworks后台配置相关/Steamworks后台配置相关-04.jpg">}}

然后点击Package Title
{{< figure src="/img/20180904-Steamworks后台配置相关/Steamworks后台配置相关-05.jpg">}}

然后点击Edit package name。
{{< figure src="/img/20180904-Steamworks后台配置相关/Steamworks后台配置相关-06.jpg">}}

### 游戏包体构建与上传（SteamPipe Depot & Build）
1，将游戏包体放在E:\SteamSdk\tools\ContentBuilder\content 目录下。一般为了区分windows / mac os，可以在 content 目录下见两个文件夹：windows 和 macos，然后将对应包体文件放在对应文件夹下。

2，
编辑 E:\SteamSdk\tools\ContentBuilder\scripts\ 下的app_build_1000.vdf 和 depot_build_1001.vdf。

将 app_build_1000.vdf 和 depot_build_1001.vdf 改名，分别改成自己项目的 appid 和 depotid，例如：
app_build_2000.vdf、depot_build_2001.vdf。

然后修改 app_build_2000.vdf 中的内容，改成正式的 appid 和 depotid
{{< figure src="/img/20180904-Steamworks后台配置相关/Steamworks后台配置相关-07.jpg">}}

修改 depot_build_2001.vdf ，注掉 “ContentRoot”。注掉则会使用 app_build_2000.vdf 中的 contentroot 配置（{{< hl-text red >}}也可以修改为本地的打包目录，这样就不用拷贝到content目录{{< /hl-text >}}）。然后修改LocalPath，指定windows或者mac的包体所在目录，{{< hl-text red >}} 注意：路径末尾一定要加星号，否则上传的文件为空。{{< /hl-text >}}
{{< figure src="/img/20180904-Steamworks后台配置相关/Steamworks后台配置相关-08.jpg">}}

3，把steamcmd.exe所在的目录加入环境变量
E:\SteamSdk\tools\ContentBuilder\builder

4，打开windows 命令行，执行命令：

    steamcmd +login "用户名带双引号" "密码带双引号" 

登陆成功后，会进入steam专用命令行，然后再执行命令：

    run_app_build E:\SteamSdk\tools\ContentBuilder\scripts\app_build_xxxxxx.vdf
    
执行后就会提示正在扫描并上传文件。

5，上传完毕后，登陆SteamWorks后台，选中最后一次Build的记录，并应用更新。
步骤：打开App Admin界面后，点击 Edit Steamworks Settings  -》 Steam Pipe -》 Builds 。
{{< figure src="/img/20180904-Steamworks后台配置相关/Steamworks后台配置相关-09.jpg">}}
{{< figure src="/img/20180904-Steamworks后台配置相关/Steamworks后台配置相关-10.jpg">}}

选中上传的版本，Branch选择 Default，然后点击 Preview Change 。
{{< figure src="/img/20180904-Steamworks后台配置相关/Steamworks后台配置相关-11.jpg">}}

点击 Set Build Live Now。
{{< figure src="/img/20180904-Steamworks后台配置相关/Steamworks后台配置相关-12.jpg">}}

然后重启steam客户端，就可以自动更新到刚刚构建上传的内容了。

##### 小结
也可以一次行执行两个操作：

    Steamcmd.exe +login "用户名带双引号" "密码带双引号" +run_app_build E:\SteamSdk\tools\ContentBuilder\scripts\app_build_xxxxxx.vdf

##### DLC上传

DLC上传的方式与游戏主程序包体的上传方式有点类似

Downloadable Content (DLC)  
https://partner.steamgames.com/doc/store/application/dlc

判断是否已经安装了DLC：

    bool ISteamApps::BIsDlcInstalled( AppId_t appID );
    
***
`见地深刻的人经常没有听众。`