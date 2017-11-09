# grid栅格布局

　　Grid布局方式借鉴了平面装帧设计中的格线系统，将格线运用在屏幕上，而不再是单一的静态页面，可以称之为真正的栅格。本文将详细介绍grid布局

&nbsp;

### 引入

　　对于Web开发者来说，网页布局一直是个比较重要的问题。但实际上，在网页开发很长的一段时间当中，我们甚至没有一个比较完整的布局模块。总的来说 Web 布局经历了以下四个阶段：

　　1、table表格布局，通过 Dreamweaver 拖拽表格或者手写 table 标签布局

　　2、float浮动及position定位布局，借助元素盒模型本身的特性以及 float position 等属性等进行布局

　　3、flex弹性盒模型布局，革命性的突破，解决传统布局方案上的三大痛点：排列方向、对齐方式，自适应尺寸，是目前最为成熟和强大的布局方案

　　4、grid栅格布局，二维布局模块，具有强大的内容尺寸和定位能力，适合需要在两个维度上对齐内容的布局

　　Grid Layout 是一种基于二维网格的布局系统，旨在完全改变我们设计基于网格的用户界面的方式，弥补网页开发在二维布局能力上的缺陷

　　与flex分为伸缩容器和伸缩项目类似，grid也分为网格容器和网格项目

&nbsp;

## 网格容器

### display

　　通过display属性设置属性值为grid或inline-grid可以创建一个网格容器。网格容器中的所有子元素就会自动变成网格项目（grid item）

<div class="cnblogs_code">
<pre>display: grid
display: inline-grid</pre>
</div>

　　网格项目默认放在行中，并且跨网格容器的全宽

<iframe style="width: 100%; height: 222px;" src="{{book.demo}}/css/grid/g1.html" frameborder="0" width="320" height="240"></iframe>

&nbsp;

### 显式网格

　　使用grid-template-columns和grid-template-rows属性可以显式的设置一个网格的列和行&nbsp;

【grid-template-rows】

　　默认值为none

　　grid-template-rows指定的每个值可以创建每行的高度。行的高度可以是任何非负值，长度可以是px、%、em等长度单位的值

<div class="cnblogs_code">
<pre>grid-template-rows: 60px 40px</pre>
</div>

　　item1和item2具有固定的高，分别为60px和40px。因为只定义了两个行的高度值，所以item3和item4的高度是根据其自身的内容来定义。

<iframe style="width: 100%; height: 356px;" src="{{book.demo}}/css/grid/g2.html" frameborder="0" width="320" height="240"></iframe>

【grid-template-columns】

　　默认值为none

　　像行一样，通过grid-template-columns指定的每个值来创建每列的列宽

<div class="cnblogs_code">
<pre>grid-template-columns: 40px 50px 60px</pre>
</div>

　　item4和item5放置在新的一行（第二行），因为grid-template-columns只定义了三列的大小，它们也分别放置在列1、列2和列3；其中列1、列2和列3的尺寸大小等于item1、item2和item3宽度。item1、item2和item3具有固定的宽度值，分别为40px、50px和60px

<iframe style="width: 100%; height: 326px;" src="{{book.demo}}/css/grid/g3.html" frameborder="0" width="320" height="240"></iframe>

【fr】

　　fr单位可以帮助我们创建一个弹列的网格轨道。它代表了网格容器中可用的空间（就像Flexbox中无单位的值）

<div class="cnblogs_code">
<pre>grid-template-columns: 1fr 1fr 2fr</pre>
</div>

　　在这个示例中，网格容器分成了4等份（1 + 1 + 2 = 4），每一份（1fr）是网格容器宽度的四分之一。所以item1和item2的宽度是网格容器的四分之一宽，item3是网格容器宽度的四分之二（2fr）

<div class="cnblogs_code">
<pre>grid-template-columns: 3rem 25% 1fr 2fr</pre>
</div>

　　当`fr`和其它长度单位的值结合在一起的时候，`fr`是基于网格容器可用空间来计算。

　　在这个示例中，网格容器可用空间是网格宽度减去`3rem`和`25%`剩下的宽度，而`fr`就是基于这个尺寸计算：

<div class="cnblogs_code">
<pre>1fr = (网格宽度 - 3rem - 网格宽度 * 25%) / 3</pre>
</div>

<iframe style="width: 100%; height: 378px;" src="{{book.demo}}/css/grid/g4.html" frameborder="0" width="320" height="240"></iframe>

【minmax()】

　　可以通过minmax()函数来创建网格轨道的最小或最大尺寸。minmax()函数接受两个参数：第一个参数定义网格轨道的最小值，第二个参数定义网格轨道的最大值。可以接受任何长度值，也接受auto值。auto值允许网格轨道基于内容的尺寸拉伸或挤压

