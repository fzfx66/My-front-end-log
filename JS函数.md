**函数对象：**

function fn(x,y){return x+y}

let fn =(x,y) =>x+y

let fn = new Function(‘x’,’y’,’return x+y’)

自身属性：‘name’，‘length’

共有属性：‘call’，‘apply’，‘bind’

函数是对象，所有函数都是Function构造的。

四种方式定义函数：

具名函数： function 函数名(形参1，形参) {语句 return 返回值}

匿名函数：let a = function(x,y){return x+y}

let a = function fn(x, y){return x+y}

fn(1,2)  //报错，fn不存在，fn作用范围只在上句等号右边

箭头函数：

let f1 = x => x*x 

let f2 = (x,y) => x+y  （两个变量）

let f2 = (x,y) => {return x+y}  （加了花括号，里面要加return）

let f4 = (x,y) => ({name:x , age :y})（直接返回对象会出错，加圆括号）

构造函数（基本没人用）：

let f = new Function(‘x’,’y’,’return x+y’)  （不知为何会报错）

函数自身（fn）与函数调用（ fn() ）
```
let fn = () => console.log(‘hi’)
let fn2 = fn
fn2()   //可以打印出hi
```
解释上述代码：fn保存了匿名函数的地址，这个地址被复制给了fn2，fn2()调用了匿名函数，fn和fn2都是匿名函数的引用而已，真正的函数既不是fn也不是fn2。

调用时机：
```
let I =0
for (i=0;i<6;i++){
setTimeout(()=> {console.log('hi')},0) } //打印出6个6
for (let i=0;i<6;i++){
setTimeout(()=> {console.log('hi')},0) }  //打印出0，1，2，3，4，5
（JS在for和let一起用的时候会加东西，每次循环会多创建一个i）
```
function fn(){ let a = 1} consule.log(a)  //a不存在，因为a作用域仅在{}

全局变量和局部变量：在顶级作用域声明的变量是全局变量，window的属性是全局变量，其他都是局部变量。 

e.g  window.变量名 ，该语句无论是全局环境还是函数内部，声明的该变量都是全局变量（不知为何实行不来）。

函数可嵌套，作用域也可嵌套。 如果多个作用域有同名变量a，那么查找a的声明时，就向上取最近的作用域（找{），即就近原则。

查找a的过程与函数执行无关，但a的值有函数执行有关（查找执行函数之前最近作用域的a的声明）。与函数执行无关的作用域称静态作用域。

如果一个函数用到了外部的变量，那么这个函数加这个变量就叫做闭包。下述 a=2 f3()就组成了闭包。
```
function f2(){ let a = 2 
function f3(){
console.log(a)
} a = 22 
f3()  }    //打印出22
```

JS传参分为值传递和地址传递。形参可认为是变量声明，形参可多可少。实参传递给形参的过程可看作是把分配给形参的内存的地址拷贝给实参（？可能为反）

所有函数都有返回值，只有函数有返回值，函数执行完了才会返回。没写return的函数的返回值是undefined。

function hi(){return console.log(‘hi’)}

hi()  // 返回值为console.log(‘hi’)的值，即undefined 。

**调用栈**：JS引擎在调用一个函数前，需要把函数所在的环境push到一个数组里，这个数组叫做调用栈，等函数执行完了，就会把环境弹（pop）出来，然后return到之前的环境，继续执行后续代码。

阶乘： 用递归函数：function f(n) {return n !=== 1 ? n*f(n-1) :1}  

（递归：先递进再回归，递进的过程就是压栈的过程，回归的过程就是弹栈的过程。）

爆栈：如果调用栈中压入的帧过多，程序就会崩溃。(10000-15000)

**函数提升：**

什么是函数提升：function fn(){} ,不管你把具名函数声明在哪里，它都会跑到第一行；

什么不是函数提升：let fn=function(){} ,这是赋值，右边的匿名函数声明不会提升。

__arguments 和this ：__

每个函数都有，除了箭头函数。

如果不传任何参数，this默认指向window。如果不加 use stict JS会尽量把你传的东西生成对象。

代码： function fn() {console.log(arguments), console.log(this)}

如何传递arguments：调用fn即可传arguments，fn(1,2,3)那么arguments就是[1,2,3]伪数组。

如何传this：目前可以用fn.call(xxx.1,2,3)传this和arguments，而且xxx会被自动转化成对象。（JS的糟粕）

this是隐藏参数，arguments是普通参数，

假设没有this：

代码：let person {name:’frank’, sayHi(){console.log(‘你好，我叫’+person.name)} }

我们可以用直接保存了对象地址的变量获取‘name’ ，这种方法叫做引用。

根据原型创建类时，这时类对应的对象还未声明，但我们在创建类时常常需要将来要创建的对象的参数（如name等），如何获取还未存在的对象的参数呢？可以用一个泛式的名字来指定我们将来要获取的参数，类似形式参数。
```
e.g class Person{
constructor(name){
 this.namee = name }   //这里的this是new强制指定的
sayHi() {console.log(???)} }
```
我们想让函数获取对象的引用，但是并不想通过变量名做到，Python通过额外的self参数做到，JS通过额外的this做到。this就是将来调用sayHi的对象。

person.sayHi()会把person自动传给sayHi，sayHi可以通过this引用person 。

两种调用方法：应该学习哪种？学习大师调用法，默认使用大师调用法。

小白：person.sayHi() ，自动把person传到函数里，作为this；

大师调用法：person.sayHi.call(person)，手动把person传到函数里，作为this。



this的两种使用方法： 隐式传递和显式传递：

fn(1,2)  //等价于fn.call(underfined,1,2)  or fn.apply(underfined,[1,2])

obj.child.fn(1)  //等价于obj.child.fn.call(obj.child, 1)

**this绑定**：

使用 .bind可以让this不被改变；并且bind还可以绑定其他参数。

function f1(p1,p2){console.log(this,p1,p2)}

let f2 = f1.bind({name:’frank’})   

// f2就是f1绑定this之后的新函数，f2()等价于f1.call({name:’frank’})

箭头函数没有this和arguments，this对于箭头函数只是普通的参数，里面的this就是外面的this，就算加call也没用。

e.g fn.call({name:’frank’})  ///window

**立即执行函数**： ES5时代，为了得到局部变量，必须引入一个函数，但如果这个函数有名字就得不偿失，于是这个函数必须是匿名函数，声明匿名函数，然后在匿名函数前加个运算符，推荐用  ！ 。
