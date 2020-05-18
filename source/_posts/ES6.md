---
date: 2019-06-23
cover: https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=1487385531,1597092167&fm=26&gp=0.jpg
---

##    1.ES6介绍

```javascript
《ECMAScript 6 入门》
《深入浅出ES6》              阮一峰
http://es6.ruanyifeng.com/

ECMAScript 6.0（以下简称 ES6）是 JavaScript 语言的下一代标准，已经在 2015 年 6 月正式发布了。它的目标，是使得 JavaScript 语言可以用来编写复杂的大型应用程序，成为企业级开发语言。

ES6 提供了许多新特性，但并不是所有的浏览器都能够完美支持。好在目前各大浏览器自身也加快速度兼容 ES6 的新特性，其中对 ES6 新特性最友好的是 Chrome 和 Firefox 浏览器。
```

### 1.1 ES6的兼容性

```javascript
一、桌面端浏览器对ES2015的支持情况
Chrome：51 版起便可以支持 97% 的 ES6 新特性。
Firefox：53 版起便可以支持 97% 的 ES6 新特性。
Safari：10 版起便可以支持 99% 的 ES6 新特性。
IE：Edge 15可以支持 96% 的 ES6 新特性。Edge 14 可以支持 93% 的 ES6 新特性。（IE7~11 基本不支持 ES6）

二、移动端浏览器对ES2015的支持情况
iOS：10.0 版起便可以支持 99% 的 ES6 新特性。
Android：基本不支持 ES6 新特性（5.1 仅支持 25%）

三、服务器对ES2015的支持情况
Node.js：6.5 版起便可以支持 97% 的 ES6 新特性。（6.0 支持 92%）

附：如何使用ES6的新特性，又能保证浏览器的兼容？
针对 ES6 的兼容性问题，很多团队为此开发出了多种语法解析转换工具，把我们写的 ES6 语法转换成 ES5，相当于在 ES6 和浏览器之间做了一个翻译官。比较通用的工具方案有 babel，jsx，traceur，es6-shim 等。
```

### 1.2 ES6语法

#### 1.2.1 变量声明let与const

```javascript
# 1. let  变量
//1.1 let声明的变量不存在预解析
//1.2 let声明的变量在同一个作用域内不允许重复
//1.3 let声明的变量一定要在声明后使用，否则报错。

//之前作用域包含：全局作用域和函数作用域，不存在块级作用域。在ES6引入了块级作用域。
//所谓块级作用域就是  { } 
if(true){
	//块级作用域内的变量不可以被外部访问
    let flag = 123;
}
console.log(flag);

//for循环()中用let声明的变量只能在循环体内使用
for(let i=0;i<5;i++){
    console.log(i);
}
console.log(i); //无法访问

//1.3 在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”
// 只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。
var tmp = 123;
if (true) {
   tmp = 'abc'; // 暂时性死区
   let tmp;
}

# 2. const  常量
const  a = 1;   //const声明的常量必须初始化
a = 2;  //错误，a不可以被改变
```

#### 1.2.2 解构赋值

```javascript
//1.什么是解构赋值
语法上就是赋值的作用。
解构:左边一种结构，右边一种结构，左右一一对应进行赋值。

//2.数组的解构赋值
{
    let [a,b,c] = [1,2,3];
    console.log(a,b,c);
}

//3.使用解构赋值进行变量交换
{
    let a=1;
    let b=2;
    [a,b] = [b,a];
    console.log(a,b);
}

//4.返回多个参数
{
    function f(){
        return [1,2];
    }
    let [a,b] = f();//[a,b]=[1,2]
    console.log(a,b);
}

//5.对象的解构赋值
{
    let {foo,bar} = {foo:'hello',bar:'hi'};
    //给对象取别名(如果有了别名，那么原来的名字就无效了)
    let {foo:abc,bar} = {foo:'hello',bar:'hi'};
    console.log(foo,bar);
    //将对象中的属性赋值给对应成员
    let {cos,sin,random} = Math;
    console.log(cos,sin,random);
}

//6.对象的解构赋值
{
    let metaData={
        title:"abc",
        test:[{
            title:"test",
            desc:"description"
        }]
    }
    let {title:esTitle,test:[{title:cnTitle}]} = metaData;
    console.log(esTitle,cnTitle);
}

//7.字符串的解构赋值
{
    let [a,b,c,d,e] = "hello";
    console.log(a,b,c,d,e);
    //获取字符串长度
    let {length} = "abc";
    console.log(length);
}
```

#### 1.2.3 字符串扩展

