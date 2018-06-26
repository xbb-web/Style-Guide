# HTML编码风格小结

ps....JavaScript这项技能牢固掌握并且运用自如以及编写规范对于作为一个合格的前端来说固然重要，但是HTML超文本标记语言的规范也是不容小觑的。以下是整理了一些HTML的书写建议,如果还有其他没写到的，大家一起来补充~~~

###黄金定律
永远遵循同一套编码规范,不管有多少人共同参与同一项目,一定要确保每一行代码都像是同一个人编写的.

#### 1.html语法
a.嵌套元素应当缩进两个空格
b.对于属性的定义,确保全部使用双引号,绝不要使用单引号, 更不要不用引号
c.大小写,以下都应该用小写：
HTML 元素名称，属性，属性值（除非 text/CDATA），CSS 选择器，属性，属性值。,
d.html注释，一般会使用在一些主要节点标签结束的后边

```
<html>  
    <head>  
    </head>      
    <body>
    	<div class="title">
    		<p></p>
    		<input type="text" value="">
    	</div>
    </body><!--body 部分-->  
</html>  
```


#### 2.语义化html标签

一方面是，利用html标签，达到语义化的目的，比如

列表：```<ul><li> ```

表格:``` <table>```

不建议什么元素都使用div。
另一方面是尽可能使用html5提供的具有语义化的标签。
以前写法

```
<div class="header"></div>
<div class="main"></div>
<div class="footer"></div>
```

建议写法
```
<header></header>
<main></main>
<footer></footer>
```
#### 3.h1-h6标签的使用

一般我们会用h1, h2 和 h3作为标题标签，标题元素意味着页面上高权值的关键词, 所以 h1, h2 和 h3 被频繁利用来为关键词加权. 而 h4, h5 和 h6 的权值并不高, 如果只为了设置字体大小，或者区分样式，不适合使用h1-h6，宁愿选择<span>,<em>这些标签

#### 4.属性顺序
HTML属性应当按照以下从左往右顺序依次排列,确保代码的易读性:
1.class   2.id,name　3.data-*   4.src,for,type,href， 5.title,alt　
class用于标示高度可复用的组件,因此应该排在首位.

#### 5.html嵌套级别不宜过多
尽量使html做到扁平化，避免嵌套过多,,尽量避免多余的父元素
```
<!-- good -->
<img class="avatar" src="image.png">

<!-- bad -->
<span class="avatar">
    <img src="image.png">
</span>
```
#### 6.把所有<特殊符号用编码表示 
任何小于号（<），不是标签的一部分，都必须被编码为& l t ; 
任何大于号（>），不是标签的一部分，都必须被编码为& g t ; 

#### .自定义属性建议使用data-
```
<div data-name="customer"></div>
```
#### 8.将样式表和脚本中的type省略，除非你不是用的css或javascript，在html5，该值默认是text/css和text/javascript
```
<!-- 省略type -->
<script src="index.js"></script>

<!-- 未省略type -->
<script src="index.js" type="text/javascript"></script> 
```
