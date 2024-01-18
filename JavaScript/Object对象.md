# Object对象
创建一个空对象  
```js
let user = new Object(); // “构造函数” 的语法
let user = {};  // “字面量” 的语法
```

```js
let user = {
	name: "john",
	age: 30,
	"likes birds": true //多词属性名必须加引号
};

alert(user.name);//john
delete user.age;//通过delete操作符移除属性
```

通过方括号访问对象内的属性
```js
let user = {};
user["likes birds"] = true;
alert(user["likes birds"]);//true
delete user["likes birds"];//通过delete操作符移除属性
```

属性名简写
```js
let user = {
	name, // 与 name: name 相同
	age,  // 与 age: age 相同
}
```
属性名称限制  
我们已经知道，变量名不能是编程语言的某个保留字，如 “for”、“let”、“return” 等……

但对象的属性名并不受此限制：
```js
// 这些属性都没问题
let obj = {
  for: 1,
  let: 2,
  return: 3
};

alert( obj.for + obj.let + obj.return );  // 6
```

属性命名没有限制。属性名可以是任何字符串或者 symbol类型。  

其他类型会被自动地转换为字符串。
例如，当数字 0 被用作对象的属性的键时，会被转换为字符串 "0"：  
```js
let obj = {
  0: "test" // 等同于 "0": "test"
};

// 都会输出相同的属性（数字 0 被转为字符串 "0"）
alert( obj["0"] ); // test
alert( obj[0] ); // test (相同的属性)
```
JavaScript 的对象有一个需要注意的特性：能够被访问任何属性。即使属性不存在也不会报错！
读取不存在的属性只会得到`undefined`。  
```js
let user = {};

alert( user.noSuchProperty === undefined ); // true 没有这个属性
```
还可以通过`in`来检查属性是否存在。  
```js
let user = { name: "John", age: 30 };
alert( "age" in user ); // true，user.age 存在
alert( "blabla" in user ); // false，user.blabla 不存在。
```
for...in循环  
遍历对象
```js
let user = {
	name: "john",
	age: 30,
	isAdmin: true
};
for(let key in user){
	alert(key);//输出user的所有属性键 name,age,isAdmin
	alert( user[key] )//输出user的属性值 john,30.true
}
```
JavaScript中还有很多其他类型的对象：
- Array用于存储有序数据集合，
- Date用于存储时间日期，
- Error用于存储错误信息。
- ...等等。

## 任务11
你好对象  
重要程度: 5  
按下面的要求写代码，一条对应一行代码：  
1.创建一个空的对象 user。  
2.为这个对象增加一个属性，键是 name，值是 John。  
3.再增加一个属性，键是 surname，值是 Smith。  
4.把键为 name 的属性的值改成 Pete。  
5.删除这个对象中键为 name 的属性。  
```js
let user = {}
// or 
// let user = new Object();
user.name = "John";
user.surname = "Smith";
user.name = "Pete";
delete user.name;
```

检查空对象  
重要程度: 5  
写一个 isEmpty(obj) 函数，当对象没有属性的时候返回 true，否则返回 false。  
```js
function isEmpty(obj){
	for (let key in obj){
		return false;
	}
	return true;
}
```
对象属性求和  
重要程度：5  
我们有一个保存着团队成员工资的对象：
```js
let salaries = {
	John: 100,
	Ann: 160,
	Pete: 130
}
let sum = 0;
for (let key in salaries){
	sum += salaries[key];
}

alert(sum);
```

将数值属性值都乘以 2  
重要程度: 3  
创建一个 multiplyNumeric(obj) 函数，把 obj 所有的数值属性值都乘以 2。  

例如：
```
// 在调用之前
let menu = {
  width: 200,
  height: 300,
  title: "My menu"
};

multiplyNumeric(menu);

// 调用函数之后
menu = {
  width: 400,
  height: 600,
  title: "My menu"
};
```
注意 multiplyNumeric 函数不需要返回任何值，它应该就地修改对象。