```javascript
{
    //常用方法
    console.log("hello world".includes("world",3));   //3指定开始搜索的位置
    console.log("hello world".startsWith("h"));
    console.log("hello world".endsWith("d"));
}

{
    //字符串复制
    let str = "abc";
    console.log(str.repeat(2)); //str重复两次
}

{
	//模板字符串  反引号
    let obj = {
        name:"zhangsan",
        age:18
    }
    function fn(gender){
        return gender;
    }
    let str = `姓名${obj.name},年龄${obj.age},性别${fn('男')}`;
}

{
    //前补后补字符串
    console.log("a".padStart(2,"0"));
    console.log("a".padEnd(2,"0"));
}

{
    //标签模板字符串
    /*
    (1)定义：模板字符串紧跟在一个函数后面，该函数将被调用来处理这个模板字符串
    (2)是函数调用的一种特殊方式，标签就是函数，紧跟在后面的模板字符串就是参数
    (3)如果模板字符串里面有变量，先将模板字符串处理成多个参数，再调用函数
    (4)函数tag会接收多个参数
    
    function tag(stringArr, value1, value2){
         // stringArr:该数组的成员是模板字符串中那些没有变量替换的部分
         // value1,...:模板字符串各个变量被替换后的值
    }
    */
    
    var a = 5;
    var b = 10;

    function tag(s,v1,v2){
        console.log(s);  //字符串模板，数组
        console.log(v1);//第一个${a+b}
        console.log(v2);//第二个${a*b}
        //通过手动return 来过滤字符串
        return s[0]+v1;
    }
    console.log(tag`Hello ${a+b} world ${a*b}`);
}
```

#### 1.2.4 函数扩展

```javascript
{
    //1.参数默认值(带有默认值的参数需要放在无默认值参数的右边)
    function foo(param = 'hello'){
        console.log(param);
    }
    foo();
    foo("你好");
}

{
    //2.参数结构赋值
    function foo({uname='lisi',age=13}={}){
        console.log(uname,age);
    }
    foo({uname:'zhangsan',age"15"});
}
    
{
    //3.rest参数  (剩余参数)  ...  将多个参数变成数组
    function foo(a,b,...param){
        console.log(a,param);
    }
    foo(1,2,3,4,5);
}

{
    //4.扩展运算符  ...  将数组变为离散值
    let arr1 = [1,2,3];
    let arr2 = [4,5,6];
    let arr3 = [...arr1,...arr2];
}

{
    //5.扩展运算符  ...  将数组变为多个参数
    function foo(a,b,c,){
         console.log(a+b+c);
    }
    let arr = [1,2,3];
    foo.apply(null,arr); //apply()方法第二个参数是数组
    foo(...arr);
}

{
    //6.箭头函数   代码块
    function foo(){
        console.log("hello");
    }

    let foo = () => {console.log("hello")};
    foo();

    let foo2 = (name) => {
        let c = 1;
        console.log("hello"+name +c);
    };
    foo2("小明");
}

{
    //7.箭头函数应用
    arr.forEach((element,index)=>{
        console.log(element,index);
    })
}

//8.箭头函数的注意事项：
{
    function foo(){
        //8.1 箭头函数中的this是定义函数时所在的执行环境
        setTimeout(()=>{
            console.log(this.num);
        },1000)
    }
    foo.call({num:1});

	//8.2 箭头函数不可以使用arguments获取参数列表，可以用reset参数替代
    //   箭头函数不能new，没有原型链
    let foo = (...param)=>{
        console.log(param);
    }
    foo(123,456)
    
    //8.3 如果箭头函数中没有形参，()不能省略
    //8.4 如果箭头函数中只有一条return语句，可以省略{}和return
}
```

#### 1.2.5 数组扩展

```javascript
//Array.from  方法从一个类似数组或可迭代对象中创建一个新的数组实例
{		
    	//去数组中的重复元素
    	let arr = [12,13,12,11,0];
        let arr1 = Array.from(new Set(arr));
        console.log(arr1);//输出：12,13,11,0
}

{
    //获取数组的所有key
    ["a","b","c"].keys();

    //获取数组的所有values 
    ["a","b","c"].values();

    //获取所有的key和value
    for(let o of ["a","b","c"]) {
        console.log(o);   
    }
}

//数组查找
{
    console.log([1,2,3,4,5,6].find(function(item){return item>3}))
    console.log([1,2,3,4,5,6].findIndex(function(item){return item>3}))//返回第一个找到的值
}

//数组包含
{
     console.log([1,2,NaN].includes(1));
     console.log([1,2,NaN].includes(NaN));//字符串处理
}
```

#### 1.2.6 对象扩展

