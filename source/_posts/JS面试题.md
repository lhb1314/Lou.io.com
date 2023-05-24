---
title: JS面试题
date: 2023-04-24 14:40:47
tags:
top_img: https://nimg.ws.126.net/?url=http%3A%2F%2Fdingyue.ws.126.net%2F2023%2F0324%2F9233c74ej00rs0r4d0013c000zk00k0m.jpg&thumbnail=660x2147483647&quality=80&type=jpg
cover: https://nimg.ws.126.net/?url=http%3A%2F%2Fdingyue.ws.126.net%2F2023%2F0324%2F9233c74ej00rs0r4d0013c000zk00k0m.jpg&thumbnail=660x2147483647&quality=80&type=jpg
---

# JS 面试题

## 1. 变量赋值

JavaScript 中的基本数据类型包括字符串  数值 布尔值 undefined Symbol

JavaScript 中的引用数据类型包括对象 数组 函数 null

```javascript
let m = 100;
let n = m;
m = 200;
console.log(n);
```

基本数据类型在进行变量赋值采用的是复制值得方式 n = m 其实就是把 m 变量的值 100 复制了一份给了变量 n 重新 为 m 变量赋值时变量 n 不会受到影响 所以变量 n 的值依然是 100

```javascript
let p1 = {age: 20};
let p2 = p1;
p2.age = 21;
console.log(p1.age);
```

```javascript
let m = 10;
let n = 20;

function display(m, n) {
    m = 100;
    n = 200;
}

display(m, n);
console.log(m);
console.log(n);
```

复杂数据类型在进行变量赋值时采用的是复制地址的方式 p2 = p1 其实就是把变量 p1 对应的对象引用地址复制了一份给了变量 p2 此时 p1 变量和 p2 变量同时指向了同一个对象 所以无论是使用 p1 更改 age 还是使用 p2 更改 age 都会收到影响 

```javascript
const o1 = {
    x: 100,
    y: 200,
};
const o2 = o1;
let x = o1.x;
o2.x = 101;
x = 102;
console.log(o1.x);
```

```javascript
let p = {name: "张三"};

function person(p) {
    p.name = "李四";
}
person(p);

console.log(p.name);
```

在 JavaScript 中 var let const 有什么区别

var const let 是 JavaScript 中用于声明变量的关键字 他们之间的主要区别在于作用域和是否可重新赋值  s

var 声明的变量具有函数作用域（function scope） 这意味着他们在整个函数体内都可见

var 可以在任何时候重新赋值 也可以在声明之前使用（hoisted）

```javascript
function testVar() {
    console.log(foo);
    var foo = "Hello";
    console.log(foo);
    foo = "World";
    console.log(foo);
}
testVar();
```

let 声明的变量具有块级作用域（block scope）这意味着他们只在定义他们的代码块内可见。

let 可以在任何时候重新赋值 但不能在声明之前使用

```javascript
function testLet() {
    let bar = "Hello";
    console.log(bar);
    bar = "World";
    console.log(bar);
    {
        let bar = "Inside block";
        console.log(bar);
    }
    console.log(bar);
}
testLet();
```

const 用于声明一个常量 他具有与 let 相同的块级作用域 但在声明时必须初始化 且之后不能重新赋值

```javascript
function testConst() {
    const baz = "hello";
    console.log(baz);
    {
        const baz = "Inside block";
        console.log(baz);
    }
    console.log(baz);
}
testConst();
```

在现代 JavaScript 开发中 一般建议尽量使用 let 和 const 以避免因 var 变量提升和函数作用域可能导致的意味行为

##  2. typeof 运算符

typeof 运算符可以识别所有的基本数据类型 函数 可以识别是否是引用数据类型

```javascript
let str = "Hello JavaScript";
let m = 100;
let isMarry = true;
let unique = Symbol("unique");
let n = undefined;
function fn() {};
let arr = ["a", "b"];
let obj = {name: "张三"};
let empty = null;

console.log(typeof str); // string
console.log(typeof m); // number
console.log(typeof isMarry) // boolean
console.log(typeof unique) // symbol
console.log(typeof n); // "undefined"
console.log(typeof fn); // "function"
console.log(typeof arr); // "object"
console.log(typeof obj); // "object"
console.log(typeof null); // "object"
```

