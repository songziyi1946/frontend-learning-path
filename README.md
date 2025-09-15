# frontend-learning-path 前端学习代码汇总

## 总览
- **9月-10月初**：JavaScript基础（4周）
- **10月-11月初**：Webpack配置（4周）
- **11月-12月底**：React基础（7周，含实战巩固）

---

## 第一阶段：JavaScript基础（4周）
目标：巩固核心概念、异步编程、ES6+、原型链等，避免“一看就会，一写就废”。

### 第1周：核心概念深化
- **周一至周三**：变量类型、类型转换、深浅拷贝、内存管理
  - 重点：`typeof`/`instanceof`/`Object.prototype.toString`区别，手写深拷贝
- **周四至周五**：作用域、闭包、`this`指向
  - 重点：闭包应用场景（防抖节流、模块化），`this`在不同场景下的值
- **周末**：练习手写题（防抖、节流）、总结笔记

### 第2周：面向对象与原型
- **周一至周三**：原型链、继承（组合继承、Class继承）
  - 重点：手写new、手写继承、理解`__proto__`与`prototype`
- **周四至周五**：事件循环（Event Loop）
  - 重点：宏任务/微任务顺序，结合Promise、setTimeout分析输出题
- **周末**：刷事件循环面试题（如：https://github.com/lydiahallie/javascript-questions）

### 第3周：异步编程与ES6+
- **周一至周三**：Promise（手写Promise.all、Promise.race）、async/await
  - 重点：错误处理、异步代码优化
- **周四至周五**：ES6+特性（解构、模块化、箭头函数、Set/Map）
- **周末**：实战：用Promise封装Ajax请求，模拟异步流程

### 第4周：JS进阶与复习
- **周一至周三**：模块化（CommonJS/ES Module区别）、垃圾回收机制
- **周四至周五**：复习薄弱点，刷算法题（数组/字符串操作，如手写map、filter）
- **周末**：模拟面试（自测JS基础题，如https://bigfrontend.dev/）

---

## 第二阶段：Webpack配置（4周）
目标：理解构建流程、常用配置优化、插件原理。

### 第5周：基础配置与原理
- **周一至周三**：核心概念（Entry/Output/Loader/Plugin）、手写简单webpack
- **周四至周五**：常见Loader（babel-loader、css-loader、file-loader）配置
- **周末**：从零配置一个支持ES6+SCSS的webpack项目

### 第6周：性能优化
- **周一至周三**：代码分割（SplitChunksPlugin）、懒加载、Tree Shaking
- **周四至周五**：缓存（hash/chunkhash）、压缩（TerserPlugin）、Bundle分析
- **周末**：优化现有项目的构建速度与体积（使用speed-measure-webpack-plugin）

### 第7周：高级特性与插件
- **周一至周三**：Plugin原理（手写一个Plugin）、HMR原理
- **周四至周五**：环境变量配置（env）、多页面应用打包
- **周末**：尝试配置微前端架构下的webpack（可选）

### 第8周：复习与实战
- **周一至周三**：对比Vite/Rollup，理解webpack的优缺点
- **周四至周五**：复习配置项，整理常见面试题（如：loader和plugin区别）
- **周末**：自测：从零搭建一个支持React+TypeScript的webpack项目

---

## 第三阶段：React基础（7周）
目标：掌握核心概念、Hooks、状态管理、常见优化。

### 第9周：基础概念与JSX
- **周一至周三**：组件生命周期（类组件+函数组件）、JSX原理
- **周四至周五**：组件通信（父子、兄弟、跨级Context）
- **周末**：实战：搭建一个TodoList（类组件+函数组件两种写法）

### 第10周：Hooks深入
- **周一至周三**：useState/useEffect/useCallback/useMemo
  - 重点：依赖项优化、闭包陷阱
- **周四至周五**：useRef/useContext/自定义Hook
- **周末**：用Hooks重构TodoList，自定义useLocalStorage Hook

### 第11周：状态管理与路由
- **周一至周三**：Redux（Redux Toolkit）、MobX（选学）
- **周四至周五**：React Router配置（路由守卫、懒加载）
- **周末**：实战：给TodoList添加路由和状态管理

### 第12周：性能优化
- **周一至周三**：React.memo、useMemo、useCallback避免重复渲染
- **周四至周五**：虚拟DOM、Diff算法原理、Fragment/Portals
- **周末**：用React DevTools分析项目性能，优化组件渲染

### 第13周：进阶与原理
- **周一至周三**：Fiber架构、并发模式（Suspense、useTransition）
- **周四至周五**：手写简易React（渲染JSX、更新机制）
- **周末**：阅读React官方文档核心章节（https://react.dev/）

### 第14周：实战项目
- **整周**：开发一个中型项目（如博客系统、后台管理）
  - 要求：使用Hooks+Redux Toolkit+React Router+Webpack

### 第15周：复习与面试准备
- **周一至周三**：整理React常见面试题（如：虚拟DOM优缺点、Hooks原理）
- **周四至周五**：复盘项目难点，总结优化策略
- **周末**：模拟面试（React+JS+Webpack综合问题）
- **求助社区**：遇到问题优先StackOverflow或掘金，避免卡壳。
- **调整节奏**：若某周进度滞后，适当延长1-2天，但尽量按计划执行。
