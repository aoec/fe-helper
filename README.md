# fe-helper
问答式前端手册（持续更新中，欢迎pr）。使用渐进式的问题带着你一起去思考相关技术，通过简洁的回答让你能快速明了其中的缘由。

# 基础

## 原型链

#### 什么是原型链？

* JS中万物皆对象
  * 基于对象声明了Function
  * 基于Function声明了Number，Boolean，String，Function
* 详解
  * \_\_proto\_\_ 指向构造函数的原型
    * null, undefined是特殊的空值，没有__proto__属性
  * prototype 构造函数的原型
```js
// 基本类型实例的__proto__指向构造函数的prototype
(0).__proto__ === Number.prototype  // true，指向Number
(false).__proto__ === Boolean.prototype  // true
('').__proto__ === String.prototype  // true
// 继续往上走则指向Object的prototype
(0).__proto__.__proto__ === Object.prototype  // true，指向Number
(false).__proto__.__proto__ === Object.prototype  // true
('').__proto__.__proto__ === Object.prototype  // true
// 再继续走指向null
(0).__proto__.__proto__.__proto__ === null  // true，指向null
(false).__proto__.__proto__.__proto__ === null  // true
('').__proto__.__proto__.__proto__ === null  // true
// 对象实例的__proto__指向Object的prototype
({}).__proto__ === Object.prototype  // true
// 继续往上则指向null
({}).__proto__.__proto__ === null  // true
// 函数实例的__proto__指向内部Function
(function(){}).__proto__ === Function.prototype  // true
// 继续往上则指向Object的prototype
(function(){}).__proto__.__proto__ === Object.prototype
// 再继续走指向null
(function(){}).__proto__.__proto__.__proto__ === null
```
  * constructor 指向构造函数
```js
// 实例的constructor指向构造函数
(0).constructor === Number  // true
(false).constructor === Boolean  // true
('').constructor === String  // true
({}).constructor === Object  // true
(function(){}).constructor === Function  // true
// 构造函数的constructor指向构造函数的constructor
Number.constructor === Function  // true
Boolean.constructor === Function  // true
String.constructor === Function  // true
Object.constructor === Function  // true
Function.constructor === Function  // true
```
  * instanceof 判断一个值是否继承至另一个值
```js
new Number(0) instanceof Number  // true
```

```js
// 基本类型值的__proto__指向对应类型的prototype
(1).__proto__ === Number.prototype  // true
(false).__proto__ === Boolean.prototype  // true
''.__proto__ === String.prototype  // true
// 对象值的__proto__指向对象类型的prototype
({}).__proto__ === Object.prototype  // true
// 函数值的__proto__指向函数类型的prototype
(function(){}).__proto__ === Function.prototype
// 基本类型、对象、函数的类型__proto__指向Function的prototype
Number.__proto__ === Function.prototype  // true
Boolean.__proto__ === Function.prototype  // true
String.__proto__ === Function.prototype  // true
Function.__proto__ === Function.prototype  // true
Object.__proto__ === Function.prototype  // true
// 函数的__proto__指向Object
Number.__proto__.__proto__ === Object.prototype  // true
Boolean.__proto__.__proto__ === Object.prototype  // true
String.__proto__.__proto__ === Object.prototype  // true
Function.__proto__.__proto__ === Object.prototype  // true
Object.__proto__.__proto__ === Object.prototype  // true
Function.prototype.__proto__ === Object.prototype  // true
// Object的__proto__指向null
Number.__proto__.__proto__.__proto__ === null  // true
Boolean.__proto__.__proto__.__proto__ === null  // true
String.__proto__.__proto__.__proto__ === null  // true
Function.__proto__.__proto__.__proto__ === null  // true
Object.__proto__.__proto__.__proto__ === null  // true
Function.prototype.__proto__.__proto__ === null  // true
```

