 # CSS 重点知识汇总



## 一、常用css选择器

1. *通用选择器：选择所有元素，不参与计算优先级，兼容性IE6+
2. X 元素选择器： 选择标所有签为X的元素，兼容性：IE6+
3. .X  id选择器：选择id值为X的元素，兼容性：IE6+
4. .X 类选择器： 选择class包含X的元素，兼容性：IE6+
5. X Y后代选择器： 选择满足X选择器的后代节点中满足Y选择器的元素，兼容性：IE6+
6. :link，:visited，:focus，:hover，:active链接状态： 选择特定状态的链接元 素，顺序LoVe HAte，兼容性: IE4+
7. X + Y直接兄弟选择器：在X之后第一个兄弟节点中选择满足Y选择器的元素，兼容性： IE7+
8. X > Y子选择器： 选择X的子元素中满足Y选择器的元素，兼容性： IE7+
9. X ~ Y兄弟： 选择X之后所有兄弟节点中满足Y选择器的元素，兼容性： IE7+
10. [attr=value]：选择属性值刚好为value的元素
11. :first-line：伪元素，选择块元素的第一行，兼容性IE5.5+ 
12. :nth-child(an + b)：伪类，选择前面有an + b - 1个兄弟节点的元素，其中n >= 0， 兼容性IE9+
   等等



## 二、HTML table  与 CSS table  类似属性 

```
HTML：
 cellspacing 规定单元格之间的空间（外间距）
 cellpadding 属性规定单元边沿与其内容之间的空白（内间距, 值都是数值）
CSS：
 border-collapse 设置是否把表格边框合并为单一的边框
 border-spacing 设置相邻单元格的边框间的距离(px cm)
```

 

##三、定位、浮动

### 定位


1.块级元素与行内元素
​     **块级元素**： 默认情况，块级元素会新起一行（自动换行）.一般块级元素可以包含 **行内元素** 和其他 **块级元素**

     包括：<div>,<h1>,<p>,<form>,<table>,<ul>,<ol>,<hr>，<canvas>,<video>
     以及 h5中实现页面构架功能的元素

   **行内元素**：默认情况，行内元素不会新起一行。一般情况下，行内元素只能包含 **数据** 和其他 **行内元素**
     包括：<span>,<a>,<br>,<img>,<button>,<input>,<select>,<label>,<textarea>, <b>,<strong>,<i>,<em> 
2.position属性 
​     一切皆为框
​          行框：由一行形成的水平框（Line Box）

​          块框：元素显示为一块内容（block Box）

​     position 属性值：

​          *static*    默认值，**没有定位**，元素框正常生成
​          *relative*    相对于**原来的位置**定位，保持原来的形状和类型（**未脱离文档流**）
​          *absolute*   元素框从文档流完全删除（**脱离文档流**），并相对于其包含块定位。元素定位后生成一个**块级框**，而不论原来它在正常流中是何种类型的框
​           绝对定位的元素的位置相对于 **最近的已定位的父元素**（这里的已定位元素指**除** **static**默认定位的其余三种），如果元素没有已定位的祖先元素，那么它的位置相对于 **最初的包含块** 相对于文档的 body 元素，并且它会随着页面滚动而移动。

​          *fixed*    是一种**特殊的绝对定位**，对其设置的偏移量永远是相对于**视窗本身**。我们常见到的 导航条 固定在页面顶部，回到页面顶部 按钮基本都是采用此定位方式。

​     z-index 只对定位元素有效果；

### 浮动

​         浮动的框可以向左或向右移动，直到它的外边缘碰到 **包含框**或 **另一个浮动框**的边框为止

​    浮动元素**特点**：

​          1.脱离文档流

​          2.块在一行显示

​          3.无论是块元素还是内联元素，没有宽度时默认**内容撑开宽度**；

​          4.使内联元素支持宽高

​          5.提升层级半级，其他元素占据该元素位置时，其内容会被挤出去

 

   **清除浮动**

​           1.使用clear 属性

```
 样式  .c{clear:both};
 如添加空的元素
 <div class ="c"></div>
```

​           2.使用overflow属性