<div class="cnblogs_code">
<pre>grid-template-rows: minmax(100px, auto);
grid-template-columns: minmax(auto, 50%) 1fr 3em;</pre>
</div>

　　在这个示例中，第一行的高度最小值是100px，但其最大值为auto，允许行的高度可以变大超过100px。第一列设置了最小值为auto，但它的最大值是50%，也就是列的最大宽度不会超过网格容器宽度的50%

<iframe style="width: 100%; height: 368px;" src="{{book.demo}}/css/grid/g5.html" frameborder="0" width="320" height="240"></iframe>

【repeat()】

　　使用repeat()可以创建重复的网格轨道。这个适用于创建相等尺寸的网格项目和多个网格项目。repeat()接受两个参数：第一个参数定义网格轨道应该重复的次数，第二个参数定义每个轨道的尺寸。

<div class="cnblogs_code">
<pre>grid-template-rows: repeat(3, 1fr);    
grid-template-columns: 30px repeat(3, 1fr) 30px;</pre>
</div>

　　在这个示例中，第一列和最后一列的宽度都是30px，并且它们之间有另列三列，这三列是通过repeat()来创建的，而且每列的列宽是1fr（1fr = (网格宽度 - 30px - 30px) / 3）

<iframe style="width: 100%; height: 378px;" src="{{book.demo}}/css/grid/g6.html" frameborder="0" width="320" height="240"></iframe>

### 间距

【grid-column-gap】&nbsp;

　　创建列与列之间的间距

【grid-row-gap】

　　创建行与行之间的间距

【grid-gap】

　　默认值为0

　　grid-gap是grid-row-gap和grid-column-gap两个属性的缩写，如果它指定了两个值，那么第一个值是设置grid-row-gap的值，第二个值设置grid-column-gap的值。如果只设置了一个值，表示行和列的间距相等，也就是说grid-row-gap和grid-column-gap的值相同

　　[注意]grid-gap只能创建列与列或行与行之间的间距，但不能创建列和行与网格容器边缘的间距

　　间距(Gap)可以设置任何非负值，长度值可以是px、%、em等单位值

<iframe style="width: 100%; height: 396px;" src="{{book.demo}}/css/grid/g7.html" frameborder="0" width="320" height="240"></iframe>

&nbsp;

## 网格项目

### 网格线

【grid-row-start】

【grid-row-end】

【grid-column-start】

【grid-column-end】

　　默认值为auto

　　通过网格线可以定位网格项目。网格线实际上是代表线的开始、结束，两者之间就是网格列或行。每条线是从网格轨道开始，网格的网格线从1开始，每条网格线逐步增加1

<div class="cnblogs_code">
<pre>grid-row-start: 2;
grid-row-end: 3; 
grid-column-start: 2; 
grid-column-end: 3;　&nbsp;</pre>
</div>

　　两列三行的网格创建三条列网格线和四条行网格线。item1就是由行和列的号码重新定位。如果一个网格项目跨度只有一行或一列，那么grid-row-end和grid-olumn-end不是必需的

<iframe style="width: 100%; height: 385px;" src="{{book.demo}}/css/grid/g8.html" frameborder="0" width="320" height="240"></iframe>

【grid-row】

【grid-column】

<div class="cnblogs_code">
<pre>grid-row: 2; 
grid-column: 3 / 4;</pre>
</div>

　　grid-row是grid-row-start和grid-row-end的简写。grid-column是grid-column-start和grid-column-end的简写。如果只提供一个值，则指定了grid-row-start(grid-column-start)值；如果提供两个值，第一个值是grid-row-start(grid-column-start)的值，第二个值是grid-row-end(grid-column-end)的值，两者之间必须要用/隔开

　　默认值为auto

【span】

　　关键词span后面紧随数字，表示合并多少个列或行

<div class="cnblogs_code">
<pre>grid-row: 1 / span 3;
grid-column: span 2;</pre>
</div>

<iframe style="width: 100%; height: 331px;" src="{{book.demo}}/css/grid/g9.html" frameborder="0" width="320" height="240"></iframe>

【grid-area】

<div class="cnblogs_code">
<pre>grid-area: 2 / 2 / 3 / 3;</pre>
</div>

　　如果指定四个值，第一个值对应grid-row-start，第二个值对应grid-column-start，第三个值对应grid-row-end，第四个值对应grid-column-end

<iframe style="width: 100%; height: 397px;" src="{{book.demo}}/css/grid/g10.html" frameborder="0" width="320" height="240"></iframe>

&nbsp;

### 网格线命名

　　通过grid-template-rows和grid-template-columns定义网格时，网格线可以被命名。网格线名称也可以设置网格项目位置

