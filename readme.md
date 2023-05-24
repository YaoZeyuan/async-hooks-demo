#   Async-Hooks-Demo

#   问题背景:如何在调用链路中保持一个公共存储空间(`Continuation-Local-Storage`)

| 思路                                                                         | 是否可用 | 原因                                                                                                                 |
| :--------------------------------------------------------------------------- | :------- | :------------------------------------------------------------------------------------------------------------------- |
| 通过全局变量/全局模块                                                        | ❌        | 所有回调函数共享同一个全局变量, 无法做到按链路独立                                                                   |
| 通过全局变量/全局模块->每次进入新函数时生成uuid作为key的路径区分不同调用链路 | ❓        | 理论上可行. 实践中需要利用babel在代码编译时进行注入                                                                  |
| 所有函数额外增加一个参数, 作为公共变量                                       | ❓        | 理论上可行. 实践中需要利用babel在代码编译时进行注入                                                                  |
| 思路打开: 重写每一个涉及异步调用的方法, 手工维护一条调用链路以实现该功能     | ❓❓❓      | 理论上可行. 实践中见[zone.js-Patch方法列表](https://github.com/angular/angular/blob/main/packages/zone.js/MODULE.md) |

#   思路的共同特征


#   参考资料

-   [zone.js-npm站点](https://www.npmjs.com/package/zone.js?activeTab=readme)
    -   [[翻译] 翻阅源码后，我终于理解了Zone.js](https://zhuanlan.zhihu.com/p/50835920)
    -   [Angular框架解读--Zone区域之zone.js](https://godbasin.github.io/2021/05/01/angular-design-zonejs/)