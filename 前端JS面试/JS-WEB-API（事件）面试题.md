## JS-WEB-API（事件）面试题

### 1. 编写一个通用的事件监听函数

```javascript
function bindEvent(elem, type, selector, fn) {
  if (fn==null) {
    fn = selecotr;
    selector = null;
  }

 elem.addEventListener(type, function(e) {
    var target;
    if (selector) {
      target = e.target;
      if(targer.matcher(selector)) {
        fn.call(target, e);
      }
    } else {
      fn(e);
    }
  });
}
```



### 2.描述事件冒泡流程

```
1.Dom 树形结构
2.事件冒泡 （一个一个往上冒，一层层触发事件）
3.阻止冒泡（e.stopPropatation();）
4.冒泡的应用（使用代理）
```



### 3.对于一个无限下拉加载图片的页面，如何给每一个图片绑定事件

```
1.使用代理
2.代理的两个优点：
--代码比较简洁，绑定一次就可以了
--对浏览器的压力比较小
（在页面上执行了一堆js和在页面上执行了一两行js，内存和渲染的压力都会比较小一些，效率会高一些）
```


