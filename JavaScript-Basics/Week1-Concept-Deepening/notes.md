# 本周核心概念笔记

## 类型转换

- **typeof 区分数据类型**：number string boolean object function undefined，返回一个字符串表示基本类型
- **显示类型转换**
  - Number(mix)：undefined - NaN, null - 0, '123abc' - NaN
  - parseInt(string, radix) 转换成整型，从数字位开始一直到非数字位截止；还可以有一个radix参数，表明以目标进制为基底转换成10进制
  - parseFloat(string)
  - String(mix)
  - Boolean()
  - toString(radix)：undefined 和 null 不能使用 toString()；以十进制转换为目标进制的过程
- **隐式类型转换**
  - isNaN()：Number()->NaN，'123' - false, 'abc' - true
  - ++/-- +/-（一元正负）：先使用Number()转成数字，再加或减
  - +加号：String()
  - -*/%：Number()
  - && || !：Boolean()
  - < > <= >=：Number()
  - == !=：Boolean()
- **不发生类型转换（绝对性）**：=== !===
- **instanceof、Object.prototype.toString 区别**：https://juejin.cn/post/7197990402720235576
  instanceof 检测一个对象是否是某个特定构造函数的实例，检查对象的原型链，返回一个布尔值
  Object.prototype.toString

## 函数

- **函数定义方式（2种）**：函数声明和函数表达式 
  - 命名函数表达式
  ```javascript
  var test = function abc(){
    console.log('a');
  }
  ```
  - 匿名函数表达式
  ```javascript
  var demo = function(){
    console.log('b');
  }
  ```
  *以上两个函数唯一的区别在于，test.name为"abc"，demo.name为"demo"，所以一般使用第二种匿名函数表达式的方式定义函数）*
- **形参和实参**：形式参数就是函数声明时括号内的，实际参数则是函数调用时传入其中的具体数据
  - 形参和实参个数可以不相等，不会报错
  - arguments是实参列表，里面存放实参
  - 形参和实参有一个映射关系，形参数值发生变化，实参也会变化，反之亦然；但是如果两者的个数不一致，比如实参比形参少，那多出来的形参或者实参就不映射了
  ```javascript
  function demo(a, b){
    b = 2
    console.log(arguments[1]) // undefined
  }
  demo(1)
  ```

## 递归
- **找规律**
- **找出口**

## JS运行分三步
- **语法分析**：先通篇扫描一遍，检查是否有低阶语法错误
- **预编译**：
  - 函数声明整体提升
  - 变量 声明提升（提升也可以理解为预先编译）
  - 预编译前奏：imply global 暗示全局变量：即任何变量，如果变量未经声明就赋值，此变量就为全局对象 window 所有；一切声明的全局变量，全是 window 的属性
  ```javascript
  function test(){
    // 赋值语句从右向左，123先赋值给b，然后声明一个变量a，将b的值赋给a
    // 此时a为局部变量，b未声明，window.b为123，window.a为undefined
    var a = b = 123; 
  }
  test()
  ```
  - 预编译四部曲：预编译发生在函数执行的前一刻
  1. 创建AO对象 Activation Object（执行期上下文）
  2. 找形参和变量声明，将变量和形参名作为AO的属性名，值为undefined
  3. 将实参值和形参统一
  4. 在函数体里面找函数声明，值赋成函数体
- **解释分析**

## 作用域
- **可访问属性**: fn.name，fn.prototype
- **不可访问属性**：[[scope]]由这个函数产生所产生的作用域，是个隐式的属性，仅供javascript引擎存取；它是**执行期上下文对象的链式集合**，这种链式链接叫**作用域链**。
- **执行期上下文（AO）**：当函数执行时，也可以理解为函数执行的前一刻，会创建一个执行器上下文的对象（AO）；函数每次执行时对应的执行上下文都是独一无二的，所以多次调用一个函数会导致创建多个执行上下文，当函数执行完毕时，所产生的执行上下文被销毁。
- **作用域链中的具体存储**：函数在被定义时，[[scope]]链中只有一个，存储的是GO（为什么是GO？存储的是函数所在环境的执行上下文，函数在全局中，所以存储的是GO），当它被执行时，会产生一个AO对象，插在GO之前
- **查找变量**：在哪个函数中查找变量，就去哪个函数的作用域链中从顶端依此向下查找.

## 闭包
- **定义**：内部函数被保存到外部，就是闭包
- **危害**：闭包导致原有作用域链不释放，造成内存泄露
- **作用**：
  - 实现公有变量：函数累加器
  ```javascript
  function a(){
    var count = 0;
    function demo(){
      count ++;
      console.log(count);
    }
    return demo;
  }
  var counter = a()
  counter();
  counter();
  counter();
  counter();
  counter();
  ```
  - 做缓存（存储结构）
  ```javascript
  function fn(){
    var food = "";
    var obj = {
      eat: () => {
        console.log('I am eating '+ food);
        food = "";
      },
      push: (newFood) => {
        food = newFood;
      }
    }
    return obj;
  }
  var eater = fn();
  eater.push('apple');
  eater.eat();
  ```
  - 可以实现封装，属性私有化
  
  - 模块化开发，防止污染全局变量

## 立即执行函数
- **格式**：此函数没有声明，一次执行完立即被销毁
```javascript
  (function (a, b, c){
    console.log(a + b + c)
  }(1, 2, 3))
```
  - 只有表达式才能被执行符号执行
  ```javascript
  function test(){
    var a = 123;
  }(); // 报错

  var test = function () {
    console.log('a')
  }(); // a
  // 如果在之后打印 test，test 为 undefined
  ```
  - 函数表达式立即执行后，会丢失函数的名字


