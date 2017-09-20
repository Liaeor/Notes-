# js 数组去重 及 求并集、交集、差集

例：给出两个数组：

```javascript
    var collection_a = [10, 27, 28, 19, 5];
    var collection_b = [5, 78, 28, 19, 23];
   /*交集：[5,28,19]
     并集：[10, 27, 28, 19, 5, 78, 23]
     差集：[10,27,78,23]*/

//1.有 collection_c = collection_a.concat(collection_b); 去掉collection_c的重复元素；
//2.求两集合的并集、交集与差集；
```

## 1.数组去重（常用方法）

​        1.最容易想到的 for循环遍历，自己实现去重。但是双重循环，时间复杂度比较高，性能比较低

```javascript
function unique(){
  var arr = [];
  var isRepeat;
  for(var i=0; i<collection_c.length; i++) {
    isRepeat = false;
    for(var j=i+1; j<collection_c.length; j++) {
      if(collection_c[i] === collection_c[j]){
        isRepeat = true;
        break;
      }
    }
    if(!isRepeat){
      arr.push(collection_c[i]);
    }
  }
  return arr;
}
或者
function unique(){
    var arr = [];
    var len = collection_c.length;
    for(var i=0; i<len; i++){
      for(var j=i+1; j<len; j++){
        if(collection_c[i] === collection_c[j]){
          j = ++i;
        }
      }
      arr.push(collection_c[i]);
    }
    return arr;
}

```

   2.使用Array.prototype.indexOf() 方法去重
​       indexOf()返回在类型数组中 可以找到给定元素 的第一个索引，如果不存在，则返回-1

   ```javascript
function unique(collection_c) {
   var arr = [];
   collection_c.forEach(function(item){
    if(arr.indexOf(item) === -1){ //类似于 includes() 方法
      arr.push(item);
    }
  });
   return arr;
}
或者
function unique(collection_c) {
    return collection_c.filter(function(item, index){
      // indexOf返回第一个索引值，
      // 如果当前索引(index)不是匹配到的元素的第一个索引(indexOf(item))，说明是重复值 返回false
        return collection_c.indexOf(item) === index;
    });
}
   ```

​     3.ES5 引入了Set 数据类型 （集合） ，集合中不允许有重复元素，如果你重复添加同一个元素的话，Set中只会存在一个，包括NaN也是这样

```javascript
function unique(){
  var set = new Set(collection_c);
  return Array.from(set);
}
```

4. ES6 引入了 Array.prototype.includes()方法 ，用于判断数组中是否包含某个元素

```javascript
function unique(){
  var arr = [];
collection_c.forEach(function (t) {
    if(!arr.includes(t)){
      arr.push(t);
    }
  })
  return arr;
}
```



## 2.求数组并集、交集与差集

​      **ES5 的filter()和indexOf ()方法** 

​          ES5可以利用filter和indexOf进行数学集操作，但是，由于indexOf方法中NaN永远返回-1，所以一般需要进行兼容处理（本题就先不考虑NaN）

​     **ES6 的 includes()方法**

​          includes()用于判断数组中是否包含某个元素

```javascript
//并集：
let pre = collection_b.filter(function (item) {
  return collection_a.indexOf(item) === -1;
  //或return !collection_a.includes(item);
})

let union = collection_a.concat(pre);

//交集：
let intersection = collection_b.filter(function (item) {
   return collection_a.indexOf(item) > -1;
  //或return collection_a.includes(item);
})

//差集：
let pre1 = collection_b.filter(function (item) {
  return collection_a.indexOf(item) === -1;
  //或return !collection_a.includes(item);
})

let pre2 = collection_a.filter(function (item) {
  return collection_b.indexOf(item) === -1;
  //或return !collection_b.includes(item);
})

let difference = pre1.concat(pre2);
```



   **ES6的Array.from()方法和Set()方法**

​      ES6引入的 Array.from()方法，用于将类数组对象和可遍历对象转化为数组。拥有一个 length 属性和若干索引属性的任意对象，基本都可以转化为数组。结合Set结构实现数学集求解，Set.prototype.has()方法。 个人觉得并集的计算  可以使用这种方法。

```javascript
//并集：
let pre = new Set(collection_a.concat(collection_b);
let union = Array.from(pre);

//交集：
let aset = new Set(collection_a);
let bset = new Set(collection_b);

let intersection = Array.from(collection_a.filter(v => bset.has(v)))

//差集：
let aset = new Set(collection_a);
let bset = new Set(collection_b);

let pre = new Set(collection_a.concat(collection_b).filter(v => !aset.has(v) || !bset.has(v)))
let difference = Array.from(pre);
```



   **总结**：

​         数组遍历及集合求法有多种，使用哪种方式要结合当前的场景来选择。比如，由于JS语言的特殊性，NaN在数组的数学集操作中有不少问题，ES6、ES7提供的新的数组方法解决了部分情况，并且更简洁。