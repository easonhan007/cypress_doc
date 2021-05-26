### 整体思路

分析cypress realworld项目，地址：https://github.com/cypress-io/cypress-realworld-app，从项目中学会

* typescript的简单语法，因为项目是typescript写的，会一点简单的语法方便我们进行源码阅读
* 体验cypress realworld项目，梳理出主要功能，这是熟悉需求
* 梳理后端接口和数据结构，这一步是了解后台逻辑实现
* 了解express,lowdb的简单使用，这一步的目的是为了让我们能看懂项目的后台代码
* 了解react,xstate的简单使用，为了看懂前端代码，这两个框架的时间投入还是值得的
* 了解cypress功能
* 了解前后端分离app的工作模式
* 单元测试怎么写?看一下实际项目中的单元测试实现
* 接口用例怎么写？看一下高水平的开发者的接口测试思路
* ui测试用例怎么写？这里很难一言以蔽之
* database seeding是什么？为什么会降低ui测试的难度？
* cypress怎么做ci/cd的？了解ci/cd的工作原理与工作流程

### 大纲草稿

* ts语法简介，主要参考微软官方文档:https://www.typescriptlang.org/docs/handbook/intro.html
* cypress realdworld项目部署(也可以不用部署)
* cypress realworld项目初体验，输出主要功能文档
* cypress的主要功能，参考https://docs.cypress.io/guides/core-concepts/introduction-to-cypress.html#Cypress-Can-Be-Simple-Sometimes
    * 重试机制
    * 元素的交互
    * 分支测试
* cypress relaworld的后台接口分析
* 如何使用express+lowdb实现后台接口
    * 数据库设计
    * 鉴权
    * 路由及持久化实现
* 分析cypress relaworld的单元测试实现
* 分析cypress relaworld的接口测试实现
* 如何使用react+xstate实现前端功能
    * react简介以及页面的渲染
    * 路由实现
    * 状态机实现
    * 与后台的交互
* 分析ui测试用例
    * 如何选取用例
    * 断言怎么写
    * 什么是db seeding，有什么好处
    * 怎么调试
    * 怎么截图和录视频
    * 怎么设置环境变量
    * 如何使用test runner去命令行跑指定用例
    * 怎么做多浏览器兼容性测试
    * 怎么做ci/cd

随便列了一下，发现内容还是相当丰富的，如果一周出一篇的话，基本上半年大半年就过去了。

### 时间计划

所以先立个flag，争取在今年年中，大概7月份之前完成吧。

在如今定量宽松的时代，投资稍有不慎贬值的机率是比较大的，不过投资自己却是少有的低成本高收益的投资方式。

新的一年，不如我们一起花点时间，让自己增值吧，也许你会发现，你自身才是自己最优质的资产。