##  3. 深拷贝

```javascript
function deepClone(target) {
    // 如果要拷贝的数据不是引用数据类型或要拷贝的数据为 null
    // 表示不需要深拷贝 直接返回数据即可
    if (typeof target !== "object" || target === null) return target;
    // 创建新的变量用于保存拷贝结果 区分要拷贝的数据是数组还是对象
    let result = target instanceof Array ? [] : {};
    // 遍历要拷贝的数据
    for (let key in target) {
        // 拷贝时排除原型对象中的属性
        if (target.hasOwnProperty(key)) {
            // 递归拷贝
            result[key] = deepClone(target[key]);
        }
    }
    // 返回拷贝结果
    return result;
}
```

```javascript
let obj1 = {
    a: 1,
    p: {
        name: "张三",
    },
};

let obj2 = deepClone(obj1);
console.log(obj1 === obj2);
console.log(obj2);
obj2.p.name = "李四";
console.log(obj1.p.name);
```

编写一个方法用于比较两个对象是否深度相等。

在 JavaScript中，可以使用递归方法来实现深度比较两个对象是否相等。

```javascript
function isEqual(obj1, obj2) {
    if (obj1 === obj2) {
        return true;
    }
    if (typeof obj1 !== "object" || typeof obj2 !== "object" || obj1 === null || obj2 === null) {
        return false;
    }
    const keys1 = object.keys(obj1);
    const keys2 = object.keys(obj2);
    if (keys1.length !== keys2.lenght) {
        return false;
    }
    for (const key of keys1) {
        if (!keys2.includes(key)) {
            return false;
        }
        if (!isEqual(obj1[key], obj2[key])) {
            return false;
        }
    }
    return true;
}
```

这个 isEqual 方法首先比较两个对象的引用是否相等，如果相等则返回 true。然后，检查两个对象是否都是对象类型，如果不是，则返回 false，接下来，比较两个对象的键的数量，如果不相等，则返回 false。最后，使用递归方法比较键值，如果存在不相等的键值，则返回 false。如果所有键值都相等，则返回 true。

##  4. 数据类型转换规则

① 其他类型的值转换为字符串

```javascript
String(null); // "null"
String(undefined); // "undefined"
String(true); // "true"
String(false); // "false"
String(10); // "10"
// 数组转为字符串是将数组中的所有元素按照 "," 连接起来
// 相当于调用数组的 Array.prototype.join(",") 方法
// 如 [1, 2, 3] 转为 "1,2,3"
// 空数组 [] 转为空字符串
// 数组中的 null 或 undefined, 会被当做空字符串处理
String([1, 2, 3]); // "1,2,3"
String([]); // ""
String([null]); // ""
String([1, undefined, 3]); // "1,,3"
// 普通对象转为字符串相当于直接使用 Object.prototype.toString() 方法
String({}); // "[object Object]"
```

② 其他类型的值转换为数值

```javascript
Number(null); // 0
Number(undefined); // NaN
Number("10"); // 10
Number(""); // 0
Number(true); // 1
Number(false); // 0
// 数组会先被转换为原始类型, 然后再将转换后的原始类型转换为数值类型
Number([]); // 0
Number(["10"]); // 10
Number(["10", "20"]); // NaN
Number({}); // NaN
```

③ 其他类型转换为布尔值

```javascript
Boolean(null); // false
Boolean(undefined) // false
Boolean("") // false
Boolean(NaN) // false
Boolean(0) // false
Boolean([]) // true
Boolean({}) // true
Boolean(Infinity) // true
```

④ 对象，数组转换为原始类型

当对象类型需要被转为原始类型时，它会先查找对象的 valueOf 方法，如果 valueOf 方法返回原始类型的值，就使用这个值作为转换结果。