```javascript
//1.es5对象和es6对象对比
{
	let o = 1;
    let k = 2;
    //es5
    let es5 = {
        o:o,
        k:k,
        say:function(){
            console.log("hello");
        }
    };
    //es6
    let es6 = {
        o,
        k,
        say(){
            console.log("say");
        }
    };
    console.log(es5,es6);
}

//2.属性表达式
{
    let a="b";
    let es5_obj = {
        a:"c"
    };
    
    let es6_obj={
        //这里的[a]这个值为上面的b
        [a]:"c"
    }
}

//3.新增API
{
    //Object.is 相当于===
    console.log(Object.is("abc","abc"));
    
    //拷贝
    console.log(Object.assign({a:"a"},{b:"b"}))

	//遍历对象
    let test = {k:123,o:456};
    for(let key in test){
        console.log(key,test[key]);
    }
}
```

#### 1.2.7 Symbol

	ES6中新增了Symbol数据类型。Symbol不可以new
	
	之前的基本数据类型有6种：Undefined、Null、布尔值（Boolean）、字符串（String）、数值（Number）、对象（Object）。
	
	Symbol声明的变量是唯一的，意义在于减少命名冲突

```javascript
{
    //Symbol的变量是唯一的，所以a1和a2永远不相等
    let a1 = Symbol();
    let a2 = Symbol();
    console.log(a1 === a2);
    
    //Symbol全局注册表是一个类似全局作用域的共享环境
    //Symbol.for()方法首先在全局Symbol注册表中搜索键为"a3"的Symbol是否存在，如果存在，直接返回已有的Symbol；否则，创建一个新的Symbol，并使用这个键在Symbol全局注册表中注册，随即返回新创建的Symbol。后续如果再传入同样的键调用Symbol.for()会返回相同的Symbol
    let a3 = Symbol.for("a3");
    let a4 = Symbol.for("a3");
    console.log(a3 === a4);  //true
}

{
    //Symbol作为key
    let a1 = Symbol.for("abc");
    let obj = {
        [a1]:"123",
        "abc":345
    }
    console.log(obj);
    
    for(let key in obj){
        console.log(key,obj[key]);
    }
}

{
    //Symbol作用：
    //有时我们可能希望在不同的代码中共享同一个Symbol，例如，在你的应用中有两种不同的对象类型，但是你希望它们使用同一个Symbol属性来表示一个独特的标识符。
    {
        let a1 = Symbol.for("abc");
        let obj = {
            [a1]:"123",
            "abc":345
        }
        console.log(obj);
    }
    {
        //这里拿到的Symbol和上面一个代码块拿到的Symbol是同一个东西
        let a1 = Symbol.for("abc");
        let obj2 = {
            [a1]:"123",
            "abc":34544
        }
        console.log(obj2);
    }
}
```

### 1.3. ES6数据结构

#### 1.3.1 Array和Set

##### a) Array

```
{
   let  arr = [1,2,3]; 
}
```

##### b) Set

```javascript
//1.Set元素是无序唯一
{
    let list = new Set();
    list.add(5);
    list.add(7);
    list.add("a");
    list.add(1);
    console.log(list);
}

//2.Set的方法
{
  let arr=['add','delete','clear','has'];
  let list=new Set(arr);

  console.log('has',list.has('add'));
  console.log('delete',list.delete('add'),list);
  list.clear();
  console.log('list',list);
}

//3.Set的遍历
{
  let arr=['add','delete','clear','has'];
  let list=new Set(arr);

  list.forEach(function(item){console.log(item);})
}

//4.Set转Array
{
    let list = new Set();
    list.add(5);
    list.add(7);
    list.add("a");
    list.add(1);
    
    let arr = [...list];
}
```

##### c) WeakSet

	WeakSet 结构与 Set 类似，也是不重复的值的集合。但是，它与 Set 有下面区别。

> 1.WeakSet 的成员只能是对象，而不能是其他类型的值。
>
> 2.WeakSet 中的对象都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中。
>
> 3.WeakSet 只有add/delete/clear/hass四个方法，不能遍历，没有size属性等

```javascript
{
  let weakList=new WeakSet();
  let arg={};
  weakList.add(arg);
  // weakList.add(2);
  console.log('weakList',weakList);
}
```

##### d) Array和Set对比

> 1.在Set中我们不能像访问数组元素那样直接通过索引来访问集合中的元素，如有需要，需要先将Set转换为数组。
> 2.Array中的数组元素是可以重复的，Set中的数组元素不能重复
> 3.Array的key默认是索引值，value是数组内容；Set的key和value都是实际内容

#### 1.3.2 Object和Map

##### a) Object

```javascript
{
    let obj = {
        key:"value"
    }
}
```

##### b) Map	

	Map结构提供了“值—值”的对应，是一种更完善的Hash结构实现。如果你需要“键值对”的数据结构，Map比Object更合适。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。

