---
title : "[hexo]server启动异常：YAMLException"
date : "2016-05-27T22:00:20+08:00"

categories:
- Tools
tags:
- Hexo

---
### 错误堆栈：

    YAMLException: end of the stream or a document separator is expected at line 15, column 1:
    url: http://yoursite.com
    ^
    at generateError (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\js-yaml\lib\js-yaml\loader.js:162:10)
    at throwError (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\js-yaml\lib\js-yaml\loader.js:168:9)
    at readDocument (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\js-yaml\lib\js-yaml\loader.js:1508:5)
    at loadDocuments (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\js-yaml\lib\js-yaml\loader.js:1544:5)
    at Object.load (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\js-yaml\lib\js-yaml\loader.js:1561:19)
    at Hexo.yamlHelper (E:\Protoss\Desktop\blog\node_modules\hexo\lib\plugins\renderer\yaml.js:7:15)
    at Hexo.tryCatcher (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\bluebird\js\release\util.js:16:23)
    at Hexo.<anonymous> (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\bluebird\js\release\method.js:15:34)
    at E:\Protoss\Desktop\blog\node_modules\hexo\lib\hexo\render.js:59:21
    at tryCatcher (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\bluebird\js\release\util.js:16:23)
    at Promise._settlePromiseFromHandler (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\bluebird\js\release\promise.js:502:31)
    at Promise._settlePromise (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\bluebird\js\release\promise.js:559:18)
    at Promise._settlePromise0 (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\bluebird\js\release\promise.js:604:10)
    at Promise._settlePromises (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\bluebird\js\release\promise.js:683:18)
    at Async._drainQueue (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\bluebird\js\release\async.js:138:16)
    at Async._drainQueues (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\bluebird\js\release\async.js:148:10)
    at Immediate.Async.drainQueues [as _onImmediate] (E:\Protoss\Desktop\blog\node_modules\hexo\node_modules\bluebird\js\release\async.js:17:14)
    at processImmediate [as _immediateCallback] (timers.js:383:17)



### 原因：

_config.yml中每个冒号后面必须跟一个空格