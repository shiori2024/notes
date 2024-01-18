# JavaScript学习笔记
我通过这个[JavaScript学习网站](https://zh.javascript.info/)进行学习  
这个JavaScript学习网站是一个开源项目，可以支持一下点个star。  
!!!本篇学习笔记涵盖JavaScript的所有语法（基本上），更多的是记录js的语法和编写规范，更多细节上的码代码还需要读者多加练习。  

> 从头开始学习JavaScript语言，您需要做好以下准备工作：
	- 安装集成开发环境（编写代码的软件）
	- 浏览器（chrome、edge、firefox等）

# JavaScript 简介
* JavaScript最开始是专门为浏览器设计的一门语言，但是现在也被用于很多其他的环境。
* JavaScript 作为被应用最广泛的浏览器语言，且与 HTML/CSS 完全集成，具有独特的地位。
* 有很多其他的语言可以被“编译”成 JavaScript，这些语言还提供了更多的功能。建议最好了解一下这些语言，至少在掌握了 JavaScript 之后大致的了解一下。

# use strict
```js
// 启用严格模式
'use strict';

```

> “class” 和 “module”默认开启“use strict”
  

es5之后为了保证旧的功能能够使用，就需要启用严格模式来激活这些特性。

# 任务1

## 使用变量
重要程度: 2  
声明两个变量：admin 和 name。  
将值 "John" 赋给 name。  
从 name 变量中拷贝其值给 admin。  
使用 alert 显示 admin 的值（必须输出 “John”）。  

```js
let admin,name;
name = John;
admin = name;
alert(admin);//John

```

## 给出正确的名字
重要程度: 3  
使用我们的星球的名字创建一个变量。你会怎么命名这个变量？  
创建一个变量来存储当前浏览者的名字。你会怎么命名这个变量？  

```js
let earth;
let viewUser;
```

## 大写的常量
重要程度: 4  
检查下面的代码：  
```js
const birthday = '18.04.1982';

const age = someCode(birthday);
```
这里我们有一个 birthday 日期常量和通过一些代码（为了保持简短这里没有提供，因为这些细节在这无关紧要）从 birthday 计算出的 age 常量。
对于 birthday 使用大写方式正确吗？那么 age 呢？或者两者都用？
```js
const BIRTHDAY = '18.04.1982'; // 使用大写？
// 应该大写
const AGE = someCode(BIRTHDAY); // 使用大写？
// 被计算出来的常量应该小写
```

# 数据类型
Number类型  
代表整数和浮点数，除了常规的数字外，还有特殊的数值Infinity、-Infinity和NaN。  

Infinity 代表无穷大
```
alert(1/0);//Infinity

alert(Infinity);//Infinity

alert("not a number" / 2);//NaN
```

八种原始数据类型：
- number
- bigint
- string
- boolean
- null
- undefined
- symbol
- object



# 任务2
## 字符串的反引号
重要程度: 5
下面的脚本会输出什么？
```
let name = "Ilya";

alert( `hello ${1}` ); // ?

alert( `hello ${"name"}` ); // ?

alert( `hello ${name}` ); // ?

```

```js
// 分别是
// hello 1
// hello name
// hello Ilya
```

# 交互
alert、prompt、confirm  
alert 显示信息  
prompt 显示信息要求用户输入，点击确定返回文本，点击取消返回null  
confirm 显示信息等待用户点击确定或取消，点击确定返回true，点击取消返回false  

# 任务3
重要程度: 4
创建一个要求用户输入 name，并通过浏览器窗口对键入的内容进行输出的 web 页面。
```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>模态框</title>
</head>
<p id="name"></p>
<body>
	<script>
		let input = prompt('请输入name','');
		alert(input)
		//let name = document.getElementById("name").innerText = ${input};
	</script>
</body>
</html>
```

# 类型转换
string  
number  
boolean  

布尔值转换
- 直观上为“空”的值（0，null，undefined，NaN）都将变为false
- 其他值变成true
`!=0`非0值都为false  

# 任务4
后置运算符和前置运算符  
重要程度: 5  
以下代码中变量 a、b、c、d 的最终值分别是多少？  
```
let a = 1, b = 1;

let c = ++a; // ?  是2
let d = b++; // ?  是1
```
```
console.log(a);// 2
console.log(b);// 2
```

赋值结果  
重要程度：3  
下面这段代码运行完成，代码中的a和x的值是多少？  
```
let a = 2;
let x = 1 + (a *= 2);
```

```js
console.log(a); //4
console.log(x); //5
```


类型转换  
重要程度: 5
下面这些表达式的结果是什么？
```
"" + 1 + 0 //"10"
"" - 1 + 0 //-1
true + false //1
6 / "3" //2
"2" * "3" //6
4 + 5 + "px" //"9px"
"$" + 4 + 5 //"$45"
"4" - 2 //2
"4px" - 2 //NaN
"  -9  " + 5 //" -9 5"
"  -9  " - 5 //-14
null + 1 //1
undefined + 1 //NaN
" \t \n" - 2 //-2
```
好好思考一下，把它们写下来然后和答案比较一下。


修正加法  
重要程度: 5  
这里有一段代码，要求用户输入两个数字并显示它们的总和。  

它的运行结果不正确。下面例子中的输出是 12（对于默认的 prompt 的值）。  

为什么会这样？修正它。结果应该是 3。  
```
let a = prompt("First number?", 1);
let b = prompt("Second number?", 2);

alert(a + b); // 12
//修改为 alert(+a + +b);
```

# 值的比较
比较字符串的大小，  
首先比较两个字符串的首位字符大小；
如果一方字符较大或较小，则继续去除两个字符串各自的后一位字符进行比较。  
重复上述步骤进行比较，直到比较完成某字符串的所有字符为止。  
如果两个字符串的字符同时用完，那么则判定他们相等，否则未结束（还有未比较的字符）的字符串更大。  

## 不同类型间的比较
当对不同类型的值进行比较时，js会首先将其转化为数字（number）再判定大小。  
```js
alert("2" > 1) //true
```

总结：
- 比较运算符始终返回布尔值，
- 字符串的比较，会按照“词典”顺序逐字符地比较大小，
- 当对不同类型的值进行比较时，它们会先被转化为数字（不包括严格相等检查）再进行比较
- 在非严格相等`==`下，`null`和`undefined`相等且不等于任何其他的值
- 在使用`>`或`<`进行比较时，需要注意变量可能为`null/undefined`的情况，比较好的办法是单独检查变量是否`null/undefined`，
- 在严格相等下，不同类型严格不相等。

# 任务5
值的比较  
重要程序：5  
以下表达式的执行结果是？
```
5 > 4 //true
"apple" > "pineapple" //false
"2" > "12" //true
undefined == null //true
undefined === null //false
null == "\n0\n" //false
null === +"\n0\n" //false
```

# 条件分支
if...else语句  
条件运算符 `?`  

条件运算符也叫三元运算符
```js
let result = condition ? value1 : value2;
// 计算条件结果，如果结果为真，则返回 value1，否则返回 value2。
```

# 任务6
if（值为 0 的字符串）  
重要程度: 5  
alert 弹窗会出来吗？  
```js
if ("0") {
  alert( 'Hello' );
}
```
会，它是`“0”`字符串0，是非空的字符串，所以为true，就会执行下面语句。  

JavaScript的名字  
重要程度：2  
使用`if...else`结构，实现提问“What’s the “official” name of JavaScript?”的代码。  
如果访问者输入了 “ECMAScript”，输出就提示 “Right!”，否则 —— 输出：“You don’t know? “ECMAScript”!”  

```js
let question = prompt("What’s the “official” name of JavaScript",'')
if(question == "ECMAScript"){
	alert("Right!");
}else{
	alert("You don’t know? ECMAScript!");
}
```

显示符号  
重要程度：2  
使用`if...else`语句，编写代码实现通过`prompt`获取一个数字并用`alert`显示结果：
- 如果这个数字大于0，就显示1，
- 如果这个数字小于0，就显示-1，
- 如果这个数字等于0，就显示0。
在这个任务中，我们假设输入永远是一个数字。  
```js
let number = prompt("please input number",'')
if(number > 0){
	alert(1);
}else if(number < 0){
	alert(-1);
}else if(number = 0){
	alert(0);
}
```


使用'?'重写'if'语句  
重要程度：5  
使用条件运算符'?'重写下面的if语句：
```js
let result;
if(a + b < 4){
	result = 'Below';
}else{
	result = 'Over';
}
```

```js
let result = (a + b < 4) ? 'Below' : 'Over';
```

使用 '?' 重写 'if..else' 语句  
重要程度: 5  
使用多个三元运算符 '?' 重写下面的 if..else 语句。  
```
let message;

if (login == 'Employee') {
  message = 'Hello';
} else if (login == 'Director') {
  message = 'Greetings';
} else if (login == '') {
  message = 'No login';
} else {
  message = '';
}
```


```js
let message = (login == 'Employee') ? 'Hello' : 
(login == 'Director') ?'Greetings' : 
(login == '') ? 'No login' : 
'';
```

# 逻辑运算符
## || 或

```js
alert(true || true);//true
alert(true || false);//true
alert(false || true);//true
alert(false || false);//false
```
如果操作数不是布尔值，那么它将会被转化为布尔值来参与运算。  
例如：
```js
if(1 || 0){
	alert('true!');
}
```

或运算寻找第一个真值  
从左到右依次计算  

1.获取变量列表或者表达式中的第一个真值。  

例如，我们有变量 firstName、lastName 和 nickName，都是可选的（即可以是 undefined，也可以是假值）。  

我们用或运算 || 来选择有数据的那一个，并显示出来（如果没有设置，则用 "Anonymous"）：  


```js
let firstName = "";
let lastName = "";
let nickName = "SuperCoder";

alert( firstName || lastName || nickName || "Anonymous"); // SuperCoder
```

2.短路求值  
`||`对其参数进行处理，直到达到第一个真值，然后立即返回该值，而无需处理其他参数。  

在下面这个例子中，只会打印第二条信息：  
```js
true || alert("not printed");//在遇到 true 时立即停止运算，所以 alert 没有运行。
false || alert("printed");
```

## && 与

```js
alert( true && true);//true
alert( false && true);//false
alert(true && false);//false
alert(false && false);//false
```
除了`true`与`true`是true,其他都为`false`。  

如果第一个操作数是真值，与运算返回第二个操作数。  
如果第一个操作数是假值，与运算将直接返回它。第二个操作数会被忽略。  
如果所有的值都是真值，最后一个值将会被返回。  
```JS
// 如果第一个操作数是真值，
// 与运算返回第二个操作数：
alert( 1 && 0 ); // 0
alert( 1 && 5 ); // 5
```
与运算的优先级比或运算的优先级要高  

## ! 非
`!`表示布尔非运算符。  
返回相反的值。  
```js
alert( !true );//false
alert( !0 );//true
```
两个非运算`!!`将值转换成布尔类型。  
```js
alert( !!"string");//true
alert( !!null );//false
```

# 任务7
或运算的结果是什么？  
重要程度：5  
如下代码将会输出什么？  
```js
alert(null || 2 || undefined);//2
```


或运算和alert的结果是什么？  
重要程度：3  
下面的代码将会输出什么？  
```js
alert(alert(1) || 2 || alert(3));
```
```
对 alert 的调用没有返回值。或者说返回的是 undefined。

第一个或运算 || 对它的左值 alert(1) 进行了计算。这就显示了第一条信息 1。
函数 alert 返回了 undefined，所以或运算继续检查第二个操作数以寻找真值。
第二个操作数 2 是真值，所以执行就中断了。2 被返回，并且被外层的 alert 显示。
这里不会显示 3，因为运算没有抵达 alert(3)。
```

与操作的结构是什么？  
重要程度：5  
下面这段代码将会显示什么？  
```js
alert(1 && null && 2);//null
```

与运算连接的alert的结果是什么？  
重要程度：3  
这段代码将会显示什么？  
```js
alert(alert(1) && alert(2));
```
```
答案：1，然后 undefined。

调用 alert 返回了 undefined（它只展示消息，所以没有有意义的返回值）。

因此，&& 计算了它左边的操作数（显示 1），然后立即停止了，因为 undefined 是一个假值。&& 就是寻找假值然后返回它，所以运算结束。

```

或运算、与运算、或运算串联的结果是什么？  
重要程度：5  
结果将会是什么？  
```js
alert( null || 2 && 3 || 4 );//3
```


检查值是否位于范围区间内  
重要程度：3  
写一个if条件语句来检查`age`是否位于`14`到`90`的闭区间。  
```js
		let age = prompt("请输入一个数",'');
		if(age >= 14 && age <= 90){
			alert("true");
		}else{
			alert("false");
		}
```

检查值是否位于范围之外  
重要程度：3  
写一个if条件语句，检查`age`是否不位于`14`到`90`的闭区间。  
```js
		let age = prompt("请输入一个数",'');
		if(!(age >= 14 && age <= 90)){
			alert("您输入的数没有在【14~90】这个范围内");
		}else{
			alert("您输入的数在【14~90】这个范围内");
		}

		// or
		/*
		let age = prompt("请输入一个数",'');
		if(age <= 14 || age >=90){
			alert("您输入的数没有在【14~90】这个范围内");
		}else{
			alert("您输入的数在【14~90】这个范围内");
		}
		*/
```

一个关于`if`的问题  
重要程度：5  
下面哪一个`alert`将会被执行  
if语句内表达式的结果是什么？  
```js
if(-1 || 0) alert('first');
if(-1 && 0) alert('second');
if(null || -1 && 1) alert('third');
```
```
第一个和第三个会执行
```

登录校验  
重要程度：3  
实现使用 prompt 进行登录校验的代码。  

如果访问者输入 "Admin"，那么使用 prompt 引导获取密码，如果输入的用户名为空或者按下了 Esc 键 —— 显示 “Canceled”，如果是其他字符串 —— 显示 “I don’t know you”。  

密码的校验规则如下：  

如果输入的是 “TheMaster”，显示 “Welcome!”，
其他字符串 —— 显示 “Wrong password”，
空字符串或取消了输入，显示 “Canceled.”。  

请使用嵌套的 if 块。注意代码整体的可读性。  
提示：将空字符串输入，prompt 会获取到一个空字符串 ''。Prompt 运行过程中，按下 ESC 键会得到 null。  
```js
let username = prompt("请输入用户名",'');
if(username == "Admin"){
	let password = prompt("请输入密码",'');
	if(password == "TheMaster"){
		alert("Welcome!")
	}else if(password != "TheMaster"){
		alert("Wrong password")
	}else if(password == null){
		alert("Canceled")
	}
}else if(username != "Admin"){
	alert("I don’t know you")
}else if(username == null){
	alert("Canceled")
}
```

# 空值合并运算符
空值合并运算符`??`  
当一个值既不是`null`也不是`undefined`时，我们称其为“已定义的”。  

例如：  
`a ?? b`的结果是：
- 如果a是已定义的，则结果为a，
- 如果a不是已定义的，则结果为b。

```js
let a,b;
a = 1;
a ?? b;// 1
// or
/*
let a,b;
a ?? b;//b
*/
```



`||` 和 `??` 的区别：

- || 返回第一个 真 值。
- ?? 返回第一个 已定义的 值。

```js
let height = 0;

alert(height || 100); // 100，返回第一个真值
alert(height ?? 100); // 0，返回已定义
```

`??` 和 `||` 优先级相同  
`??`空值合并运算符常被用于为变量分配默认值，它可以区分出`null`和`undefinded`  
`??`的优先级非常低，仅略高于`?`和`=`  ，在使用表达式时考虑添加括号，如果没有添加括号不能和`||` 或 `&&`一起使用。  

# 循环
循环 while和for  

## 标签
标签 是在循环之前带有冒号的标识符  

```js
labelName: for(...){...}
```

```js
outer: for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // 如果是空字符串或被取消，则中断并跳出这两个循环。
    if (!input) break outer; // (*)

    // 用得到的值做些事……
  }
}

alert('Done!');
```

三种循环语句：
- while——每次迭代前都要检查条件
- do...while——每次迭代后都要检查条件
- for(;;)——每次迭代前都要检查条件，可以使用其他设置（无限循环）

# 任务8
最后一次循环的值  
重要程度：3  
此代码最后一次alert值是多少？为什么？  
```js
let i = 3;

while (i) {
  alert( i-- );//2 1
}
```
```
最后一次alert值是：1
```

while 循环显示哪些值？  
重要程度：4  
对于每次循环，写出你认为会显示的值，然后与答案比较  
以下两个循环的alert值是否相同？  
1.前缀形式`++i`
```js
let i = 0;
while(++i < 5) alert(i);//1 2 3 4
```

2.后缀形式`i++`
```js
let i = 0;
while(i++ < 5)alert(i);//1 2 3 4 5
```

for循环显示哪些值？  
重要程度：4  
对于每次循环，写下它将显示的值。然后然后与答案进行比较。  

两次循环 alert 值是否相同？  

1.后缀形式
```js
for (let i = 0; i < 5; i++) alert( i );//0 1 2 3 4
```
2.前缀形式
```js
for (let i = 0; i < 5; ++i) alert( i );//0 1 2 3 4
```
相同  

使用for循环输出偶数  
重要程度：5  
使用for循环输出2到10的偶数  
```js
for(let i = 2;i<11;i++){
	if(i % 2  == 0){
		alert(i)
	}
}
```

用`while`替换`for`  
重要程度：5  
重写代码，在保证不改变其行为的情况下，将 for 循环更改为 while（输出应保持不变）。  
```
for (let i = 0; i < 3; i++) {
  alert( `number ${i}!` );
}
```
```js
let i = 0;
while(i < 3){
	alert(`number ${i}！`);
	i++;
}
```


重复输入，直到正确为止  
重要程度：5  
编写一个提示用户输入大于`100`的数字的循环。如果用户输入其他数值 —— 请他重新输入。  

循环一直在请求一个数字，直到用户输入了一个大于 100 的数字、取消输入或输入了一个空行为止。  

在这我们假设用户只会输入数字。在本题目中，不需要对非数值输入进行特殊处理。  
```js
let tip = prompt("请输入大于100的数字",'')
for(;tip < 100;){
	if(tip < 100){
		tip = prompt("请重新输入",'');
		if(tip == null || tip == ' '){
			break;
		}
	}
}
```


输出素数  
重要程度：3  
```
大于 1 且不能被除了 1 和它本身以外的任何数整除的整数叫做素数。

换句话说，n > 1 且不能被 1 和 n 以外的任何数整除的整数，被称为素数。

例如，5 是素数，因为它不能被 2、3 和 4 整除，会产生余数。

写一个可以输出 2 到 n 之间的所有素数的代码。

当 n = 10，结果输出 2、3、5、7。

P.S. 代码应适用于任何 n，而不是对任何固定值进行硬性调整。
```

```js
let num = prompt("请输入一个范围",'');
nextPrime:for(let i = 2;i <= num;i++){
		for(let j = 2;j <= i;j++){
			if(i % j == 0) continue nextPrime;
		}
		alert(i);
}
```
这段代码有很大的优化空间。例如，我们可以从 2 到 i 的平方根之间的数中寻找除数。无论怎样，如果我们想要在很大的数字范围内实现高效率，我们需要改变实现方法，依赖高等数学和复杂算法，如二次筛选法（Quadratic sieve），普通数域筛选法（General number field sieve）等。

译注：素数也称为质数，对本答案的代码进一步优化，其实就是一道 LeetCode 算法题，感兴趣的可以点击链接查看如何通过 埃拉托斯特尼筛法筛选素数。

# switch

# 函数
一个函数一个行为  
可以被调用很多次，而不需要写重复的代码。  
为了使代码简洁易懂，建议在函数中主要使局部变量和参数。  
## 局部变量

## 外部变量

## return
可以在函数任意位置，当执行到达时，将值返回给调用代码。  
空值的return或没有return的函数返回`undefined`  

# 任务9
是否需要"else"  
重要程度：4  
如果参数age大于18，那么下面的函数将返回 true。  
否则它将会要求进行确认，并返回确认结果：  
```js
function checkAge(age){
	if(age > 18){
		return true;
	}else{
		return confirm('父母允许吗？');
	}
}
```

如果 else 被删除，函数的工作方式会不同吗？
```js
function checkAge(age){
	if(age > 18){
		return true;
	}
	return confirm('父母允许吗？');
}
```

这两个变体的行为是否有区别？  
答：有区别，第一个是，age大于18会返回true，否则返回return confirm；第二是，不管age返回是否为true，都会返回一个return confirm。  



使用"?"或者"||"重写函数  
重要程度：4  
如果参数 age 大于 18，那么下面的函数返回 true。

否则它将会要求进行确认，并返回确认结果：  
```
function checkAge(age) {
  if (age > 18) {
    return true;
  } else {
    return confirm('Do you have your parents permission to access this page?');
  }
}
```
重写这个函数并保证效果相同，不使用 if，且只需一行代码。

```js
function checkAge(age){
	return (age > 18) ? true : confirm('Do you have your parents permission to access this page?');
	// or
	// return (age > 18) || confirm('Do you have your parents permission to access this page?');
}
```

函数min(a,b)  
重要程度：1  
写一个返回数字`a`和`b`中较小的那个数的函数`min(a,b)`。  
例如：
```
min(2, 5) == 2
min(3, -1) == -1
min(1, 1) == 1
```

答：  
```js
function calcMin(a,b){
	return a > b ? b : a;
}
calcMin(1,4);//1
```

函数pow(x,n)
重要程度：4  
写一个函数pow(x,n)，返回x的n次方。  
例如：
```
pow(3, 2) = 3 * 3 = 9
pow(3, 3) = 3 * 3 * 3 = 27
pow(1, 100) = 1 * 1 * ...*1 = 1
```
答：
```js
function calcPow(){
	let x = prompt('输入一个数','');
	let n = prompt(`你想计算${x}的几次方？`,'');
	return x ** n
}
alert(calcPow());
```

# 函数表达式
function 关键字后面没有函数名。函数表达式允许省略函数名。  

# 回调函数

# 函数声明，函数表达式
在函数声明被定义之前，它就可以被调用。
函数声明的另一个特殊的功能是它的块级作用域。  
严格模式下，当一个函数声明在一个代码块内时，它在该代码块内的任何位置都是可见的。但在代码块外不可见。  


# 箭头函数
```js
let func = (arg1,arg2,...,argN) => expression;
```
```js
let sum = (a,b) => a+b;
alert(sum(1,2));//3
```
如果只有一个参数时，我们还可以省略掉参数外的括号，使代码更短。
```js
let d = n => n*2;
alert(d(2));//4
```

# 任务10
用箭头函数重写

# 

