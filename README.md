# 1. 前言

`Vue next` 每天依旧在进行着改变，但核心部分基本确定了下来，没有太多的其他代码干扰，正是理解 `vue next` 的好时候。

本文截取并简化 Vue next 部分的源代码，提供一种阅读框架源码的开始方式，来初步进入并了解 Vue next 框架的底层世界。

# 2. 学习规划

## 2.1 源码学习目录

本项目所剖析的 `Vue next` 源码版本为 v3.0.0-alpha.10 (2020-03-24) ，其代码目录如下：

``` bash
learn-vue-next-source-code
├─ .circleci              # 使用 CircleCI 2.0 进行持续集成/持续部署
├─ .vscode                # vs code 配置
├─ CHANGELOG.md           # 更改日志
├─ api-extractor.json     # @microsoft/api-extractor
├─ jest.config.js         # jest 配置
├─ packages
│    ├─ compiler-core     # 编译器核心
│    ├─ compiler-dom      # 编译(虚拟)DOM
│    ├─ compiler-sfc      # 编译 SFC(single file components)更底层的使用工具
│    ├─ compiler-ssr      # 编译 SSR(server side render)
│    ├─ global.d.ts       # 全局变量声明
│    ├─ reactivity        # 响应式相关
│    ├─ runtime-core      # 运行时核心(仅用于输入和构建自定义渲染器)
│    ├─ runtime-dom       # 运行时DOM(生成虚拟DOM)
│    ├─ runtime-test      # 运行时测试
│    ├─ server-renderer   # 服务端渲染器
│    ├─ shared            # 共享内部的方法与常量(通过@vue)
│    ├─ size-check        # 检查基准运行时规模
│    ├─ template-explorer # 动态探测模板编译输出
│    └─ vue               # 构建包
├─ scripts                # 与项目构建相关的脚本和配置文件
├─ test-dts               # 项目测试代码声明文件
```

上面的目录结构与vue2. X已经有了很大差别，其中很多单元被独立了出来，从而可以单独使用。 目前 `Vue next` 的整个项目包含了编译相关、响应式相关、运行时相关的代码。

目前 `package` 中出现的代码正好是属于 `vue next` 核心相关的部分，没有平台无关、测试等代码干扰，正是进行学习的好时候。

## 2.2 学习路线

在学习之前，我们需要先制定一个学习路线，循序渐进的学习，这样不至于一头雾水，无处下手。后面的学习路线如下：

1. 变化侦测篇

   学习 `Vue next` 中如何实现数据的响应式系统，从而达到数据驱动视图，这是 `Vue next` 的核心所在。

2. 虚拟 DOM 篇

   学习什么是虚拟 DOM，以及 `Vue` 中的 `DOM-Diff` 原理

3. 模板编译篇

   学习 `Vue` 内部是怎么把 `template` 模板编译成虚拟 `DOM` , 从而渲染出真实 `DOM` 

4. 实例方法篇

   学习 `Vue` 中所有实例方法(即所有以`# 1. 前言

## 2.3 学习输出

通过一步步的学习，博主打算在学习过程中输出以下三个东西：

* 以文字形式记录学习过程；
* 为 `clone` 下来的 `Vue` 源码添加尽可能详细的注释；
* 做一份思维导图，以宏观角度总览源码；

# 3. 致谢

本系列文档是作者通过学习 `Vue next` 源码和参照 [Learn-Vue-Source-Code](https://github.com/NLRX-WJC/Learn-Vue-Source-Code/blob/master/README.md) 时所记录的学习笔记。文档中的内容绝大部分是来自个人对源码的真实理解，另外，文档格式我就直接引用 [Learn-Vue-Source-Code](https://github.com/NLRX-WJC/Learn-Vue-Source-Code/blob/master/README.md) 的啦。:)

另外，感谢 [难凉热血](https://github.com/NLRX-WJC) 的辛勤付出，才能够让我们后来者站在巨人的肩膀上，学习更多的知识。

最后，预祝大家阅读愉快。