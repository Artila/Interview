## JS-WEB-API（Ajax、JSONP）面试题

### 1. 手动编写一个ajax，不依赖第三方库

```js
//ajax实现的原理
var xhr = new XMLHttpRequest();
xhr.open("GET", "/api", false);
xhr.onreadystatechange = function(){
    // 这里的函数异步执行，可参考之前JS基础中的异步模块
    if(xhr.readyState == 4){ // 说明已经完成了
        // 服务端返回的200 返回成功
        if(xhr.status == 200){
            // responseText 服务端返回的内容
            alert(xhr.responseText);
        }
        
    }
};
xhr.send(); // 发送
```



### 2. 跨域的几种实现方式

> 1. JSONP
> 2. 服务器端设置 http header


