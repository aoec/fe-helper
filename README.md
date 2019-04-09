# fe-helper
你值得拥有的问答式前端手册（持续更新中，欢迎pr）。使用渐进式的问题带着你一起去思考相关技术，配以简洁的回答让你能快速明了其中的缘由。

# 基础

## 原型链

#### 什么是原型链？

## this

#### this是什么？

#### this指向谁？

#### 如何修改this的指向？

## Layout

#### 浏览器是如何渲染DOM的？

#### 渲染过程中存在着哪些问题？

#### 如何优化渲染过程？

* 长列表优化
* DOM节点操作优化

#### 浏览器支持哪些布局方式？

#### 不同地方声明的同名样式，浏览器如何选择？

# ES6

## Promise

#### Promise是什么？

#### 什么情况下我需要使用Promise？

#### Promise怎么顺序执行？

#### Promise的规范有哪些？

## Async

#### Async是什么？

#### 什么情况下需要使用Async？

## Proxy

#### Proxy是什么？

#### 什么情况下我需要使用Proxy？

#### Proxy的兼容性怎么样？

# 工程

## 模块

#### 模块化的方案有哪些？
* AMD、CMD、COMMONJS。

#### 如何根据平台使用不同的打包方案？
* 使用UMD。

## 编译

#### 如果让ES6运行在低版本浏览器上？
* 使用Babel进行转译。

## 打包

#### 常用的打包工具有哪些？
* Webpack、Rollup、Gulp。
#### 他们各自的优劣是什么呢？

# 框架

## Vue

#### Vue的编译过程是怎样的？

#### Vue的运行过程是怎样的？

#### 如果用最简单的方式实现双向绑定？

#### 前端路由的运行过程是怎样的？

#### Vue使用过程中可能会遇到的坑有哪些？

# 设计模式

# 数据结构

# 算法

# 数据

## 正则

#### 正则是什么？

#### 正则引擎是如何工作的？

#### 常用的正则用法有哪些？

#### 正则常用场景有哪些？
* 匹配手机号
* 匹配邮箱
* 匹配网址

## JSON

#### JSON的规范有哪些？

#### JSON在使用过程中可能会遇到的问题有哪些？
* JSON不支持Function

## Git

#### Git是什么？

#### 什么情况下我需要使用Git？

#### 如何配置Git环境？

#### fetch和pull有什么不同？

#### 如何通过git进行团队合作和需求上线？

#### Git使用过程中可能会遇到哪些坑？

## NPM

#### NPM是什么？
* 意义
  * NPM是NodeJS的包管理工具，可以为开发者提供方便的发布和下载Node包的服务。
* 创始
  * 创始于2009年。
* 参考链接
  * [npm About](https://www.npmjs.com/about)

#### NPM安装包的时候，速度慢怎么办？
* 切换为淘宝的安装源
  * 安装cnpm
    * npm install -g cnpm --registry=https://registry.npm.taobao.org
  * 使用源
    * cnpm install
  * 参考链接
    * [淘宝 NPM 镜像](https://npm.taobao.org/)


#### 如何更方便的切换安装源？
* 使用安装源切换工具（nrm）
  * 安装
    * npm install -g nrm
  * 查看源列表
    * nrm ls
  * 切换源
    * nrm use cnpm
  * 使用源
    * npm install
  * 参考链接
    * [Pana/nrm: NPM registry manager, fast switch between different registries: npm, cnpm, nj, taobao](https://github.com/Pana/nrm)


#### devDependencies和dependencies的区别是什么？
* 使用npm install --production安装的时候，devDependencies中的依赖不会被安装，dependencies中的依赖会被安装。不加入--production安装则行为一致。
* 参考链接
    * [What's the difference between dependencies, devDependencies and peerDependencies in npm package.json file?
](https://stackoverflow.com/questions/18875674/whats-the-difference-between-dependencies-devdependencies-and-peerdependencies)

#### NPM使用过程中可能会遇到哪些坑？
* 如果文件夹名与需要安装的包名相同，通过npm install packageName的方式安装会报错
  * 问题原因
    * npm的包安装算法使用的是递归安装，为避免出现死循环，默认不安装和当前文件夹名称一致的包。
  * 解决方案
    * 方案1：文件夹改名（推荐）
    * 方案2：手动在package.json里面加上依赖并使用npm i的方式安装
  * 参考链接
    * [Limitations of npm’s Install Algorithm](https://docs.npmjs.com/cli/install#limitations-of-npms-install-algorithm)
* 未锁定版本情况下，依赖的包新版本出现问题，导致当前应用出现问题
  * 问题原因
    * 依赖的包新版本出现问题
  * 解决方案
    * 方案1：对于出现问题的依赖包进行锁版本（推荐）
    * 方案2：对所有依赖包进行锁版本

## HTTP

#### HTTP缓存的方式有哪些？

#### HTTP的重定向方式有哪些？
