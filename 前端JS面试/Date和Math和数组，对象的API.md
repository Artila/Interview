## Date和Math和数组，对象的API

#### 1. Date

```javascript
Date.now(); // Date.now() 方法返回自1970年1月1日 00:00:00 UTC到当前时间的毫秒数

var dt = new Date(); // 

dt.getTime();      // 获取毫秒数

dt.getFullYear();  // 年

dt.getMonth();     // 月（0-11）,一般都会 +1

dt.getDate();      // 日（0-11）

dt.getDay();       // 星期几， 0 代表星期日， 1 代表星期一，2 代表星期二， 依次类推。

dt.getHours();     // 小时（0-23）

dt.getMinutes();   // 分钟（0-59）

dt.getSeconds();   // 秒（0-59）

// 还可以设置时间，setTime，setDate等等，把get改为set即可

```



#### 2. Math

**Math** 是一个内置对象， 它具有数学常数和函数的属性和方法。不是一个函数对象。

- Math.abs(x)    返回x的绝对值；

- Math.ceil(x)    返回x向上取整后的；

- Math.floor(x)      返回小于x的最大整数；

- Math.round(x)   返回四舍五入后的整数；

- Math.random()  返回0到1之间的伪随机数；

- Math.max([x[,y[,…]]])  返回0个到多个数值中最大值；

- Math.min([x[,y[,…]]])   返回0个到多个数值中最小值；

- Math.sqrt(x) 返回x的平方根。

  ​



#### 3. 数组API

- forEach 遍历所有元素　

- every 判断所有元素是否都符合条件

- some 判断是否有至少一个元素符合条件

- sort 排序

- map 对元素重新组装，生成新数组　

- filter 过滤符合条件的元素

  ​



```javascript
    // 1.forEach
    var arr = [1,2,3];
    arr.forEach(function(item, index) {
        // 遍历数组的所有元素
        // item是元素的值  index是元素的索引（位置）
        console.log(index,item); // 0 1 ;1 2 ;2 3
    });
    
    // 2.every
    var arr = [1,2,3];
    var result = arr.every(function(item,index) {
        // 用来判断所有的数组元素，都满足条件
        if(item < 4 ){
            return true;
        }
    });
    console.log(result); //true
    
    // 3.some
    var arr = [1,2,3];
    var result = arr.some(function(item,index) {
        // 用来判断所有的数组元素，只要有一个满足条件即可
        if(item < 2){
            return true;
        }
    });
    console.log(result);  //true
    
    // 4.sort
    var arr = [1,4,2,3,5];
    var arr2 = arr.sort(function(a,b) {
        // 从小到大排序
        return a - b;
        
        // 从大到小排序
        // return  b - a;
    });
    console.log(arr2);
    
    // 5.map
    var arr = [1,2,3,4];
    var arr2 = arr.map(function(item, index) {
        // 将元素重新组装，并返回
        return '<b>' + item +'</b>'
    });
    console.log(arr2);
    
    // 6.filter
    var arr = [1,2,3];
    var arr2 = arr.filter(function(item, index) {
        // 通过某一个条件过滤数组
        if(item >= 2){
            return true;
        } 
    });
    console.log(arr2); // 2,3

```



#### 4. 对象API

```javascript
var obj = {
    x: 100,
    y: 200,
    z: 300
};
var key;
// key就是obj的一个属性名，这里key去的是 x y z
for (key in obj){
    // 证明这个属性名字x y z 是obj原生的属性，而不是从原型中拿过来的属性
    if (obj.hasOwnProperty(key)) {
        console.log(key, obj[key]); // x 100; y 200; z 300
    }
}
```



#### 5. 数组的常用方法

```javascript
// 创建数组
let fruits = ["Apple", "Banana"];
console.log(fruits.length); // 2

// 通过索引访问数组元素
let first = fruits[0];
// Apple

let last = fruits[fruits.length - 1];
// Banana


// 遍历数组，item 和 index 的位置不可以反过来写
// 数组当前项的值 数组当前项的索引 数组对象本身
fruits.forEach(function (item, index, array) {
    console.log(item, index);
});
// Apple 0
// Banana 1


// 添加元素到数组的末尾
var newLength = fruits.push("Orange"); // 3 返回数组的新长度。
// ["Apple", "Banana", "Orange"]


// 删除数组末尾的元素
let last = fruits.pop(); // Orange 返回被删的元素
// ["Apple", "Banana"];


// 删除数组最前面（头部）的元素
let first = fruits.shift(); // Apple 
// ["Banana"];


// 添加到数组的前面（头部）
let newLength = fruits.unshift("Strawberry"); // 2 返回数组的新长度。
// ["Strawberry", "Banana"];


// 找到某个元素在数组中的索引
fruits.push('Mango');
// ["Strawberry", "Banana", "Mango"]

let index = fruits.indexOf("Banana");
// 1

// 通过索引删除某个元素
let removedItem = fruits.splice(index, 1); // Banana 返回被删的元素
// ["Strawberry", "Mango"]


// 从一个索引位置删除多个元素
let vegetables = ['Cabbage', 'Turnip', 'Radish', 'Carrot'];
console.log(vegetables); 
// ["Cabbage", "Turnip", "Radish", "Carrot"]

let pos = 1, n = 2;

let removedItems = vegetables.splice(pos, n); // 位置，需要删除的个数

console.log(vegetables); // ["Cabbage", "Carrot"] 原数组会受影响

console.log(removedItems); // ["Turnip", "Radish"] 返回删除的元素

// 复制一个数组
var shallowCopy = fruits.slice(); 

// ["Strawberry", "Mango"]

// 一般删除的会返回被删的元素，添加的会返回数组的新长度
```



#### 6. 鉴定数组

```javascript
// 1. Array.isArray() 用于确定传递的值是否是一个 Array。
// 下面的函数调用都返回 true
Array.isArray([]);
Array.isArray([1]);
Array.isArray(new Array());
// 鲜为人知的事实：其实 Array.prototype 也是一个数组。
Array.isArray(Array.prototype); 

// 下面的函数调用都返回 false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(17);
Array.isArray('Array');
Array.isArray(true);
Array.isArray(false);
Array.isArray({ __proto__: Array.prototype });

// 2. 当检测Array实例时, Array.isArray 优于 instanceof,因为Array.isArray能检测iframes.
var iframe = document.createElement('iframe');
document.body.appendChild(iframe);
xArray = window.frames[window.frames.length-1].Array;
var arr = new xArray(1,2,3); // [1,2,3]

// Correctly checking for Array
Array.isArray(arr);  // true
// Considered harmful, because doesn't work though iframes
arr instanceof Array; // false

// 3. 假如不存在 Array.isArray()
if (!Array.isArray) {
  Array.isArray = function(arg) {
    return Object.prototype.toString.call(arg) === '[object Array]';
  };
}
```

