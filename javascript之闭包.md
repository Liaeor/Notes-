# javascript 之闭包



​        闭包（Closures）是JavaScript中一个特色，正因为它的与众不同，也使得闭包理解起来有一定的难度，下面结合个人的理解予以总结。

<!-- more -->

 综合各种对闭包的定义，基本上大同小异。个人认为较容易理解的是以下形式：

> 闭包就是 某个函数作用域下的**函数** 和 这个作用域中**变量** 的 结合

通常我们用和其相应的函数来指代闭包，可以简单解释为：

> 有权访问另一个函数作用域中的变量的函数。 



理解闭包之前，首先要理解作用域链。

​              当我们在一个作用域查找变量的时候，会先从当前上下文的变量对象(VO)中查找，如果没有找到，就会从父级(词法层面上的父级)执行上下文的变量对象中查找，一直找到全局上下文的变量对象，也就是全局对象。这样由多个执行上下文的变量对象构成的链表就叫做作用域链。

例：

```javascript
var scope = "global scope";
function checkscope(){
    var scope = "local scope";
    function f(){
        return scope;
    }
    return f;
}

var foo = checkscope();
foo(); //local scope
```

**分析一下函数执行过程**：

​        当 f 函数执行的时候，checkscope 函数上下文已经被销毁了啊(即从执行上下文栈中被弹出)，怎么还会读取到 checkscope 作用域下的 scope 值呢？

当我们了解了具体的执行过程后，我们知道 f 执行上下文维护了一个作用域链：

```
fContext = {
    Scope: [AO, checkscopeContext.AO, globalContext.VO],
}
```

​       对的，就是因为这个作用域链，f 函数依然可以读取到 checkscopeContext.AO 的值，说明当 f 函数引用了 checkscopeContext.AO 中的值的时候，即使 checkscopeContext 被销毁了，但是 JavaScript 依然会让 checkscopeContext.AO 活在内存中，f 函数依然可以通过 f 函数的作用域链找到它，正是因为 JavaScript 做到了这一点，从而实现了闭包这个概念。**上面例子中 f() +值为“local scope” 的 变量 scope  构成了一个闭包**

 **闭包常见用途**：

1. 创建特权方法用于访问控制（可以访问函数内部变量）
2. 事件处理程序及回调

​       由于闭包会使得函数中的**变量都被保存在内存中**，内存消耗很大；一般情况应避免使用闭包，它会对脚本性能有负面影响，比如处理速度、内存消耗。解决方法是，在退出函数之前，将不使用的局部变量全部删除。



理解下面一个**闭包实例**：

```javascript
var data = [];

for (var i = 0; i < 3; i++) {
  data[i] = function () {
    console.log(i);
  };
}

data[0]();
data[1]();
data[2]();
```

答案是都是 3，让我们分析一下原因：

当执行到 data[0] 函数之前，此时全局上下文的 VO 为：

```javascript
globalContext = {
    VO: {
        data: [...],
        i: 3
    }
}
```

当执行 data[0] 函数的时候，data[0] 函数的作用域链为：

```javascript
data[0]Context = {
    Scope: [AO, globalContext.VO]
}
```

data[0]Context 的 AO 并没有 i 值，所以会从 globalContext.VO 中查找，i 为 3，所以打印的结果就是 3。

data[1] 和 data[2] 是一样的道理。

所以让我们**改成闭包**看看：

```javascript
var data = [];

for (var i = 0; i < 3; i++) {
  data[i] = (function (i) {
        return function(){
            console.log(i);
        }
  })(i);
}

data[0]();
data[1]();
data[2]();
```

当执行到 data[0] 函数之前，此时全局上下文的 VO 为：

```javascript
globalContext = {
    VO: {
        data: [...],
        i: 3
    }
}
```

跟没改之前一模一样。

当执行 data[0] 函数的时候，data[0] 函数的作用域链发生了改变：

```javascript
data[0]Context = {
    Scope: [AO, 匿名函数Context.AO globalContext.VO]
}
```

匿名函数执行上下文的AO为：

```javascript
匿名函数Context = {
    AO: {
        arguments: {
            0: 0,
            length: 1
        },
        i: 0
    }
}
```

data[0]Context 的 AO 并没有 i 值，所以会沿着作用域链从匿名函数 Context.AO 中查找，这时候就会找 i 为 0，找到了就不会往 globalContext.VO 中查找了，即使 globalContext.VO 也有 i 的值(值为3)，所以打印的结果就是0。

data[1]（值为1） 和 data[2]（值为2） 是一样的道理。



[相关知识：js执行上下文](https://github.com/mqyqingfeng/Blog/issues/8)

