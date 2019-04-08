# fe-helper
你值得拥有的问答式前端手册（持续更新中，欢迎pr）。使用渐进式的问题带着你一起去思考相关技术，配以简洁的回答让你能快速明了其中的缘由。

# 基础

## 原型链

> 什么是原型链？

## this

> this是什么？

> this指向谁？

> 如何修改this的指向？

# ES6

## Promise

> Promise是什么？

> 什么情况下我需要使用Promise？

> Promise怎么顺序执行？

> Promise的规范有哪些？

## Async

> Async是什么？

> 什么情况下需要使用Async？

## Proxy

> Proxy是什么？

> 什么情况下我需要使用Proxy？

> Proxy的兼容性怎么样？

# 工程

## 模块

> 模块化的方案有哪些？
* AMD、CMD、COMMONJS。

> 如何根据平台使用不同的打包方案？
* 使用UMD。

## 编译

> 如果让ES6运行在低版本浏览器上？
* 使用Babel进行转译。

## 打包

> 常用的打包工具有哪些？
* Webpack、Rollup、Gulp。
> 他们各自的优劣是什么呢？

# 框架

## Vue

> Vue的编译过程是怎样的？

> Vue的运行过程是怎样的？

> 如果用最简单的方式实现一个双向绑定库？

# 设计模式

# 数据结构

# 算法

# 数据

## 正则

> 正则是什么？

> 正则引擎是如何工作的？

> 常用的正则用法有哪些？

> 正则常用场景有哪些？
* 匹配手机号
* 匹配邮箱
* 匹配网址

## JSON

> JSON的规范有哪些？
* 

> JSON在使用过程中可能会遇到的问题有哪些？
* JSON不支持Function

## Git

> Git是什么？

> 什么情况下我需要使用Git？

> 如何配置Git环境？

> fetch和pull有什么不同？

> 如何通过git进行团队合作和需求上线？

> Git使用过程中可能会遇到哪些坑？

## NPM

> NPM是什么？

> NPM按照包的时候，速度慢怎么办？

> 如果更方便的切换安装源？

> devDependencies和dependencies的区别是什么？

> NPM使用过程中可能会遇到哪些坑？
* 如果文件夹名需要安装的包名相同，通过npm install packageName的方式安装会提示错误信息，手动在package.json里面加上依赖并npm i的方式则可以正常安装。