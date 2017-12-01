## JS-WEB-API（事件）

### 1. 通用事件绑定

```javascript
var btn = document.getElementById('btn1');
btn.addEventListener('click', function(event){
    console.log('clicked');
});   
 
 
function bindEvent(elem, type, fn){
    elem.addEventListener(type, fn);
}
 
var a = document.getElementById('link1');
 
bindEvent(a, 'click', function(e){
    e.preventDefault(); // 阻止默认行为
    alert('clicked');
});
```

　　

#### 1.1 关于IE低版本的兼容性

> IE低版本使用 attachEvent 绑定事件，和W3C标准不一样；
> IE低版本使用量已经非常少，很多网站都早已不支持了；
> 建议对IE低版本的兼容性：了解即可，无需深究；
> 如果遇到对IE版本要求苛刻的面试，果断放弃；



### 2. 事件冒泡（冒泡的特点就是往上）

> 需求：点击激活弹出激活，点击取消弹出取消
>
> body里面绑定click事件，点击激活，首先要触发绑定在它身上的事件，
>
> 然后再去触发绑定在它父节点（div1）上的事件，
>
> 然后再去触发绑定在它父节点的父节点（body）上的事件，
>
> 如果还有父节点还会往上冒；
>
> 顺着DOM的一个树形结构底层叶的节点的一个点击事件会一层一层根据树形结构
> 往它的父元素触发。

```js
<body>
    <div id="div1">
        <p id="p1">激活</p>
        <p id="p2">取消</p>
        <p id="p3">取消</p>
        <p id="p4">取消</p>
    </div>
    <div id="div2">
        <p id="p5">取消</p>
        <p id="p6">取消</p>
    </div>
</body>
 
function bindEvent(elem, type, fn){
    elem.addEventListener(type,fn);
}
 
var p1= document.getElementById('p1');
var oBody = document.body;
 
bindEvent('p1','click',function(e){
    e.stopPropatation(); // 阻止冒泡
    alert('激活') ;
});
 
bindEvent(body,'click', function(e){
    alert('取消');
});
```



### 3. 代理（事件冒泡的具体应用）

```js
// 代理的原理：
// 1.通过事件冒泡的机制
// 2.我们在上层的一个绑定可以通过target属性拿到它真实触发的元素
 
//需求：给所有的a标签弄个click事件
<div id="div1">
  <a href="#">a1</a>
  <a href="#">a2</a>
  <a href="#">a3</a>
  <a href="#">a4</a>
  <!- 会随时新增更多了 a 标签->
</div>
 
var oDiv = document.getElementById('div1'):
oDiv.addEventListener('click', function(e){
  e.preventDefault();
  var target = e.target; // target点击是从哪触发的
  if(target.nodeName== 'A'){
    alert(target.innerHTML);
  }
});
```



### 4. 完善通用绑定事件的函数

> **代理的好处：**
>
> 1.代码简洁
> 2.减少浏览器内存占用

```js
function  bindEvent(elem,type,selector,fn){
  if(fn == null){
    //如果第三个参数没有
    fn = selector;
    selector = null;
  }
     
  elem.addEventListener(type,function(e){
    var target;
    if(selector){
      // 代理
      target = e.target;
      // matches是不是符合目标的代理元素；
      /*如果target是触发事件的目标,dom节点是不是和
            selector选择器匹配的 */
      if(target.matches(selector)){
        // target----this
        fn.call(target, e);
      }
    }else{
      // 不是代理
      fn(e);
    }
  });
}
 
// 使用代理
var div1 = document.getElementById('div1');
bindEvent(div1,'click','a',function(e){
    e.preventDefault();
    console.log(this.innerHTML);
});
 
 
// 不使用代理
var a = document.getElementById('a1');
bindEvent(div1,'click',function(e){
    console.log(a.innerHTML);
});
```