* 参考
  * [深度解析原型中的各个难点](https://github.com/KieSun/Dream/issues/2)

## 闭包

#### 什么是闭包？

* 一个函数内返回另一个函数，则会形成闭包

```js
const fun = () => {
  const variable = 'closure sample'
  return closureFun = () => {
    return variable
  }
}
```
* 函数内声明的变量外部无法访问，通过闭包可以访问

```js
const closureFun = fun()
closureFun()  // "closure sample"
```

* 一般来说，函数执行完后，内部的变量会被清除
* 通过在闭包内访问变量的方式，可以使变量的值一直存在

#### 闭包的应用

* 链式调用

```js
const setColor = function(color) {
  this.color = color;
  return this
}
const setVisible = function(visible) {
  this.visible = visible
  return this
}
const Utils = {
  color: '',
  visible: false,
  setColor,
  setVisible
}
Utils.setColor('blue').setVisible(true)  // {color: "blue", visible: false, setColor: ƒ, setVisible: ƒ, visivle: true}
```

* 工具封装
  * 闭包内的变量外部无法访问，可以避免闭包内变量污染全局作用域

```js
((instance) => {
  const setColor = function(color) {
    this.color = color;
    return this
  }
  const setVisible = function(visible) {
    this.visible = visible
    return this
  }
  instance.Util = {
    color: '',
    visible: false,
    setColor,
    setVisible
  }
})(window)
```

#### 闭包的应用

## this

#### this是什么？

#### this指向谁？

* this指向调用者

```js
var variable = 'sample variable in window'
var obj = {
  variable: 'sample variable in fun',
  fun: function (paramOne, paramTwo) {
    console.log(this.variable, paramOne, paramTwo)
  }
}
obj.fun('one', 'two')  // sample variable in fun one two，调用者为obj，this指向obj
const fun = obj.fun
fun('one', 'two')  // sample variable in fun one two，调用者为window，this指向window
```

#### 如何修改this的指向？

* call
  * 第一个参数为所需指向的位置
  * 第二个参数为数组，里面是函数入参

```js
fun.call(obj, 'one', 'two')  // sample variable in fun one two
```

* apply
  * 第一个参数为所需指向的位置
  * 第二个及以后的参数为函数入参

```js
fun.apply(obj, ['one', 'two'])  // sample variable in fun one two
```

* bind
  * 第一个参数为所需指向的位置
  * 指向过后返回绑定了this的新函数
    * 新函数的第一个及以后的参数为函数入参

```js
fun.bind(obj)('one', 'two')  // sample variable in fun one two
```

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

## 排序

#### 冒泡排序
* 简介
  * 从左至右依次对比当前值和下一个值的大小，如果当前值大于下一个值，则交换，每轮产生一个排好序的值。
  * [可视化动画](https://visualgo.net/zh/sorting)

* 步骤
  * 第一轮
    * 4 和 2 比较，4 > 2，交换，新值为 `[2,4,1,5,3]`
    * 4 和 1 比较，4 > 1，交换，新值为 `[2,1,4,5,3]`
    * 4 和 5 比较，4 < 5，交换，不变
    * 5 和 3 比较，5 > 3，交换，新值为 `[2,1,4,3,5]`
    * 当前产生一个最大数，5
  * 第二轮
    * ...
* 关键点
  * 第一层循环需要走几次？
    * 假设待排序的数长度是2个，第一轮冒泡产生一个排好序的值，剩下的一个值无需排序，所以走1次；
    * 假设待排序的数长度是3个，第一轮冒泡产生一个排好序的值，第二轮也产生一个，剩下的一个值无需排序，所以走2次；
    * ...
    * 以此类推，第一轮需要走 `n-1` 次。
  * 第二层循环需要走几次？
    * 假设待排序的数长度是2个
      * 第一轮，需要比较1次；
    * 假设待排序的数长度是3个
      * 第一轮，需要比较2次；
      * 第二轮，待排序的数长度变成了2，因此需要比较1次；
    * 假设待排序的数长度是4个
      * 第一轮，需要比较3次；
      * 第二轮，待排序的数长度变成了3，因此需要比较2次；
      * 第三轮，待排序的数长度变成了2，因此需要比较1次；
    * 以此类推，第二层需要走 `n-1-已排好序数量`
  * 如果第二层循环，直到遍历结束也没发现需要交换的值
    * 则表示已经排序完成
    * 第一层循环可以直接退出

* 示例（两层for循环）
```js
const bubbleSort = (arr) => {
  let switched = true;
  let temp = null;
  let left = null;
  let right = null;
  for (var loop1Index = 0; loop1Index < arr.length - 1; loop1Index++) {
    if (!switched) break;
    for (var loop2Index = 0; loop2Index < arr.length - 1 - loop1Index; loop2Index++) {
      switched = false;
      left = arr[loop2Index];
      right = arr[loop2Index + 1];
      if (left > right) {
        switched = true;
        temp = left;
        arr[loop2Index] = right;
        arr[loop2Index + 1] = temp;
      }
    }
  }
  return arr;
}
const sampleArr = [4,2,1,5,3];
bubbleSort(sampleArr)  // [1, 2, 3, 4, 5]
```

* 示例（do...while）

```js
const bubbleSort = (arr) => {
  let tail = arr.length - 1;
  let switched = true;
  let temp = nul;
  do {
    switched = false;
    for (var x = 0; x < tail; x++) {
      if (arr[x] > arr[x+1]) {
        switched = true;
        temp = arr[x];
        arr[x] = arr[x+1];
        arr[x+1] = temp;
      }
    }
  }
  while(switched && tail)
  return arr;
}
const sampleArr = [4,2,1,5,3];
bubbleSort(sampleArr)  // [1, 2, 3, 4, 5]
```

#### 快速排序

* 简介
  * 采用分治的思想，以基准值为界，基准值左右分别处理成小于和大于基准值的序列。然后分别对左右值按照第一句描述的步骤进行递归，直到左值或有值的大小等于1时退出。

* 步骤
  * 选出基准点（通常选中间值）
  * 声明两个变量left,right分别储存数组的首尾下标
  * left的值小于基准点则继续向右移动
  * 大于则停止
    * right的值大于基准点则继续向左移动
    * 小于则停止
      * 两者都停止的时候，则交换arr[left]和arr[right]的值
      * 否则继续移动，直到left>right
        * 紧接着继续按照left为基准点，从步骤二开始对左右两部分数据分别递归
* 关键点

* 示例（while）

```js
const quickSort = (arr, left, right) => {
  const swap = (swapArr, leftIndex, rightIndex) => {
    const temp = swapArr[leftIndex];
    swapArr[leftIndex] = swapArr[rightIndex];
    swapArr[rightIndex] = temp;
  }
  const partition = (partArr, partHead, partTail) => {
    const pivot = partArr[Math.floor((partHead+partTail)/2)];
    let left = partHead;
    let right = partTail;
    while (left <= right) {
      while (partArr[left] < pivot) left++;
      while (partArr[right] > pivot) right--;
      if (partArr[left] > partArr[right]) {
        swap(partArr, left, right);
        left++;
        right--;
      }
    }
    return left;
  }
  if (arr.length > 1) {
    const index = partition(arr, left, right);
    if (left < index - 1) quickSort(arr, left, index - 1);
    if (right > index) quickSort(arr, index, right);
  }
  return arr;
}
const sampleArr = [4,2,1,5,3];
quickSort(sampleArr, 0, sampleArr.length - 1)  // [1, 2, 3, 4, 5]
```

* 示例（concat）

```js
const quickSort = (arr) => {
  if (arr.length <= 1) return arr;
  const [pivot, ...rest] = arr;
  const left = [];
  const right = [];
  rest.forEach((v) => {
    if (v < pivot) left.push(v);
    else right.push(v);
  })
  return [...quickSort(left), pivot, ...quickSort(right)]
};
const sampleArr = [4,2,1,5,3];
quickSort(sampleArr) // [1, 2, 3, 4, 5]
```

#### 选择排序

#### 归并排序

#### 插入排序

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

## chrome插件

#### 如何写插件？