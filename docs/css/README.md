# CSS

## CSS语法格式

### 注释

```css
/*注释*/
```

### 行内式

行内式将样式定义在具体html元素的style属性中。以行内式写的CSS耦合度高，只适用于当前元
素，在设定某个元素的样式时比较常用。但是这种写法会使得页面非常杂乱无章，真正开发中实际上是
使用嵌入式或引入外联样式文件的方式来进行渲染的。

```html
<div style="width:200px;height:300px;background:black;"></div>
```

### 嵌入式

在`<head>`标签里放`<style>`标签

```html
选择器名称 {
属性:属性值;
...
}
<style type="text/css">
/* 使用元素选择器给所有div设置宽度和高度，背景色为黑色 */
div {
width:200px;
height:300px;
background:black;
}
</style>
```

!>css 声明要以分号 ; 结束，声明以 {} 括起来。
!>建议一行书写一个属性。
!>若值为若干单词，则要给值加引号，如 font-family: "agency fb";

### 引入外联样式文件

在实际开发当中，很多时候都使用引入外联样式文件，这种形式可以使html页面更加清晰，而且可
以达到更好的重用效果。

style.css

```css
/* 使用元素选择器给所有div设置宽度和高度，背景色为黑色 */
div {
width:200px;
height:300px;
background:black;
}
```

index.html

```html
<link rel="stylesheet" type="text/css" href="style.css" />
```

`rel` : 规定当前文档与被链接文档之间的关系。
`stylesheet` : 文档的外部样式表。
很多时候，大量的 HTML 页面使用了同一个CSS。那么就可以将这些 CSS 样式保存在一个单独
的 `.css` 文件中，然后通过 `<link />` 元素去引入它。

## CSS选择器

### 基本选择器

#### 通用选择器

```css
/* 初始所有元素的内外间距为0 */
*{
margin:0;
padding:0;
}
```

#### 元素选择器

```css
选择器名称 {
属性:属性值;
...
}
/* 使用元素选择器给所有div设置宽度和高度，背景色为黑色 */
div {
width:200px;
height:300px;
background:black;
}
```

#### 类选择器

```css
.class属性值 {
属性:属性值;
...
}
/* 使用类选择器给所有class="dv"的元素设置宽度和高度，背景色为黑色 */
.dv {
width:200px;
height:300px;
background:black;
}
```

#### id选择器

```css
#id属性值 {
属性:属性值;
...
}
/* 使用id选择器给id="dv"的元素设置宽度和高度，背景色为黑色 */
#dv {
width:200px;
height:300px;
background:black;
}
```

#### 分组选择器

```css
选择器1，选择器2{
	属性：属性值；
	...
}
p,#name {
color: red;
font-size: 20px;
}
```

### 组合选择器

#### 后代选择器

```css
父元素 子元素(可以继续获取子元素的子元素) {
   属性:属性值;
   ...
}
/*
 使用类选择器给所有class="food"的元素
 的所有子元素li设置蓝色的边框
*/
.food li {
    border: 1px solid blue;
}

```

## CSS常用属性

### 背景

#### background-color

设置元素的背景颜色。

```css
/*
 设置body元素的背景色为灰色
 两种方式效果一致
*/
body {
    background-color:gray;
    /* 另一种方式 */
    background:gray;
}
```

#### background-image

设置元素的背景图像，默认情况下，背景图像进行平铺重复显示，以覆盖整个元素实体。

```css
/*
 设置body元素的背景为图片
 两种方式效果一致
*/
body {
    background-image: url(img/Daniel_Wu.jpg);
    /* 另一种方式 */
    background: url(img/Daniel_Wu.jpg);
}

```

#### background-repeat

设置是否重复图像及如何重复背景图像。

```css
/*
 设置body元素的背景为图片，图片不重复显示
 两种方式效果一致
*/
body {
    background-image: url(img/Daniel_Wu.jpg);
    background-repeat: no-repeat;
    /* 另一种方式 */
    background: url(img/Daniel_Wu.jpg) no-repeat;
}
```

可选值

| 值        | 描述                                 |
| --------- | ------------------------------------ |
| repeat    | 默认。背景图像将在垂直和水平方向重复 |
| no-repeat | 背景图像仅显示一次                   |
| repeat-x  | 背景图像水平方向重复                 |
| repeat-y  | 背景图像垂直方向重复                 |

### 文本

#### color

设置文本颜色

```css
/* 字体颜色蓝色 */
body {
    color:blue;
}
/* 字体颜色绿色 */
h1 {
    color:#00ff00;
}
/* 字体颜色红色 */
h2 {
    color:rgb(255,0,0);
}
```

#### text-align

设置文本对齐方式，center（居中），le（左对齐），right（右对齐）。

```css
body {
    text-align:center;
}
```

#### text-decoration