如果 valueOf 方法返回的不是原始类型的值，尝试调用对象的 toString 方法，使用该方法的返回值作为转换结果。

valueOf 方法用于返回对象的原始类型，一般由系统自动调用。

```javascript
// 创建字符串对象
let strObject = new String("Hello");
// 输出它字符串对象
strObject; // String {0: "H", 1: "e", 2: "l",  3: "l", 4: "o"}
// 输出它字符串对象的类型
typeof strObject; // "object"
// 获取字符串对象 strObject 的原始值
strObject.valueOf(); // "Hello"
```

```javascript
let object = {};
let array = [];

object.valueOf() // {}
console.log(array.valueOf()) // []
```

```javascript
let object = {};
let array = [];

object.prototype.valueOf = function () {
    return 100;
};

console.log(object.valueOf()); // 100
console.log(array.valueOf()); // 100
```

```javascript
// 将数组转换为数值类型
// 系统会先调用数组下的 valueOf 方法, 但是当前 valueOf 方法返回的就是数组, 所以系统去调用 toString 方法
// toString 方法调用之后返回了一个空字符串, 将空字符串转换为数值会得到 0
Number([])
```

```javascript
// 在以下运算式中由于 + 号两边都不是数值, 所以要进行字符串连接操作
// 系统会先调用对象下的 valueOf 方法, 但是当前 valueOf 方法返回的就是对象, 所以系统去调用 toString 方法
// toString 方法调用后返回了 '[object Object]', 所以最终连接的结果就是 '[object Object][object Object]'
({}) + ({})
```

##  5. 宽松比较中的隐式转换

在 JavaScript 中宽松比较会发生隐式类型转换，严格比较不会发生隐式类型转换。

① 布尔类型和其他类型的相等比较

布尔类型的值在参数比较时值会被转换为数值类型，true 转换为1，false 转换为 0

```javascript
false == 0 // true
true == 1 // true
true == 2 // false
```

```javascript
const x = 10;
if (x == true) {
    console.log(x); // ? 是否会被输出
}
```

② 数值类型和字符串类型的相等比较

当数值类型和字符串类型做相等比较时，字符串类型会被转换为数值类型。

如果字符串为数值字符串，则将其转换为对应的数值，如果是空字符串转换为 0，其他一律转换为 NaN。

NaN 和任何值比较都不相等，包括它自己。

```javascript
0 == "" // true
1 == "1" // true
true == "1" // true
false == "0" // true
false == "" // true
```

③ 对象类型和原始类型的相等比较

当对象类型和原始类型做相等比较时，对象类型要被转换为原始类型。

```javascript
'[object Object]' == {} // true
'1,2,3' == [1, 2, 3] // true
```

```javascript
// 在以下比较中, 数组需要被转换为原始类型, 系统先调用 valueOf 方法, 但返回值不是原始值
// 系统继续调用 toString 方法, 得到 "2"
// "2" == 2 比较, 字符串会被转换为数值 2, 所以 2 == 2 比较, 得到的结果是 true
[2] == 2 
```

```javascript
[null] == 0 // true
[undefined] == 0 // true
[] == 0 // true
```

```javascript
// "" == false
// "" == 0
// 0 == 0
[] == ![] // true
```

```javascript
// "[object Object]" == false
// "[object Object]" == 0
// NaN == 0
{} == !{} // false
```

```javascript
// 当两个操作数都是对象时，JavaScript 会比较其内存中的引用地址
[] == []
{} == {}
```

④ null、undefined和其他类型的比较

null 和 undefined 宽松相等的结果为 true，null 和 null 相等，undefined 和 undefined 相等。

null 和 undefined 和其他值比较时都不相等。

null 和 undefined 都是假值。

```javascript
null == undefined // true
null == false // false
undefined == false // false
```

总结：在日常工作中进行相等比较时一律使用严格比较避免隐式类型转换产生的不可预知问题。

只有一种情况除外，当我们要判断对象中是否存在某一个属性时，可以使用宽松比较。

如果一个对象中的属性的值是null或是undefined，我们都认为这个属性是不存在的。

