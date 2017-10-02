# javascript之 call(),apply()与bind()

## apply()、call()

在javascript中，call和apply都是为了改变某个函数运行时的上下文（context）而存在的，换句话说，就是为了改变函数内部this的指向。

javascript的一大特点，函数存在“定义时上下文”和“运行时上下文”以及“上下文是可以改变”的这样的概念。

举个例子：

```
function fruits() {}

fruits.prototype = {
	color: "red",
	say: function() {
		console.log("My color is " + this.color);
	}
}

var apple = new fruits;
apple.say(); // My color is red

```

但是如果我们有一个对象banana = {color: "yellow"}，我们不想对它重新定义say方法，那么我们可以通过call或apply用apple的say方法：

```
banana = {
	color: "yellow"
};
apple.say.call(banana); // My color is yellow
apple.say.apply(banana); // My color is yellow

```

所以，可以看出call和apply是为了改变this而出现的，当一个object没有某个方法（banana没有say方法），但其他的有（apple有say方法），我们可以借助call或apply用其它对象的方法来操作。

## apply、call 区别

对于apply、call二者而言，作用是一样的，只是接受参数的方式不太一样。例如有一个函数定义如下：

```
var func = function(arg1, arg2) {
	
}
```

就可以通过如下方式来调用：

```javascript
func.call(this, arg1, arg2);
func.apply(this, [arg1, arg2]);
```

其中this是你想指定的上下文，它可以是任何一个javascript对象（javascript中一切皆对象），call需要**把参数按顺序传递进去**，而apply则是**把参数放在数组里**。

javascript中，某个函数的参数数量是不固定的，因此要说使用条件的话，当你的参数是明确知道属性时用call。

而不确定的时候用apply，然后把参数push进数组传递进去。当参数数量不确定时，函数内部也可以通过arguments这个数组来遍历所有参数。

为了巩固加深记忆，下列举一些常用用法：

> 1.数组之间追加

```javascript
var array1 = [12, "foo", {name: "Joe"}, -2458];
var array2 = ["Doe", 555, 100];
Array.prototype.push.apply(array1, array2); // 返回数组长度 7

// array1 值为  [12 , "foo" , {name "Joe"} , -2458 , "Doe" , 555 , 100] 
```

> 2.获取数组中的最大值和最小值

```javascript
var numbers = [5, 121, 324, -243];
var maxInNumbers = Math.max.apply(Math, numbers), // 324
	maxInNumbers = Math.max.call(Math, 5, 121, 324, -243); //324
```

number本身没有max方法，但是Math有，我们接触call或者apply使用其方法。

> 3.验证是否是数组（前提是toString()方法没有被重写过）

```javascript
fuction isArray(obj){
	return Objext.prototype.toString.call(obj) === '[object Array]';
}
```

> 4、类（伪）数组使用数组方法

```javascript
var domNodes = Array.prototype.slice.call(document.getElementsByTagName('*'));
```

​        Javascript中存在一种名为维数组的对象结构。比较特别的是arguments对象，还有像调用getElementByTagName，document.childNodes之类的，它们返回NodeList对象都属于伪数组。不能应用Array下的push，pop等方法。

但我们都能通过Array.prototype.slice.call转换为真正的数组的带有length属性的对象，这样domNodes就可以应用Array下的所有方法了。

## 深入理解运用apply()、call()

给出一个实例，如下：

​    定义一个log方法，让它可以代理console.log方法，最常见的解决方法：

```javascript
function log(con){
	console.log(con);
}
log(1); // 1
log(1,2); // 1
```

上面的方法可以解决最基本的需求，但当传入参数的个数不确定的时候，上面的方法就失效了，这个时候就可以考虑使用apply或者call，注意这里传入多少个参数是不确定的，所以使用apply是最好的，方法如下：

```javascript
function log(){
	console.log.apply(console, arguments);
};
log(1); // 1
log(1,2); // 1 2
```

接下来的要求时给每一个log消息添加一个“（app）”的前缀，比如：

