## JS-WEB-API（Ajax、JSONP）


### 1.XMLHttpRequest

> **IE兼容性问题**
> 1.IE低版本使用ActiveXObject，和W3C标准不一样
> 2.IE低版本使用量已经非常少，很多网站都早已不支持
> 3.建议对IE低版本的兼容性：了解即可，无需深究
> 4.如果遇到对IE低版本要求苛刻的面试，果断放弃


```js
//ajax实现的原理
var xhr = new XMLHttpRequest();
xhr.open("GET","/api",false);
xhr.onreadystatechange = function(){
    //这里的函数异步执行，可参考之前JS基础中的异步模块
    if(xhr.readyState == 4){ //说明已经完成了
        //服务端返回的200 返回成功
        if(xhr.status == 200){
            //responseText 服务端返回的内容
            alert(xhr.responseText);
        }
        
    }
};
xhr.send(null); //发送
```

 

### 2.状态码说明


| readyState |                                |
| ---------- | ------------------------------ |
| 0          | (未初始化)还没有调用send()方法            |
| 1          | （载入）已调用send()方法，正在发送请求         |
| 2          | （载入完成）send()方法执行完成，已经接收到全部响应内容 |
| 3          | （交互）正在解析响应内容                   |
| 4          | （完成）响应内容解析完成，可以在客户端调用了         |


| status |                                          |
| ------ | ---------------------------------------- |
| 2xx    | 表示成功处理请求。如200                            |
| 3XX    | 需要重定向，浏览器直接跳转                            |
| 4XX    | 客户端请求错误，如404（客户端发的地址服务端没定义，发了一个不存在的地址）   |
| 5XX    | 服务器端错误（服务端的代码错误没执行完就出现bug了）504 -服务端连接数据库超时 |

### 3.跨域

#### 3-1 什么是跨域（跨域ajax不能去请求）

##### 3-1-1 浏览器有同源策略，不允许ajax访问其他域接口；

- http://www.yourname.com/page1.html （你的网站要访问慕课网的一个接口是不允许的）
- 接口：http://m.imooc.com/course/ajaxcourserecom?cid=549





##### 3-1-2：跨域条件：协议、域名、端口，有一个不同就算跨域

 http 端口没写就是默认的80；https 默认端口443

 - http://www.yourname.com:80/page1.html 
 - http://m.imooc.com:80/course/ajaxcourserecom?cid=549





##### 3-1-3 有三个标签允许跨域加载资源

1. <img src=xxx> (防盗链处理（百度、知乎），只能自己产品可以用)
2. <link href=xxx>
3. <script src=xxx>

三个标签的使用场景（能逃避过同源策略可以跨域加载资源）：

1. <img> 用于打点统计，统计网站可能是其他域（img不受跨域限制，没有浏览器兼容性问题）
2. <link><script> 可以引用CDN，CDN的也是其他域（bootCDN）
3. <script> 可以用于JSONP





##### 3-1-4 跨域注意事项

1. 所有的跨域请求都必须经过信息提供方允许
2. 如果未经允许获取，那是浏览器同源策略出现漏洞





#### 3-2 JSONP

##### 3-2-1 JSONP实现原理

```
1. eg.加载http://coding.m.imooc.com/classindex.html
  1. 不一定服务器端真正有一个classindex.html文件
  2. 服务器可以根据请求，动态生成一个文件，返回
  3. 同理于<script src="http://coding.m.imcooc.com/api.js'>

2. 你的网站要跨域访问慕课网的一个接口
  1. 慕课网给你一个地址:http://coding.m.imooc.com/api.js, 可以动态返回你想要的数据；
  2. 返回内容格式如callback({x:100,y:200})(可动态生成)
```


```js
<script>
  window.callback = function(data){
    //这是我们跨域得到的信息
    console.log(data);
  };
</script>
<script src="http://coding.m.imooc.com/api.js"></script>
<!-以上将返回callback({x:100,y:200})->
```



#### 3-3 服务器端设置http header

另外一个解决跨域的简洁方法，需要服务器端来做

（但是作为交互方，我们必须知道这个方法，是将来解决跨域问题的一个趋势） 


```js
// 注意：不同后端语言的写法可能不一样
// 第二个参数填写允许跨域的域名称，不建议直接写“*”
response.setHeader("Access-Control-Allow-Origin", "http://a.com,http://b.com");
response.setHeader("Access-Control-Allow-Hearders", "X-Requested-with");
response.setHeader("Access-Control-Allow-Methods", "PUT,POST,GET,DELETE,OPTIONS");

// 接收跨域的cookie
response.setHeader("Access-Control-Allows-Credentials", "true");
```