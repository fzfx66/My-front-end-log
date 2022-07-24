# JavaScript 的诞生

JavaScript是一种高级的、解释型的编程语言，是一门基于原型、头等函数的语言，是一门多范式的语言，它支持面向对象程序设计，指令式编程，以及函数式编程。它提供语法来操控文本、数组、日期以及正则表达式等，不支持I/O，比如网络、存储和图形等，但这些都可以由它的宿主环境提供支持。

JavaScript被世界上的绝大多数网站所使用，也被世界主流浏览器（Chrome、IE、Firefox、Safari、Opera）支持，使用和学习的人不计其数。JavaScript已然如日中天，但说起他的诞生却颇有戏剧色彩。

1995年前后，网景公司发布了Navigator浏览器0.9版，轰动一时。然而该浏览器海还存在许多不足，网景公司急需一种网页脚本语言，使得浏览器可以与网页互动。

彼时Sun公司向市场推出Java 语言，网景公司动了心，决定与Sun公司结盟。网景公司把编写新语言的任务交给布兰登（Brendan Eich），并要求未来的脚本语言必须"看上去与Java足够相似"，但是比Java简单，使得非专业的网页作者也能很快上手。布兰登不喜Java，为了应付公司安排的任务，他只用10天时间就把设计出了Javascript。

JS的设计思路如下：
1. 借鉴C语言的基本语法；
2. 借鉴Java语言的数据类型和内存管理；
3. 借鉴Scheme语言，将函数提升到"第一等公民"（first class）的地位；
4. 借鉴Self语言，使用基于原型（prototype）的继承机制。

因此，Javascript语言实际上是两种语言风格的混合产物----（简化的）函数式编程+（简化的）面向对象编程。这是由Brendan Eich（函数式编程）与网景公司（面向对象编程）共同决定的。

多年以后，Brendan Eich仍然不喜Java，乃至对JavaScript也不喜欢。"与其说我爱Javascript，不如说我恨它。它是C语言和Self语言一夜情的产物。十八世纪英国文学家约翰逊博士说得好：'它的优秀之处并非原创，它的原创之处并不优秀。'（the part that is good is not original, and the part that is original is not good.）"

##  Javascript的十个缺陷

### 一、为什么Javascript有设计缺陷？
1.	设计阶段过于仓促、
2.	没有先例
3.	过早的标准化

### 二、Javascript的10个设计缺陷
1.	不适合开发大型程序（没有名称空间，难以模块化）
2.	非常小的标准库
3.	null和undefined（在编程实践中，null几乎没用，根本不应该设计它。）
4.	全局变量难以控制

    Javascript的全局变量，在所有模块中都是可见的；任何一个函数内部都可以生成全局变量，这大大加剧了程序的复杂性。
5.	自动插入行尾分号
6.	加号运算符（+号作为运算符，有两个含义，可以表示数字与数字的和，也可以表示字符与字符的连接。）
7.	NaN
8.	数组和对象的区分
由于Javascript的数组也属于对象（object），所以要区分一个对象到底是不是数组，相当麻烦。
9.	== 和 ===

    ==用来判断两个值是否相等。当两个值类型不同时，会发生自动转换，得到的结果非常不符合直觉。因此，推荐任何时候都使用"==="（精确判断）比较符。
10.  基本类型的包装对象

Javascript有三种基本数据类型：字符串、数字和布尔值。它们都有相应的建构函数，可以生成字符串对象、数字对象和布尔值对象。

### 三、如何看待Javascript的设计缺陷？

回答是Javascript并不算糟糕，相反它的编程能力很强大，前途很光明。首先，如果遵守良好的编程规范，加上第三方函数库的帮助，Javascript的这些缺陷大部分可以回避。

其次，Javascript目前是网页编程的唯一语言，只要互联网继续发展，它就必然一起发展。目前，许多新项目大大扩展了它的用途，node.js使得Javascript可以用于后端的服务器编程，coffeeScript使你可以用python和ruby的语法，撰写Javascript。

---

## 参考：
* 维基百科——JavaScript
* Javascript的10个设计缺陷（作者：阮一峰  2011年6月30日）
  
  http://www.ruanyifeng.com/blog/2011/06/10_design_defects_in_javascript.html

* Javascript诞生记（作者：阮一峰  2011年6月24日）
  
  http://www.ruanyifeng.com/blog/2011/06/birth_of_javascript.html
