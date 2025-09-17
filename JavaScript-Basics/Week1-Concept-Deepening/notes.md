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