P.S. 用 typeof 检查值类型。

```js
let menu = {
  width: 200,
  height: 300,
  title: "My menu"
};

function multiplyNumeric(obj){
	for(let i in obj){
		if(typeof obj[i] == 'number'){
			obj[i] *= 2;
			alert(obj[i]);
		}
	}
}
multiplyNumeric(menu);
```

## 对象引用和复制
对象的复制与变量的复制有所不同，  
当一个对象变量被复制 —— 引用被复制，而该对象自身并没有被复制。  
通过引用来比较
```js
let a = {};
let b = a; // 复制引用

alert( a == b ); // true，都引用同一对象
alert( a === b ); // true
```
```js
let a = {};
let b = {}; // 两个独立的对象

alert( a == b ); // false
```
那么，拷贝一个对象变量会又创建一个对相同对象的引用。  

但是，如果我们想要复制一个对象，那该怎么做呢？  

我们可以创建一个新对象，通过遍历已有对象的属性，并在原始类型值的层面复制它们，以实现对已有对象结构的复制。  
我们也可以使用`Object.assign`方法来达成同样的效果。
```js
Object.assign(dest, [src1, src2, src3...])
```

## 深层克隆
到现在为止，我们都假设 user 的所有属性均为原始类型。但属性可以是对其他对象的引用。  
例如：
```js
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

alert( user.sizes.height ); // 182
```
现在这样拷贝 clone.sizes = user.sizes 已经不足够了，因为 user.sizes 是个对象，它会以引用形式被拷贝。因此 clone 和 user 会共用一个 sizes：
```js
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

let clone = Object.assign({}, user);

alert( user.sizes === clone.sizes ); // true，同一个对象

// user 和 clone 分享同一个 sizes
user.sizes.width++;       // 通过其中一个改变属性值
alert(clone.sizes.width); // 51，能从另外一个获取到变更后的结果
```
为了解决这个问题，并让 user 和 clone 成为两个真正独立的对象，我们应该使用一个拷贝循环来检查`user[key]`的每个值，如果它是一个对象，那么也复制它的结构。这就是所谓的“深拷贝”。  
我们可以使用递归来实现它。或者为了不重复造轮子，采用现有的实现，例如 lodash 库的 _.cloneDeep(obj)。

对象通过引用被赋值和拷贝。  
一个变量存储的不是"对象的值"，而是一个对值的"引用"（内存地址）。因此，拷贝此类变量所拷贝的是引用，而不是对象本身。  
所有通过被拷贝的引用的操作都作用在同一个对象上。  
为了创建真正的拷贝（克隆），我们可以使用`Object.assign`来作"浅拷贝"，或者使用“深拷贝”函数，例如 `_.cloneDeep(obj)`。

## 垃圾回收
JavaScript 的内存管理是自动的、无形的。  
### 可达性
JavaScript 中主要的内存管理概念是 可达性。  
“可达”值是那些以某种方式可访问或可用的值。它们一定是存储在内存中的。  
例如：
对一个对象引用
```js
let user = {
	name : "John"
};

user = null;//如果user的值被重写了，这个引用就没有了，变为不可达，垃圾回收器会认为它是垃圾数据并进行回收，然后释放内存。
```
### 内部算法
垃圾回收的基本算法被称为 “mark-and-sweep”。
闲时收集（Idle-time collection）—— 垃圾收集器只会在 CPU 空闲时尝试运行，以减少可能对代码执行的影响。  

垃圾回收是自动完成的，我们不能强制执行或是阻止执行。  
当对象是可达状态时，它一定是存在与内存中的。  
被引用与可访问（从一个根）不同，一组相互连接的对象可能整体都不可达。  

## this
对象方法this  
方法可以将对象引用为`this`
this的值是在程序运行时得到的。
- 一个函数在声明时，可能就使用了this，但是这个this只有在函数被调用时才会有值。
- 可以在对象之间复制函数。
- 以"方法"的语法调用函数时：`object.method()`，调用过程中的this值时object。
箭头函数没有this，在箭头函数内部访问到的this都是外部获取的。  

