# 新增声明命令let和const

在es6中通常用 let 和 const 来声明，let 表示变量、const 表示常量。

特点：

let 和 const 都是块级作用域。以{}代码块作为作用域范围 只能在代码块里面使用。
不存在变量提升，只能先声明再使用，否则会报错。在代码块内，在声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）。
在同一个代码块内，不允许重复声明。
const声明的是一个只读常量，在声明时就需要赋值。（如果 const 的是一个对象，对象所包含的值是可以被修改的。抽象一点儿说，就是对象所指向的地址不能改变，而变量成员是可以修改的。）

# 模板字符串（Template String）

用一对反引号(`)标识，它可以当作普通字符串使用，也可以用来定义多行字符串，也可以在字符串中嵌入变量，js表达式或函数，变量、js表达式或函数需要写在${ }中。

var str = `abc
def
gh`;
console.log(str);
let name = "小明";
function a() {
  return "ming";
}
console.log(`我的名字叫做${name}，年龄${17+2}岁，性别${'男'}，游戏ID：${a()}`);

# 函数的扩展

函数的默认参数
ES6为参数提供了**默认值**。在定义函数时便初始化了这个参数，以便在参数没有被传递进去时使用。

function A(a,b=1){
  console.log(a+b);
}
A(1);   //2
A(2+3);  //5

# 箭头函数 

在es6中，提供了一种简洁的函数写法，我们称作“箭头函数”。

写法：函数名=(形参)=>{……}   当函数体中只有一个表达式时，{}和return可以省略，当函数体中形参只有一个时，()可以省略。

特点：箭头函数中的this始终指向箭头函数定义时的离this最近的一个函数，如果没有最近的函数就指向window。

箭头函数不能作为构造函数，不能被new；箭头函数没有原型

//省略写法
var people = name => 'hello' + name;

var getFullName = (firstName, lastName) => {
  var fullName = firstName + lastName;
  return fullName;
} 

# 对象的扩展 

1属性的简写。ES6 允许在对象之中，直接写变量。这时，属性名为变量名, 属性值为变量的值。
var foo = 'bar';
var baz = {foo};  //等同于  var baz = {foo: foo};
方法的简写。省略冒号与function关键字。
var o = {
 method() {
  return "Hello!";
 }
};

// 等同于
var o = {
 method: function() {
  return "Hello!";
 }
};
Object.keys()方法，获取对象的所有属性名或方法名（不包括原形的内容），返回一个数组。
Object.is()方法 等同于===

# for...of 循环

是遍历所有数据结构的统一的方法。for...of循环可以使用的范围包括数组、Set 和 Map 结构、某些类似数组的对象（比如arguments对象、DOM NodeList 对象）、Generator 对象，以及字符串。**不能便利对象**

var arr=["小林","小吴","小佳"];
for(var v of arr){
  console.log(v);   
}
//小林 
//小吴 
//小佳

和 for in的区别，for in主要用于遍历对象，for in 遍历的是 键名

# 模块化 import和export

模块化：

​	就是把代码进行拆分，方便重复利用，模块功能主要由两个命令构成：export和import。将一个复杂的程序依据一定的规则(规范)封装成几个块(文件), 并进行组合在一起；
块的内部数据/实现是私有的, 只是向外部暴露一些接口(方法)与外部其它模块通信；

模块化的概念初始于服务端编程，CommonJS规范 通过require引入模块，model.exports导出模块。commonjs引入模块的方式是同步的，在服务端加载模块只是从硬盘中加载，比较快。但是浏览器端，模块存在web服务器中，大量的引入会很费时间，在浏览器端不适用。于是有了amd异步模块定义规范。这些规范都是es5时期的。

ES6中无需引入别的js文件，ES6 在语言标准的层面上，实现了模块功能，而且实现得相当简单，完全可以取代 CommonJS 和 AMD 规范，成为浏览器和服务器通用的模块解决方案。
ES6 模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。

commonjs和es6module区别

1、CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。

2、CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。

3、CommonJs 是单个值导出，ES6 Module可以导出多个

4、CommonJs 是动态语法可以写在判断里，ES6 Module 静态语法只能写在顶层

5、CommonJs 的 this 是当前模块，ES6 Module的 this 是 undefined

# Promise对象

Promise是异步编程的一种解决方案，将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。

它有三种状态，分别是pending-进行中、resolved-已完成、rejected-已失败。

Promise 构造函数包含两个参数。一个带有 resolve（解析）和 reject（拒绝）两个参数的回调。在回调中执行一些操作（例如异步），如果一切都正常，则调用 resolve，否则调用 reject。对于已经实例化过的 promise 对象可以调用 promise.then() 方法，传递 resolve 和 reject 方法作为回调。then()方法接收两个参数：onResolve和onReject，分别代表当前 promise 对象在成功或失败时。

var promise = new Promise((resolve, reject) => {
  var success = true;
  if (success) {
    resolve('成功');
  } else {
    reject('失败');
  }
}).then(
  (data) => { console.log(data)},
  (data) => { console.log(data)}
)
promise的执行过程

setTimeout(function() {
  console.log(0);
}, 0);
var promise = new Promise((resolve, reject) => {
  console.log(1);
  setTimeout(function () {
    var success = true;
    if (success) {
      resolve('成功');
    } else {
      reject('失败');
    }
  },2000);
}).then(
  (data) => { console.log(data)},
  (data) => { console.log(data)}
);
console.log(promise);   //<pending> 进行中
setTimeout(function () {
  console.log(promise);   //<resolved> 已完成
},2500);
console.log(2);

//1
//Promise {<pending>}
//2
//0
//成功
//Promise {<resolved>: undefined}

# 解构赋值

ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

数组的解构赋值
数组中的值会自动被解析到对应接收该值的变量中，数组的解构赋值要一一对应 如果有对应不上的就是undefined

var [name, pwd, sex]=["小周", "123456", "男"];
console.log(name) //小周
console.log(pwd)//123456
console.log(sex)//男
对象的解构赋值
对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

var obj={name:"小周", pwd:"123456", sex:"男"}
var {name, pwd, sex}=obj;
console.log(name) //小周
console.log(pwd)//123456
console.log(sex)//男

//如果想要变量名和属性名不同，要写成这样
let { foo: foz, bar: baz } = { foo: "aaa", bar: "bbb" };
console.log(foz) // "aaa"
console.log(foo) // error: foo is not defined

# set数据结构

Set数据结构，类似数组。所有的数据都是唯一的，没有重复的值。它本身是一个构造函数。

属性和方法：

size 数据的长度
add() 添加某个值，返回 Set 结构本身。
delete() 删除某个值，返回一个布尔值，表示删除是否成功。
has() 查找某条数据，返回一个布尔值。
clear() 清除所有成员，没有返回值。
应用：数组去重。

var arr = [1,1,2,2,3];
var s = new Set(arr);
console.log(s);   //{1, 2, 3}

console.log(s.size);   //3
console.log(s.add(4));   //{1, 2, 3, 4}
console.log(s.delete(4));   //true
console.log(s.has(4));   //false
s.clear();

# map数据结构

ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。

# Spread Operator 展开运算符(...)

将字符串转成数组
var str="abcd";
console.log([...str]) // ["a", "b", "c", "d"]
将集合转成数组
var sets=new Set([1,2,3,4,5])
console.log([...sets]) // [1, 2, 3, 4, 5]
两个数组的合并
var a1=[1,2,3];
var a2=[4,5,6];
console.log([...a1,...a2]); //[1, 2, 3, 4, 5, 6]
在函数中，用来代替arguments参数
rest参数  …变量名称



