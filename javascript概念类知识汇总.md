# javascript概念类知识汇总

​      

​        前一段时间看到一位大佬说过的一句话：“对我来说，博客首先是一种知识管理工具，其次才是传播工具。我的技术文章，主要用来整理我还不懂的知识。我只写那些我还没有完全掌握的东西，那些我精通的东西，往往没有动力写。炫耀从来不是我的动机，好奇才是。”

​       这句话我很赞同，我想这也是万千编程爱好者，乃至各方面学习爱好者应该抱有的学习态度。因此，这也将鼓励着我们每个人坚持学习，热爱学习，一步一步迈向那个“梦想的国度”！

##一、js  typeof操作符返回哪些数据类型？

首先，javascript包括 基本数据类型 和引用类型

- 基本类型：Number，String，Boolean，Null，Undefined，Symbol(ECMAScript 6 新增)



- 引用类型：Object


​typeof 返回一个字符串，所以可能值有："number","string","boolean","object","undefined", "function"   

```javascript
例：  typeof (typeof 1) === 'string';   // typeof总是返回一个字符串
     typeof  null === 'object'  //null  特殊的object，空对象引用
     typeof  NaN === 'number' // NaN 非数值（Not a Number）是一个特殊的数值number
```



## 二、js 数据类型转换

-  显式（强制）类型转换：


​            使用函数、方法

​                     Number(),String(),Boolean(),parseInt(),parseFloat(),toString()

```javascript
例：
    Number('324') // 324  字符串：如果可以被解析为数值，则转换为相应的数值
    Number('324abc') // NaN 字符串：如果不可以被解析为数值，只要有一个字符无法转成数值，整个字符串就会被转为 NaN
    Number('') // 0  空字符串转为0
    Number(undefined) // NaN  undefined：转成 NaN
    Number(null) // 0  null：转成0
    Number('\t\v\r12.34\n') // 12.34 Number函数会自动过滤一个字符串前导和后缀的空格
    Number({a: 1}) // NaN
    Number([1, 2, 3]) // NaN
    Number([5]) // 5	Number方法的参数是对象时，将返回NaN，除非是包含单个数值的数组

    parseInt('42 cats') // 42  parseInt逐个解析字符，而Number函数整体转换字符串的类型

    String({a: 1}) // "[object Object]"
    String([1, 2, 3]) // "1,2,3"  如果是对象，返回一个 类型字符串；如果是数组，返回该数组的字符串形式

    Boolean(undefined) // false
    Boolean(null) // false
    Boolean(0) // false
    Boolean(NaN) // false
    Boolean('') // false  除了以上五个值的转换结果为false，其他的值全部为true
```

​            

-  隐式（自动）类型转换：


​              以下三种情况时，JavaScript会自动转换数据类型

​                         1. 不同类型的数据互相运算

​                         2.对非布尔值类型的数据求布尔值

​                         3. 对非数值类型的数据使用一元运算符（即“+”和“-”）

```javascript
例：
  自动转换为布尔类型：
     if ( !undefined
        && !null
        && !0
        && !NaN
        && !''
      ) {
        console.log('true');
      } // true   if语句的条件部分，非布尔值的参数自动转换为布尔值

  自动转换为字符串类型：
    '5' + 1 // '51'
    '5' + true // "5true"
    '5' + {} // "5[object Object]"
    '5' + [] // "5"
    '5' + function (){} // "5function (){}"
    '5' + undefined // "5undefined"
    '5' + null // "5null" 字符串和非字符串加法运算时，系统内部会自动调用String函数，转换为字符串

  自动转换为数值：
    '5' - '2' // 3
    '5' * '2' // 10
    true - 1  // 0
    false - 1 // -1
    '1' - 1   // 0
    '5' * []    // 0
    false / '5' // 0
    'abc' - 1   // NaN 除了加法运算符有可能把 运算子 转为字符串，其他运算符都会把 运算子 自动转成 数值

    +'abc' // NaN
    -'abc' // NaN
    +true // 1
    -false // 0  一元运算符也会把 运算子 转成数值
```



## 三、null 与undefined

-  null是一个对象，空对象指针，表示 保存对象的变量还没有真正保存对象（空值），就应该让该值保存null


