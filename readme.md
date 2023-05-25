#   Async-Hooks-Demo

问题背景: 如何追踪一整条调用链路(traceId)

实质: 如何在调用链路中保持一个公共存储空间(`Continuation-Local-Storage`)

排除直接使用全局变量方案 => 所有回调函数共享同一个全局变量, 无法做到按链路独立

方案一: 在所有函数调用前添加一个变量, 作为整条回调链路的公共存储空间. 

方案1.1: 
由babel维护, 只在特定入口函数前创建新公共存储空间, 其他函数复用上一个函数传来的空间. 从而保证对整个链路的追踪
方案1.2: 
由开发人员手工维护, 调用子函数时, 主动决定使用复链路上的哪个空间作为子函数存储空间
方案1.3:
由库函数负责维护存储空间链路, 只允许通过特定方法执行回调(例如`Zone.run`), 在该方法内的所有函数链路共享同一个存储空间


#   思路的共同特征


#   参考资料

-   [zone.js-npm站点](https://www.npmjs.com/package/zone.js?activeTab=readme)
    -   [[翻译] 翻阅源码后，我终于理解了Zone.js](https://zhuanlan.zhihu.com/p/50835920)
    -   [Angular框架解读--Zone区域之zone.js](https://godbasin.github.io/2021/05/01/angular-design-zonejs/)
    -   [理解Zones](https://zhuanlan.zhihu.com/p/89173083)