## 任务12
在对象字面量中使用 "this"  
重要程度: 5  
这里 makeUser 函数返回了一个对象。  

访问 ref 的结果是什么？为什么？  
```js
function makeUser() {
  return {
    name: "John",
    ref: this
  };
}

let user = makeUser();

alert( user.ref.name ); // 结果是什么？
```
```
答：结果是，
John
```
创建一个计算器  
重要程度: 5  
创建一个有三个方法的 calculator 对象：  

read() 提示输入两个值，并将其保存为对象属性，属性名分别为 a 和 b。  
sum() 返回保存的值的和。  
mul() 将保存的值相乘并返回计算结果。  
```js
let calculator = {
  // ……你的代码……
	read: function(){
		this.a = prompt("请输入一个数",'');
		this.b = prompt("请再输入一个数",'');
	},
	sum(){
		let sum = +this.a + +this.b;
		return "两数和为："+sum;
	},
	mul(){
		let mul = +this.a * +this.b;
		return "两数乘积为："+mul;
	}
};

calculator.read();
alert( calculator.sum() );
alert( calculator.mul() );
```

链式（调用）  
重要程度: 2  
有一个可以上下移动的 ladder 对象：  
```js
let ladder = {
  step: 0,
  up() {
    this.step++;
  },
  down() {
    this.step--;
  },
  showStep: function() { // 显示当前的 step
    alert( this.step );
  }
};
```
现在，如果我们要按顺序执行几次调用，可以这样做：
```js
ladder.up();
ladder.up();
ladder.down();
ladder.showStep(); // 1
ladder.down();
ladder.showStep(); // 0
修改 up，down 和 showStep 的代码，让调用可以链接，就像这样：

ladder.up().up().down().showStep().down().showStep(); // 展示 1，然后 0
```
这种方法在 JavaScript 库中被广泛使用。

## 构造器和操作符"new"
### 构造函数
构造函数在技术上是常规函数。不过有两个约定：

- 它们的命名以大写字母开头。
- 它们只能由 "new" 操作符来执行。
例如：
```js
function User(name){
	this.name = name;
	this.isAdmin = false;
}
let user = new User("Jack");
alert(user.name);//Jack
```
当一个函数被使用new操作符执行时，它按照以下步骤：
1.一个新的空对象被创建并分配给this
2.函数体执行。通常它会修改this，为其添加新的属性。
3.返回this的值。
换句话说，new User(...)做的就是类似的事情：  
```js
function User(name){
	// this = {};(隐式创建)
	this.name = name;
	// return this;(隐式返回)
}
```
这是构造器的主要目的 —— 实现可重用的对象创建代码。  
构造函数只能使用 new 来调用。这样的调用意味着在开始时创建了空的 this，并在最后返回填充了值的 this。  

## 任务13
两个函数 —— 一个对象  
重要程度: 2  
是否可以创建像 new A() == new B() 这样的函数 A 和 B？  
```js
function A() { ... }
function B() { ... }

let a = new A;
let b = new B;

alert( a == b ); // true
```
```js
let obj = {};
let A = function(){
	return obj;
};
let B = function(){
	return obj;
};

let a = new A;
let b = new B;
alert( a == b);
```

创建 new Calculator  
重要程度: 5  
创建一个构造函数 Calculator，它创建的对象中有三个方法：  

read() 使用 prompt 请求两个值并把它们记录在对象的属性中。  
sum() 返回这些属性的总和。  
mul() 返回这些属性的乘积。  
例如：
```js
let calculator = new Calculator();
calculator.read();

alert( "Sum=" + calculator.sum() );
alert( "Mul=" + calculator.mul() );
```
答：
```js
function Calculator(){
	this.read = function(){
		this.a = prompt("请输入一个数",'');
		this.b = prompt("请再输入一个数",'');
	},
	this.sum = function(){
		return +this.a + +this.b;
	},
	this.mul = function(){
		return this.a * this.b;
	}
};

let calculator = new Calculator();
calculator.read();

alert( "Sum=" + calculator.sum() );
alert( "Mul=" + calculator.mul() );
```

