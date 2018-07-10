+++
title= "GitHub Pages 对自定义域名支持 HTTPS"
date= "2018-07-10T14:19:40+08:00"
categories= ["Web"]
tags= ["github"]
+++

keywords：github pages、custom domain、https

我的github pages的默认域名为：dawnarc.github.io，以修改该域名为自定义域名：dawnarc.com 为例

##### 1，域名解析设置

以美橙互联为例：

<table>
    <thead>
        <tr>
            <th>主机名</th>
            <th>记录类型</th>
            <th>记录值</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>@</td>
            <td>A记录</td>
            <td>github pages的ip地址</td>
        </tr>
        <tr>
            <td>xxx</td>
            <td>CNAME记录</td>
            <td>dawnarc.github.io.</td>
        </tr>
    </tbody>
</table>

##### 2，CNAME文件修改
dawnarc.github.io仓库下的CNAME修改

    dawnarc.com


##### 3，enforce HTTPS 勾选
上面第二步的CNAME文件修改以后，再刷新 `dawnarc.github.io` 的 GitHub Pages 设置，就可以勾选 `Enforce HTTPS `。稍等片刻，就可以以https打开自己的自定义域名。

##### 注意事项
如果使用 Chrome 访问 https 地址栏左侧仍未出现小绿锁，请检查自己的网站引用的资源文件有没有使用了 http 协议，请替换成相应的 https 资源。


参考自：GitHub Pages 对自定义域名支持 HTTPS  
https://likfe.com/2018/05/03/github-pages-custom-domains-support-https/