```javascript
{
  //基本使用
  let map = new Map();
  let arr=['123'];
  map.set(arr,456);//为map添加或更新一个指定了键(key)和值(value)的(新)键值对。
  console.log('map',map,map.get(arr));//get获取对应的值
}

{
  //Map的第二种定义
  let map = new Map([['a',123],['b',456]]);
  console.log('map args',map);
  console.log('size',map.size);
  console.log('delete',map.delete('a'),map);
  console.log('clear',map.clear(),map);
}

{
    //has(key),delete(key),clear()
    let m = new Map();

    m.set('edition', 6);
    m.set(262, 'standard');
    m.set(undefined, 'nah');

    m.has('edition')     // true
    m.has('years')       // false
    m.has(262)           // true
    m.has(undefined)     // true

    m.delete(undefined)
    m.has(undefined)       // false
}

{
    //Map的遍历  Map遍历的顺序就是插入的顺序
    let map = new Map([
      ['F', 'no'],
      ['T',  'yes'],
    ]);

    //遍历map
    map.forEach(function (value, key, map) {
       console.log(key,value);
    });
}
```

##### c) WeakMap

> 1.WeakMap的key值只能是对象，而不能是其他类型的值。
>
> 2.WeakMap中的key值都是弱引用
>
> 3.WeakMap不能遍历，没有size属性等

```javascript
{
  let weakmap=new WeakMap();

  let o={};
  weakmap.set(o,123);
  console.log(weakmap.get(o));
}
```

##### d) Object和Map区别

> 1. 一个对象的键只能是字符串或者 Symbols，但一个 Map 的键可以是任意值，包括函数、对象、基本类型。
> 2. Map 中的键值是有序的，而添加到对象中的键则不是。因此，当对它进行遍历时，Map对象是按插入的顺序返回键值。
> 3. 通过 size 属性直接获取一个 Map 的键值对个数，而 Object 的键值对个数只能手动计算。
> 4. Map 在频繁增删键值对的场景下会有些性能优势。

### 1.4 Proxy和Reflect

#### 1.4.1 Proxy介绍

	Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。Proxy 这个词的原意是代理，用在这里表示由它来“代理”某些操作，可以译为“代理器”。

```
var p = new Proxy(target, handler);
参数一target：目标对象，即拦截目标，可以是原生对象或者内置对象（比如是Object或者其他）；
参数二handler：拦截配置。你对参数一拦截哪些属性，拦截后的操作如何，都是在这里配置的；
返回值p：返回代理对象。需要注意，p和target并不相等。对返回值p进行的操作，会触发handler中自定义的方法。
```

```javascript
{
    let person={
        time:'2017-03-11',
        name:'小明',
        age:18
    };

    let monitor=new Proxy(person,{
        // 拦截对象属性的读取
        get(target,key){
            if(key === "name"){
                return "不告诉你";
            }
            return target[key];
        },
        // 拦截对象设置属性
        set(target,key,value){
            if(key==='time'){
                return target[key]=value;
            }else{
                return target[key];
            }
        },
        // 拦截key in object操作
        has(target,key){
            if(key==='name'){
                return target[key]
            }else{
                return false;
            }
        },
        // 拦截delete
        deleteProperty(target,key){
            if(key === "age"){
                delete target[key];
                return true;
            }else{
                return false;
            }
        },
        // 拦截Object.keys,Object.getOwnPropertySymbols,Object.getOwnPropertyNames
        ownKeys(target){
            return Object.keys(target).filter(item=>item!='time')
        }
    });

    //直接访问name。会被拦截
    console.log(monitor.name);

    //修改time成功，修改age被拦截
    monitor.time='2018';
    monitor.age= 200;
    console.log(monitor);

    //name值为true，time值为false 被拦截了
    console.log('name' in monitor,'time' in monitor);

    //age被删除，name不被删除
    delete monitor.age;
    delete monitor.name;
    console.log(monitor);

    //因为写了ownKeys的拦截，此时所有的time都不会被打印
    console.log(monitor);
}
```

#### 1.4.2 Proxy实现对象属性值的校验

```javascript
let animal = {
    name:'dog'
}

let monitor=new Proxy(animal,{
    set: function(target, key, value) {
        //animalValidator中对应属性的校验逻辑是否存在
        if (animalValidator[key]) {
            //调用animalValidator对应属性的校验方法，入参属性值，如果条件满足
            if (animalValidator[key](value)) {
                target[key] = value;
            } else {
                console.log(`Cannot set ${key} to ${value}. Invalid.`)
            }
        } else {
            target[key] = value
        }
    }
});

//校验逻辑
var animalValidator = {
    name: function(name) {
        // 动物的名字必须是字符串类型的
        return typeof name === 'string';
    }
};

monitor.name = 'dog';
console.log(monitor.name);
// Uncaught Error: Cannot set name to 123. Invalid.
monitor.name = 123;
```

