---
date: 2019-05-05
cover: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1588050593598&di=93a1337c9cc7403816253ba76c3786b0&imgtype=0&src=http%3A%2F%2Fku.90sjimg.com%2Felement_origin_min_pic%2F00%2F85%2F77%2F1956e9e3afe5091.jpg
---

# 基础语法

## 学习目标


* 了解


  - 回顾js基础  变量/数据类型/顺序结构/数组
  - 构造函数创建对象存在的问题

* 重点

  * 知道函数有原型对象

  * 构造函数,原型对象和实例三者的关系

  * 原型链

  * 会给内置的对象添加自定义的方法

  * 会使用更简单的原型使用方式

    

## 1. 回顾

### 1.1 作用域: 

####1.1.1 全局作用域

整个js执行的环境就是一个全局作用域

####1.1.2 局部作用域

es5规范中: 只有函数才能构成一个局部作用域

####1.1.3 作用域链

将js执行时变量查找的方式,以链式形式表示出来

```javascript
var num = 0;
function fn(){
    var num1;
    num1 = 1;
    console.log(num1);
    function fnSon(){
        var num2 = 2;
        console.log(num2)
        console.log(num1)
    }
}
```

将上面的代码用链式的形式展示出来


### 1.2 词法作用域规则

> 词法作用域又叫静态作用域. 

- 作用域是在代码书写完毕之后就形成了,与代码执行无关

- 内部作用域可以访问外部作用域的变量,但是外部不可以访问内部的

- 函数的形参就相当于在当前函数的作用域中申明了这个变量

- 访问变量时,先在自己的作用域中查找,如果没有则沿着作用域链往上找,直到全局.如果全局也没有就报错

  <img src="media/%E6%8A%A5%E9%94%991.png">

- 给变量赋值之前,要先找变量.查找变量也是沿着作用域链查找,直到全局,如果全局也没有,则会再全局作用域创建这个变量(隐式全局)

- 代码执行之前先考虑预解析规则,调用函数时,执行函数里的代码之前,函数内也要先执行预解析规则

  

  

###真实面试题:

```javascript
var a;
if ("a" in window) {
    var a = 10;
}
alert(a);  //
//=============================================
var foo = 1;
function bar() {
    var foo
    if (!foo) {
        foo = 10;
    }
    alert(foo); //
}
 bar();
//================================================
var num = 123;
function f1(num) {
    console.log(num); //  
}
function f2() {
    var num = 456;
    f1(num);
}
f2();

//======================================================
 function fn(){
   var a = 1, b = 1, c = 1;
 }
 fn();
 console.log(c); //
 console.log(b); //
 console.log(a); //
  
 function fn1(){
   var a = b = c = 1;
     var a=1;
     b=1;
     c=1
 }
 fn1();
 console.log(c); //
 console.log(b); //
 console.log(a); //
//========================================================
var a = 1;
function fn(){
    var a = 2;
    function fnSon(a){//形参+
        var a
        a = 3;
        console.log(a); //3
    }
    fnSon();
    console.log(a);  // 2
}
console.log(a);  // 1
fn();
console.log(a); // 1

//==========================================================
var a ;   
function a(){
    console.log('呵呵')
    function a(){
        a = 4;
        console.log('哈哈')
    }
    a();
    console.log(a);  //4
}
a();
console.log(a); //f
//=================================================================
var a = 1;
function a(){
    a++;
}
console.log(a) //

//==================================================================
 var a = { x : 1 }
 var b = a;
 a.x = a = { n : 1}; 
 console.log(a.x); //
 console.log(b.x); //
```



###1.3. 创建对象的方式

####1.3.1 简单方式

我们可以直接通过 `new Object()` 创建：

```javascript
var person = new Object() 
person.name = 'Jack';
person.age = 18;
person.sayName = function () {
  console.log(this.name);   //jack
}
```

每次创建通过 `new Object()` 比较麻烦，所以可以通过它的简写形式对象字面量来创建：

>字面量形式的创建方式,底层也是new Object创建出来的

```javascript
var person = {
  name: 'Jack',
  age: 18,
  sayName: function () {
    console.log(this.name);
  }
}
```

上面的写法比较简单，但是如果我们要创建多个person对象呢？

```javascript
var person1 = {
  name: 'Jack',
  age: 18,
  sayName: function () {
    console.log(this.name);
  }
}

var person2 = {
  name: 'Mike',
  age: 16,
  sayName: function () {
    console.log(this.name);
  }
}

var person3 = {
  name: 'zs',
  age: 17,
  sayName: function () {
    console.log(this.name);
  }
}
```

通过上面的代码我们不难看出，这样写的代码太过冗余。

####1.3.2 简单方式的改进：工厂函数

我们可以写一个函数，解决代码重复问题：

```javascript
function createPerson (name, age) {
  return {
    name: name,
    age: age,
    sayName: function () {
      console.log(this.name);
    }
  }
}
```

然后生成对象：

```javascript
var p1 = createPerson('Jack', 18);
p1.sayName(); //jack
var p2 = createPerson('Mike', 18);
p2.sayName(); // Mike
```

####1.3.3 更优雅的方式(更推荐使用的一种方式)：构造函数

一种更优雅的工厂函数就是下面这样，构造函数：

```javascript
function Person (name, age) {
  this.name = name;
  this.age = age;
  this.sayName = function () {
    console.log(this.name);
  }
}

var p1 = new Person('Jack', 18);
p1.sayName() // => Jack

var p2 = new Person('Mike', 23);
p2.sayName() // => Mike
```

**构造函数中new关键字做了4件事:**

