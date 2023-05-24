---
title: Js入门到精通
date: 2023-04-06 16:59:52
tags:
top_img: https://img1.baidu.com/it/u=2320525308,409915113&fm=253&fmt=auto&app=138&f=JPEG?w=650&h=366
cover: https://img1.baidu.com/it/u=2320525308,409915113&fm=253&fmt=auto&app=138&f=JPEG?w=650&h=366
---

#  JS入门到精通

##  前言

 JavaScript（简称“JS”） 是一种具有函数优先的轻量级，解释型或即时编译型的[编程语言](https://baike.baidu.com/item/编程语言/9845131)。它是作为开发[Web](https://baike.baidu.com/item/Web/150564)页面的[脚本语言](https://baike.baidu.com/item/脚本语言/1379708)而出名，JavaScript 基于原型编程、多范式的动态[脚本语言](https://so.csdn.net/so/search?q=脚本语言&spm=1001.2101.3001.7020)，并且支持[面向对象](https://baike.baidu.com/item/面向对象/2262089)、命令式、声明式、[函数](https://baike.baidu.com/item/函数/301912)式编程范式。 

##   1. JavaScript是什么

  JavaScript（简称“JS”） 是一种具有函数优先的轻量级，解释型或即时编译型的[编程语言](https://baike.baidu.com/item/编程语言/9845131) 。 

###  1-1.主要的功能

	1. 嵌入 [动态文本](https://baike.baidu.com/item/动态文本)于HTML页面。
 	2.  对浏览器事件做出响应
 	3. 读写 [HTML元素](https://baike.baidu.com/item/HTML元素)。 
 	4. 在数据被提交到服务器之前验证数据。
 	5.  检测访客的浏览器信息。控制cookies，包括创建和修改等 
 	6. 基于[Node.js](https://baike.baidu.com/item/Node.js/7567977)技术进行服务器端编程

###   1-2. 语言的组成

[ECMAScript](https://baike.baidu.com/item/ECMAScript)，描述了该语言的语法和基本[对象](https://baike.baidu.com/item/对象/2331271)。

[文档对象模型](https://baike.baidu.com/item/文档对象模型)（DOM），描述处理网页内容的方法和接口。

浏览器对象模型（[BOM](https://baike.baidu.com/item/BOM/1801)），描述与浏览器进行交互的[方法](https://baike.baidu.com/item/方法/3009367)和[接口](https://baike.baidu.com/item/接口)。



##  2. JS 基础内容

###  2-1. hello world js

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!-- js代码需要编写在scrpit标签内 -->
    <script>
 
        // 控制浏览器弹出警告框
        alert("这是我的第一行js代码!");
 
        // 让计算机在页面输出内容
        document.write("Hello World!!!");
 
        // 向控制台输出内容
        console.log("你猜猜我在哪呢!!!");
 
 
        // alert("这是一个弹窗！！");
        // document.write("这是一个文本内容！！");
        // console.log("这是控制台输出内容");
    </script>
</head>
<body>
    
</body>
</html>

```

运行结果：
{% asset_img 1.png This is an example image %}
{% asset_img 2.png This is an example image %}

###   2-2. js编写的位置

js有三种编写位置的方式

第一种：直接在标签内部使用

第二种：在script标签内使用

第三种：在外部js文件中编写，通过script标签引入（推荐使用）

 **代码如下（示例）：** 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>js编写位置</title>
    <!-- 
        可以将js代码编写到外部js文件中，然后通过script标签引入
        写到外部文件中可以在不同页面同时使用，也可以利用浏览器缓存机制
        推荐使用
    -->
    <!-- 
        script标签一旦引入外部文件了，就不能在此标签内写代码了，即使编写也不会被编译
        如果需要则可以在创建一个新的script标签用于编写内部代码
     -->
    <script src="./js/scrpit.js"></script>
 
 
    <!-- 
            可以将代码编写到script标签内 
        <script>
            alert("我是script标签内的js代码")
        </script>
    -->
</head>
<body>
    <!-- 
        可以将js代码写在标签的onclick属性中
        当我们点击按钮时，js代码才会执行
     -->
    <button onclick="alert('讨厌，你点我干嘛！！！')">点我一下</button>
    <!-- 
        可以将js代码写在超链接的href属性中，当点击超链接时，会执行js代码
     -->
     <a href="javascript:alert('让你点你就点')">你也点我一下</a>
     <a href="javascript:">你也点我一下</a>
</body>
</html>

```

 **运行效果（示例）：**  

{% asset_img 3.png This is an example image %}
{% asset_img 4.png This is an example image %}

###  2-3. js基本语法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>js基本语法</title>
    <script>
        /*
            多行注释
            JS注释
            多行注释：注释中的内容不会被执行，但可以在源代码中查看
        */
        // 单行注释
        // alert("hello");
 
        /*
        * 1.JS严格区分大小写
        * 2.JS中每一条语句中以;结尾
        * 3.JS中会自动忽略多个空格和换行，可以对代码进行格式化
        * 
        */
    //    Alert("该语法不会被执行");
    </script>
</head>
<body>
    
</body>
</html>
```



###  2-4. js字面量和变量

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /*
        * 字面量：都是不可变的值
        *   比如： 1 2 3 4...
        *   字面量可以直接使用，但我们一般不会直接使用字面量
        * 
        * 变量：变量可以用来保存字面量，而且变量可以任意改变
        *    变量可以更加方便使用,在开发中都是使用变量保存一个字面量
        *    而很少直接用字面量
        *    可以通过变量对字面量描述
        *    x=123546
        */
    //    alert(123456)
 
        // 声明变量
        // 在js中使用var关键字声明一个变量
        var a;
        // 为变量赋值
        a = 123;
        a = 456;
        console.log(a);
 
        // 声明和赋值同时进行
        var b = 789 ;
        console.log(b);
 
        var age = 80;
        console.log(age);
    </script>
</head>
<body>
    
</body>
</html>
```



###  2-5. js标识符

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /*
        标识符：
            在js中所有可以由我们自主命名的都可以称为标识符
            例如：变量名、函数名、属性名都属于标识符
            命名要符合一下规则：
                1.标识符中可以含义字母、数字、_、$
                2.标识符不能以数字开头
                3.标识符不能是ES中的关键字和保留字
                4.标识符一般采用驼峰命名法
                                --首字母小写，每个单词的首字母大写，其余小写
            
        */
       var a1_$ = 123;
        // var 22a1_$ = 123;(不能以数字开头)
        // var var = 123;(var是关键字)
        var helloWorld;
    </script>
</head>
<body>
    
</body>
</html>
```



###  2-6. js基本数据类型

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /*
            数据类型指的是字面量的类型
                在js中一共有8大基本数据类型
                    String 字符串
                    Number  数值
                    Boolean 布尔
                    Null    空值
                    Undefined 未定义
                    Object      对象
                    Array    数组
                    Function  函数
            其中String、Number、Boolean、Null、Undefined 为基本数据类型
            Object、Array、Function为引用数据类型
        */
 
        /*
            String字符串
                在js中字符串需要使用引号引起来
                使用双引号和单引号都可以，但是不要混着用
        */
       /*
            在字符串中我们可以使用\作为转义字符
                当表示特殊符号时使用\转义
                \" 表示"
                \' 表示'
                \n 表示换行
                \t 表示制表符
                \\ 表示\
        */
       var str = "hello";
       var str1 = "我说：\"今天是周二!\"";
       console.log(str1);       // 我说："今天是周二!"
       // 输出字面量 字符串str    
       console.log(str);        // hello
       // 输出变量str    
       console.log("str");      // str
 
 
        /*
            Number数值
                在js中所有的数值都是Number类型
                包括整数、小数（浮点数）
                js中可以表示的最大值
                    Number.MAX_VALUE
                js中最小的正值
                    Number.MIN _VALUE
                    Infinity表示正无穷
                    -Infinity表示负无穷
                NaN 是一个特殊的数字
                    使用typeof检查一个NaN也会返回一个number
        */
        //    数值 123
       var a = 123;
        //    字符串 123
       var b = "123";
        /*
            可以使用typeof来检查变量的数据类型
            语法：typeof 变量
            当检查字符串时 会返回string
            检查数值时 会返回 number
        */
       console.log(typeof a);   //number
       console.log(a);  // 123
       console.log(b);  // 123
       console.log(typeof b);  // string
       max = Number.MAX_VALUE;
       console.log(max);
 
    //    使用js整数的运算基本是可以实现准确
        var num = 2 + 4 ;
        console.log(num);   //6
    // 如果使用js进行浮点元素，可能得到一个不精确的结果
        var cc = 0.1 + 0.2 ;
        console.log(cc);    //0.30000000000000004
 
 
 
        /*
            Boolean 布尔值
                布尔值只有两个，主要作为逻辑判断
                true  真
                false  假
        */
        var bool = true;
        console.log(bool);  //true
        console.log(typeof bool);  //boolean
 
 
        /*
            Null类型的值只有一个 就是null
                null这个值专门用来表示空对象
                使用typeof检查null时，返回一个object
        */
       var nul = null;
       console.log(nul); //null
       console.log(typeof nul); //object
 
 
       /*
            Undefined类型的值只有一个 就是Undefined
                当声明一个变量时，但是不给其变量赋值，它的值就是Undefined
        */
        var und;
       console.log(und); //undefined
       console.log(typeof und); //undefined
    </script>
</head>
<body>
    
</body>
</html>
```



###  2-7. js强制类型转换（转为String）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /*
            强制类型转换
                将一个数据类型转换为其他数据类型
                类型转换主要是：将其他的数据类型。转换为
                    string 、 number 、boolean
        **/
       /*
            将其他类型转为string
                方式一：
                    调用被转换数据类型的toString()方法
                    该方法不会影响到原变量，会将转换的结果返回
                    null和undefined这两个值没有toString方法
                方式二：
                    调用String()函数，并将被转换的数据作为参数传递给函数
                        对于number和boolean实际上就是调用的toString()方法
                        但是对于null和undefined，不会调用toString()
                            它会将null转为"null"
                            它会将undefined转为"undefined"
                
       */
        var  a = 123;
        // 调a的toString()的方法
        // a = a.toString()
        // 调用String()函数
        a = null; 
        a = undefined; 
        a = String(a)
        console.log(a);
        console.log(typeof a);
    </script>
</head>
<body>
    
</body>
</html>
```



###  2-8. js强制类型转换（转为Number）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /*
            强制类型转换
                将一个数据类型转换为其他数据类型
                类型转换主要是：将其他的数据类型。转换为
                    string 、 number 、boolean
        **/
       /*
            将其他类型转为number
                方式一：
                    使用我们Number()函数
                            --》字符串转 数字
                               1.如果是纯数字的字符串，则直接转换为数字
                               2.如果是非数字的字符串。则转为NaN
                               3.如果是空字符串，则转为0
                            --》布尔值转 数字
                                true，转为1，false转为0
                            --》null转 数字
                                null转数字为0
                            --》undefined转 数字
                                null转数字为NaN
                            
                方式二：
                    此方式专门对字符串
                    parseInt() 将字符串转为一个整数
                    parseFloat() 将字符串转为一个浮点数
                    如果对非字符串使用，会将其先转为string，然后操作
       */
        var  a = "123";
        var  b = "123px";
        var  c = "3.1415926px";
        // 调用Number()函数将a转换为数值类型
        a = Number(a)
        console.log(a);
        console.log(typeof a);
        // 调用parseInt()函数将a转换为数值类型
        b = parseInt(b)
        console.log(b);
        console.log(typeof b);
        // 调用parseFloat()函数将a转换为数值类型
        c = parseFloat(c)
        console.log(c);
        console.log(typeof c);
    </script>
</head>
<body>
    
</body>
</html>
```



###  2-9. 其他进制的数字

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        
        var a = 123;
 
        /*
            在js中，如果需要表示16进制的数字，则要以0x开头
                    如果需要表示8进制的数字，则以0开头
                    如果需要表示2进制的数字，则要以0b开头,但不是所有的浏览器都支持
        */
        //16进制
        a = 0x10
        // 2进制
        a = 0b10
        // 8进制
        a = "070"
        a = parseInt(a,10)
        console.log(a);  //表示以10进制的方式转换
    </script>
</head>
<body>
    
</body>
</html>
```





###  2-10. js强制类型转换（转为boolean）

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /*
            强制类型转换
                将一个数据类型转换为其他数据类型
                类型转换主要是：将其他的数据类型。转换为
                    string 、 number 、boolean
        **/
       /*
            将其他类型转为boolean
                调用Boolean()函数来转换
                    数字--》布尔
                        除了0和NaN都是true
                    字符串--》布尔
                        除了空串，其余都是true
                    null和undefined都是false
                    对象也会转换为true
       */
      var a = 123;  //true
      a = 0;        //fasle
      a = NaN;       //fasle
      a = Infinity;   //true
      a = "66465";   //true
      a = "";         //fasle
      a = null;         //fasle
      a = undefined;   //fasle
      a = Boolean(a);
      console.log(a);
      console.log(typeof a);
 
    </script>
</head>
<body>
    
</body>
</html>
```

###  2-11. js算术运算符

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
       /*
        运算符也叫操作符
            通过运算符可以对一个或者对个值进行运算
            比如：typeof就是运算符，可以来获取一个值的类型
                    它会将该值的类型以字符串的形式返回
       
            算术运算符
              + 
              两个字符串相加等于拼接的数值
              true + false等于转为数值再相加
              任何数和NaN相加都是NaN
              任何值和字符串做加法运算都会先转为字符串，再拼接
                    我们可以利用此特点，将任意数据类型加上空串，就可以变成字符串
                -
               可以对两个数减法运算，并将结果返回
                *
                可以对两个数进行乘法
                /
                可以对两个数进行除法
                % 取余数
        */
      var a = 123;
      var res = typeof a;
    //   console.log(typeof res);
        a = a + 1; //124
        console.log(a);
        console.log(true + false);  // 1
        console.log(1 + NaN);       // NaN
        console.log("1" + "3");     // 13
        console.log( 1 + "3");      // 13
        console.log( "he" + "llo");      // hello
        console.log(1+2+"3");   //33
        console.log("1"+2+3);   //123
 
    //   任何值做 - * % 都会转为number
            // 可以利用此特点进行类型转换
        console.log(100 - 99);  //1
        console.log(100 - "99");  //1
 
        console.log(2 * 2);     //4
        console.log(2 * "2");     //4
        console.log(2 * null);     //0
        console.log(2 * undefined);     //NaN
 
 
        console.log(4 / 2);     //2
        console.log(4 / undefined);     //NaN
 
 
        console.log(9 % 3);     //0
        console.log(9 % 2);     //1
    </script>
</head>
<body>
    
</body>
</html>

```
###  2-12. js一元运算符
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
       /*
        一元运算符，只需要一个操作数
        +   正号
                正号不会对数字产生任何影响
        -   负号
                负号可以对数字取反
            对于非number的值，先转为number再运算
            可以对其他数据类型进行+，就转为number
       */
        var a = 123;
        a = -a;
        a = true;
        a = "18";
        console.log(-a);
        console.log(1 + +"2" +3);   //6
    </script>
</head>
<body>
    
</body>
</html>
```

###  2-13. js自增和自减
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /*
        自增
            通过自增可以使变量在自身基础上+1
                自增分为两种：后++(a++),前++(++a)
                无论是a++,还是++a，都会使原变量立即自增
                    不同的是a++,++a的值不同
                a++的值等于自增之前的值(原变量的值)
                ++a的值等于自增之后的值(原变量的新值)
            通过自减可以使变量在自身基础上-1
                无论是a--还是--a，都会立即使原变量自减1
                    a--是变量的原值（自减前的值）
                    --a是变量的新增（自减以后的值）
            */
    //    var a = 1;
    //     //使a自增+1
    //     // a++;    
    //     // a++;    
    //     console.log(++a);
    //     console.log(a);
    var c = 10;
    c++;        //在10基础上自增
    console.log(c++);   //11    在11的基础上自增
 
    var d = 20;
    // console.log(++d); //21
    // console.log(++d); //22
 
    //20 + 22 +22
    // var res = d++ + ++d + d;
    // console.log(res);   
 
    d = d++;
    console.log(d);
 
    var num = 10;
    --num;
    console.log(num);   //9
    </script>
</head>
<body>
</body>
</html>
```
###  2-14.  js逻辑运算符
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /*
            js中为我们提供三种逻辑运算符
                ! 非
                    !可以用来对一个值进行非运算
                        非可以对布尔值进行取反
                        true变false，false变true
                        对于非布尔值，则会先转为布尔值，然后再取反
                            可以利用此特点，来将其他数据类型转为布尔类型
                && 与
                    &&可以对符号的两侧的值进行与运算，并返回结果
                    运算规则
                        两个值中只要有一个值为false，就是fasle，反之true
                            如果第一个值是false，则不会校验第二个值，直接false
                            如果第一个值是true，则会校验第二个值
                || 或
                    可以对符号两侧的值进行运算并返回结果
                    运算规则
                        两个值只要有一个true就会返回true
                        两个值都为false，会返回false
                    JS中的或，属于短路的或
                        如果第一个值为true，不会检查第二个值
                        如果第一个值为false，不会检查第二个值
        */
 
        var res = true && false;
        console.log(res);   //false
 
 
        var a = true;
        // 对a进行!运算
        a = !a;
        console.log(a); //false
        var b = 0;
        b = !b;
        console.log(b); //true
 
 
        var ress = true && true;         //true
        var ress = false && false;        //false
        var ress = false && true;        //false
        console.log(ress);
 
        var h = true || true;   //true
        var h = true || false;  //true
        var h = false || true;  //true
        var h = false || false;  //false
        console.log(h); 
 
        true || alert('不会找到我')
        false || alert('会找到我')
    </script>
</head>
<body>
    
</body>
</html>
```

###  2-15. js非布尔值得与或
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /*
            && || 非布尔值的情况
                对于非布尔值进行与或运算，先转为布尔值，再进行运算,并且返回原值
            与运算：
                如果第一个值为true，则必然返回第二个值
                如果第一个值为false，直接返回第一个值
            或
                如果第一个值true,直接返回第一个值
                如果第一个值false,直接返回第二个值
                */
        // true && true;
            // 与运算,如果两个值都为true,则返回第二个值
       var res = 1 && 2;
        // false && true;
            //如果有false，返回false
           res = 2 && 0;
        // false && false;
            //两个都为false，返回前面的值
           res = NaN && 0;
 
        // true && true;
        // 如果第一个值true,直接返回第一个值
           res = 1 || 2;
        // 如果第一个值false,直接返回第二个值
           res = 0 || 2;
           res = "" || "hello";
           res = -1 || "hello";
       console.log(res);
    </script>
</head>
<body>
    
</body>
</html>

```

###  2-16. js赋值运算符
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
       /*
            =
                可以将符号右侧的值赋值给左侧的变量
            +=
                a += 5; ===> a = a + 5; 
            -=
                a -= 5; ===> a = a - 5; 
            *=
                a *= 5; ===> a = a * 5; 
            /=
                a /= 5; ===> a = a / 5; 
            %=
                a %= 5; ===> a = a % 5; 
       */
      var a = 10;
    // a += 5;
    // a -= 5;
    // a *= 5;
    // a /= 5;
    a %= 3;
      console.log(a);
    </script>
</head>
<body>
    
</body>
</html>

```

###  2-17. js关系运算符
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /*
            通过关系运算符，可以比较两个值之间的大小关系
                如果关系成立返回true，反之false
            对于非数字先转为数值，再进行比较
            任何值和NaN作比较都是false
            如果两边都是字符串，不会将其转为数值，而会转为字符串的unicode编码进行比较
            > 大于号
            < 小于号
            >=  大于等于
            <=  小于等于
            ==  等于
                当使用==会字符串先转为数值型，再进行比较
            ===  绝对等于
            !=   不等于
            !==   绝对不等于
        */
        /*
            undefined 衍生自 null
                所以这两个值做相等判断时，会返回true
            NaN 不和任何值相等，包括它本身
        */
       /*
        可以通过isNaN()函数来判断是否是NaN
       
       */
        console.log(5>10);
        console.log(5<10);
        console.log(1>true);
        console.log(1>NaN);
        console.log("5">"10");
        console.log(5<=10);
        console.log(undefined==null);
        console.log(NaN==NaN);
        console.log(5==10);
        console.log(5===5);
        console.log(5!=10);
        console.log(5!==10);
    </script>
</head>
<body>
    
</body>
</html>

```

###  2-18. js编码
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /*
            在字符串中使用转译字符输入Unicode编码
                \u四位编码  16进制编码
        */
        console.log("\u2620");
    </script>
</head>
<body>
    <!-- 在网页中使用Unicode编码 10进制编码 -->
    <h1 style="font-size:100px;">&#9760;</h1>
    <h1 style="font-size:100px;">&#9856;</h1>
</body>
</html>

```

###  2-19. js条件运算符（三元运算符）
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /* 
            条件运算符也叫三元运算符
                语法：
                    条件表达式?语句1:语句2;
                执行流程：
                    条件表达式在执行时，首先对条件表达式进行求值
                        如果值为true，则执行语句1，否则执行语句2
        */
        var a = 10;
        var b = 20;
        var c = 50;
        a > b ? alert('a大'):alert('b大')
        // 不推荐使用 不方便阅读
        var max = a > b ? (a > c ? a : c): (b > c ? b : c);
        console.log(max);
    </script>
</head>
<body>
</body>
</html>
```
###  2-20. js运算符的优先级
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /*
            , 运算符
                使用,可以分割多个语句，一般可以在声明多个变量使用
        */
        //    使用,声明多个变量
        var a , b , c;
 
        /*
        运算符的优先级
            比如先乘除后加减
        */
        console.log(2 + 2*6);
 
        //
        var res = 1 || 2 && 3;
        console.log(res);
    </script>
</head>
<body>
</body>
</html>

```
附：
{% asset_img 5.png This is an example image %}

###  2-21. js代码块
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title></title>
    <script>
        /*
            我们的程序是由一条条语句构成的
                语句是按照自上向下一条条执行
                    同一个{}中的语句称为一条语句
                    他们要么都执行，要么都不执行
                    一个{}中的语句我们称之为一个代码块
                    在代码块的后面不需要写分号
                    js中的代码块只有分组的作用，没有其他作用
                        代码块内容的内容，在外部是完全可见得
                    
        */
        {
            var a = 13;
            alert('hello');
            console.log(6666);
            document.write("语句")
        }
        console.log(a);
        {
            alert('hello');
            console.log(6666);
            document.write("语句")
        }
    </script>
</head>
<body>
</body>
</html>

```

## 总结