```javascript
log('hello world'); // (app)hello world
```

该怎么做比较优雅？这个时候需要想到arguments参数是个伪数组，通过Array.prototype.slice.call转化为标准数组，在使用数组方法unshift，像这样：

```javascript
function log(){
	var args = Array.prototype.slice.call(arguments);
	args.unshift('(app)');
	console.log.apply(console, args);
};
```

## bind()

bind() 方法与 apply 和 call 很相似，也是可以改变函数体内 this 的指向。

MDN解释：bind()方法会创建一个新函数，称为绑定函数，当调用这个绑定函数时，绑定函数会以创建它时传入bind()方法的第一个参数作为this，传入bind()方法的第二以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。

直接来看看具体如何使用，在常见的单体模式中，通常我们会使用_this，that，self等保存this，这样我们可以改变上下文之后继续引用到它。像这样：

```javascript
var foo = {
	bar: 1,
	eventBind: function(){
		var _this = this;
		$('.someClass').on('click', function(event) {
			// Act on the event
			console.log(_this.bar); // 1
		})
	}
}
```

由于javascript特有的机制，上下文环境在eventBind:function(){}过渡到$('.someClass').on('click', function(event){})发生了改变，上述使用变量保存this这些方式都是有用的，也没有什么问题。当然使用bind()可以更加优雅的解决这个问题：

```javascript
var foo = {
	bar: 1,
	eventBind: function(){
		$('.someClass').on('click', function(event){
			// Act on the event
			console.log(this.bar); // 1
		}).bind(this));
	}
}
```

在上述代码中，bind()创建了一个新函数，当这个click事件绑定在被调用的时候，它的this关键词会被设置成被传入的值（这里指调用bind()时传入的参数）。因此，这里我们传入想要的上下文this（其实就是foo），到bind()函数中。然后，当回调函数被指定的时候，this便指向foo对象。再来一个简单的例子：

```javascript
var bar = function(){
	cvonsole.log(this.x);
}
bar(); // undefined
var func = bar.bind(foo);
func(); // 3
```

这里我们创建了一个新的函数func，当使用bind()创建一个绑定函数之后，它被执行的时候，它的this会被设置成foo，而不是向我们调用bar()时的全局作用域。

有个有趣的问题，如果连续bind()两次，或者连续bind()三次那么输出的值是什么呢？像这样：

```javascript
var bar = function(){
	console.log(this.x);
};
var foo = {
	x: 3
};
var sed = {
	x: 4
};
var func = bar.bind(foo).bind(sed);
func(); // ?
var fiv = {
	x: 5
};
var func = bar.bind(foo).bind(sed).bind(fiv);
func(); // ?
```

答案是，两次都仍将输出3，而非期待中的4和5，在javascript中，对此bind()是无效的的。更深层次的原因，bind()的实现，相当于使用函数内部包含一个call/apply，第二次bind()相当于在保住一次bind()，所以第二次以后的bind()是无法生效的。

## apply()、call()、bind()比较

那么apply、call、bind三者相比较，之间又有什么异同呢？何时使用apply、call何时使用bind。举个简单的例子：

```javascript
var obj = {
	x: 81
};
var foo = {
	getX: function(){
		return this.x;
	}
}
console.log(foo.getX.bind(obj)()); // 81
console.log(foo.getX.call(obj));   // 81
console.log(foo.getX.apply(obj));  // 81
```

三个都输出81，但是注意看使用bind()方法，它后面多了对括号。

也就是说，区别是，当你希望改变上下文环境之后立即执行，而是回调执行的函数，使用bind()方法。而apply()/call()则会立即执行函数。

## 总结

- apply、call、bind 三者都是利用改变函数的this对象的指向
- apply、call、bind 三者第一个参数都是this要指向的对象，也就是想指定的上下文
- apply、call、bind三者都可以利用后续参数传参
- bind是返回对应函数，便于稍后调用；apply、call则是立即调用

