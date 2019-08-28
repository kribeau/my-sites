---
title: 简单理解JavaScript闭包
date: 2019-08-28 13:50:27
categories:
  - js
  - 闭包
tags:
  - js
  - front-end
---

![image of closure](https://images.unsplash.com/photo-1526649661456-89c7ed4d00b8?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1471&q=80)

闭包总是晦涩难懂的，我们在阅读大量关于闭包的文章后，甚至是频繁使用闭包时，也可能并没有意识到自己正在使用闭包。

<!-- more -->

### 现在作者将用形象的方式讲解闭包到底是什么。（作者假定读者已经了解作用域和词法环境...）


#### 闭包，顾名思义，我们可以将它类比为一个背包，当一个函数被创建并传递或从另一个函数返回时，它带有一个背包，并且在背包中装有声明函数时存在函数作用域中的所有变量。

下面让我们来看一个例子：

我们先定义一个对象hero
```JavaScript
//hero
let hero(){
  name: '亚索',
  category: {'战士'，'刺客'},
  position: '中单',
}
```
当我们需要为hero添加属性时，我们可以使用:

```JavaScript
hero.feature = '快乐'
```
这样确实很方便，不是吗？但是，当我们的程序很复杂的时候，在程序运行时有可能会不小心改变一些东西。所以这样并不安全。

这时我们可以将它定义为一个函数：
```JavaScript
function (name) {
  var category
  return {
    getName: function () {
      return name
    },
    setName: function (newName) {
      name = newName
    },
    getCategory: function () {
      return category
    },
    setCategory: function (newCategory) {
      category = newCategory
    },
  }
}
```
这样我们就只能通过get方法和set方法来存取管理属性值了。
#### 这也是闭包的一个优点，我们可以通过母函数来获取到子函数的函数作用域然后去存取里面的值。这样更加安全。
#### 总之，闭包的本质就相当于一个用来存储数据的函数，它里面存储了函数声明时存在函数作用域中的所有变量，在函数执行完后并不会立即消失，而是储存在内存上，所以，闭包是通过消耗内存成本来提高数据安全性。