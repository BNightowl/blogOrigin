title: CSS设计指南笔记(3)
date: 2015-08-17
tags: CSS3
---
# 一.盒模型
所谓盒模型，就是浏览器为页面中每个HTML元素生成的矩形盒子。这些盒子们都要按照可见版式模型(visual formatting model)在页面上排布。可见的页面版式主要由三个属性控制：
position属性：控制页面上元素之间的位置关系。
display属性：控制元素是堆叠，并排还是根本不在页面显示。
float属性：提供控制的方式，以便把元素组成成多栏布局。

	
# 二.浮动与清除
浮动，意思就是把元素从常规文档流中拿出来。一是可以实现传统出版物上那种文字绕排图片的效果，二是可以让原来上下堆叠的块级元素，变成左右并列，从而实现布局中的分栏。
浮动元素脱离了常规文档流后，原来紧跟其后的元素就会在空间允许的情况下，向上提升到与浮动元素平起平坐。
<!--more-->
### 1.围住浮动元素的三种方法
方法一：为父元素添加overflow:hidden
方法二：同时浮动父元素
方法三：添加非浮动的清除元素
方式1：简单地在父元素的最后添加一个非浮动的子元素，并给它应用clear属性
方式2：用CSS来添加清除元素，该元素为伪元素。并且给父元素添加一个类，例如：
```
	clearfix
	其CSS规则为：
		.clearfix:after{
			content:".";
			display:block;
			height:0;
			visibility:hidden;
			clear:both;
		}
```

注意：如果没有父元素，使用第三种方式即可。
	
# 三.定位
CSS布局的核心是position属性，对元素盒子应用这个属性，可以相对于它在常规文档流中的位置重新定位。
position四个值：static,relative,absolute,fixed,默认为static。
```
static:静态定位下的块级元素会在默认文档流中上下堆叠。
relative:相对定位下，可以利用top和left属性相对于元素在文档流中的常规位置(也就是它原来在文档流中的位置)重新定位。
absolute:绝对定位下，元素从文档流中被“连根拔起”，然后相对于其他元素(默认的定位上下文是body，事实上，绝对定位的任何祖先元素都可以成为它的定位上下文，只要你把祖先元素的position设定为relative即可。)定位。
fixed:固定定位，与绝对定位类似，不同的是它定位的上下文是浏览器窗口或手持移动设备的屏幕。
```

# 四.显示属性
显示属性也就是display属性，主要用于块级元素和行内元素的相互转换。常用属性值为block和inline。
注意display属性的none值和visibility属性的hidden值的区别：
```
display属性值设为none，会让该元素及包含在里面的元素都隐藏掉，它原先所占据的所有空间也会被“回收”。
visibility设为hidden，和dispaly设为none的区别是，它原先所占据的空间仍然“虚位以待”。
```
# 五.背景
每个盒子都可以想象成由两个图层组成，元素的前景层包含内容(如文本和图片)和边框,元素的背景层可以用实色填充，也可以包含任意多个背景图片，背景图片叠加在背景颜色之上。
### 1.背景粘附：
background-attachment属性控制滚动元素的背景图片是否随元素滚动而移动。默认值是scroll,即背景图片随元素滚动而移动。如果改为fixed,那么背景图片不会随元素滚动而移

动。
background-attachment:fixed一般用于给body元素添加淡色水印，让水印不随页面滚动而移动。
### 2.背景渐变
```
 /*默认从上到下*/
background:linear-gradient(red,blue);
/*从左到右*/
background:linear-gradient(left,red,blue);
/*从左上到右下*/
background:linear-gradient(-45deg,red,blue);
```

### 3.渐变点
 渐变点就是渐变方向上的点，可以在这些点上设定颜色和不透明度。通过设定下一个渐变点的颜色值，就可以控制渐变的效果。可以添加任意多个渐变点。位置一般用整个渐变宽度的百分比来表示。
```
例如：background:linear-gradient(red,green 50%,blue);（一个渐变点）
或者
background:linear-gradient(red 30%,green 50%,blue);（两个渐变点）等等。自己可以去尝试。
```
### 4.放射性渐变
放射性渐变的话我们可以将它看成是一个函数，然后我们给它一些参数，用这些参数指定形状，位置，尺寸，颜色和不透明度。
```
例如：
background:-webkit-radial-gradient(red,green 50%,blue);/*这是默认渐变形状，渐变效果会填充元素，如果元素是正方形，渐变会是圆形*/
background:-webkit-radial-gradient(circle,red,green 50%,blue);/*这是形状关键字circle,渐变形状变得均匀，渐变会是圆形*/
background:-webkit-radial-gradient(20px 20px,red,green 50%,blue);/*这是将渐变圆心移到了靠近左上角的位子*/
```
注意：像这里面的-webkit-包括我们平时用的-moz-,-ms-和-0-等等，是一个厂商前缀VSP(Vendor Specific Prefixes)，以前我只知道这是做浏览器兼容的，却不知道专名词，VSP是为了鼓励浏览器厂商今早采用W3C的CSS3推荐标准而产生的概念。


	