创建 new Accumulator
重要程度: 5
创建一个构造函数 Accumulator(startingValue)。

它创建的对象应该：

将“当前 value”存储在属性 value 中。起始值被设置到构造器 startingValue 的参数。
read() 方法应该使用 prompt 来读取一个新的数字，并将其添加到 value 中。
换句话说，value 属性是所有用户输入值与初始值 startingValue 的总和。

下面是示例代码：
```js
let accumulator = new Accumulator(1); // 初始值 1

accumulator.read(); // 添加用户输入的 value
accumulator.read(); // 添加用户输入的 value

alert(accumulator.value); // 显示这些值的总和
```

答：
```js
function Accumulator(startingValue){
	this.read = function(){
		let a = prompt("请输入一个数字",'');
		this.value = +a + +startingValue;
	}
}

let accumulator = new Accumulator(1); // 初始值 1

accumulator.read(); // 添加用户输入的 value

alert(accumulator.value); // 显示这些值的总和
```

## 可选链"?."
这是一个最近添加到 JavaScript 的特性。 旧式浏览器可能需要 polyfills.  
可选链 ?. 是一种访问嵌套对象属性的安全的方式。即使中间的属性不存在，也不会出现错误。  
```js
let user = {}; // user 没有 address 属性

alert( user?.address?.street ); // undefined（不报错）
```
可选链 ?. 不是一个运算符，而是一个特殊的语法结构。它还可以与函数和方括号一起使用。  

## symbol 类型
根据规范，只有两种原始类型可以用作对象属性键：

- 字符串类型
- symbol 类型
“symbol” 值表示唯一的标识符。  
可以使用 Symbol() 来创建这种类型的值：
```js
let id = Symbol();
```
创建时，我们可以给 symbol 一个描述（也称为 symbol 名），这在代码调试时非常有用：
```js
// id 是描述为 "id" 的 symbol
let id = Symbol("id");
```
symbol 是带有可选描述的“原始唯一值”。
```js
let id1 = Symbol("id");
let id2 = Symbol("id");
alert(id1 == id2);//false
```
symbol 不会被自动转换为字符串，symbol 比较特殊，它不会被自动转换。

例如，这个 alert 将会提示出错：  
```js
let id = Symbol("id");
alert(id); // 类型错误：无法将 symbol 值转换为字符串。
```
这是一种防止混乱的“语言保护”，因为字符串和 symbol 有本质上的不同，我们需要调用`.toString()`，
```js
let id = Symbol("id");
alert(id.toString()); // Symbol(id)，现在它有效了
```
或者获取 symbol.description 属性，只显示描述（description）：
```js
let id = Symbol("id");
alert(id.description); // id
```
symbol 允许我们创建对象的“隐藏”属性
```js
let user = { // 属于另一个代码
  name: "John"
};

let id = Symbol("id");

user[id] = 1;

alert( user[id] ); // 我们可以使用 symbol 作为键来访问数据
```
使用 Symbol("id") 作为键，比起用字符串 "id" 来有什么好处呢？
由于 user 对象属于另一个代码库，所以向它们添加字段是不安全的，因为我们可能会影响代码库中的其他预定义行为。但 symbol 属性不会被意外访问到。第三方代码不会知道新定义的 symbol，因此将 symbol 添加到 user 对象是安全的。  

如果我们要在对象字面量 {...} 中使用 symbol，则需要使用方括号把它括起来。
```js
let id = Symbol("id");

let user = {
  name: "John",
  [id]: 123 // 而不是 "id"：123
};
```
symbol 属性不参与 for..in 循环。  
Object.assign 会同时复制字符串和 symbol 属性。

