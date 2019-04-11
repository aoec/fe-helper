# fe-helper
问答式前端手册（持续更新中，欢迎pr）。使用渐进式的问题带着你一起去思考相关技术，通过简洁的回答让你能快速明了其中的缘由。

# 基础

## 原型链

#### 什么是原型链？

## 闭包

#### 什么是闭包？

#### 闭包的应用

## this

#### this是什么？

#### this指向谁？

#### 如何修改this的指向？

## GC

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
* 参考链接
  * [正则表达式 - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)

#### 正则引擎是如何工作的？

#### 常用的正则用法有哪些？
* 匹配范围内的字符
  * 语法
    * `/[]/`
  * 用例
    * 查询单个
      * `'aBc'.match(/[abc]/)`
    * 查询多个
      * `'aBc'.match(/[abc]/g)`
    * 忽略大小写
      * `'aBc'.match(/[abc]/i)`
    * 查询多个且忽略大小写
      * `'aBc'.match(/[abc]/gi)`
* 范围外的字符
  * 语法
    * `/[^]/`
  * 用例
    * `'aBc'.match(/[^a]/)`
* 匹配特定类型字符
  * 语法
    * 数字 `/\d/`
    * 非数字 `/\D/`
    * 数字大小写字母下划线 `/\w/`
    * 非数字大小写字母下划线 `/\w/`
    * 空白符号 `/\s/`
    * 非空白字符 `/\S/`
    * 非换行符的任意字符 `/./`
* 匹配边界
  * 语法
    * 开头 `/^/`
    * 结尾 `/$/`
  * 用例
    * `'hello world'.match(/^hello world&/)`
* 分组匹配
  * 语法
    * `/()/`
  * 用例
    * `'hello world'.match(/hello (world)!/)`
* 选择匹配
  * 语法
    * `/|/`
  * 用例
    * `'hello world'.match(/h|w/)`
* 零宽断言
  * 语法
    * 正向肯定断言 `/?=/`
    * 正向否定断言 `/?!/`
    * 反向肯定断言 `/?<=/`
    * 反向否定断言 `/?<!/`
  * 用例
    * 正向肯定断言 `'hello world'.match(/hello (?=world)/)`
    * 正向否定断言 `'hello world'.match(/hello (?!world)/)`
    * 反向肯定断言 `'hello world'.match(/(?<=hello )world/)`
    * 反向否定断言 `'hello world'.match(/(?<!hello )world/)`
* 重复匹配
  * 语法
    * 匹配零次或一次 `/hel?o/`
    * 匹配一次或以上 `/hel+o/`
    * 匹配零次或以上 `/hel*o/`
    * 固定数量 `/{2}/`
    * 范围内数量 `/{2,4}/`
  * 应用
    * `'hello world'.match(/ ?hel+o */)`
* 动态创建正则
  * 语法
    * `new RegExp()`
  * 用例
    * `'hello world'.match(new RegExp('hello world'))`

#### 正则常用场景有哪些？
* 匹配手机号
* 匹配邮箱
* 匹配网址

## JSON