​                  DOM中，试图获取一个不存在的元素返回一个null值

​                  通过分配null值，有效地**清除引用**，并假设对象没有引用其他代码，指定垃圾收集，确保**回收内存**



- undefined 表示"缺少值"，就是此处应该有一个值，但是还没有定义


​                  变量定义了，但没有赋值 就等于undefined

​                  对象没有赋值的属性，该属性的值为undefined。

​                  函数没有返回值时，默认返回undefined。



## 四、“===” 与“==”运算符判断相等的流程

- **“===”运算符**：

   要求较严格，两个值是相同类型且值要相同，才相等。

  1. 如果两个值**不是相同类型**，它们**不相等**

  2. 如果两个值都是null或者都是undefined，它们相等

  3. 如果两个值都是布尔类型true或者都是false，它们相等

  4. 如果其中有一个是NaN，它们不相等

  5. 如果都是数值型并且数值相等，他们相等， -0等于0

  6. 如果他们都是字符串并且在相同位置包含相同的16位值，他它们相等；

     如果在长度或者内容上不等，它们不相等；

     两个字符串显示结果相同但是编码不同==和===都认为他们不相等

  7. 如果他们指向相同对象、数组、函数，它们相等；

     如果指向不同对象，他们不相等。

- **“==”运算符**： 

  1. 如果两个值类型相同，按照===比较方法进行比较

  2. 如果类型不同，使用如下规则进行比较：

        如果其中一个值是null，另一个是undefined，它们相等

        如果一个值是**数字**另一个是**字符串**，将**字符串转换为数字**进行比较

        如果有布尔类型，将**true转换为1，false转换为0**，然后用==规则继续比较

        如果一个值是对象，另一个是数字或字符串，将对象转换为原始值然后用==   规则继续比较



## 五、<,>,<=,>=的比较规则

​      所有比较运算符都支持任意类型，但是**比较只支持数字和字符串**，所以需要执行必要的转换然后进行比较，转换规则如下:

1. 如果操作数是对象，转换为原始值：如果valueOf方法返回原始值，则使用这个值，否则使用toString方法的结果，如果转换失败则报错
2. 经过必要的对象到原始值的转换后，如果两个操作数都是字符串，按照字母顺序进行比较（他们的16位unicode值的大小）
3. 否则，如果有一个操作数不是字符串，**将两个操作数转换为数字**进行比较



## 六、+运算符工作流程

1. 如果有操作数是对象，转换为原始值（基本数据类型值）
2. 此时如果有**一个操作数是字符串**，其他的操作数都转换为字符串并执行连接
3. 否则：**所有操作数都转换为数字并执行加法**



## 七、对象转换为数字与字符串的步骤

- **转换为数字**

  1. 如果对象有valueOf()方法并且返回原始值，javascript将返回值转换为数字作为结果
  2. 如果对象有toString()并且返回原始值（primitive value如：string number boolean），javascript将返回结果转换为数字作为结果
  3. 否则，throws a TypeError

- **转换为字符串**

  1. 如果对象有toString()并且返回原始值，javascript将返回结果转换为字符串作为结果
  2. 如果对象有valueOf()方法并且返回原始值，javascript将返回值转换为字符串作为结果

  3. 否则，throws a TypeError



## 八、javascript中定义对象的方式

1. 对象字面量： `var obj = {};`

2. 构造函数： `var obj = new Object();`

3. Object.create(): `var obj = Object.create({x:1,y:2});`

   ​

## 九、javascript中 定义函数的方式

1. 函数声明

2. 函数表达式

3. Function 构造函数

4. arrow function(ES6)

   [具体请参考](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Functions)

   ​



## 十、函数内部arguments变量有哪些特性,有哪些属性,如何将它转换为数组

- arguments所有函数中都包含的一个局部变量，是一个**类数组对象**，对应函数调用时的实参。如果函数定义同名参数会在调用时覆盖默认对象
- arguments[index]分别对应函数调用时的实参，并且通过arguments修改实参时会同时修改实参
- arguments.length为实参的个数（Function.length表示形参长度）
- **arguments.callee**为当前正在执行的函数本身，使用这个属性进行递归调用时需注意this的变化
- arguments.caller为调用当前函数的函数（已被遗弃）
- 转换为数组：`var args = Array.prototype.slice.call(arguments, 0);`