```javascript
const object = {
  x: 100,
};
// 因为 x 无论是 null 还是 undefined, 和 null 进行比较时都会相等
if (object.x == null) {
  console.log("不存在");
} else {
  console.log("存在");
}
```

## 6. 运算中的隐式转换

在使用 + - * / 进行运算时，数据类型会发生隐式类型转换。

\+ 号两边只要有一个运算数是字符串类型，其他运算数都会被转换成字符串类型。

除了 \+ 号以外的其他运算符，比如 - * / 等都会将运算数转换为数值类型。

\+ 作为正号使用会将运算数转换为数值类型。

```javascript
"11" + 11 
"11" - 11
11 + +"11"
```


## 7. 原型对象基本使用

在 javascript 中每一个构造函数都会配备一个名字叫做 prototype 的对象，我们称它为原型对象。

原型对象的作用是为了在实例对象之间进行属性共享。

```javascript
// Person 构造函数
function Person() {}
// Person 构造函数的原型对象
console.log(Person.prototype); 
```

```javascript
// Person 构造函数
function Person(name) {
  this.name = name;
}

// 在 Person 构造函数的原型对象中添加 sayHello 方法
// 所有通过 Person 构造函数创建出来的实例对象都可以调用该方法
Person.prototype.sayHello = function () {
  alert(`Hello, 我是${this.name}`);
};

// 创建 p1 实例
const p1 = new Person("张三");
// 创建 p2 实例
const p2 = new Person("李四");

// 验证 p1 实例是否可以调用 sayHello 方法
p1.sayHello();
// 验证 p2 实例是否可以调用 sayHello 方法
p2.sayHello();
// 验证 p1 和 p2 调用的是否是同一个 sayHello 方法
alert(p1.sayHello === p2.sayHello);
```

实例对象在查找属性时，先在自身进行查找，自身如果找不到再去构造函数的原型对象中查找。

```javascript
p1.sayHello = function () {
  alert(`Hello, 我是${this.name}, 我是实例对象自身身上的 sayHello 方法`);
};

p1.sayHello();
p2.sayHello();
```

在实例对象身上有一个属性叫做 \_\_proto\_\_，它指向了实例的构造函数的原型对象，实例对象在查找属性时就是通过它找到的原型对象。

```javascript
alert(p1.__proto__ === Person.prototype);
```

__proto__ 被称之为隐式原型对象，实例会自动通过它去原型对象中查找，开发者不需要显式的去调用它。

```javascript
alert(p2.sayHello === p2.__proto__.sayHello);
```

在每一个原型对象中都会有一个名字叫做 constructor 的属性，该属性指向了构造函数。

```javascript
alert(Person.prototype.constructor === Person);
alert(p1.constructor === Person);
```

## 8. 原型对象进阶

Person.prototype 对象是 Object 构造函数的实例。

```javascript
// 以下代码不需要开发者编写
Person.prototype = new Object()
```

```javascript
// 此处 p1 调用的 hasOwnProperty 方法以及 toString 方法均来自 Object 构造函数的原型对象
alert(p1.hasOwnProperty("name"));
alert(p1.toString());
```

```javascript
function Person() {}																					

let p1 = new Person();
p1.__proto__ === Person.prototype // true
Person.prototype.__proto__ === Object.prototype // true
Object.prototype.__proto__ === null // true
```

```javascript
function Person() {}
Person.__proto__ === Function.prototype // true
Function.prototype.__proto__ === Object.prototype // true
Object.prototype.__proto__ === null // true
```
## 09. 继承

```javascript
function Person(name) {
  this.name = name;
}

function Student(name, number) {
  this.number = number;
}

const s1 = new Student("张三", 01);
```

```javascript
function Student(name, number) {
  // 继承父类实例属性
  Person.call(this, name);
}
// 继承父类原型属性
Student.prototype.__proto__ = Person.prototype;

const s1 = new Student("张三", 01);
```

