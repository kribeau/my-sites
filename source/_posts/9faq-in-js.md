---
title: 9faq in js
date: 2019-08-28 12:20:02
categories:
  - js
  - web
tags:
  - js
  - front-end
---
![Image of coding](https://images.unsplash.com/photo-1503252947848-7338d3f92f31?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1489&q=80)

JavaScript 被认为是对初学者很友好的一门语言。部分原因在于她在互联网上的广泛使用，还有一部分在于她的一些功能使得编写不完美的代码仍然可以运行（她不像许多其他语言那样严格，你不必再受分号或者内存管理的折磨)。
<!-- more -->
## 本文中，我们将介绍一些有趣的 JavaScript 问题。

### 1. 为什么 Math.max()小于 Math.min()?

Math.max() > Math.min()返回 false 的事实听起来是荒唐的，但它确实有点意思。

如果没有给出参数，则 Math.min( ) 返回 infinity 而 Math.max( ) 返回 -infinity。这只是 max( ) 和 min( ) 方法规范的一部分，但在这背后有很好的逻辑。要了解原因，请查看一下代码：

```JavaScript
Math.min（1）
// 1
Math.min（1，infinity）
// 1
Math.min（1，-infinity）
//  - 无穷大
```

如果 `-infinity`被认为是 Math.min( )的默认参数 ,那么每个结果都是`infinity`,这是毫无意义的!如果默认参数是`infinity`,则添加任何其他参数将返回该数字——这才是我们想要的结果。

---

### 2. 为什么 0.1 + 0.2 === 0.3 返回 false？

简而言之，这与 JavaScript 在二进制文件中存储浮点数的准确程度有关。如果您在 Google Chrome 控制台中输入以下公式，您将获得：

````JavaScript
0.1 + 0.2
// 0.30000000000000004
0.1 + 0.2  -  0.2
// 0.10000000000000003
0.1 + 0.7
// 0.7999999999999999 ```
````

如果您在不需要高精度的情况下执行简单的方程式，这不太可能导致问题。但是如果你需要测试相等性，它甚至可以在简单的应用程序中引起麻烦。有一些解决方案。

> #### 固定小数点
>
> 例如，如果你知道所需的最大精度（例如，如果你正在处理货币），则可以使用整数类型来存储该值。因此\$4.99 ，您可以存储 499 并执行任何方程式。然后，您可以使用`result = (value / 100).toFixed(2)` 返回字符串的表达式将结果显示给最终用户。
>
> #### 二进制编码的小数
>
> 如果精度非常重要，另一种选择是使用二进制编码的十进制（BCD）格式，您可以使用此`BCD`库在 JavaScript 中访问该格式。每个十进制值分别存储在一个字节（8 位）中。这是低效的，因为一个字节可以存储 16 个单独的值，并且该系统仅使用值 0-9。但是，如果精度对你的应用很重要，那么可能值得权衡。

---

### 3. 为什么 018 减 017 等于 3 ?

`018-017`返回的结果`3`是默认类型转换的结果。在这种情况下，我们谈论的是八进制数。

#### 八进制数简介

你知道在计算中使用二进制（base-2）和十六进制（base-16）数字系统，但是八进制（base-8）在计算机历史中也占有突出地位：在 20 世纪 50 年代后期和 20 世纪 60 年代，它被用来缩写二进制。在高昂的制造系统中削减材料成本！

之后不久就出现了十六进制（base-8）。

#### 八进制数还有用吗？

在现代编程语言中，八进制有用吗？对于某些用例，Octal 比十六进制有优势，因为它不需要任何非数字数字（使用 0-7 而不是 0-F）。

一个常见用途是 Unix 系统的文件权限，其中有八个权限变体：

> 4 2 1
> 0 - - - 无权限
> 1 - - x 仅执行
> 2 - x - 仅写
> 3 - xx 写入并执行
> 4 x - - 仅读取
> 5 x - x 读取并执行
> 6 xx - 读取和写入
> 7 xxx 读取，写和执行

出于类似的原因，它也用于数字显示器。

#### 回到问题

在 JavaScript 中，前缀 0 会将任何数字转换为八进制。但是，8 不会在八进制中使用，并且任何包含 an 的数字 8 都将以静默方式转换为常规十进制数。

因此，018 — 017 实际上相当于十进制表达式 18 — 15 ，因为它 017 是八进制但是 018 十进制。

---

### 4. 函数表达式与函数声明的不同之处是什么？

