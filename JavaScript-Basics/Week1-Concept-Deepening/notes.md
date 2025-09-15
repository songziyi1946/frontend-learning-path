## 本周核心概念笔记

1. 类型转换

- typeof 区分数据类型：number string boolean object function undefined，返回一个字符串表示基本类型
- 显示类型转换
  Number(mix)：undefined - NaN, null - 0, '123abc' - NaN
  parseInt(string, radix) 转换成整型，从数字位开始一直到非数字位截止；还可以有一个radix参数，表明以目标进制为基底转换成10进制
  parseFloat(string)
  String(mix)
  Boolean()
  toString(radix)：undefined 和 null 不能使用 toString()；以十进制转换为目标进制的过程
- 隐式类型转换
  isNaN()：Number()->NaN，'123' - false, 'abc' - true
  ++/-- +/-（一元正负）：先使用Number()转成数字，再加或减
  +加号：String()
  -*/%：Number()
  && || !：Boolean()
  < > <= >=：Number()
  == !=：Boolean()
- 不发生类型转换（绝对性）
  === !===
- instanceof、Object.prototype.toString 区别：https://juejin.cn/post/7197990402720235576
  instanceof 检测一个对象是否是某个特定构造函数的实例，检查对象的原型链，返回一个布尔值
  Object.prototype.toString 
