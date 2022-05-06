#  什么是HTML

HTML 也叫做超文本标记语言。“超文本”就是表示页面内可以包含非 文字元素，如：图片、链接、音乐等。在Web服务中，信息一般是使用 HTML 格式以超文本和超媒体 方式传送的，所使用的 Internet 协议是 HTTP 协议。



>HTML 是用来描述网页的一种语言。
>
>- HTML 指的是超文本标记语言 (Hyper Text Markup Language) 
>- HTML 是一种标记语言 (markup language) 
>- 标记语言是一套标记标签 (markup tag) 
>- HTML 使用标记标签来描述网页

```html
<!DOCTYPE html>
<html>
     <head>
     <meta charset="UTF-8">
     <title></title>
     </head>
     <body>
     </body>
</html>
```

# HTML基础语法

```html
<!DOCTYPE html><!-- 必须写在HTML文件首行 -->
<html><!-- HTML文档的开始 -->
        
    <head><!-- HTML文档的开头部分 -->
        
        <!-- SEO搜索引擎优化策略 -->
        <!-- 网站标题 -->
        <title>网站标题</title>
        <!-- 网站图标 -->
        <link rel="icon" href="图标地址">
        <!-- 详细描述 -->
        <meta name="description" content="这里写网站内容描述" />
        <!-- 关键词 -->
        <meta name="keywords" content="这里写关键词" />
        
    </head><!-- HTML文档的开头结束 -->
    
    <body><!-- HTML文档的主体部分开始 -->
        
    </body><!-- HTML文档的主体部分结束 -->
    
</html><!-- HTML文档的结束 -->
```

# HTML常用标签和属性

## HTML标题

```html
<body>
    <!-- HTML 标题（Heading）是通过 <h1> - <h6> 等标签进行定义的 -->
    <h1>This is a heading</h1>
    <h2>This is a heading</h2>
    <h3>This is a heading</h3>
    <h4>This is a heading</h4>
    <h5>This is a heading</h5>
    <h6>This is a heading</h6>
</body>
```

## HTML段落

```html
<body>
    <!-- HTML 段落是通过 <p> 标签进行定义的 -->
    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
</body>
```

!>**注意**：浏览器会自动地在标题和段落的前后添加空行。

## HTML水平线

`<hr/>`

## HTML注释

`<!-- 编写注释在这里 -->`

## HTML链接

```html
<body>
    <!-- HTML 链接是通过 <a> 标签进行定义的 -->
    <a href="http://www.shsxt.com">This is a link</a>
</body>
```

## HTML图像

```html
<body>
    <!-- HTML 图像是通过 <img /> 标签进行定义的 -->
    <img src="img/1.jpg" title="这是一个图片" />
</body>
```

## div和span

`div` 是一个块级元素，通常与css配合使用，用于布局。 

`div` 标签可以把文档分割为独立的、不同的部分。它可以用作严格的组织工具，并且不使用任 何格式与其关联。

`<div>` 是一个块级元素。这意味着它的内容自动地开始一个新行。实际上，换行是 `<div>`  固有 的唯一格式表现。可以通过 `<div>`  的 `class` 或 `id` 应用额外的样式。



**标签的分类**：HTML 中标签元素三种不同类型：块状元素，行内元素，行内块状元素。

>- 块级元素特点： 元素都从新的一行开始，并且其后的元素也另起一行；元素的高度、宽度、行高 以及顶和底边距都可设置；元素宽度在不设置的情况下，是它本身父容器的 100%（和父元素的宽 度一致），除非设定一个宽度。 
>- 行内元素特点 ：和其他元素都在一行上；元素的高度、宽度及顶部和底部边距不可设置；元素的 宽度就是它包含的文字或图片的宽度，不可改变。
>-  行内块状元素的特点：和其他元素都在一行上；元素的高度、宽度、行高以及顶和底边距都可设 置。

!>后期可以通过 CSS 进行修改。

## HTML表格

表格由 `<table>` 标签来定义。每个表格均有若干行（由 `<tr>` 标签定义），每行被分割为若干 单元格（由 `<td>`标签定义）。字母 td 指表格数据（table data），即数据单元格的内容。数据单 元格可以包含文本、图片、列表、段落、表单、水平线、表格等等。

```html
<!DOCTYPE html>
<html>
     <head>
         <meta charset="UTF-8">
         <title>HTML表格</title>
     </head>
     <body>
         <!-- 表格标签 属性border="1" 添加表格边框粗细为1 -->
         <table border="1">
             <!-- 设置表格标题 -->
             <caption><h3>这是一个表格</h3></caption>
             <!-- 定义行 -->
             <tr>
                 <!-- th定义列 一般写在表格首行 内容会被加粗居中 -->
                 <th>Heading</th>
                 <th>Another Heading</th>
             </tr>
             <tr>
                 <!-- td定义列 -->
                 <td>row 1, cell 1</td>
                 <td>row 1, cell 2</td>
             </tr>
             <tr>
                 <td>&nbsp;</td>
                 <td>row 2, cell 2</td>
             </tr>
         </table>
     </body>
</html>
```

## HTML列表

```HTML
<!DOCTYPE html>
<html>
     <head>
         <meta charset="UTF-8">
         <title>HTML列表</title>
     </head>
     <body>
         <h4>一个有序列表：</h4>
         <ol>
             <li>咖啡</li>
             <li>牛奶</li>
             <li>茶</li>
         </ol>
         <h4>一个无序列表：</h4u>
         <ul start="50">
             <li>咖啡</li>
             <li>牛奶</li>
             <li>茶</li>
         </ul>
     </body>
</html>

```

## HTML表单

```html
<form action="http://www.shsxt.com" method="post">
   First name:
    <input type="text" name="firstname" value="Mickey" />
    <br/>
   Last name:
    <input type="text" name="lastname" value="Mouse" />
    <br/><br/>
    <input type="submit" value="Submit" />
</form>
```

## HTML属性