函数声明使用关键字`function` ，后跟函数的名称。相反，函数表达式以函数名称和赋值运算符开头`var` ，`let`或者`const`后跟函数名称`=` 。这里有些例子：

```JavaScript
// Function Declaration
function sum(x, y) {
 return x + y
}
// Function Expression: ES5
var sum = function(x, y) {
 return x + y
}
//函数表达式：ES6 +
const sum =（x，y）=>{ return x + y }
```

在使用中，关键的区别在于函数声明被提升，而函数表达式则没有。这意味着 JavaScript 解释器将函数声明移动到其作用域的顶部，因此您可以定义函数声明并在代码中的任何位置调用它。相比之下，您只能以线性顺序调用函数表达式：您必须在调用它之前定义它。

如今，许多开发人员更喜欢函数表达式，这有几个原因：

- 首先，函数表达式强制实施更可预测的结构化代码库。当然，结构化代码库也可以使用声明; 它只是声明允许您更容易地摆脱凌乱的代码。
- 其次，我们可以使用 ES6 语法函数表达式：这个一般比较简洁，let 并 const 在一个变量是否可以重新分配提供更多的控制与否，我们将在接下来的问题中看到的。

---

### 5. var，let，和 const 有什么区别？

var 是第一版 JavaScript 中的变量声明关键字。但它的缺点导致在 ES6 中采用了两个新的关键词：let 和 const 。

#### i）分配

最基本的区别是，let 并 var 同时可以重新分配 const 不能。这是 const 不需要更改的变量的最佳选择，它可以防止意外重新分配等错误。注意，const 它允许变量变异，这意味着如果它表示一个数组或一个对象，它们可以改变。您无法重新分配变量本身。

双方 let 并 var 可以重新分配，而是-因为以下几点应明确-  let 超过了显著的优势 var ，使得它在大多数更好的选择，如不及时救治变量需要改变的所有情况。

#### ii）变量提升

类似于函数声明和表达式之间的区别（如上所述），使用声明的变量 var 总是被提升到它们各自范围的顶部，而变量声明使用 const 和 let 被提升，但是如果你在声明之前尝试访问它们，那么你将会出现“暂时死区”错误。这是有用的行为，因为 var 可能更容易出错，例如意外重新分配。请看以下示例：

```JavaScript
var x =“global scope”;
function foo（）{
  var x =“functional scope”
  的console.log（X）
}
FOO（） //“functional scope”
console.log（x） //“global scope”
```

在这里，结果 foo()和 console.log(x)我们期望的一样。但是，如果我们放下第二个 var 呢？

```JavaScript
var x = "global scope"

function foo() {
  x = "functional scope"
  console.log(x)
}

foo(); // "functional scope"
console.log(x) // "functional scope"
```

尽管在函数内定义，但 x = "functional scope"已覆盖全局变量。我们需要重复关键字 var 以指定第二个变量 x 的范围仅限于 foo() 。

#### iii）作用域

虽然 var 是函数作用域的，let 并且 const 是块作用域的：通常，块是花括号内的任何代码{} ，包括函数，条件语句和循环。为了说明差异，请查看以下代码：

```JavaScript
var a = 0
let b = 0
const c = 0

if (true) {
  var a = 1
  let b = 1
  const c = 1
}

console.log(a) // 1
console.log(b) // 0
console.log(c) // 0
```

在我们的条件块，全局作用域 var a 已经被重新定义，但全局范围的 let b 并 const c 没有。一般而言，确保本地分配保持在本地将使代码更清晰，错误更少。

---

### 6. 如果你指定不带关键字的变量会怎样？

如果您在不使用关键字的情况下定义变量会怎样？从技术上讲，如果`x`还没有定义，那么`x = 1`就是简写`window.x = 1` 。这是内存泄漏的常见原因。

为了避免这种情况，你可以使用严格模式（ES5 中引入）。通过在文档顶部或特定函数中编写`use strict`。之后，当你尝试声明没有关键字的变量时，你将收到错误：`Uncaught SyntaxError: Unexpected indentifier` 。

---

### 7. 面向对象编程（OOP）和函数式编程（FP）之间有什么区别？

JavaScript 是一种多范式语言，意味着它支持多种不同的编程风格，包括事件驱动，功能和面向对象。

有许多不同的编程范式，但在当代计算中，两种最流行的样式是函数式编程（FP）和面向对象编程（OOP） - 而 JavaScript 可以同时执行这两种操作。

