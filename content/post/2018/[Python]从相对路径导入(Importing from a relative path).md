+++
title= "[Python]从相对路径导入(Importing from a relative path)"
date= "2018-01-31T20:02:40+08:00"
categories= ["Python"]
tags= ["Python"]
+++

假设python工程结构如下：

    Proj/
        Client/
            Client.py
        Server/
            Server.py
        Common/
            __init__.py
            Common.py
            
要在Client.py中import Common目录。代码如下：
            
    import sys, os
    sys.path.append(os.path.join(os.path.dirname(__file__), '..', 'Common'))
    import Common
    
其中os.path.dirname(__file__)表示当前python脚本的所在目录。

参考：  
Importing from a relative path in Python  
https://stackoverflow.com/questions/7505988/importing-from-a-relative-path-in-python