规定添加到文本的修饰，属性值：none、underline、overline、line-through。

#### text-indent

设置文本首行缩进。

```css
p {
    text-indent: 2em;
}
```

### 字体

#### font-family

文本字体，该属性设置文本的字体。

```css
/* 靠前的先生效 */
p {
    font-family: "微软雅黑", "黑体", "agency fb";
}
```

#### font-size

文本大小

```css
/* 字体大小50px */
body {
    font-size: 50px;
}
```

#### font-weight

```css
body {
    font-weight: 100;
    font-weight: 900;
    /* 下面两种方式效果一致 */
    font-weight: 700;
    font-weight: blod;
    /* 下面两种方式效果一致 */
    font-weight: 400;
    font-weight: normal;
}
```

### 列表

#### list-style

```css
/* 列表样式无标记 */
.food li ul li {
    list-style: none;
}
```

### 对齐方式

#### text-align

规定元素中的文本的水平对齐方式。

#### display

display属性用于定义元素的显示类型。

| 值           | 描述                                             |
| ------------ | ------------------------------------------------ |
| none         | 此元素不会被显示                                 |
| block        | 此元素将被显示为块级元素，此元素前后会带有换行符 |
| inline       | 此元素被显示为内联元素，元素前后没有换行符       |
| inline-block | 行内块元素，li中使用会变为类似导航的效果         |

### 盒子模型

border、padding、margin三个属性构成了盒子模型。

![](https://img-blog.csdnimg.cn/20210729225531146.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3lhbmcxMTQ1NDQ=,size_16,color_FFFFFF,t_70)

#### border

设置所有的边框属性。

1.可同时设置边框的宽度、样式、颜色

```css
/* 设置边框和宽高 */
div{
    border: 1px solid black;/* 设置粗细为1px的黑色实心线边框 */
    width: 200px;/* 宽 */
    height: 100px;/* 高 */
}
```

使用border-width、border-style、border-color单独设置

```css
div {
    border-width: 1px;/* 粗细1px */
    border-style: solid;/* 实心线 */
    border-color: black;/* 黑色 */
}
```

#### padding

设置元素所有内边距的宽度，默认按照上右下左的顺序设定，或者设置各边上内边距的宽度。

```css
/* 设置上右下左的内边距 */
div {
    padding:10px 5px 15px 20px;
}
```

#### margin

```css
/* 设置上右下左的外边距 */
div {
    margin:10px 5px 15px 20px;
}
```

auto 可以设置居中效果。

```css
div {
    margin: 0px auto;
}
```

auto：自动，可以理解为居中的意思，浏览器自动计算外边距。

margin: 0px auto; 0 或者 0px 表示上下间距为0px，auto表示左右外边距自动计算，表现为 居中状态。

##  CSS定位和浮动

​		CSS 定位 (positioning) 属性允许你对元素进行定位 ，定位的基本思想很简单，它允许你定义元素框 相对于其正常位置应该出现的位置，或者相对于父元素、另一个元素甚至浏览器窗口本身的位置。

CSS 有三种基本的定位机制：普通流、浮动和定位

​		除非专门指定，否则所有框都在普通流中定位，即普通流中的元素的位置由元素在HTML 中的位置 决定浏览器在读取 HTML 源代码的时候是根据元素在代码出现的顺序读取，最终元素的呈现方式是依据 元素的盒子模型来决定的。行内元素是从左到右，块状元素是从上到下。默认的书写方式即是普通流。

### 定位position

通过使用 position 属性，我们可以选择 4 种不同类型的定位，这会影响元素框生成的方式。

| 值       | 描述                                             |
| -------- | ------------------------------------------------ |
| static   | 默认值，普通流                                   |
| relative | 相对定位，其子元素如果使用定位相对于它的位置改变 |
| absolute | 绝对定位，相对于其父元素的位置作为参照物         |
| fixed    | 固定定位，相对于浏览器窗口作为参照物             |

**static**：默认值，普通流（忽略 left ， top ， right ， bottom 或者 z-index 声明）。 

**relative**：生成相对定位的元素，相对于其正常位置进行定位。元素的位置通过 left ， top ， right ， bottom 属性进行改变，其子元素如果使用定位相对于它的位置改变。 

**absolute**：生成绝对定位的元素，相对于其第一个父元素进行定位，如果父元素没有设置 relative 属性，则向上继续寻找，直到body元素。元素的位置通过 left ， top ， right ， bottom 属性进行规定。 

**fixed**：生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过 left ， top ， right ， bottom 属性进行规定。

### 浮动float

float 的属性值有 none 、 left 、 right 。

| 值    | 描述                                    |
| ----- | --------------------------------------- |
| none  | 默认值，不浮动                          |
| left  | le 左浮动，元素从左边开始并列显示为一行 |
| right | 右浮动，元素从右边开始并列显示为一行    |

