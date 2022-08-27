## JavaScript

JS的组成

- ECMAscript (JavaScript语法)
- DOM（页面文档对象模型）
- BOM（浏览器对象模型）

### ECMAscript (JavaScript语法)

- JS有3种书写位置：行内、内嵌、外部

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  <!--  内嵌式的js-->
	<!--  <script>-->
	<!--    alert('摔坏的恐龙');-->
	<!--  </script>-->
  	<!--外部 -->
 
   <script src="./js/my.js"></script>
</head>
<body>
  <!--行内式的js，直接写到元素的内部-->
  <input type ="button" value="卓卓" onclick="alert('蔡程昱')">
</body>
</html>
```

##### 输入输出语句

![image-20220821151943486](C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220821151943486.png)

##### 变量

变量是用于存放数据的容器，通过变量名获取数据吗，甚至修改数据。

变量是程序在内存中申请的一块用来存放数据的空间

变量使用分为两步：1.声明变量  2.赋值

```js
//声明变量
var var_name ; 
//赋值
age =10;
//输出结果
console.log(age);
//变量的初始化
var name ='pei';//声明变量同时赋值为18
var address = '重庆市';
var age = 27;

//弹出一个输入框，提示用户输入姓名
var = myname = prompt('请输入姓名');
// 弹出一个对话框，输出用户刚才输入的姓名
alert(myname);
```

<img src="C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220821155354581.png" alt="image-20220821155354581" style="zoom:67%;" />

```js
//  交换两个变量的值
var  temp;
var  app1 ='red';
var app2 = 'yellow';
temp = app1;
app1 = app2;
```

##### 数据类型

js的变量数据类型是只有程序在运行过程中，根据等号右边中的值来确定。

- 简单数据类型

![image-20220821160344449](C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220821160344449.png)

- 复杂数据类型

Object

##### 运算符

- 算数运算符

<img src="C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220821161746181.png" alt="image-20220821161746181" style="zoom:67%;" />

- 递增或递减运算符

- 比较运算符

<img src="C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220821161952287.png" alt="image-20220821161952287" style="zoom:67%;" />

- 逻辑运算符

<img src="C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220821162026830.png" alt="image-20220821162026830" style="zoom:67%;" />

- 赋值运算符

<img src="C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220821162342910.png" alt="image-20220821162342910" style="zoom:67%;" />

- 运算符优先级

<img src="C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220821162414954.png" alt="image-20220821162414954" style="zoom:67%;" />

##### 流量控制

![image-20220821163035704](C:\Users\pyao\AppData\Roaming\Typora\typora-user-images\image-20220821163035704.png)

```js
if (条件表达式1){
    //执行语句1
} else if(条件表达式2){
    //语句2
} else if(条件表达式3){
    //执行语句3
    
} else{
    //执行语句4
}
```

```js
switch(表达式){
    case value1:
        执行语句1;
        break;
    
    case value2:
        执行语句2;
        break;
    
    case value2:
        执行语句2;
        break;
    default:
        执行最后的语句;
}
```

```js
for(var i =1;i<=100;i++){
    
}
```

```js
while(条件表达式){
    //循环体
}
```

```js
do{
    
}while(条件表达式)
```

##### 数组

```js
//创建数组
var 数组名 = new Array();
var arr = new Array(); //创建一个新的空数组

var arr = [];
var arr = [1,2,3,4,'pink',true];
//获取数组元素
数组名[索引号];

//遍历数组
for(var i=0;i<arr.length;i++){
    
}
//数组中新增元素
//通过修改length长度新增数组元素
arr.length = 56;
//通过修改数组索引新增数组元素。修改索引号，追加数组元素
arr[4] ='red'; 
```

##### 函数

```js
//声明函数
function 函数名(形参1,形参2,...){
    //函数体
}
//形参可以看做是不用声明的变量。调用时没有实参对应就是undefined 
//形参的默认值是undefined
function getSum(num1,num2){
    var sum = 0;
    sum = num1 + num2;
}

//函数表达式声明函数，匿名函数
var 变量名 = function(){};

//调用函数
函数名(实参1,实参2,...);
getSum(1,2);

//函数有返回值
//函数如果有return，返回return后面的结果
//函数如果无return, 返回undefined
function 函数名(){
    return 需要返回的结果;
}

//当我们不确定有多少个参数传递时，可以用arguments来获取
function fn(){
    console.log(arguments);
    for(var i = 0; i<arguments.length;i++){
        
    }
    
}
fn(1,2,3);
fn(1,2)
```

- 函数形参和实参个数不匹配问题

实参的个数 > 形参的个数，会取到形参的个数

实参的个数 < 形参的个数，多余的形参定义为undefined，结果为NaN

- arguments的使用

当我们不确定有多少个参数传递时，可以用arguments来获取。

在JS中，arguments实际上是一个内置对象。所有函数都内置了一个arguments对象，arguments对象中存储了传递的所有实参。

arguments是一个伪数组，并不是一个真正的数组。但它由三个特性：具有数组的length属性；可以用索引号访问元素；没有真正数组的一些方法。

##### JavaScript作用域

- 作用域

  - 全局作用域

    整个script标签，或者是一个单独的js文件

  - 局部作用域

​               在函数内部就是局部作用域

- 全局变量和局部变量

  - 全局变量
    - 在全局作用域下的变量，在全局下都可以使用
    - 如果在函数内部，没有声明直接赋值的变量也属于全局变量

  - 局部变量
    - 在局部作用域下的变量
    - 函数的形参也是局部变量
  - 从执行效率来看全局变量和局部变量：
    - 全局变量：只有浏览器关闭的时候才会销毁，比较占内存资源
    - 局部变量：当程序执行完毕就会销毁，比较节约内存资源
  - 作用域链
    - 如果函数中还有函数，那么在这个作用域下又可以产生一个作用域
    - 内部函数可以访问外部函数。
    - 根据在内部函数可以访问外部函数变量的机制，用链式查找确定哪些数据能被内部函数访问。（就近原则）
    - 

```js
function fn(){//外部函数
    var num =20;
    function fun(){//内部函数
        console.log(num);       
    }
}
```