```typescript
// ES6 语法糖
class Person {
  constructor(name) {
    this.name = name;
  }
  sayHello() {
    console.log(`Hello, 我是${this.name}`);
  }
}

class Student extends Person {
  constructor(name, number) {
    super(name);
    this.number = number;
  }
  sayNumber() {
    console.log(`我是${this.name}, 我的学号是${this.number}`);
  }
}

console.log(typeof Person); // "function"
const tom = new Student("Tom", 1);
tom.sayHello();
tom.sayNumber();
```

## 10. instanceof

instanceof 运算符用于检查对象的类型，它返回一个布尔值，如果为真则表示该对象是特定类的实例，如果为假则不是。 

```javascript
tom instanceof Student // true
tom instanceof Person  // true
tom instanceof Object  // true
```

```javascript
[] instanceof Array   // true
[] instanceof Object  // true
{} instanceof Object  // true
```

## 11. 作用域

作用域是指变量和函数的可访问范围。

JavaScript 中有全局作用域、局部作用域和块级作用域。

(1) 全局作用域

在全局作用域中声明的变量和函数可以在代码中的任何位置被访问。

```javascript
// 全局作用域中声明变量
var globalVariable = 'global variable';

// 全局作用域中声明函数
function globalFunction() {
  console.log('global function');
}

// 在函数中访问全局变量和函数
function myFunction() {
  console.log(globalVariable);
  globalFunction();
}

// 输出：global variable 和 global function
myFunction(); 
```

(2) 局部作用域

局部作用域是指在函数内部声明的变量和函数，只能在函数内部访问。

```javascript
function myFunction() {
  // 在函数内部声明局部变量
  var localVariable = 'local variable';

  // 在函数内部声明局部函数
  function localFunction() {
    console.log('local function');
  }

  console.log(localVariable);
  localFunction();
}

myFunction(); // 输出：local variable 和 local function
console.log(localVariable); // 报错：localVariable is not defined
```

(3) 块级作用域

块级作用域是指在 if、for、while 等语句中产生的作用域，在其中声明的变量和函数只在该代码块内部有效。

在 ES6 中使用关键字 let 和 const 声明的变量具有块级作用域。

```javascript
// 使用 let 和 const 声明变量具有块级作用域
if (true) {
  let x = 1;
  const y = 2;
}
console.log(x); // 报错：x is not defined
console.log(y); // 报错：y is not defined
```


```javascript
var a = 100;
function print(fn) {
  var a = 200;
  fn();
}
function fn() {
  console.log(a);
}
print(fn);
```

```javascript
for (var i = 1; i <= 3; i++) {
  setTimeout(() => {
    console.log(i);
  }, 0);
}
```

```typescript
for (let i = 1; i <= 3; i++) {
  setTimeout(() => {
    console.log(i);
  }, 0);
}
```

```javascript
console.log(a);
var a = 12;
function fn() {
  console.log(a);
  var a = 13;
}
fn();
console.log(a);
```

```javascript
console.log(a);
var a = 12;
function fn() {
  console.log(a);
  a = 13;
}
fn();
console.log(a);
```

```javascript
console.log(a);
a = 12;
function fn() {
  console.log(a);
  a = 13;
}
fn();
console.log(a);
```

```javascript
var foo = 1;
function bar() {
  if (!foo) {
    var foo = 10;
  }
  console.log(foo);
}
bar();
```

```javascript
var foo = 1;
function bar() {
  // 不管条件是否成立都会进行变量提升 var foo = undefined;
  // if (!undefined) => 将 undefined 转换为布尔值再取反 !false => true
  if (!foo) {
    var foo = 10;
  }
  console.log(foo);
}
bar();
```

```javascript
var a = 10,
  b = 11,
  c = 13;

function test(a) {
  a = 1;
  var b = 2;
  c = 3;
}

test(10);

console.log(a); // 10
console.log(b); // 11
console.log(c); // 3
```

```javascript
if (!("a" in window)) {
  var a = 10;
}
console.log(a);
```