#### 面向对象编程（OOP）

OOP 基于“对象”的概念。这些是包含数据字段的数据结构 - 在 JavaScript 中称为“属性” - 和“方法”。

一些 JavaScript 的内置对象包括`Math`（用于方法例如`random` ，`max`和`sin`）， `JSON`（用于解析 JSON 数据），和原始数据类型，如`String` ，`Array` ，`Number`和`Boolean` 。

无论何时依赖内置的方法，原型或类，实际上你都在使用面向对象的编程。

#### 函数式编程（FP）

FP 基于“纯函数”的概念，它避免了共享状态，可变数据和副作用。这可能看起来像很多术语，但你可能已经在代码中创建了许多纯函数。

给定相同的输入，纯函数总是返回相同的输出。它没有副作用：除了返回结果之外，这些都是任何东西，例如记录到控制台或修改外部变量。

至于共享状态，这里有一个简单的例子，即状态可以改变函数的输出，即使输入是相同的。让我们设置一个具有两个函数的场景：一个用于将数字加 5，另一个用于乘以 5。

```JavaScript
const num = {
  val：1
}
const add5 =（）=> num.val + = 5
const multiply5 =（）=> num.val * = 5
const multiply5 =（）=> num.val * = 5
```

如果我们 add5 先调用第一个`multiply5`，那么总体结果是`30` 。但是如果我们以相反的方式调用函数并记录结果，我们会得到一些不同的值：`10` 。

这违背了函数式编程的原理，因为函数的结果根据上下文而不同。我们可以重新编写上面的代码，以便结果可预测：

```JavaScript
const num = {
  val：1
}
const add5 =（）=> Object.assign（{}，num，{val：num.val + 5}）
const multiply5 =（）=> Object.assign（{}，num，{val：num.val * 5}
```

现在，`num.val`的值总是`1` ，无关上下文,`add5(num)`或者`multiply5(num)`总是会产生相同的结果。

### 8. 命令式编程和声明式编程之间有什么区别？

我们还可以根据“命令”和“声明”编程之间的区别来考虑 OOP 和 FP 之间的区别。

这些是描述多种不同编程范例之间共享特征的总称。FP 是声明性编程的一个例子，而 OOP 是命令式编程的一个例子。

从基本的意义上讲，命令式编程关注的是你如何做某事。它阐述了最重要的方式，步骤，特点是`for`和`while`循环，`if`和`switch`表达式等等。

```JavaScript
const sumArray = array => {
  let result = 0
  for (let i = 0; i < array.length; i++) {
    result += array[i]
  }
  return result
}
```

与此相反，声明式编程关注的是*要做什么*，它抽象掉了如何依靠表达式。这通常会导致更简洁的代码，但是在规模上，调试会变得更加困难，因为它的透明度要低得多。

以下是`sumArray()`函数的简写：

```JavaScript
const sumArray = array => { return array.reduce((x, y) => x + y) }
```

---

### 9. 什么是基于原型的继承？

最后，我们来了解基于原型的继承。有几种不同风格的面向对象编程，JavaScript 使用的是基于 Prototype 的继承。该系统允许通过使用充当“原型”的现有对象来重复行为。

即使原型的想法对你来说是新的，你也会通过使用内置方法遇到原型系统。例如，使用的功能来操作像`map`，`reduce` ，`splice`等等基于`Array.prototype`的对象的所有方法。事实上，一个数组的每个实例（定义使用方括号[]，或使用 new Array()）继承 Array.prototype ，这就是为什么类似的方法 map ，reduce 并 splice 默认可用。

同样，几乎所有其他内置对象，如`strings`和`booleans`：只有少部分，如`Infinity` ，`NaN` ，`null`和`undefined`没有属性或方法。

在原型链的末端，我们发现`Object.prototype` ，几乎每一个对象在`JavaScript`中是一个 Object.prototype：Array.prototype 和 String.prototype 的实例，它们都继承了 Object.prototype 的属性和方法 。

要使用原型语法向对象添加属性和方法，只需将对象作为函数调用，然后使用 prototype 关键字添加属性和方法：

```JavaScript
function Person() {}
Person.prototype.forename = "John"
Person.prototype.surname = "Smith"
```

#### 我们应该覆盖还是扩展原型的行为？

可以像我们创建和扩展我们自己的原型一样改变内置原型的行为，但是大多数开发人员（以及大多数公司）会建议不要这样做。