##十一、什么是闭包,闭包有什么用

​      **闭包是在某个作用域内定义的函数，它可以访问这个作用域内的所有变量**（简单理解为函数+函数可以访问的自由变量）。

例：

```javascript
function makeFunc() {
  var name = "Mozilla";
  function displayName() {
    alert(name);
  }
  return displayName;
}

var myFunc = makeFunc();
myFunc();
```

​     `myFunc` 变成一个 *闭包* 了。 闭包是一种特殊的对象。它由两部分构成：函数，以及创建该函数的环境。环境由闭包创建时在作用域中的任何局部变量组成。在我们的例子中，`myFunc` 是一个闭包，由 `displayName` 函数和闭包创建时存在的 "Mozilla" 字符串形成。

**闭包作用域链通常包括三个部分**：

1. 函数本身作用域。
2. 闭包定义时的作用域。
3. 全局作用域。

**闭包常见用途**：

1. 创建特权方法用于访问控制
2. 事件处理程序及回调

一般情况应避免使用闭包，它会对脚本性能有负面影响，比如处理速度、内存消耗。



## 十二、new 操作符的“实质”

​             当使用new操作符调用构造函数，new操作符实际进行了如下操作：

```javascript
1.创建一个新对象
var obj = new object();
2.设置原型链
obj.__proto__ = fn.prototype;
3.让fn的this指向obj，并执行fn函数体
var result = fn.call(obj);
4.判断fn的返回值类型，如果是值类型，返回obj。如果是引用类型，就返回这个引用类型的对象
if (typeof(result) == "object"){  
    fnObj = result;  
} else {  
    fnObj = obj;
}  
```



## 十三、js DOM事件流

​        **事件流**描述的是从页面中接收事件的顺序,也可理解为 事件在页面中传播的顺序

​       "DOM2级事件"规定的事件流包括三个阶段：事件捕获阶段、处于目标阶段、事件冒泡阶段

