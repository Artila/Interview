# CSS布局详解（二）——标准流布局（Nomal flow）

转载：http://www.cnblogs.com/liugblog/p/4982684.html



### 一、正常流

这是指西方语言中文本从左向右，从上向下显示，这也是我们熟悉的传统的HTML文档中的文本布局。

注意，在非西方的语言中，流方向可能不同。大多数元素都在正常流中，要让一个元素不在正常流中，唯一的方法就是使之成为*浮动元素*或*定位元素*。

标准流中，块级元素独占一行，垂直放置。

行级元素在水平方向上一个接一个的排列。



### 二、垂直外边距的合并问题（margin collapse）

在标准流布局中垂直外边距的合并有两种情况。

##### 1、在标准流中上下两个盒子的外边距回合，即上盒子的`margin-bottom`会与下盒子的`margin-top`合并为两者之间的最大值。

```css
 div{
    width: 100px; height: 100px; 
 }
.top{
    margin-bottom: 50px; background: purple; 
 }
.bottom{
    margin-top: 20px; background: pink; 
 }
    
<div class="top"></div>
<div class="bottom"></div>
```

![垂直外边距的合并](https://github.com/Artila/Interview/blob/master/%E8%B5%84%E6%96%99%E6%94%B6%E9%9B%86/img/margin2.jpg)

##### 2、一个盒子包裹另一个盒子，当包裹盒子没有设置border和padding时，里边盒子的设置的上边距不会起作用。

```css
.father{
	width: 400px; 
	height: 400px; 
	background: pink; 
} 
.son{
	width: 200px; 
	height: 200px; 
	background: purple; 
	margin-left: 100px; 
	margin-top: 50px; 
} 
<div class="father">
   <div class="son">
</div>
```

![外边距不起作用](https://github.com/Artila/Interview/blob/master/%E8%B5%84%E6%96%99%E6%94%B6%E9%9B%86/img/margin3.jpg)

设置边框后：

![设置边框后](https://github.com/Artila/Interview/blob/master/%E8%B5%84%E6%96%99%E6%94%B6%E9%9B%86/img/margin4.jpg)

**解释：**

对于父块DIV内含子块DIV的情况，就会按另一条CSS惯例来解释了，那就是：对于有块级子元素的元素计算高度的方式,如果元素没有垂直边框和填充,那其高度就是其子元素顶部和底部边框边缘之间的距离。



**解决方法：**

解决父子DIV中顶部margin cllapse的问题，需要给父div设置：



（1）边框，当然可以设置边框为透明;

```
   border:1px solid transparent
或
   border-top:1px solid transparent
```



（2）为父DIV添加padding，或者至少添加padding-top;

​	此外，还可以通过over-flow来解决，给父DIV写入：

```
   over-flow:hidden;    
```



### 三、BFC

##### 1、BFC是什么？

在解释 BFC 是什么之前，需要先介绍 `Box、Formatting Context`的概念。

Box 是 CSS 布局的对象和基本单位， 直观点来说，就是一个页面是由很多个 Box 组成的。

元素的类型和 display 属性，决定了这个 Box 的类型。 

不同类型的 Box， 会参与不同的 Formatting Context（一个决定如何渲染文档的容器），因此Box内的元素会以不同的方式渲染。让我们看看有哪些盒子：

block-level box: display 属性为 block, list-item, table 的元素，会生成 block-level box。并且参与 block fomatting context；

inline-level box: display 属性为 inline, inline-block, inline-table 的元素，会生成 inline-level box。并且参与 inline formatting context；



**Formatting context**


Formatting context 是 W3C CSS2.1 规范中的一个概念。

它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。

最常见的 Formatting context 有 Block fomatting context (简称BFC)和 Inline formatting context (简称IFC)。

CSS2.1 中只有 BFC 和 IFC, CSS3 中还增加了 GFC 和 FFC。



**BFC 定义**


BFC(Block formatting context)直译为"块级格式化上下文"。

它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。

**BFC布局规则：**

- 内部的Box会在垂直方向，一个接一个地放置。
- Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠
- 每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。
- BFC的区域不会与float box重叠。
- BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。
- 计算BFC的高度时，浮动元素也参与计算。



##### 2、哪些元素会生成BFC?

- 根元素

- float属性不为none

- position为absolute或fixed

- display为inline-block, table-cell, table-caption, flex, inline-flex

- overflow不为visible

  ​

##### 3、BFC的作用及原理

1. 自适应两栏布局
	
   ![两栏布局](https://github.com/Artila/Interview/blob/master/%E8%B5%84%E6%96%99%E6%94%B6%E9%9B%86/img/BFC1.png)	
	
   根据BFC布局规则第3条：

   > 每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反)。即使存在浮动也是如此。

   因此，虽然存在浮动的元素aslide，但main的左边依然会与包含块的左边相接触。

   ![生成BFC](https://github.com/Artila/Interview/blob/master/%E8%B5%84%E6%96%99%E6%94%B6%E9%9B%86/img/BFC6.png)	

   根据BFC布局规则第四条：

 > BFC的区域不会与float box重叠。

   我们可以通过通过触发main生成BFC， 来实现自适应两栏布局。

   ```
   .main {
	overflow: hidden;
     }
   ```

    当触发main生成BFC后，这个新的BFC不会与浮动的aside重叠。因此会根据包含块的宽度，和aside的宽度，自动变窄。



2.  清除内部浮动

   ```css
   <style>
   .par {
       border: 5px solid #fcc;
       width: 300px;
   }

   .child {
       border: 5px solid #f66;
       width:100px;
       height: 100px;
       float: left;
   }
   </style>
   <body>
   <div class="par">
       <div class="child"></div>
       <div class="child"></div>
   </div>
   </body>
   ```

   ![浮动问题](https://github.com/Artila/Interview/blob/master/%E8%B5%84%E6%96%99%E6%94%B6%E9%9B%86/img/BFC2.png)	

   根据BFC布局规则第六条：

  > 计算BFC的高度时，浮动元素也参与计算

　　为达到清除内部浮动，我们可以触发par生成BFC，那么par在计算高度时，par内部的浮动元素child也会参与计算。

　　代码：

     ```
     .par {
       overflow: hidden;
      }
     ```

　　效果如下：

    ![清除浮动](https://github.com/Artila/Interview/blob/master/%E8%B5%84%E6%96%99%E6%94%B6%E9%9B%86/img/BFC3.png)	

3. 防止垂直 margin 重叠

   ```
   <style>
   p {
       color: #f55;
       background: #fcc;
       width: 200px;
       line-height: 100px;
       text-align:center;
       margin: 100px;
   }
   </style>
   <body>
     <p>Haha</p>
     <p>Hehe</p>
   </body>
   ```

  ![防止垂直 margin 重叠](https://github.com/Artila/Interview/blob/master/%E8%B5%84%E6%96%99%E6%94%B6%E9%9B%86/img/BFC4.png)	

    两个p之间的距离为100px，发送了margin重叠。
    
　　根据BFC布局规则第二条：

  > Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠

　　我们可以在p外面包裹一层容器，并触发该容器生成一个BFC。那么两个P便不属于同一个BFC，就不会发生margin重叠了。


	```css
	<style>
	.wrap {
	    overflow: hidden;
	}
	p {
	    color: #f55;
	    background: #fcc;
	    width: 200px;
	    line-height: 100px;
	    text-align:center;
	    margin: 100px;
	}
	</style>
	<body>
	<p>Haha</p>
	<div class="wrap">
	    <p>Hehe</p>
	</div>
	</body>
	```
![防止垂直 margin 重叠](https://github.com/Artila/Interview/blob/master/%E8%B5%84%E6%96%99%E6%94%B6%E9%9B%86/img/BFC5.png)

#### 总结

其实以上的几个例子都体现了BFC布局规则第五条：

> BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。反之也如此。

因为BFC内部的元素和外部的元素绝对不会互相影响，因此， 当BFC外部存在浮动时，它不应该影响BFC内部Box的布局，BFC会通过变窄，而不与浮动有重叠。同样的，当BFC内部有浮动时，为了不影响外部元素的布局，BFC计算高度时会包括浮动的高度。避免margin重叠也是这样的一个道理。



### IFC

IFC(Inline Formatting Contexts)直译为"内联格式化上下文"，IFC的line box（线框）高度由其包含行内元素中最高的实际高度计算而来（不受到竖直方向的padding/margin影响)。

IFC中的line box一般左右都贴紧整个IFC，但是会因为float元素而扰乱。float元素会位于IFC与与line box之间，使得line box宽度缩短。 

同个ifc下的多个line box高度会不同。 IFC中时不可能有块级元素的，当插入块级元素时（如p中插入div）会产生两个匿名块与div分隔开，即产生两个IFC，每个IFC对外表现为块级元素，与div垂直排列。
那么IFC一般有什么用呢？

水平居中：当一个块要在环境中水平居中时，设置其为inline-block则会在外层产生IFC，通过text-align则可以使其水平居中。
垂直居中：创建一个IFC，用其中一个元素撑开父元素的高度，然后设置其vertical-align:middle，其他行内元素则可以在此父元素下垂直居中

### GFC

GFC(GridLayout Formatting Contexts)直译为"网格布局格式化上下文"，当为一个元素设置display值为grid的时候，此元素将会获得一个独立的渲染区域，我们可以通过在网格容器（grid container）上定义网格定义行（grid definition rows）和网格定义列（grid definition columns）属性各在网格项目（grid item）上定义网格行（grid row）和网格列（grid columns）为每一个网格项目（grid item）定义位置和空间。

那么GFC有什么用呢，和table又有什么区别呢？首先同样是一个二维的表格，但GridLayout会有更加丰富的属性来控制行列，控制对齐以及更为精细的渲染语义和控制。

### FFC

FFC(Flex Formatting Contexts)直译为"自适应格式化上下文"，display值为flex或者inline-flex的元素将会生成自适应容器（flex container），可惜这个牛逼的属性只有谷歌和火狐支持，不过在移动端也足够了，至少safari和chrome还是OK的，毕竟这俩在移动端才是王道。

Flex Box 由伸缩容器和伸缩项目组成。通过设置元素的 display 属性为 flex 或 inline-flex 可以得到一个伸缩容器。设置为 flex 的容器被渲染为一个块级元素，而设置为 inline-flex 的容器则渲染为一个行内元素。

伸缩容器中的每一个子元素都是一个伸缩项目。伸缩项目可以是任意数量的。伸缩容器外和伸缩项目内的一切元素都不受影响。简单地说，Flexbox 定义了伸缩容器内伸缩项目该如何布局。