#### JSON的规范有哪些？
* [JSON](https://www.json.org/)
  * 全称
    * JavaScript Object Notation
  * 应用
    * 原生JS使用的是标准的JSON格式
* [JSON5](https://json5.org/)
  * 意义
    * JSON5是JSON的超集，目标是通过提供部分ES5中的特性来缓解JSON的限制。
  * 新特性
    * 对象
      * 对象key可以是ES5.1中的[标志符](https://www.ecma-international.org/ecma-262/5.1/#sec-7.6)名
      * 对象运行有单个拖尾逗号
    * 数组
      * 数组值允许有单个拖尾逗号
    * 字符串
      * 字符串值可以用单引号包裹
      * 字符串值可以通过新行字符（\）多行书写
      * 字符串值可以包含转义字符
    * 数字
      * 数字值可以是十六进制
      * 数字值可以是+infinity，-infinity和NaN
      * 数字值可以以+号开始
    * 注释
      * 支持多行注释
    * 空格
      * 允许出现多余的空格

#### JSON在使用过程中可能会遇到的问题有哪些？
* 标准JSON的值只支持有限的数据类型
   * 支持的类型
     * object | array | string | number | "true" | "false" | "null"
   * 常见问题示例
     * 不支持的类型在转换过程中会丢失
       * JSON.parse(JSON.stringify({fun: () => {}}))  // {}

## Git

#### Git是什么？
* 意义
  * 分布式版本管理系统。
* 创始
  * 创始于2005年。
* 参考链接
  * [1.2 起步 - Git 简史](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-Git-%E7%AE%80%E5%8F%B2)
  * [1.2 Getting Started - A Short History of Git](https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git)

#### 什么情况下我需要使用Git？

#### 如何配置Git环境？
* 安装
  * [1.5 起步 - 安装 Git](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)
* 配置用户名和邮箱
  * git config --global user.name "John Doe"
  * git config --global user.email johndoe@example.com
* 生成ssh通讯公钥
  * ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
* 查看公钥
  * cat ~/.ssh/id_rsa.pub
* 添加ssh key
  * github
    * 头像 -> settings -> SSH and GPG keys > New SSH key
      * title 选填
      * key 把查看的公钥粘贴到这里
* 初始化git项目
  * 本地
    * git init
  * github
    * git clone https://github.com/aoec/fe-helper.git


#### fetch和pull有什么不同？
* 相关信息
  * pull等同于fetch+merge
* 参考链接
  * [What is the difference between 'git pull' and 'git fetch'?
](https://stackoverflow.com/questions/292357/what-is-the-difference-between-git-pull-and-git-fetch)

#### 如何通过git进行团队合作和需求上线？
* 开发准备
  * 基于master分支checkout出一个开发分支A
* 上线阶段
  * 基于master分支checkout一个预上线分支B
  * 开发分支A对预上线分支B发pr

#### Git使用过程中可能会遇到哪些坑？
* 错误的把代码A合到了预上线分支B，并且在你之后继续有代码合并到此分支，如何把分支A合并到分支B的部分提交记录从分支B中删除？
* 开发需求A的过程中，来了一个优先级高的需求B，开发中的需求A的代码未自测，不希望提交进代码库。这时应该如何为需求B创建分支并切换过去？

#### Git是如何工作的？

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

#### NPM是如何工作的？

## HTTP

#### HTTP缓存的方式有哪些？
* Cache-Control
  * 示例
    * `Cache-Control: no-store`
      * 不缓存
    * `Cache-Control: no-cache`
      * 每次向服务器验证缓存是否过期
    * `Cache-Control: private`
      * 默认值
      * 中间人（中间代理、CDN等）不能缓存
    * `Cache-Control: public`
      * 中间人可缓存
    * `Cache-Control: max-age=31536000`（强缓存）
      * 可以被缓存的时长（秒）
    * 参考链接
      * [Cache-Control - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cache-Control)
* Pragma（强缓存）
  * `Pragma: no-cache`
    * 用来向后兼容只支持 HTTP/1.0 协议的缓存服务器
    * 等效于`Cache-Control: no-cache`
  * 参考链接
    * [Pragma - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Pragma)
* Etag（强缓存）
  * 缓存的条件
    * ETag和If-None-Match一致
  * 示例
    * `ETag: "33a64df551425fcc55e4d42a148795d9f25f89d4`
    * `If-None-Match: "33a64df551425fcc55e4d42a148795d9f25f89d4"`
  * 参考链接
    * [ETag - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/ETag)
* Expires（强缓存）
  * 缓存的条件
    * 到达或超过过期时间
  * 示例
    * `Expires: Wed, 21 Oct 2015 07:28:00 GMT`
  * 参考链接
    * [Expires - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Expires)
* 参考链接
  * [HTTP 缓存 - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Caching_FAQ)

#### HTTP的重定向方式有哪些？
* 场景
* 示例
* 状态码
  * 301 Moved Permanently 永久重定向
  * 302 Found 临时重定向
  * 304 Not Modified 缓存有效
* 参考链接
  * [HTTP 的重定向 - HTTP | MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Redirections)

## WebSocket

## PWA

## Service Worker