#### 1.4.3 Reflect

	反射机制是指程序在运行的时候访问、检测和修改它本身状态或行为的一种能力，例如一个对象能够在运行时知道自己有哪些方法和属性。
	
	反射的概念在编译型的编程语言中比较明显，比如java、C#、Object-c等。对于     `JavaScript`来说，反射就是获取对象的内部结构的信息，所以JS中的反射随处可见，比如for...in方式遍历对象。
	
	从ECMAScript6开始，JS引入Reflect这个API专门用于操作反射。
	
	Reflect引入的目的主要有下面几个：

##### 	a) 抽取语言内部的方法

	从ECMAScript6开始，JS将Object对象的一些明显属于语言内部的方法（ 比如Object.defineProperty）放到Reflect对象上。 现阶段某些方法同时在Object和Reflect对象上部署， 未来的新方法将只部署在Reflect对象上。并且修改某些 Object 方法的返回结果， 让其变得更合理。 比如， Object.defineProperty(obj, name, desc) 在无法定义属性时， 会抛出一个错误，而Reflect.defineProperty(obj, name, desc) 则会返回false。

```javascript
let person = {}
let temp = null

try{
    //一旦定义属性不成功会抛出一个异常
    Object.defineProperty(person, 'name', {
        get: function () {
            return temp
        },
        set: function (val) {
            console.log("sss")
            //异常 ： 程序出现的不正常现象
            var a = null;
            console.log(a.toString())
            //产生异常之后的代码都不会执行

            temp = val
        }
    })
    person.name = "xxxx";

    console.log("aaaa");
}
catch(e){
    console.log("异常被捕获了");
    //一旦处理了异常之后，程序就可以继续向下执行了
    console.log(person);
}


//  新写法
if(Reflect.defineProperty(target, property, attributes)) {
	// success
} else {
	// failure
}
```

##### 	c) 让Object操作都变成函数行为。

	 某些Object操作是命令式， 比如name in obj和delete obj[name]，而Reflect.has(obj, name) 和Reflect.deleteProperty(obj, name) 让它们变成了函数行为。

```javascript
//  老写法
'assign' in Object // true
//  新写法
Reflect.has(Object, 'assign') // true
```

##### 	c) Proxy和Reflect结合使用

```javascript
var loggedObj = new Proxy(obj, {
	get(target, name) {
		console.log('get', target, name);
		return Reflect.get(target, name);
	},
	deleteProperty(target, name) {
		console.log('delete' + name);
		return Reflect.deleteProperty(target, name);
	},
	has(target, name) {
		console.log('has' + name);
		return Reflect.has(target, name);
	}
});
```

##### 	d) 代码可读性更好

```javascript
#1. Reflect.apply()
{
     //Math的min只能获取指定参数中的最小值，要获取指定数组中的最小值，这个方法就不行了。
    Math.min(10,8,3,29);
    
    //要获取数组中的最小值，我们可以使用Math.min.apply(thisArg,[params])方法，apply()方法两个参数，第一个用作修改调用函数中的this指向，第二个给指定函数传递参数(数组)
    var ages = [11, 33, 12, 54, 18, 96];
    var youngest = Math.min.apply(Math, ages);  
    var oldest = Math.max.apply(Math, ages);  
    //输出youngest的类型
    var type = Object.prototype.toString.call(youngest);

    //以上是之前的解决方案，有了反射之后，我们可以使用Reflect.apply()方法
    /*
       Reflect.apply()方法有三个参数：
    　 第一个参数为： 需要执行的函数；
　　 第二个参数为： 需要执行函数的上下文this；
　 　第三个参数为： 是一个数组或者伪数组， 会作为执行函数的参数；
　 */
    var youngest = Reflect.apply(Math.min, Math, ages);  
    var oldest = Reflect.apply(Math.max, Math, ages);  
    var type = Reflect.apply(Object.prototype.toString, youngest , [youngest]);
}
```

### 1.5 类和对象

	ES6引入了Class（类）这个概念，作为对象的模板。通过class关键字，可以定义类。基本上，ES6的class可以看做只是一个语法糖，它的绝大部分功能，ES5都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

#### 1.5.1 类的定义和创建实例

```javascript
//es6对js的类进行了规范：方法写在原型上，把属性写在构造函数里面
{
  // 基本定义和生成实例
  class Parent{
    constructor(name='zs'){
      this.name=name;
    }
    showMsg(){    //定义在原型上
		console.log(this.name)
	}
  }
  let v_parent=new Parent('v');
  console.log('构造函数和实例',v_parent);
}
```