​                 给 浮动元素 的容器添加overflow:hidden;或overflow:auto;可以清除浮动



## 四、display属性

用来改变元素生成的框的类型

   属性值：

​       *none*  元素不显示 且 **不会占据**它本来应该显示的 空间；

​       *inline*  默认。此元素会被显示为内联元素，元素前后没有换行符；

​       *block*  此元素将显示为块级元素，此元素前后会**带有换行符；**

​       *inline-block*  行内块元素。



**display:none与visibility:hidden区别**：

​        都能让元素不可见。

区别：

1. display:none;会让元素完全从渲染树中消失，渲染的时候不占据任何空间；visibility: hidden;不会让元素从渲染树消失，渲染师元素继续占据空间，只是内容不可见
2. display: none;是非继承属性，子孙节点消失由于元素从渲染树消失造成，通过修改子孙节点属性无法显示；visibility: hidden;是继承属性，子孙节点消失由于 继承了hidden，通过设置visibility: visible;可以让子孙节点显式
3. 修改常规流中元素的display通常会造成文档重排。修改visibility属性只会造成本元素的重绘。




**display:block 与 display:inline** (结合块级元素和行内元素)

- block特性：
  - 可以设置width、height，实际宽高为“本身宽高+padding”，未设置宽高会扩展宽高以包含子元素
  - 独占一行（自动换行）


- inline特性：          

  - width、height属性设置无效

    实际宽高为“内部元素宽高+padding”（margin/padding在顶部和底部无效，两侧上有效）

  - 不独占一行




**display,float,position的关系**

1. 如果`display`为none，那么position和float都不起作用，这种情况下元素不产生框

2. 否则，如果position值为absolute或者fixed，框就是绝对定位的，float的计算值为none，display根据下面的表格进行调整。

3. 否则，如果float不是none，框是浮动的，display根据下表进行调整

4. 否则，如果元素是根元素，display根据下表进行调整

