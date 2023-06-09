# this指向
普通的function函数，this指向Window，严格模式下指向undefined；
对象中的方法（不能是箭头函数）中，this指向该对象；
new 构造函数（不能是箭头函数）中，this指向实例对象；
HTML 事件函数（不能是箭头函数）中，this 指向了接收事件的 HTML 元素；
call，apply，bind可以显示绑定this，指向当前环境的this
箭头函数没有this，会沿着作用域链向上查找this，直到找到为止。他会捕获自己在定义时（不是调用时），外层环境的this。


# 词法作用域【https://zh.javascript.info/closure#ci-fa-huan-jing】

javascript 采用的是静态作用域

1. 词法环境 Lexical Environment
   环境记录 Environment Record ：一个存储所有局部变量作为其属性(如 this)的对象（一个特数据的内部对象，局部变量是他的一个属性，“获取或修改变量”意味着“获取或修改词法环境的一个属性”）
   对外部词法环境的引用 outer

1.1 变量 
【一个“变量”】只是 【环境记录】 这个特殊的内部对象的一个【属性】,与当前正在执行的（代码）块/函数/脚本有关。
操作变量实际上是操作该对象的属性。

1.2 函数声明
不同之处在于函数声明的初始化会被立即完成。（这种行为仅适用于函数声明，而不适用于我们将函数分配给变量的函数表达式，例如 let say = function(name)）
【可以在声明自身之前调用一个以函数声明】

1.3 内部和外部的词法环境 Lexical Environment of the call
在一个函数运行时，在调用刚开始时，会自动创建一个[新的词法环境]以存储这个调用的局部变量和参数。
内部->外部的词法环境->全局词法环境
  ``` javascript
  let phrase = "hello"
  function say(name) {
    console.log(`${phrase}, ${name}`); // lexical Environment of the call : [name]:John -> outer:[say]: function, [phrase]: "Hello" -> null
    // 当代码要访问一个变量时 —— 首先会搜索内部词法环境，然后搜索外部环境，然后搜索更外部的环境，以此类推，直到全局词法环境。
  }
  ```

1.4 返回函数

``` javascript
function makeCounter() {
  let count = 0;

  return function() {
    return count++;
  };
}

let counter = makeCounter();
```

所有函数都有名为 [[Environment]] 的隐藏属性，该属性保存了对创建该函数的词法环境的引用。
JavaScript 中的函数会自动通过隐藏的 [[Environment]] 属性记住创建它们的位置，所以它们都可以访问外部变量。
当调用 counter() 时，会为该调用创建一个新的词法环境，并且其外部词法环境引用获取于 counter.[[Environment]]
函数记住它创建于何处的方式，与函数被在哪儿调用无关。[[Environment]] 引用在函数创建时被设置并永久保存。

---
# 闭包

  闭包 是指一个函数可以记住其外部变量并可以访问这些变量。
  ！！！！！！！new Function除外，new Function 创建一个函数，那么该函数的 [[Environment]] 并不指向当前的词法环境，而是指向全局环境。

---
- 垃圾回收

---
- 函数对象
```javascript
// name
// length
// 属性
function sayHi(){}
sayHi.counter = 0 //属性与变量不同
```
---
# 动态作用域 （bash）

# 执行上下文

execution context stack

```
  ECStack = [
    globalContext
  ];
```
1. 变量对象(Variable object，VO)
2. 作用域链(Scope chain)
3. this

# 变量对象
1. 全局上下文中的变量对象就是全局对象
2. 函数上下文 AO

# 作用域链
https://zh.javascript.info/closure

