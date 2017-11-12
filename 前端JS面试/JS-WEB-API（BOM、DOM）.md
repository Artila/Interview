## JS-WEB-API（BOM、DOM）

#### 一、JS-WEB-API

##### 回顾 JS 基础知识：

- 变量类型和计算
- 原型和原型链
- 闭包和作用域
- 异步和单线程
- 其他（如日期、Math、各种常用API）

**特点：表面看来并不能用于工作中开发代码**

内置函数：Object Array Boolean String ……

内置对象：Math JSON ……



**JS 基础知识：**基于 ECMA 262 标准（规定基础语法、规则）

**JS-web-API：**基于 W3C 标准（在规则上怎么用）



W3C 标准中关于 JS 的规定有：

- DOM操作（增删改查，修改网页的结构，页面的动态效果）
- BOM操作（获取浏览器特性、当前屏幕尺寸宽高、当前地址栏地址）
- 事件绑定（click，keyon，mouseenter，mouseup等）
- ajax请求（包括http协议）
- 存储

**浏览器即要遵循浏览器对 JS 的运行的定义，又要遵循 ECMA262，又要遵循 W3C 标准。**



页面弹框是 `window.alert(123);`，浏览器需要做：

- 定义一个 window 全局变量，对象类型

- 给它定义一个 alert 属性，属性值是一个函数

  ​

获取元素`document.getElementById(id);` ，浏览器需要：

- 定义一个 document 全局变量，对象类型

- 给它定义一个 getElementById 的属性，属性值是一个函数

  ​


##### W3C 标准没有规定任何 JS 基础相关的东西

**不管什么变量类型、原型、作用域和异步（ECMA 262）**

**只管定义用于浏览器中JS操作页面的API和全局变量**



##### JS 内置的全局函数和对象有哪些：(可以拿来直接用的)

- 之前讲过的 Object Array Boolean String Math JSON等


- 刚刚提到的 window document 


- 未定义的全局变量，如：navigator.userAgent

  ​



##### 常说的 JS（浏览器执行的 JS ）包含两部分：

- JS 基础知识（ **ECMA262标准**）
- JS-Web-API（ **W3C标准**）




#### 二、 DOM 

##### 什么是 DOM ?

DOM 是 W3C（万维网联盟） 的推荐标准。

DOM 定义了访问诸如 XML 和 XHTML 文档的标准。

> “W3C 文档对象模型（DOM）是一个使程序和脚本有能力动态地访问和更新文档的内容、结构以及样式的平台和语言中立的接口。”

W3C DOM 被分为 3 个不同的部分/级别（parts / levels）：

- 核心 DOM

  用于任何结构化文档的标准模型

- XML DOM

  用于 XML 文档的标准模型

- HTML DOM

  用于 HTML 文档的标准模型

DOM 定义了所有文档元素的*对象和属性*，以及访问它们的*方法*（接口）。



HTML DOM 是：

- HTML 的标准对象模型
- HTML 的标准编程接口
- W3C 标准

HTML DOM 定义了所有 HTML 元素的*对象*和*属性*，以及访问它们的*方法*。

**换言之，HTML DOM 是关于如何获取、修改、添加或删除 HTML 元素的标准**



XML DOM 是：

- 用于 XML 的标准对象模型
- 用于 XML 的标准编程接口
- 中立于平台和语言
- W3C 的标准

XML DOM 定义了所有 XML 元素的*对象和属性*，以及访问它们的*方法（接口）*。

换句话说：

**XML DOM 是用于获取、更改、添加或删除 XML 元素的标准。**



DOM 可以说：浏览器把拿到的html代码，结构化成浏览器可识别、js可操作的一个模型而已。

是针对XML的基于树的API。描述了处理网页内容的方法和接口，是HTML和XML的API。



##### DOM节点操作

- property是DOM中的属性，是JavaScript里的对象；
- attribute是HTML标签上的特性，它的值只能够是字符串；
- **Attribute** （标签属性）用于拓展HTML  tag， 可改变标签行为或提供元数据，属性总是以name = value的格式（属性的键对应相应的值）

```javascript
// 获取 DOM 节点
var div1 = document.getElementById('div1');         // 元素
var divList = document.getElementsByTagName('div'); // 集合
console.log(divList.length);
console.log(divList[0]);

var containerList = document.getElementsByClassName('.container'); // 集合
var pList =  document.querySelectorAll('p');                       // 集合


// DOM有其默认的基本属性，而这些属性就是所谓的 “property”，无论如何，它们都会在初始化的时候在DOM对象上创建。
// 如果在TAG对这些属性进行赋值，那么这些值就会作为初始值赋给DOM的同名property。

var pList =  document.querselectorAll('p');
var p = pList[0];
console.log(p.style.width); // 获取样式
p.style.width = '100px';    // 修改样式
console.log(p.className);   // 获取class
p.className = 'p1';         // 修改class

// 获取nodeName 和 nodeType
console.log(p.nodeName);
console.log(p.nodeType);

// x 是 obj 的一个 property
var obj = {x:100, y:200};
console.log(obj.x);      // 100

// nodeName 是 p 的一个property
var p = document.getElementsByTagName('p')[0];
console.log(p.nodeName); // P

// property
var div = document.getElementById('div1');
console.log(div1.className);
div1.className = 'abc';
console.log(div1.className);

// HTML标签中定义的属性和值会保存该DOM对象的attributes属性里面；
// 这些attribute属性的JavaScript中的类型是Attr，而不仅仅是保存属性名和值这么简单；
var pList = document.queryselectorAll('p');
var p = pList[0];
p.getAttribute('data-name');
p.setAttribute('data-name','imocc');
p.getAttribute('style');
p.setAttribute('style','font-size:30px');
```



