## 第二章 语法

1.  /* */ 注释的内容，如果其中有正则相关的符号，是可能使得注释提前结束导致报错的

   如 `/* var rm_a =/a*/.match(s);` ①

2. > JavaScript 不允许对象字面量中，或者用点运算符提取对象属性时，使用保留字作为对象的属性名

   目前的 JavaScript 版本已经支持了 ① 

3. 数字字面量若有指数部分，则这个字面量的值为 e 之前的数字与 10 的 e 之后的数字的次方相乘

   如 `100 = 1e2` ②

4. JavaScript 在被创建的时候，Unicode 是一个 16 位的字符集，所以 JavaScript 中所有的字符都是 16 位的 ②

5. false, null, undefined, 空字符串, 0, NaN 为假值（falsy），其他都为真 ①

6. JavaScript 不允许在 return 关键字与表达式之间换行 ①

   [^boen]: 是因为自动插入分号作祟

   

   ```js
   // bad:
   function a(){
     return
     {
       b: 1
     }
   }
   
   // good:
   function a(){
     return {
       b: 1
     }
   } 
   ```

7. JavaScript 中的 % 是求余，与通常数学意义下的模运算有不同，在两个运算符是正数的情况下，求模与求余结果相等，负数反之 ②

## 第三章 对象

1. 对象通过引用来传递，永远不会被复制 ①
2. for in 对象时的顺序是不固定的 ①
3. delete 运算符 只会删除对象自身的属性，不会删除原型链上的 ②

## 第四章 函数

1. 每个函数对象在创建时也会有一个 prototype 属性。它的值是一个拥有 constructor 属性且值为这个函数的对象 ③

2. 调用一个函数会暂停当前函数的执行，传递控制权和参数给新函数 。除了声明时定义的形式参数，每个函数还接收两个附加的参数：this 和 arguments ②

3. 四种调用模式

   1. 方法调用

      一个函数被保存为一个对象的属性时，称它为方法，当一个方法被调用时，this 被绑定到该对象 

   2. 函数调用

      以此模式调用函数时，this 被绑定到全局对象

   3. 构造器调用

      一个函数使用 new 来调用时，会创建一个新对象，将函数放到其原型上，此时函数中的 this 指代的新对象

      [^boen]: 新对象的 \_\_proto\_\_ 属性就指向喊函数的 prototype

   4. Apply 调用

      通过 apply 方法或者 call 显式的指定调用函数的 this

      ③

4. 函数 new 调用时，如果返回值不是一个对象，就会返回上述规则产生的新对象 ②

5. > 一些语言提供了尾递归优化······遗憾的是，JavaScript 当前并没有提供尾递归优化

   当前最新已提供，参见：[阮一峰-ES6](<http://es6.ruanyifeng.com/#docs/function#%E5%B0%BE%E8%B0%83%E7%94%A8%E4%BC%98%E5%8C%96>) ③

6. > 大多数类 C 语言都有块级作用域······糟糕的是，尽管 JavaScript 的代码块语法貌似支持块级作用域，但实际上 JavaScript 并不支持

   ES6 已支持 ①

7. 一个函数能访问它被创建时所处的上下文，被称为闭包 ②

8. 一个对象里的方法在调用完成时返回对象（this）本身，既能达成级联的效果，也被称为链式调用 ①

9. [函数的柯里化](<https://juejin.im/entry/58b316d78d6d810058678579>) ②

10. [函数的记忆（memoization）](<https://juejin.im/post/59af56a96fb9a0248f4aadb8>) 利用闭包通过对函数参数和执行结果的缓存，减少函数的运算次数  ② 

## 第五章 继承

此章主要以各种技巧去使用函数，去扩展函数的功能或职责，但在 es6 中有更多更方便的方式达到相同目的，所以只需理解其为何如此设计即可

## 第六章 数组

1. 数组是一段线性分配的内存，它通过整数计算偏移并访问其中的元素 ，但在 JavaScript 中没有此类数据结构。作为替代，JavaScript 中提供的是类数组的对象，把数组的下标转成字符串并用其作为属性 ①
2. 数组的常用内置方法都储存在 Array.prototype 中 ①

## 第七章 正则表达式

1. `(?:)` 表示非捕获性分组，`()`表示捕获性分组。捕获性分组会将匹配的字符串放置到最后的结果数组中

   [相关文章](<https://blog.csdn.net/lihefei_coder/article/details/53022253>) ③

2. 正则表达式标识：

   1. g 全局的，匹配多次
   2. i 大小写不敏感
   3. m 多行匹配

   [^boen]: es6 新增标识符 [见阮一峰的书籍](<http://es6.ruanyifeng.com/#docs/regex#u-%E4%BF%AE%E9%A5%B0%E7%AC%A6>)  ①

3. 匹配次数的量词形式如：

   1. {3} 匹配三次
   2. {3, 6} 匹配三到六次
   3. {3, } 匹配三次或更多
   4.  ? 号 等于 {0, 1}  *号等于 {0, }  +号等于 {1, }  ②

## 第八章 方法

1. [array 内置方法](<https://segmentfault.com/a/1190000011467723#articleHeader7>)  [ES6 新增的](<http://es6.ruanyifeng.com/#docs/array>) ④
2. [ function 的 apply 和 call](<https://github.com/lin-xin/blog/issues/7>) ③
3.  number.toFixed() 保留指定位数小数常用 ②
4. 正则对象内置常用有 exec 与 test，前者返回匹配结果的数组或 null 后者返回一个布尔值 ②
5. string内置的 match 方法，参数是一个正则表达式，执行结果与上一条中的 exec 一致 。此外 string 内置的 replace 和 search 都与正则相关②
6. [string 内置方法](<https://segmentfault.com/a/1190000011467723#articleHeader19>)  [ES6 新增的](<http://es6.ruanyifeng.com/#docs/string-methods>) ③

## 第九章 代码风格

[更适合的文章](<http://es6.ruanyifeng.com/#docs/style>)

## 第十章 优美的特性

无笔记

## 附录 A 毒瘤

1. Unicode 

   JavaScript 设计之初，Unicode 预计最多会有 65536 个字符，但那以后它的容量慢慢增长到一百多万个 

   剩下的百万字符，都可以用这六万多个两两组队表示

   Unicode 把一对字符也视为单一的，但 JavaScript 却认为是两个不同的字符 

2. > parseInt 解析的字符串第一位是 0 的话，会基于八进制而不是十进制，除非明确加上第二个参数表示进制

   最新的处理方式已变更：如果省略该参数或其值为 0，则数字将以 10 为基础来解析。如果它以 “0x” 或 “0X” 开头，将以 16 为基数。

## 附录 B 糟粕

1. 避免使用 with 和 eval

2. 移除循环中的 continue 可以改善性能

   [^boen]: 半信半疑

## 附录 C JSLint

此目录 为介绍 JSLint 的广告

## 附录 D 语法图

天书

## 附录 E JSON

