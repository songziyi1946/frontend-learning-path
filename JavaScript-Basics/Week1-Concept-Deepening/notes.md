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
  ```javascript
   var inherit = (function(){
      var F = function (){}; // 过渡函数
      return function (Target, Origin){ // 在这里会形成闭包，F就变成私有化变量
        F.prototype = Origin.prototype;
        Target.prototype = new F(); 
        Target.prototype.constructor = Target;
        Target.prototype.uber = Origin.prototype;
      }
   }());
  ```
  - 模块化开发，防止污染全局变量
  ```javascript
  var name = 'abc';
  var init = (function(){
    var name = '123';

    function callName(){
      console.log(name);
    }
    return function(){
      callName();
    }
  }());
  init(); // '123'
  ```
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

## 对象
- **对象的创建方法**：
  - var obj = {}：plainObject 对象字面量/对象直接量
  - 构造函数：
    1）系统自带的构造函数：new Object()
    2）自定义构造函数（大驼峰式命名规则）
      - new 关键字：在函数体最前面隐式的加上 *var this = {}*；执行 *this.xx = xxx*；隐式的返回 *return this*
      <mark>可以在自定义构造函数中显式的返回一个对象，但不可以返回原始值，否则 new 会自动用 this 代替<mark>
- **原型**：原型是function对象的一个属性，定义了构造函数制造出的对象的公共祖先。通过该构造函数产生的对象，可以继承该原型的属性和方法。原型也是一个对象。
```javascript
// Person.prototype -- 原型
// Person.prototype = {} 是祖先
Person.prototype.name = 'szy';
function Person () {}
var person = new Person(); // 打印 person，是一个Person的空对象 
```
  - 提取共有属性
  - constructor 构造器
  ```javascript
  function Car(){}
  var car = new Car();
  console.log(car.constructor); // 继承 Car.prototype 原型中的 constructor，这个 constructor 指向 function Car(){} 构造函数
  ```
  - 原型链 __proto__
  ```javascript
  function Father () {
    this.money = {
      card:'visa'
    }
  }
  function Son () {}
  var son = new Son();
  console.log(son.money); // { card: 'visa' }
  son.money = { card: 'master' };
  console.log(son.money); // { card: 'master'}
  console.log(father.money); // { card: 'visa'}
  ```
  - 绝大多数对象的最终都会继承自Object.prototype，为什么不是全部对象呢？因为如果是使用Object.create(null)，这样创建出来的对象，是没有__proto__属性的
  ```javascript
  var obj = {};
  // obj.__proto__ == Object.prototype
  ```
  - Object.create(原型)：对象或者null都可以
- **call/apply**：改变this指向。
  - 两者区别：穿参列表不同（call 需要把实参按照形参的个数传进去，apply 需要传一个arguments）
  ```javascript
  function Person(name, age){
    this.name = name;
    this.age = age;
  }
  function Student(name, age, grade){
    Person.call(this, name, age);
    this.grade = grade;
  }
  var stu = new Student();
  ```
  *如何实现链式调用模式（模仿jQuery）: 在一个函数的方法中使用 return this*
  ```javascript
  var obj = function(){
    eat: function(){
      console.log('Eating');
      return this;
    },
    smoke: function(){
      console.log('Smoking');
      return this;
    },
    drink: function(){
      console.log('Drinking');
      return this;
    },
    sleep: function(){
      console.log('Sleeping');
      return this;
    }
  }
  obj.eat().smoke().drink().sleep();
  ```
- **对象的枚举**：
  - for..in：遍历对象的属性
  - hasOwnProperty：判断属性是否是对象自己的方法
  - in：判断这个对象上是否有这个属性，不管是在对象自身的方法上，还是原型链上
  - A instanceof B：A对象的原型链上有没有B的原型
  
## 继承模式 extends
- **借用构造函数**：
  - 不能继承借用构造函数的原型
  - 每次构造函数都要多走一个函数
```javascript
function Person(name, age, sex){
  this.name = name;
  this.age = age;
  this.sex = sex;
}

function Student(name, age, sex, grade){
  Person.call(this, name, age, sex);
  this.grade = grade;
}

var student = new Student();
```
- **共有原型**：缺点是Son上无法添加独属于自己的属性
```javascript
function Father(){}
Father.prototype.lastName = 'Li';
function Son(){}
function inherit(Target, Origin){
  Target.prototype = Origin.prototype;
}
inherit(Son, Father);
var son = new Son();
```
- **圣杯模式**：
```javascript
function inherit(Target, Origin){
  function F (){}
  F.prototype = Origin.prototype;
  Target.prototype = new F();
  Target.prototype.constructor = Target;
  Target.prototype.uber = Origin.prototype;
}
Father.prototype.lastName = 'Li';
function Father(){}
function Son(){}
inherit(Son, Father);
var son = new Son();
var father = new Father();
```