5. 其他情况下display的值为指定值 

    总结起来：**绝对定位、浮动、根元素都需要调整display**  规则如下：![display转换规则](http://owj66num8.bkt.clouddn.com/display-adjust.png)



## 五、如何确定一个元素的包含块(containing block)

​        根元素的包含块叫做初始包含块，在连续媒体中他的尺寸与viewport(视口)相同并且锚定在画布起点；对于paged media，它的尺寸等于page area。初始包含块的direction属性与根元素相同。

确定包含块的过程完全依赖于这个包含块的 position属性：

1. `position`为`relative`或者`static`的元素，它的包含块由最近的（`display`为`block`,`list-item`, `table`）祖先**块元素**的内容框组成

2. 如果元素`position`为`fixed`。对于连续媒体，它的包含块为**viewport**；对于paged media，包含块为**page area**

3. 如果元素`position`为`absolute`，它的包含块由祖先元素中最近一个`position`为`relative`,`absolute`或者`fixed`的元素产生，规则如下：

   - 如果祖先元素为行内元素，the containing block is the bounding box around the **padding boxes** of the first and the last inline boxes generated for that element.（包含块是为该元素生成的第一个和最后一个内联框的填充框包含的框）
   - 其他情况下包含块由祖先节点的**padding edge**组成

   如果找不到定位的祖先元素，包含块为**初始包含块**



## 六、元素居中

​     **水平居中**

- 如果需要居中的元素为**常规流中inline元素**，为父元素设置text-align: center;

- 如果需要居中的元素为**常规流中block元素**，1）为元素设置宽度，2）设置左右margin为auto。(margin: 0  auto;)

- 如果需要居中的元素为**浮动元素**，1）为元素设置宽度，2）`position: relative;`，3）浮动方向偏移量（left或者right）设置为50%，4）浮动方向上的margin设置为元素宽度一半乘以-1

  > ```
  >         width: 500px;         /* 1 */
  >         float: left;
  >         position: relative;   /* 2 */
  >         left: 50%;            /* 3 */
  >         margin-left: -250px;  /* 4 */
  > ```

- 如果需要居中的元素为**绝对定位元素**，1）为元素设置宽度，2）偏移量设置为50%，3）偏移方向外边距设置为元素宽度一半乘以-1

    或者1）为元素设置宽度，2）设置左右偏移量都为0,3）设置左右外边距都为auto

  > ```
  >         width: 800px;
  >         position: absolute;
  >         left: 50%;
  >         margin-left: -400px;
  >         或者
  >         width: 800px;
  >         position: absolute;
  >         margin: 0 auto;
  >         left: 0;
  >         right: 0;
  > ```



​    **垂直居中**

- 需要居中元素为**单行文本**，为包含文本的元素设置大于`font-size`的`line-height`

- 使用绝对定位 和 负外边距，1）为元素设置宽度，2）偏移量设置为50%，3）偏移方向外边距设置为元素宽度一半乘以-1

  > ```
  >     width: 150px;
  >     height: 100px;
  >     position: absolute;
  >     top: 50%;
  >     margin: -50px 0 0 0;
  > ```

- 使用绝对定位 和 transform ，元素的大小可以是未知的

  > ```
  >     position: absolute;
  >     top: 50%;
  >     transform: translate(0, -50%);
  >     /* 也可以transform: translateY(-50%) //相对于自身尺寸 */
  > ```


- 使用flex布局，适用于块级元素

  > ```
  > #parent {
  >     width: 300px;
  >     height: 300px;
  >     display: flex;
  >     align-items: center;
  > }
  > ```

[具体请参考](http://www.jianshu.com/p/969a4315e879)



## 七、层叠上下文(stacking context),布局规则

z轴上的**默认层叠顺序**如下（从下到上）：

1. 根元素的边界和背景
2. 常规流中的元素按照html中顺序
3. 浮动块
4. positioned元素按照html中出现顺序

如何**创建stacking context**：

1. 根元素
2. z-index不为auto的定位元素
3. z-index不为auto的flex item
4. opacity小于1的元素



## 八、外边距折叠(collapsing margins)

毗邻的两个或多个`margin`会合并成一个margin，叫做外边距折叠。规则如下：

1. 两个或多个毗邻的普通流中的块元素垂直方向上的margin会折叠（取较大值）
2. 浮动元素/inline-block元素/绝对定位元素的margin不会和垂直方向上的其他元素的margin折叠
3. 创建了块级格式化上下文的元素，不会和它的子元素发生margin折叠
4. 元素自身的margin-bottom和margin-top相邻时也会折叠



##九、css sprite是什么,有什么优缺点

概念：将多个小图片拼接到一个图片中。通过background-position和元素尺寸调节需要显示的背景图案。

优点：

1. 减少HTTP请求数，极大地提高页面加载速度
2. 增加图片信息重复度，提高压缩比，减少图片大小
3. 更换风格方便，只需在一张或几张图片上修改颜色或样式即可实现

缺点：

1. 图片合并麻烦
2. 维护麻烦，修改一个图片可能需要从新布局整个图片，样式



## 十、什么是FOUC?如何避

Flash Of Unstyled Content：用户定义样式表加载之前浏览器使用默认样式显示文档，用户样式加载渲染之后再从新显示文档，造成页面闪烁。

**解决方法**：把样式表放到文档的`head`



## 十一、specified value,computed value,used value 的计算方法

- specified value: 计算方法如下：
  1. 如果样式表设置了一个值，使用这个值
  2. 如果没有设置值，这个属性是继承属性，从父元素继承
  3. 如果没设置，并且不是继承属性，使用css规范指定的初始值
- computed value: 以specified value根据规范定义的行为进行计算，通常将相对值计算为绝对值，例如em根据font-size进行计算。一些使用百分数并且需要布局来决定最终值的属性，如width，margin。百分数就直接作为computed value。line-height的无单位值也直接作为computed value。这些值将在计算used value时得到绝对值。**computed value的主要作用是用于继承**
- used value：属性计算后的最终值，对于大多数属性可以通过window.getComputedStyle获得，尺寸值单位为像素。以下属性依赖于布局，
  - background-position
  - bottom, left, right, top
  - height, width
  - margin-bottom, margin-left, margin-right, margin-top
  - min-height, min-width
  - padding-bottom, padding-left, padding-right, padding-top
  - text-indent