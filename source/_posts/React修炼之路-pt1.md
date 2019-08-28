---
title: React修炼之路(pt1)
date: 2019-08-28 13:55:37
categories:
  - React
  - js
tags:
  - React
  - js
  - front-end
---

![Image of React](https://colorhub.me/imgserv/46Q_-gwTDzyL15v9tDAyEbgsZAotMgAj-o1WdWak-LY/fill/0/500/ce/0/bG9jYWw6Ly8vMmQv/NTgvZDE0NWZlODJh/Y2UyYmI1ZWYwZjdh/OGYxODNkMThmYzVl/ZTMyMmQ1OC5qcGc.jpg)
### 这个系列将介绍React的要点，跟着作者一起玩转React吧！😉

### 什么是声明式编程 ？

- 声明式编程是一种编程范式，与命令式编程相对立，它专注于你在做**什么**事而不是你**怎样**做这件事的。它表达了逻辑而没有明确定义步骤。 这意味着我们需要根据逻辑计算声明组件显示的内容。 它没有描述控制流程步骤。 声明性编程的示例是 HTML，SQL 等。

  _eg_ :

  ```html
  // html
  <div><p>声明式编程</p></div>
  ```

  ```sql
  // sql
  select * from heroes where name = "亚索"
  ```

  <!-- more -->

### 声明式编程和命令式编程的区别 ？

- 声明式编程描述了应该做什么，而命令式编程描述了如何做。声明式编程中，你可以让编译器来决定如何执行操作。声明式编程更容易理解，因为代码本身描述了它正在做什么！

  _eg_ ：

  ```javascript
  const numbers = [1, 2, 3, 4, 5]

  //声明式编程
  const doubleUseDec = numbers.map(number => number * 2)
  console.log(doubleUseDec)

  //命令式编程
  const doubleUseImp = []
  for (let i = 0; i < numbers.length; i++) {
    const numberdouble = numbers[i] * 2
    doubleUseImp.push(numberdouble)
  }
  console.log(doubleUseImp)
  ```

### 什么是函数式编程 ？

- 函数式编程是另一种编程范式。在 JavaScript 中，函数是一等公民。函数是数据，你可以像变量一样在整个应用中保存、检索和传递这些函数。

### 函数式编程的要点。

- ##### 不变性

  - 不变性意味着不能更改，在函数式编程中，你不能直接更改数据。如果要达到修改的目的，必须复制数据并使用复制的版本进行更改。

    例如，下面是一个 hero 对象和 changeTitle 函数，如果要更改英雄的名称，则需要先复制 hero 对象，然后返回新对象。

    ```javascript
    let hero = {
      title: '疾风剑豪',
      name: '亚索',
      职业: '战士'
    }
    function changeTitle(hero) {
      let copiedHero = Object.assign({}, hero)
      copiedHero.title = '快乐风男'
      return copiedHero
    }

    console.log(changeTitle(hero))
    console.log(hero)
    ```

- ##### 纯函数（Pure Functions）

  - 纯函数是始终接受一个或多个参数后计算参数并返回数据或函数的函数。 它没有副作用，例如设置全局状态，更改应用程序状态，它总是将参数视为不可变数据。

    例如，我们使用名为 appendAddress 的函数向 hero 对象添加一个地址。 如果查看非纯函数，它没有参数，它通过直接更改英雄对象来更改全局状态或应用程序状态。

    ```javascript
    let hero = {
      title: '疾风剑豪',
      name: '亚索',
      职业: '战士'
    }

    // 非纯函数
    function appendAddress() {
      hero.address = {
        country: '艾欧尼亚'
      }
    }

    console.log(appendAddress())

    // 纯函数
    function appendAddress(hero) {
      let copyhero = Object.assign({}, hero)
      copyhero.address = {
        country: '艾欧尼亚'
      }
      return copyhero
    }

    console.log(appendAddress(hero))

    console.log(hero)
    ```

- ##### 数据转换（Pure Functions）

  - 我们正在谈论不变性，如果数据是不可变的，那么我们如何改变数据呢？ 如上一小节，我们总是生成原始数据的转换副本，而不是直接更改原始数据。
    我们将聊聊一些`JavaScript`内置函数。 还有很多其他类似的函数，下面有一些例子。 所有这些函数都不会更改现有数据，而是返回新数组或对象。

    ```JavaScript
    let countries = ["艾欧尼亚","祖安","诺克萨斯"]
    //我们可以得到一个逗号分开的列表
    console.log(countries.join(','))
    // 艾欧尼亚，祖安，诺克萨斯

    //如果我们想得到以'艾'开头的countries
    const I = countries.filter(country => country[0] === '艾')
    console.log(I)
    //['艾欧尼亚']
    ```

- ##### 高阶函数
  - 高阶函数是将函数作为参数或返回函数的函数， 这些高阶函数可以操纵其他函数。


    `Array.map`, `Array.filter` 和 `Array.reduceare` 都是高阶函数，因为它们都接收函数作为参数。

    ```JavaScript
    const numbers = [10,20,30,40,50]

    const output1 = numbers.map(num => num * 100)
    console.log(output1)
    // [1000,2000,3000,4000,5000]

    const output2 = numbers.filter(num => num > 30)
    console.log(output1)
    // [40,50]

    const output3 = numbers.reduce((out,num) => out + num)
    console.log(output3)
    // 150
    ```

    下面是另一个高阶组件的例子：

    ```JavaScript
    const isYoung = age => age < 25

    const message = msg => "He is " + msg

    function isOld (age, isYoung, message) {
      const returnMessage =
        isYoung(age) ? message("young") : message("old")
      return returnMessage
    }

    //传递函数作为参数
    console.log(isOld(13,isYoung,message))
    // He is young
    ```

- ##### 递归

  - 递归是一种技术，函数调用自身直到满足某个条件。 尽可能使用递归而不是循环更好。但必须小心使用递归，因为浏览器不能处理太多的递归和抛出错误。

    下面这个例子用来演示打印像梯形那样的名称的递归。 (当然也可以使用 for 循环)


    ```JavaScript
    function printMyName(name,count) {
      if (count <= name.length) {
        console.log(name.substring(0,count))
        printMyName(name,++count)
      }
    }
    console.log(printMyName("Yasuo",1))

    /*
    Y
    Ya
    Yas
    Yasu
    Yasuo
    */


    //使用for循环
    var name = 'Yasuo'
    var output = "",
    for(let i=0; i<name.length; i++){
      output = output + name[i]
      console.log(output)
    }
    ```

- ##### 组合

  - 在 React 中，我们将应用划分为小型可重用的纯函数，我们必须将所有这些可重用的函数放在一起，使其成为最终产品。 将所有较小的函数组合成更大的函数，最终，您将得到一个应用程序。 这称为组合。实现组合有许多不同的实现和方法。 我们从 Javascript 中了解到的一种常见方法是链接。 链接是一种使用点表示法调用前一个函数的返回值的函数的方法。

    这是一个例子。 我们有一个 name，如果 firstName 和 lastName 大于 4 个单词的大写字母，我想要返回，并且我想打印 name 的名称和长度。

    ```JavaScript
    const name = "Steven Curry";

    const output = name.split(" ")
        .filter(name => name.length > 4)
        .map(val => {
        val = val.toUpperCase();
        console.log("Name:::::"+val);
        console.log("Count::::"+val.length);
        return val;
    });

    console.log(output)
    /*
    Name:::::STEVEN
    Count::::6
    Name:::::STEVEN
    Count::::6
    [ 'STEVEN', 'CURRY' ]
    */
    ```

  - 在 React 中，我们使用除了链接(chaining)之外的其他方法，因为如果你有非常多的函数则很难进行链接。这里的目标是组合所有更简单的函数来生成更高阶函数。

    ```JavaScript
    const name = compose(
      splitmyName,
      countEachName,
      comvertUpperCase,
      returnName
    )
    console.log(name)
    ```

> 未完待续~~~