##### DOM结构操作

```javascript
// 1. 新增节点
var div1 = document.getElementById('div1');

// 添加新节点
var p1 = document.createElement('p');
p1.innerHTML = 'this is p1';
div1.appendChild(p1); 

// 移动已有的节点
var p2 = document.getElementById('p2');
div1.appendChild(p2);

// 2. 获取父元素
var div1 = document.getElementById('div1');
var parent = div1.parentElement; // 和 parentNode 的区别

// 3. 获取子元素
var child = div1.childNodes;
// 4. 删除节点
div1.removeChild(child[1]);

```

>获取节点的父元素，建议使用parentNode 不要使用parentElement
>
>原因如下：
>
>parentNode返回的是节点Node
>
>parentElement返回的是Elment元素
>
>而节点与元素的区别大家应该明白，Element是继承自Node的，也就是实现了Node接口。
>
>另外 Element也是一个Document对象。
>
>虽然大部分情况下这两个属性的功能是一样的，但是还是有特例。
>
>html的parentNode 是 document
>
>而 parentElement 却是 null 
>
>为什么？因为document 是Node， 但是它的NodeType值却是DOCUMENT_NODE
>
>并不是ELEMENT_NODE 所以返回值才为null



>parentElement 获取对象层次中的父对象。 
>parentNode 获取文档层次中的父对象。 
>childNodes 获取作为指定对象直接后代的 HTML 元素和 TextNode 对象的集合。 
>children 获取作为对象直接后代的 DHTML 对象的集合。 
>
>parentElement 属性，这个属性好理解，就是在 DOM 层次结构定义的上下级关系，如果元素A包含元素B，那么元素B就可以通过 parentElement 属性来获取元素A。 



#### 三、BOM

BOM 是 Browser Object Model，浏览器对象模型。

刚才说过 DOM 是为了操作文档出现的接口，那 BOM 顾名思义其实就是**为了控制浏览器的行为**而出现的接口。
浏览器可以做什么呢？比如跳转到另一个页面、前进、后退等等，程序还可能需要获取屏幕的大小之类的参数。
所以 BOM 就是为了解决这些事情出现的接口。比如我们要让浏览器跳转到另一个页面，只需要
`location.href = "http://www.xxxx.com";`
这个 location 就是 BOM 里的一个对象。

**window**
window 也是 BOM 的一个对象，除去编程意义上的“兜底对象”之外，通过这个对象可以获取窗口位置、确定窗口大小、弹出对话框等等。例如我要关闭当前窗口：
`window.close();`



- **DOM 是为了操作文档出现的 API，document 是其的一个对象；**
- **BOM 是为了操作浏览器出现的 API，window 是其的一个对象。**





**BOM是浏览器对象模型，DOM是文档对象模型，前者是对浏览器本身进行操作，而后者是对浏览器（可看成容器）内的内容进行操作。**

![img](http://img.blog.csdn.net/20160826135345273?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)



 BOM部分主要是针对浏览器的内容，其中常用的就是window对象和location。

- window 是全局对象很多关于浏览器的脚本设置都是通过它。
- location 则是与地址栏内容相关，比如想要跳转到某个页面，或者通过URL获取一定的内容。
- navigator 中有很多浏览器相关的内容，通常判断浏览器类型都是通过这个对象。
- screen 常常用来判断屏幕的高度宽度等。
- history 不太常用，一般应该不会有写关于历史记录的脚本。


```javascript
// navigator
var ua = navigator.userAgent;
var isChrome = ua.indexOf('chrome');
console.log(isChrome); 

// screen
console.log(screen.width);
console.log(screen.height);

// location
console.log(location.href);         // 获取页面的地址
location.href = 'http://imooc.com'; // 修改页面的地址

console.log(location.protocol); // 协议 'http:' 'https:'
console.log(location.host);     // 域名 'www.baidu.com'
console.log(location.pathname); // 路径 '/learn/199.html'
console.log(location.search);   // url的？后面查询字符串、参数 ?cid=99&a=b
console.log(location.hash);     // url中#后面的参数 #mid=100

// history
history.back();    // 返回
history.forward(); // 前进
```



![img](http://images2015.cnblogs.com/blog/449064/201509/449064-20150901201202388-1759134225.png)

补充资料：http://blog.csdn.net/qq877507054/article/details/51395830





