## 全局 symbol
```js
// 从全局注册表中读取
let id = Symbol.for("id"); // 如果该 symbol 不存在，则创建它

// 再次读取（可能是在代码中的另一个位置）
let idAgain = Symbol.for("id");

// 相同的 symbol
alert( id === idAgain ); // true
```
对于全局Symbol，`Symbol.for(key)`按名字返回一个Symbol。通过全局 Symbol 返回一个名字，我们可以使用 Symbol.keyFor(sym)：
```js
// 通过 name 获取 symbol
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// 通过 symbol 获取 name
alert( Symbol.keyFor(sym) ); // name
alert( Symbol.keyFor(sym2) ); // id
```
所有 symbol 都具有 description 属性。
```js
let globalSymbol = Symbol.for("name");
let localSymbol = Symbol("name");

alert( Symbol.keyFor(globalSymbol) ); // name，全局 symbol
alert( Symbol.keyFor(localSymbol) ); // undefined，非全局

alert( globalSymbol.description ); // name
alert( localSymbol.description ); // name
```
[symbol规范表](https://tc39.es/ecma262/#sec-well-known-symbols)  

## 对象 —— 原始值转换
### hint
"string"  
对象到字符串的转换，当我们对期望一个字符串的对象执行操作时，如 “alert”：  
```js
// 输出
alert(obj);

// 将对象作为属性键
anotherObj[obj] = 123;
```
"number"  
对象到数字的转换，例如当我们进行数学运算时：
```js
// 显式转换
let num = Number(obj);

// 数学运算（除了二元加法）
let n = +obj; // 一元加法
let delta = date1 - date2;

// 小于/大于的比较
let greater = user1 > user2;
```
### Symbol.toPrimitive
我们从第一个方法开始。有一个名为 Symbol.toPrimitive 的内建 symbol，它被用来给转换方法命名，像这样：
```
obj[Symbol.toPrimitive] = function(hint) {
  // 这里是将此对象转换为原始值的代码
  // 它必须返回一个原始值
  // hint = "string"、"number" 或 "default" 中的一个
}
```

```js
let user = {
  name: "John",
  money: 1000,

  [Symbol.toPrimitive](hint) {
    alert(`hint: ${hint}`);
    return hint == "string" ? `{name: "${this.name}"}` : this.money;
  }
};

// 转换演示：
alert(user); // hint: string -> {name: "John"}
alert(+user); // hint: number -> 1000
alert(user + 500); // hint: default -> 1500
```
从代码中我们可以看到，根据转换的不同，user 变成一个自描述字符串或者一个金额。`user[Symbol.toPrimitive]` 方法处理了所有的转换情况。  
### toString/valueOf
默认情况下，普通对象具有 toString 和 valueOf 方法：  
- toString 方法返回一个字符串 "[object Object]"。
- valueOf 方法返回对象自身。

### 进一步的转换
```js
let obj = {
  // toString 在没有其他方法的情况下处理所有转换
  toString() {
    return "2";
  }
};

alert(obj * 2); // 4，对象被转换为原始值字符串 "2"，之后它被乘法转换为数字 2。
```
总结：  
对象到原始值的转换，是由许多期望以原始值作为值的内建函数和运算符自动调用的。  

这里有三种类型（hint）：  

"string"（对于 alert 和其他需要字符串的操作）  
"number"（对于数学运算）  
"default"（少数运算符，通常对象以和 "number" 相同的方式实现 "default" 转换）  
规范明确描述了哪个运算符使用哪个 hint。  
转换算法是：  
调用`obj[Symbol.toPrimitive](hint)`如果这个方法存在，
否则，如果 hint 是 "string"
尝试调用 obj.toString() 或 obj.valueOf()，无论哪个存在。
否则，如果 hint 是 "number" 或者 "default"
尝试调用 obj.valueOf() 或 obj.toString()，无论哪个存在。  
所有这些方法都必须返回一个原始值才能工作（如果已定义）。  

在实际使用中，通常只实现 obj.toString() 作为字符串转换的“全能”方法就足够了。