```javascript
var a = 4;

function b(x, y, a) {
  console.log(a);
  // 在 JS 非严格模式下实参集合与形参变量存在映射关系, 严格模式下该关系比切断了
  arguments[2] = 10;
  console.log(a);
}

a = b(1, 2, 3);
console.log(a);
```

```javascript
var foo = "hello";
(function (foo) {
  console.log(foo);
  var foo = foo || "world";
  console.log(foo);
})(foo);
console.log(foo);
```



## 12. 闭包

闭包就是一个函数，一个引用了上级作用域链中的变量的函数，即使外部函数已不存在，也可以通过作用域链访问到外部函数中声明的变量。

```javascript
function outer() {
  var testVar = "test";
  return function() {
    console.log(testVar);
  }
}

var inner = outer();
inner();
```

使用闭包实现模块化开发

```javascript
var module = (function () {
  var privateVar = '这个变量是私有的';
  
  function privateFunction() {
    console.log('私有函数');
  }
  
  return {
    publicVar: '这个变量是公开的',
    publicFunction: function() {
      console.log('公开函数');
    }
  };
})();

console.log(module.publicVar);
module.publicFunction();
```

使用闭包实现计数器功能

```javascript
function counter() {
  var count = 0;
  return function() {
    count++;
    console.log(count);
  }
}

var countFunc = counter();
countFunc(); // 1
countFunc(); // 2
```

使用闭包实现缓存功能

```javascript
function cache() {
  var results = {};
  return function(key, val) {
    if(results[key]) {
      return results[key];
    } else {
      results[key] = val;
      return val;
    }
  }
}

var getResults = cache();
console.log(getResults('a', 1)); // 1
console.log(getResults('a', 2)); // 1
console.log(getResults('b', 2)); // 2
```

使用闭包实现一次性函数

```javascript
function singleUse() {
  var isUsed = false;
  return function() {
    if(!isUsed) {
      console.log('执行一次');
      isUsed = true;
    } else {
      console.log('无法执行！');
    }
  }
}

var useFunc = singleUse();
useFunc(); // 执行一次
useFunc(); // 无法执行！
```

面试题

```javascript
var n = 0;
function a() {
  var n = 10;
  function b() {
    n++;
    console.log(n);
  }
  b();
  return b;
}

var c = a();
c();
console.log(n);
```

## 13. this

JavaScript 中的 this 是一个指向当前执行环境的关键字，用来访问当前执行环境的上下文。

this 具体指向的对象要取决于当前调用方式。

(1) 默认绑定：函数调用时没有明确指定 this 的指向，或者使用的是独立的函数调用方式时，this 会绑定到全局对象上。

```js
function test() {
  console.log(this);
}
test(); // Window (浏览器) / global (Node.js)
```

(2) 隐式绑定：函数作为对象的属性调用时，this 会绑定到该对象。

```js
const obj = {
  name: 'Alice',
  sayName() {
    console.log(this.name);
  }
};
obj.sayName(); // Alice
```

(3) 显式绑定：使用 apply、call、bind 等函数显式调用时，可以指定 this 的指向。

```js
function greet() {
  console.log(`Hello, ${this.name}!`);
}
const person1 = { name: 'Alice' };
const person2 = { name: 'Bob' };
greet.call(person1); // Hello, Alice!
greet.apply(person2); // Hello, Bob!
const boundGreet = greet.bind(person1); // bind 方法返回一个新函数
boundGreet(); // Hello, Alice!
```

(4) new 绑定：使用 new 关键字创建对象时，this 会绑定到新创建的对象上。

```javascript
function Person(name) {
    this.name = name;
}
const person = new Person('Alice');
console.log(person.name); // Alice
```

(5) 箭头函数：箭头函数没有自己的 this 绑定，会继承上一层作用域中的 this。

```js
const obj = {
    name: "Alice",
    logMyName: () => {
        console.log(this.name);
    }
};
obj.logMyName(); // undefined
```
需要注意的是，箭头函数中的 this 不可以被显式地绑定或修改，因为箭头函数根本没有自己的 this。

## 14. 手写 bind 方法

```javascript

```
