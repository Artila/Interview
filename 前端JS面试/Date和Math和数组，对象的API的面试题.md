## Date和Math和数组，对象的API的面试题

#### 1. 获取2017-06-10格式的日期

```javascript
function formatDate(dt) {

  if(!dt){
      dt = new Date();
  }

  var year = dt.getFullYear();
  var month = dt.getMonth() + 1;
  var date = dt.getDate();

  if (month < 10) {
      //强制类型转换
      month = '0' + month;
  }

  if (date < 10) {
      //强制类型转换
      date = '0' + date;
  }
  //强制类型转换
  return year + '-' + month + '-' + date;
}

var dt = new Date();
var formatDate = formatDate(dt);
console.log(formatDate);

```



#### 2.获取随机数，要求是长度一致（一样长）的字符串格式

```javascript
var random = Math.random();

random = random+'0000000000'; //后面加上10个零

random = random.slice(0,10);  //从第一位开始到第10位结束

console.log(random);

```



#### 3.写一个能遍历对象和数组的通用forEach函数


```javascript
function forEach(obj, fn) {
    var key;
    if(obj instanceof Array){
        //准备判断是不是数组
        obj.forEach(function(item,index) {
            fn(index, item);
        });
    }else{
        //不是数组就是对象
        for(key in obj){
            if(obj.hasOwnProperty(key)) {
                fn(key,obj[key]);
            }
        }
    }   
}

var arr = [1,2,3];

//注意，这里参数的顺序换了，为了和对象的遍历格式一致
forEach(arr,function(index,item) {
    console.log(index, item);
}); // 0 1 ; 1 2 ; 2 3 

var obj = {x:100,y:200};
forEach(obj, function(key,value) {
   console.log(key, value); //x 100 ; y 200
});
```