#### 1.5.2 继承

```javascript
{
  // 继承
  class Parent{
    constructor(name='zs'){
      this.name=name;
    }
  }

  class Child extends Parent{

  }
  console.log('继承',new Child());
}


{
  // 继承传递参数
  class Parent{
    constructor(name='zs'){
      this.name=name;
    }
  }

  class Child extends Parent{
    constructor(name='child'){
      //先初始化父亲的信息，在初始化自己的信息  
      super(name);
      this.type='child';
    }
  }
  console.log('继承传递参数',new Child('hello'));
}
```

#### 1.5.3 getter和setter

```javascript
//getter和setter方法的作用：给成员变量赋值
class Person{
    constructor (name, age) {
        this.name = name;   //访问set name()方法
        this.age = age;         //由于age没有get和set方法，所以这里直接给age成员变量赋值
    }
    set name (name) {
        console.log("setter");
        this._name = name;
    }
    get name () {
        console.log("getter");
        return this._name;
    }
}

var p = new Person("zhang", 25);
console.log(p._name);     //访问真实成员变量_name
console.log(p.name);      //访问get  name()方法，在这个方法中再去访问真实成员变量_name

#getter和setter注意点：
1.一旦某个属性写了getter和setter方法，则在使用this.xxx,p.xxx的时候都是去访问getter和setter方法
2.一旦某个属性写了getter和setter方法，真实的成员变量就不在是xxx了，而是_xxx
3.getter和setter方法要写就都一起写上
4.getter和setter方法中注意死循环的问题
```

#### 1.5.4 静态方法和静态属性

```javascript
//静态方法和静态属性：属于类/函数的信息，可以直接通过类名和函数名直接访问，不需要创建对象
//实例对象访问不到
{
  // 静态方法
  class Parent{
    constructor(name='zs'){
      this.name=name;
    }

    static tell(){
      console.log('tell');
    }
  }
  Parent.tell();
}

{
  // 静态属性
  class Parent{
    constructor(name='zs'){
      this.name=name;
    }

    static tell(){
      console.log('tell');
    }
  }

  Parent.type='test';
  console.log('静态属性',Parent.type);
}
```

### 1.6 异步

#### 1.6.1 异步的问题

```javascript
var fs = require('fs')//require('fs')（fs模块用于对系统文件及目录进行读写操作。）

fs.readFile('./data/a.txt', 'utf8', function (err, data) {
    if (err) {
        throw err
    }
    console.log(data)
})

fs.readFile('./data/b.txt', 'utf8', function (err, data) {
    if (err) {
        throw err
    }
    console.log(data)
})

fs.readFile('./data/c.txt', 'utf8', function (err, data) {
    if (err) {
        throw err
    }
    console.log(data)
})
# 上面代码的问题：无法保证a文件读完了接着读取b，b文件读完了接着读取c
```

#### 1.6.2 方案1:使用异步回调

```javascript
var fs = require('fs')

fs.readFile('./data/a.txt', 'utf8', function (err, data) {
  if (err) {
    throw err
  }
  console.log(data)
  fs.readFile('./data/b.txt', 'utf8', function (err, data) {
    if (err) {
      throw err
    }
    console.log(data)
    fs.readFile('./data/c.txt', 'utf8', function (err, data) {
      if (err) {
        throw err
      }
      console.log(data)
    })
  })
})

# 回调的问题：回调地狱，回调的层次太深，代码很难维护
```

#### 1.6.3 方案2:使用Promise

##### a) Promise介绍

	所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。

```javascript
var fs = require('fs')

console.log(1);
new Promise(function (resolve, reject) {
    console.log(2);
    fs.readFile('./data/a.txt', 'utf8', function (err, data) {
        if (err) {
            console.log(err)
        } else {
            console.log(data);
        }
    })
})

console.log(3);

#1.通过打印顺序我们可以发现 1-->2-->3 -->"aaa"
#2. Promise本身不是异步的，只是Promise中的任务是异步的
#3. Promise中第一个参数的function是new之后就立刻执行的
```

##### b) Promise的状态

	Promise有三种状态：

> - Pending（进行中、未完成的）
> - Resolved（已完成，又称 Fulfilled）
> - Rejected（已失败）。
>

```javascript
var fs = require('fs')

new Promise(function (resolve, reject) {
    fs.readFile('./data/a.txt', 'utf8', function (err, data) {
        if (err) {
            //异步任务完毕，修改Promise状态，向下一个then传递数据
            reject(err)
        } else {
            resolve(data)
        }
    })
}).then(function(data){
    console.log(data)
},function(error){
    console.log(error);
})
//then方法需要Promise对象来调用，表示异步任务执行完毕之后做的事情
```