​                                  ![事件流](http://owj66num8.bkt.clouddn.com/%E4%BA%8B%E4%BB%B6%E6%B5%81.png)



​            **事件捕获阶段**：事件从Document节点自上而下向目标节点传播的阶段，首先发生的是事件捕获，为父元素截获事件提供了机会 。上面例子中，事件从 document 到<html>再到<body>后就停止了。

​            **处于目标阶段**： 实际的目标节点接收到事件。事件在<div>上发生，并在事件处理中被看成冒泡阶段的一部分 

​            **事件冒泡阶段**：事件从目标节点自下而上向Document节点传播，事件又传回文档。这个阶段可以处理事件（调用事件处理程序，对事件做出响应）

​            

​          ps： “DOM2 级事件” 定义了两个方法，用于处理指定和删除事件处理程序的操作 ：

​		   addEventListener()     处理指定事件处理程序

​		   removeEventListener()     移除事件处理程序	

​	                  都接受 3 个参数：要处理的事件名、作为事件处理程序的函数 和 一个布尔值。                                                           

​                                      布尔值 true，表示在 捕获阶段调用 事件处理程序

​                                                  false，表示在 冒泡阶段调用 事件处理程序



## 十四、Ajax 及 其基本步骤

​              **AJAX**即“Asynchronous Javascript And XML”（异步 JavaScript 和 XML），是指一种创建交互式网页应用的网页开发技术。通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

​              实现Ajax的基本步骤：

​                     1.初始化XMLHttpRequest（XHR）对象，也就是创建一个异步调用对象

​                     2.创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息

​                     3.设置响应HTTP请求状态变化的函数

​                     4.发送HTTP请求

​                     5.获取异步调用返回的数据

​                     6.使用JavaScript和DOM实现局部刷新

```javascript
//创建XHR对象
var xhr = new XMLHttpRequest(); 
//创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息 ,async：true（异步）或 false（同步）
xhr.open(method,URL,async);
//设置响应HTTP请求状态变化的函数
xhr.onreadystatechange = function(){}
//发送HTTP请求
xhr.send(data)
//获取异步调用返回的数据
xhr.readyState == 0;//0: 请求未初始化
                    //1: 服务器连接已建立
                    //2: 请求已接收
                    //3: 请求处理中
                    //4: 请求已完成，且响应已就绪
xhr.responseText;//获得字符串形式的响应数据
xhr.responseXML;//获得 XML 形式的响应数据
```



​           Ajax的**局限性**：

​                   AJAX 不支持浏览器 back 按钮；

​                   （ 安全问题） AJAX 暴露了与服务器交互的细节

​                   对搜索引擎的支持比较弱。 不会执行你的 JS 脚本，只会操作你的网页源代码

​                  跨域请求有一定限制

## 十五、GET 与 POST 

​          **GET**:一般用于查询数据，获取资源信息,使用URL传递参数；

​                 由于浏览器对地址栏长度有限制，所以对使用get方式所发送信息的数量有限制；

​                 同时浏览器会记录（历史记录，缓存）保留请求地址的信息，请求的数据会保存在URL之后；

​                 get 只能发送普通格式（URL 编码格式）的数据。

​          

​          **POST**:一般用于向服务器发送数据，可能改变服务器上的资源的请求；

​                     对所发送的数据的大小理论上是没有限制；

​                     浏览器会缓存记录地址，但是不会记录 post 提交的数据；

​                     post 可以发送纯文本、URL编码格式、二进制格式的字符串，形式多样。

​         

​         使用POST的情况：

​                 无法使用缓存文件（更新服务器上的文件或数据库）；

​                 向服务器发送大量数据（POST 没有数据量限制）；

​                 发送包含未知字符的用户输入（私密信息）时（POST 比 GET 更稳定、更安全、也更可靠  ）

​                 上传文件图片时

​                 

##十六、js 同步和异步

​             同步和异步关注的是消息通信机制。

​                         同步的情况下，是由处理消息者自己去等待消息是否被触发；

​                         异步的情况下，是由 触发机制 来通知处理消息者；

​            javascript语言是单线程机制。所谓单线程就是按次序执行，执行完一个任务再执行下一个。对于浏览器来说，也就是**无法在渲染页面的同时执行代码**。单线程机制的优点在于实现起来较为简单，运行环境相对简单。缺点在于，如果中间有任务需要响应时间过长，经常会导致页面加载错误或者浏览器无响应的状况。这就是所谓的“同步模式”，**程序执行顺序与任务排列顺序一致**。

​           对于浏览器来说，同步模式效率较低，耗时长的任务都应该使用异步模式；而在服务器端，异步模式则是唯一的模式



## 十七、js 原型 原型链

​             **原型**： 每创建一个函数，函数上都有一个原型属性为 prototype，它的值是一个对象。 这个对象的作用  **在于使函数创建的实例能够共享原型上的属性和方法。**

​            **原型链**：每个函数都有一个原型属性prototype指向函数自身的原型，而由这个函数创建的对象也有一个`__proto__`属性指向这个原型，而函数的原型是一个对象，所以这个对象也会有一个`__proto__`指向自己的原型，这样逐层深入直到Object对象的原型(null)，这样就形成了原型链。

​            

​           原型链图解：

![js_intermediate_proto_link_map](http://owj66num8.bkt.clouddn.com/js_intermediate_proto_link_map.jpg)



​               1.实例对象（通过new XX() 所得到的实例），跟原型链相关的只有 `__proto__`属性，指向其对应的原型对象 *.prototype 。

​               2.构造函数对象分原生和自定义两类。跟原型链相关的有 `__proto__`属性，除此之外还有 prototype 属性。它们的 `__proto__`属性都是指向 Function.prototype 这个原型对象的。prototype 也是指向对应的原型对象。

​               3.原型对象除了一样拥有 `__proto__`外，也拥有独有的属性 constructor 。它的`__proto__`指向的都是Object.prototype ，除了 Object.prototype 本身，它自己是指向 null 。而 constructor 属性指向它们对应的构造函数对象。

​               4.原型链是基于 `__proto__`的。实例只能通过其对应原型对象的 constructor 才能访问到对应的构造函数对象。构造函数只能通过其对应的 prototype 来访问相应的原型对象。



