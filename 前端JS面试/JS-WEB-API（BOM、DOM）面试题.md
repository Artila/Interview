## JS-WEB-API（BOM、DOM）面试题

#### 1. DOM 是哪种基本的数据结构？

> 树



#### 2. DOM 操作的常用 API 有哪些？

- 获取DOM节点，以及节点的property和Attribute；
- 获取父节点，获取子节点
- 新增节点，删除节点




#### 3. DOM 节点的 attr 和 property 有何区别？

- property 只是一个 JS 对象的属性的修改
- Attribute 是对 html 标签属性的修改




#### 1. 如何检测浏览器的类型

```javascript
var explorer = navigator.userAgent ;
//ie 
if (explorer.indexOf("MSIE") >= 0) {
	alert("ie");
}
//firefox 
else if (explorer.indexOf("Firefox") >= 0) {
	alert("Firefox");
}
//Chrome
else if(explorer.indexOf("Chrome") >= 0) {
	alert("Chrome");
}
//Opera
else if(explorer.indexOf("Opera") >= 0) {
	alert("Opera");
}
//Safari
else if(explorer.indexOf("Safari") >= 0) {
	alert("Safari");
} 
//Netscape
else if(explorer.indexOf("Netscape")>= 0) { 
	alert('Netscape'); 
} 
```



#### 2. 拆解url的各部分

```javascript
//location
console.log(location.href);  //获取页面的地址
location.href = 'http://imooc.com'; //修改页面的地址

console.log(location.protocol); //协议 'http:' 'https:'
console.log(location.host);  //域名 'www.baidu.com'
console.log(location.pathname); //路径 '/learn/199.html'
console.log(location.search); //url的？后面查询字符串、参数 ?cid=99&a=b
console.log(location.hash);  //url中#后面的参数 #mid=100
```