##### c) Promise的链

```javascript
{
    new Promise(function(resolve,reject){
        console.log("11111")
        setTimeout(function () {
            resolve()
        }, 1000);
    }).then(function(){
        console.log("22222")
        //注意：如果此处返回的不是Promise对象，那么再后面一个then不会异步
        //要保证Promise的链式编程，需要在当前then中返回Promise
        return new Promise(function(resolve,reject){
            setTimeout(function () {
                resolve()
            }, 2000);
        });
     }).then(function(){
        console.log('3333');
    })
}
```

##### e) 使用Promise读文件

```javascript
#1.基本实现
var fs = require('fs')

new Promise(function (resolve, reject) {
    fs.readFile('./data/a.txt', 'utf8', function (err, data) {
        if (err) {
            reject(err)
        } else {
            console.log(data);
            resolve(data)
        }
    })
}).then(function(data){
    return new Promise(function (resolve, reject) {
        fs.readFile('./data/b.txt', 'utf8', function (err, data) {
            if (err) {
                reject(err)
            } else {
                console.log(data);
                resolve(data)
            }
        })
    })
}).then(function(data){
    fs.readFile('./data/c.txt', 'utf8', function (err, data) {
        if (err) {
            console.log(err)
        } else {
            console.log(data);
        }
    })
})


#2.代码封装
var fs = require('fs')

function pReadFile(filePath) {
  return new Promise(function (resolve, reject) {
    fs.readFile(filePath, 'utf8', function (err, data) {
      if (err) {
        reject(err)
      } else {
        resolve(data)
      }
    })
  })
}

pReadFile('./data/a.txt')
  .then(function (data) {
    console.log(data)
    return pReadFile('./data/b.txt')
  })
  .then(function (data) {
    console.log(data)
    return pReadFile('./data/c.txt')
  })
  .then(function (data) {
    console.log(data)
  })
```

##### f) Promise的异常捕获

```javascript
{
    let fs = require("fs");

    //创建一个Promise实例
    //1.Promise中的function是new Promise()的时候就执行的
    //2.Promise可以帮我们解决异步回调的问题(当你有异步回调操作的时候就可以用Promise)
    //3.Promise本身不是异步的，只不过Promise中可以有异步任务
    let p = new Promise(function(resolve,reject){	
        console.log("111");
        //fs.readFile()是一个异步操作
        fs.readFile("./m.txt",function(err,data){
            if (err) {
                console.log("222");
                console.log("出错了"+err);
                reject("错错错");
            }
            else{
                console.log(data.toString("utf-8"));
                console.log("333");
                resolve("返回文件数据");
            }
        })
    })
    
    //p是一个Promise对象
    //Promise对象有一个then方法,then方法的第一个函数是在Promise中的function的函数中调用resolve() 之后执行的
    //then方法的第二个函数是在Promise中的function的函数中调用reject() 之后执行的
    //.catch(function(error){}) 主要用来捕获promise中的异常的，注意点：不要在promise的function中抛出异常，catch方法是捕获不到的。可以在
    //reject的回调函数中抛出异常，这样catch方法可以捕获reject回调函数抛出的异常
    p.then(function(data){
        console.log("4444");
        console.log(data);
    },function(data){
        console.log("5555");
        console.log(data);
        //抛出异常
        throw new Error("错错错错匆促错");
    })
    .catch(function(error){
        //捕获异常的代码
        console.log("66666",error);
    })

}
```

##### g) Promise.all和Promise.race

```javascript
//1.Promise.all   等所有的promise执行完了再执行then
var p1 = new Promise(function (resolve, reject) {
    setTimeout(function(){
        resolve("P1");
    },500);
});
var p2 = new Promise(function (resolve, reject) {
    setTimeout(function(){
        resolve("P2");
    },2000);
});
Promise.all([p1, p2]).then(function (results) {
    console.log(results); // 获得一个Array: ['P1', 'P2']
});


//2.Promise.race   有任何一个promise执行完了就执行then
var p1 = new Promise(function (resolve, reject) {
     setTimeout(function(){
        resolve("P1");
    },500);
});
var p2 = new Promise(function (resolve, reject) {
    setTimeout(function(){
        resolve("P2");
    },2000);
});
Promise.race([p1, p2]).then(function (result) {
    console.log(result); // 'P1'
});
```

#### 1.6.4 jquery中Promise