1. 创建一个新对象
2. 让 this 就指向了这个新对象
3. 执行构造函数中的代码
4. 返回新对象



## 2. 构造函数的问题

>使用构造函数带来的最大的好处就是创建对象更方便了，但是其本身也存在一个浪费内存的问题：

```javascript
function Person (name, age) {
  this.name = name;
  this.age = age;
  this.sayHello = function () {
    console.log('hello ' + this.name);
  }
}
var p1 = new Person('Tom', 18); {name,age,sayHello}
var p2 = new Person('Jack', 16);

```

以上代码的图示:

<img src=":title/:构造函数的问题.png">

通过上面的图示,我们发现,每一个对象都引用了一个函数,我们创建了多少个对象,对应的就会在内存中创建出对应数量的一样的函数.这样造成了内存的极大浪费

##3 解决构造函数浪费内存的方法:

###3.1 把对象的行为定义在构造函数外面

```javascript
function Person (name, age) {
  this.name = name;
  this.age = age;
  this.sayHello = say;
}
  
function say (){
   console.log('hello ' + this.name);
}
    
var p1 = new Person('Tom', 18);
var p2 = new Person('Jack', 16);
p1.sayHello(); // hello Tom
p2.sayHello(); // hello Jack
```

<img src=":title/:解决构造函数的问题01.png">

**注意: **  这种方式,可以解决构造函数浪费内存的问题,但是,同时又出现了一个新的问题,我们把函数定义在了全局,

全局的函数,很容易被别人写的代码覆盖.

###3.2 利用函数的原型对象(更优雅的解决方案)

>js给每一个函数,提供了一个对应的原型对象.可以通过函数的prototype属性访问到这个原型对象.
>
>原型对象有一个constructor的属性会指向自己对应的函数
>
>而我们通过  `new 函数`  创建出来的实例对象,默认可以访问到函数对应的原型对象上的属性

```javascript
function Person (name, age) {
  this.name = name;
  this.age = age;
}
  
Person.prototype.sayName = function (){
   console.log('hello ' + this.name);
}
    
var p1 = new Person('Tom', 18);
var p2 = new Person('Jack', 16);
p1.sayName(); // hello Tom
p2.sayName(); // hello Jack
```

<img src=":title/:构造函数,实例,原型关系图.png">

**注意: **为了我们方便查看,实例和原型的关系.浏览器很贴心的帮我们实现了一个属性 `__proto__`, 通过这个属性,我们可以在控制台上清楚的看到原型.但是`__proto__`不是w3c标准的属性,所以不要在生产环境(上线)下使用.

```javascript
function Person (name, age) {
  this.name = name;
  this.age = age;
    
}
function say(){
    
}

var p1 = new Person();

console.log(Perosn.prototype === p1.__proto__) //true
```



### 3.3 小结: 

- 利用原型对象,可以更加优雅的解决构造函数浪费内存的问题
- 一般对象私有的属性直接写在构造函数中,而对象公有的属性写在原型对象上
- 函数对应有一个自己的原型对象 , 通过prototype属性可以访问
- 原型对象有一个constructor属性,可以指回自己的对应的函数
- 通过函数new出来的实例,默认可以访问到原型对象的属性 ,我们可以通过`__proto__`在控制台看到


## 3. 原型链

>原型对象也是对象,那么这个对象的是被谁创建出来的呢?

```javascript
function Person (name, age) {
  this.name = name;
  this.age = age;
}

var p1 = new Person();

console.log(Person.prototype) // 指向Person的原型对象
console.log(Person.prototype.__proto__.constructor) // 我们可以看到Person的原型对象是Object的实例
```

<img src=":title/:原型链.png">

从实例开始，实例默认可以访问自己构造函数的原型，这个原型也是其他构造函数的实例，也还可以访问自己的构造函数的原型，原型和原型之间连接的关系，我们称之为原型链

## 4. js中对象属性的查找规则

>因为这个查找规则,所以Object函数原型对象上的所有属性都可以被其他对象访问到

- 访问对象的属性时,先在对象自己身上找,找到就直接返回
- 如果对象的身上没有这个属性,就会往原型上面找,如果找到就直接返回
- 如果原型上也没有,就往原型的原型上面找(沿着原型链一直往上找),找到就立即返回
- 如果最终都没有找到,则返回undefined

```javascript
function Student(){}
var s1 = new Student();
s1.toString()  //[object Object]  
```

## 5. 内置对象的原型

- Array.prototype

- String.prototype

  ...

  通过观察内置函数的原型,我们发现我们在js基础阶段学习的数组/字符串常用的API,其实都定义在他们对应的原型上的.所以所有的数组对象/字符串,都能使用这些API.

  <img src=":title/:Array.prototype.png"> 



**小测试: 给数组添加一个我们自己定义的去重方法**

var arr=new Array(1,2,5,1,5,1)

##6. 更简单的原型使用方式

> 如果我们有很多公用的属性,那么一个一个的添加在函数的原型上就比较麻烦,我们还可以有一种更简单的方式
>
> 直接新建一个对象赋值给函数的prototype属性

```javascript
function Person (name, age) {
  this.name = name;
  this.age = age;
}
{
    constructor
}
Person.prototype = {
  constructor: Person, // => 手动定义一个 constructor 属性, 指向正确的构造函数
  sayHello: function () {
    console.log('我叫' + this.name + '，我今年' + this.age + '岁了');
  }
  eat : function(){
    console.log('吃饭ing...');
  }
}

var p1 = new Person('zs', 18);
```

<img src=":title/:原型的简单使用方式.png"> 











