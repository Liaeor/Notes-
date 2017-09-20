# js 数组的比较 、数组降维 与 数组中位数

## 数组比较

​      Js不能直接用==或者===来判断两个数组是否相等是，数组是Object，直接比较相当于 比较内存 地址是否一样;

​     一般要将数组转换成字符串（toString()）再作比较，如果数组元素顺序不一样，应该先进行排序（sort()）;

```javascript
var collection_a = [1,11,27,20,4,9,15];
var collection_b = [1,11,27,20,4,9,15];

return collection_a.sort().toString() === collection_b.sort().toString();
```

## 数组降维

```javascript
//将数组转换为一维数组
var collection = [1, [2], [3, 4]];
```

### 1.根据数组特性 遍历

​           二维数组拆分成一维数组，构成新数组：

```javascript
function reduceDimension(collection) {
  let arr=[];
  collection.forEach(function (t) {
    if(t[0]=== undefined){ 
       arr.push(t);
    }
    else {
      t.forEach(function (f) {
         arr.push(f);
      })
    }
  })
  return arr;
}
```



### 2.利用concat()方法转换

​         二维数组每个元素连接成新数组：

```javascript
function reduceDimension(arr) {
  var reduced = [];
  for (var i = 0; i < arr.length; i++) {
      reduced =reduced.concat(arr[i]);
  }
  return reduced;
}
或者
function reduceDimension(arr) {
   return Array.prototype.concat.apply([],arr);
}
//apply方法的第一个参数会作为被调用函数的this值，apply方法的第二个参数（一个数组或者类数组对象，其中的数组元素将作为单独的参数传给 concat 函数）会作为被调用对象的arguments值，也就是说该数组的各个元素将会依次成为被调用函数的各个参数；效果等同于[].concat(1,[2], [3,4])
```



## 数组中位数

​       步骤：1.数组排序

​                   2.求中位数

```javascript
var collection = [1, 4, 6, 2, 3, 10, 9, 8, 11, 20, 19, 30];

function compute_median(collection) {
  collection.sort((a,b)=>a-b); //排序 从小到大
  
  let low = Math.floor((collection.length-1)/2);
  let high = Math.ceil((collection.length-1)/2); //找到中位数 的 位置
  
  let median = (collection[low]+collection[high])/2;
  
  return median;
}
```