```html
<body>
  <input type="button" value="获取数据" id="btn">
  <script src="./lib/jquery/dist/jquery.min.js"></script>
  <script>
    $(function () {
      $('#btn').on('click', function () {
        $.ajax({
          //请求本地数据
          url: './data.json',
          type: 'get',
          dataType: 'json'
        })
          .then(function (data) {
            console.log(data)
          })
      })
    });
  </script>
</body>
```

### 1.7 Iterator

#### 1.7.1 遍历方式的总结

##### a) 普通for循环

	自Javascript诞生起就一直用的 就是for循环，它用来遍历数组

```javascript
var arr = [1,2,3,4]
for(var i = 0 ; i< arr.length ; i++){
    console.log(arr[i])
}
```

##### b) forEach

	从ES5开始 Javascript内置了forEach方法用来遍历数组

```javascript
let arr = ['a', 'b', 'c', 'd']
arr.forEach(function (val, idx, arr) {
    console.log(val + ', index = ' + idx) // val是当前元素，index当前元素索引，arr数组
    console.log(arr)
})
//写法简单了很多，但是也存在一个局限 就是你不能中断循环(使用break语句或使用return语句）
```

##### c) for-in

	for in更适合遍历对象，不要使用for in遍历数组，虽然for in也可以遍历数组，但是会存在以下问题：
	
	1.index索引为字符串型数字，不能直接进行几何运算
	
	2.遍历顺序有可能不是按照实际数组的内部顺序
	
	3.使用for in会遍历数组所有的可枚举属性，包括原型。例如原型方法method和name属性

```javascript
let obj = {a: '1', b: '2', c: '3', d: '4'}
for (let o in obj) {
    console.log(o)    //遍历的实际上是对象的属性名称 a,b,c,d
    console.log(obj[o])  //这个才是属性对应的值1，2，3，4
}
```

##### d) for…of

	它是ES6中新增加的语法,主要用来循环实现了Iterator接口类型的对象。for of遍历的只是数组内的元素，而不包括数组的原型属性method和索引name。但是for...of不可以遍历对象，因为对象没有实现Iterator接口。

```javascript
//for ... of 可以遍历Array、Set、Map不能遍历Object 
let arr = ['China', 'America', 'Korea']
for (let o of arr) {
    console.log(o) //China, America, Korea
}


for(let [index,value] of ["a","b","c"].entries()) {
    console.log(index,value);   
}


```

#### 1.7.2 迭代器介绍

1.遍历器（Iterator）是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署Iterator接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。

2.Iterator的作用有三个：

	一是为各种数据结构，提供一个统一的、简便的访问接口；
	
	二是使得数据结构的成员能够按某种次序排列；
	
	三是ES6创造了一种新的遍历命令for...of循环，Iterator接口主要供for...of消费。

3.在ES6中，有些数据结构原生具备Iterator接口（比如数组），即不用任何处理，就可以被for...of循环遍历，有些就不行（比如对象）。凡是部署了Symbol.iterator属性的数据结构，就称为部署了遍历器接口。调用这个接口，就会返回一个遍历器对象。

4.在ES6中，有三类数据结构原生具备Iterator接口：数组、某些类似数组的对象、Set和Map结构。

```javascript
//iterator基本使用
{
      let arr=['hello','world'];
      //获取迭代器对象
      let map=arr[Symbol.iterator]();
      console.log(map.next());
      console.log(map.next());
      console.log(map.next());
    
      //内部遍历的时候就使用了迭代器
  	  for (let item of arr) {
    	  console.log(item); 
  	  }
}
```

#### 1.8 async和await

```javascript
let fs = require("fs");

function readFile(file){
	//返回一个Promise()
	return new Promise(function(resolve,reject){
		//Promise中有一个读文件的异步任务
		fs.readFile(file,function(err,data){
			if(err){
				reject("cuowu")
			}
			else{
				//console.log(data.toString("utf-8"))
				//当文件读取成功返回成功的数据
				resolve(data.toString("utf-8"));
			}
		})
	})
}

/*readFile("./a.txt")
.then(function(){
	return readFile("./b.txt")
})
.then(function(){
	return readFile("./c.txt")
})
*/


//async 加在函数上，表示该函数是一个异步函数
//如果函数上有声明async，此时在函数内部就可以使用await
//await 表示等待，可以将原来异步的任务变成同步
//这里的read方法里面的几个读取文件的任务由于加了await，所有此时这些任务是同步的，会按照顺序向下执行
async function read(){
	console.log("3")
	var data = await readFile("./a.txt");
	console.log(data);

	var data = await readFile("./b.txt");
	console.log(data);

	var data = await readFile("./c.txt");
	console.log(data);
	console.log("4")
}

console.log("1")
read();  //这个read方法是异步的，所以程序不会停在48行等read方法执行完毕
console.log("2")

```
