# CSS布局详解——盒模型

转载来自：http://www.cnblogs.com/liugblog/p/4965330.html



### 一、网页布局的几种情况

CSS布局可以分为以下几大块：

- 盒子内部的布局
  - 文本的布局
  - 盒模型本身的布局
- 盒子之间的布局 visual formatting
  - 脱离正常流 normal flow 的盒子布局
    - absolute 布局
    - float 布局
  - 正常流 normal flow 下的盒子布局
    - BFC 布局
    - IFC 布局
    - FFC 布局
    - table 布局
    - grid 布局



### 二、盒模型（Box moudle)

1. 基本框

   CSS 假定每个元素都会生成一个或多个矩形框，这称为元素框。各元素框中心都有一个内容区(content area)。

   这个内容区周围有可选的内边距（padding）、边框（border）、外边距（margin）。这就是css中的盒模型。

2. 包含块

   每个元素都相对于其包含块摆放，可以这么说，包含块就是一个元素的“布局上下文”。

   包含块由最近的块级祖先元素、表单元格或行内块祖先元素的内容边界（content edge）构成。考虑下面的代码：

   ```html
   <body>
     <div class="father">
       <p class="son">This is paragraph</p>
     </div>
   </body>
   ```

   在这个例子中p的包含块是div元素，因为div是p元素最近的块级祖先元素，类似的，div的包含块是body。所以，p的布局依赖div的布局，而div的布局依赖body的布局。



### 三、块级元素与行级元素的对比

1. **块级元素的解析**

   1. **块级元素的特点**

      默认情况下，块级元素会在其框前和框后产生“换行”，并尽可能的充满整个容器。

      ​

   2. **元素的水平格式化**

      水平格式化的7大属性是：margin-left，border-left，padding-left，width，padding-right，border-right，margin-right。

      这7个属性值加起来往往是包含块width值。

      ​

   3. **负外边距**

      在盒模型中，内边距、边框、和内容宽度（及高度）不能为负值，只有外边距可以为负值。利用定位以及负margin可以设置盒子在页面中的居中。

      ```html
      .box {
        width: 100px; 
        height: 100px; 
        position: absolute; 
        left: 50%; 
        top: 50%; 
        margin-left: -50px; 
        margin-top:-50px;
        background:red;
      }
      <div class="box"></div>
      ```
       ![负外边距居中](https://github.com/Artila/Interview/blob/master/%E8%B5%84%E6%96%99%E6%94%B6%E9%9B%86/img/box1.jpg)

      ​

   4. **垂直外边距合并**

      垂直外边距合并：当两个垂直外边距相遇时，它们将形成一个外边距。

      合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。

      ```css
      div{
      	width: 200px; height: 200px; background: red; 
      }
      .box1{
      	margin-bottom: 100px;
      }
      .box2{
      	margin-top:50px;
      }
      ```
       ![垂直外边距合并](https://github.com/Artila/Interview/blob/master/%E8%B5%84%E6%96%99%E6%94%B6%E9%9B%86/img/margin1.jpg)

   5. **设置值为auto**

      其中margin-left，width，margin-right可以设置为auto。

      当设置margin-left与margin-right的值为auto而width的值为特定值时，会使盒子水平居中。

      当设置三个值都为auto时，浏览器会将margin-left与margin-right设置为0，而将width会尽可能的宽。

      而当设置三个值为固定值时，按css术语来讲，这些格式化属性过分受限，此时总会把margin-right强制为auto；

      ​

2. **行级元素的解析**

   行内元素不会另起一行只占据它对应的标签的边框所包含内容的空间，只能包含数据和其他行内元素。

   行级元素不能设置宽高，不能设置上下`margin`、和`padding` 。

   行内元素会生成一个**内容区**，类似于块级元素的content部分，**内容区**的大小与字体的大小相等。

   内容区加上文字的上下边距就等于**行内框**的高度，可以通过设置line-height的高度控制行内框的高度。**行框**是包含该行中行内框最高点和最低点的最小框。如下图:
   
   ![行内元素](https://github.com/Artila/Interview/blob/master/%E8%B5%84%E6%96%99%E6%94%B6%E9%9B%86/img/inline1.png)



3. **行级元素与块级元素的嵌套关系**

- 行级元素嵌套行级元素
- 块级元素嵌套块级元素，块级元素内嵌套行级元素。
- 少数块级级元素不能嵌套块级元素例如：**p不能嵌套div标签,标题标签中最好不要嵌套div。**