　　分配网格线名称必须用方括号[网格线名称]，然后后面紧跟网格轨道的尺寸值。定义网格线名称时需要避免使用规范中出现的关键词，以免导致混乱。

<div class="cnblogs_code">
<pre>grid-template-rows: [row-1-start] 1fr [row-2-start] 1fr [row-2-end];
grid-template-columns: [col-1-start] 1fr [col-2-start] 1fr [col-3-start] 1fr [col-3-end];</pre>
</div>

![namedGridLines](https://pic.xiaohuochai.site/blog/CSS_layout_namedGridLines.png)

　　可以在方括号中添加多个名称来命名网格线名称，使用多外名称命名网格线名称时，名称间要用空格隔开。每一个网格线的名称可以用来定位网格项目的位置

<div class="cnblogs_code">
<pre>grid-template-rows: [row-start row-1-start] 1fr [row-1-end row-2-start] 1fr [row-2-end row-end]; 
grid-template-columns: [col-start] 1fr [col-2-start] 1fr [col-3-start] 1fr [col-end];</pre>
</div>

![namedGridLines2](https://pic.xiaohuochai.site/blog/CSS_layout_namedGridLines2.png)

　　使用网格线名称设置网格项目位置和使用网格线号码设置网格项目位置类似，引用网格线名称的时候不应该带方括号

<iframe style="width: 100%; height: 427px;" src="{{book.demo}}/css/grid/g11.html" frameborder="0" width="320" height="240"></iframe>

　　使用repeat()函数可以给网格线分配相同的名称。这可以节省一定的时间。

<div class="cnblogs_code">
<pre>grid-template-rows: repeat(3, [row-start] 1fr [row-end]);
grid-template-columns: repeat(3, [col-start] 1fr [col-end]);</pre>
</div>

　　使用repeat()函数可以给网格线命名，这也导致多个网格线具有相同的网格线名称。相同网格线名称指定网格线的位置和名称，也且会自动在网格线名称后面添加对应的数字，使其网格线名称也是唯一的标识符

![namedGridLines3](https://pic.xiaohuochai.site/blog/CSS_layout_namedGridLines3.png)

　　使用相同的网格线名称可以设置网格项目的位置。网格线的名称和数字之间需要用空格分开&nbsp;

<div class="cnblogs_code">
<pre>grid-row: row-start 2 / row-end 3;
grid-column: col-start / col-start 3;</pre>
</div>

<iframe style="width: 100%; height: 390px;" src="{{book.demo}}/css/grid/g12.html" frameborder="0" width="320" height="240"></iframe>

### 网格区域命名

【grid-template-areas】

　　像网格线名称一样，网格区域的名称可以使用grid-template-areas属性来命名。引用网格区域名称也可以设置网格项目位置

<div class="cnblogs_code">
<pre>grid-template-areas:   "header header"   "content sidebar"    "footer footer";
grid-template-rows:    150px 1fr 100px;
grid-template-columns: 1fr 200px;</pre>
</div>

　　设置网格区域的名称应该放置在单引号或双引号内，每个名称由一个空格符分开。网格区域的名称，每组（单引号或双引号内的网格区域名称）定义了网格的一行，每个网格区域名称定义网格的一列

　　[注意]grid-template-areas: "header header" "content sidebar" "footer footer";不可以简写为grid-template-areas: "header" "content sidebar" "footer";

![namedGridLines4](https://pic.xiaohuochai.site/blog/CSS_layout_namedGridLines4.png)

　　grid-row-start、grid-row-end、grid-column-start和grid-column-end以及简写的grid-row、grid-column、grid-area都可以引用网格区域名称，用来设置网格项目位置

<iframe style="width: 100%; height: 393px;" src="{{book.demo}}/css/grid/g13.html" frameborder="0" width="320" height="240"></iframe>

### 隐式网格

【grid-auto-flow】

　　网格默认流方向是row，可以通过grid-auto-flow属性把网格流的方向改变成column　　&nbsp;

<div class="cnblogs_code">
<pre>grid-auto-flow: column</pre>
</div>

<iframe style="width: 100%; height: 262px;" src="{{book.demo}}/css/grid/g14.html" frameborder="0" width="320" height="240"></iframe>

　　当网格项目确认在显式网格之外时就会创建隐性网格，当没有足够的空间或者显式的网格轨道来设置网格项目，此时网格项目就会自动创建隐式网格

【grid-auto-rows】

【grid-auto-columns】

　　使用grid-auto-rows和grid-auto-columns属性可以定义隐式的网格

　　默认值为auto

<div class="cnblogs_code">
<pre>grid-template-rows:    70px;
grid-template-columns: repeat(2, 1fr);
grid-auto-rows:        140px;</pre>
</div>

　　在上面这个例子中我们只定义了一行（轨道），所以item1和item2的高都是70px。第二行（轨道）自动创建了item3和item4空间。grid-auto-rows定义隐式网格中的行（轨道）的大小，因此item3和item4的高度是140px

![gridAutoFlow](https://pic.xiaohuochai.site/blog/CSS_layout_gridAutoFlow.png)

<iframe style="width: 100%; height: 445px;" src="{{book.demo}}/css/grid/g15.html" frameborder="0" width="320" height="240"></iframe>

### 隐式命名

【隐式命名网格区域名称】

　　通常可以将网格线命名成任何想命名的名称，如果网格线名称添加-start和-end的后缀，其实也隐式的创建一个网格区域，可以用来设置网格项目的位置

<div class="cnblogs_code">
<pre>grid-template-rows:    [outer-start] 1fr [inner-start] 1fr [inner-end] 1fr [outer-end];
grid-template-columns: [outer-start] 1fr [inner-start] 1fr [inner-end] 1fr [inner-end];</pre>
</div>

　　在这个示例中，行和列都具有inner-start和inner-end网格线名称，同时也对应的创建一个隐式网格区域名称inner

<div class="cnblogs_code">
<pre>grid-area: inner</pre>
</div>

　　网格项目定位可以通过网格区域名称来设置，而不需要使用网格线名称

![gridAutoFlow2](https://pic.xiaohuochai.site/blog/CSS_layout_gridAutoFlow2.png)

【隐式命名网格线名称】

　　隐式的指定网格线反向指定了隐式的网格区域名称，命名的网格区域隐式的命名了网格线名称&nbsp;

<div class="cnblogs_code">
<pre>grid-template-areas:   "header header" "content sidebar" "footer footer";
grid-template-rows:    80px 1fr 40px;
grid-template-columns: 1fr 200px;</pre>
</div>

　　指定网格区域会给网格区域边线添加隐式的网格线名称。这些网格线的命名是基于网格区域来命名，只是在网格区域名称的后面添加后缀-start或-end

![gridAutoFlow3](https://pic.xiaohuochai.site/blog/CSS_layout_gridAutoFlow3.png)
<div class="cnblogs_code">
<pre>grid-row-start: header-start; 
grid-row-end: content-start; 
grid-column-start: footer-start; 
grid-column-end: sidebar-end;</pre>
</div>

　　在这个示例中，`header`通过隐式的网格线名称设置其位置

![gridAutoFlow4](https://pic.xiaohuochai.site/blog/CSS_layout_gridAutoFlow3.png)

&nbsp;

### 网格项目层级

　　网格项目可以具有层级和堆栈，必要时可能通过z-index属性来指定&nbsp;

<div class="cnblogs_code">
<pre>.item-1,.item-2 {
    grid-row-start:  1;
    grid-column-end: span 2;
}
.item-1 { 
    grid-column-start: 1; 
    z-index: 1; 
}
.item-2 { 
    grid-column-start: 2 
}</pre>
</div>

　　在这个例子中，item1和item2的开始行都是1，item1列的开始是1，item2列的开始是2，并且它们都跨越两列。两个网格项目都是由网格线数字定位，结果这两个网格项目重叠了。

　　默认情况下，item2在item1上面，但是，我们在item1中设置了z-index:1;，导致item1在item2之上

<iframe style="width: 100%; height: 410px;" src="{{book.demo}}/css/grid/g16.html" frameborder="0" width="320" height="240"></iframe>

### 对齐

【网格项目对齐方式（Box Alignment）】

　　CSS的Box Alignment Module补充了网格项目沿着网格行或列轴对齐方式。

【justify-items】

【justify-self】

　　justify-items和justify-self指定网格项目沿着行轴对齐方式；align-items和align-self指定网格项目沿着列轴对齐方式。

　　justify-items和align-items应用在网格容器上

【align-items】

【align-self】

　　align-self和justify-self属性用于网格项目自身对齐方式

　　这四个属性主要接受以下属性值：

<div class="cnblogs_code">
<pre>auto | normal | start | end | center | stretch | baseline | first baseline | last baseline</pre>
</div>

<iframe style="width: 100%; height: 423px;" src="{{book.demo}}/css/grid/g17.html" frameborder="0" width="320" height="240"></iframe>

【网格轨道对齐方式】

　　网格轨道对齐可以相对于网格容器行和列轴。

　　align-content指定网格轨道沿着行轴对齐方式；justify-content指定网格轨道沿着列轴对齐方式。它们支持下面属性：

<div class="cnblogs_code">
<pre>normal | start | end | center | stretch | space-around | space-between | space-evenly | baseline | first baseline | last baseline</pre>
</div>

<iframe style="width: 100%; height: 423px;" src="{{book.demo}}/css/grid/g18.html" frameborder="0" width="320" height="240"></iframe>
