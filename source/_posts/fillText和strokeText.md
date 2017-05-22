title: Canvas:绘制文本
date: 2017-05-22
tags: [html5,canvas]
---
`Canvas`除了能绘制图片之外，还有绘制文本的基本功能，如填充和描边，向`Canvas`放置文本信息，以及一些其他控制文本布局的方法，如环形文本等。

在Canvas中的`CanvasRenderingContext2D`对象中提供了填充和描边两种文本绘制方法：

-`fillText(text,x,y,maxWidth)`:绘制填充文本
-`strokeText(text,x,y,maxWidth)`:绘制描边文本

然后`Canvas`可以设置类似于`CSS`的一些属性，比如：

-`fillStyle/strokeText = value`：填充/描边颜色
-`font = value`:字体大小、样式，类似`css`的`font`
-`textAlign = value`:文本对齐方式，类似于`css`的`text-align`
-`textBaseline = value`:文本基线对齐设置
-`direction = value`:文本方向设置

除此之外还提供了一个`measureText(text)`的测量方法，用来测量文本的宽度;
返回数据：`TextMetrics {width: xxxx}`
<!--more-->

## 填充和描边

`fillText(text,x,y,maxWidth)`用来绘制填充文本：

-`text`:绘制的文本内容
-`x`:文本绘制x轴的开始坐标
-`y`:文本绘制y轴的开始坐标
-`maxWidth`:文本绘制的最大宽度

例如：
```
var canvas = document.getElementById("mycanvas");
var context = canvas.getContext("2d");//获取2D绘画环境
var w = 800,h = 250;
canvas.width = w;
canvas.height = h;

var text = "Hello World!";
context.fillStyle = "Green";//设置绘制颜色
context.textAlign = "center";
context.font = "italic 48px 微软雅黑";

context.fillText(text,w/2,h/2-50);
context.fillText(text,w/2,h/2,200);
console.log(context.measureText(text));
```
效果：
<img src="http://bnightowl.com/img/source/20170522/fillText.png">

通过测量方法`measureText`测出text原长度为`290`，通过设置`maxWidth`,被压缩到了`200`。

然后strokeText(text,x,y,maxWidth)和fillText大同小异，例如：
```
var text = "Hello World!";
context.strokeStyle = "red";//设置绘制颜色
context.textAlign = "center";
context.font = "italic 48px 微软雅黑";

context.strokeText(text,w/2,h/2-50);
context.strokeText(text,w/2,h/2,200);
```
效果：
<img src="http://bnightowl.com/img/source/20170522/strokeText.png">

除此之外，我们可以两者结合，绘制带有描边的填充文字，例如：
```
var text = "Hello World!";
context.strokeStyle = "red";//设置绘制颜色
context.fillStyle = "Green";//设置绘制颜色
context.textAlign = "center";
context.font = "italic 48px 微软雅黑";

context.fillText(text,w/2,h/2);
context.strokeText(text,w/2,h/2);
```
效果：
<img src="http://bnightowl.com/img/source/20170522/fillTextandstroke.png">

如果说想更方便的应用文本绘制，可以封装成一个函数：
```
	/**	
	*@param ctx:canvas的2D绘画环境
	*@param text:要绘制的文本内容
	*@param x:绘制文本的x轴起始坐标
	*@param y:绘制文本的y轴起始坐标
	*@param color:文本颜色
	*@param isFill:是否填充
	*@param isMaxWidth:是否设置文本绘制的最大宽度
	*@param maxWidth:文本最大宽度
	**/
	function drawText(ctx,text,x,y,color,isFill,isMaxWidth,maxWidth){
		if(isFill){
			ctx.fillStyle = color;
			if(isMaxWidth){
				ctx.fillText(text,x,y,maxWidth);
			}else{
				ctx.fillText(text,x,y);
			}
		}else{
			ctx.strokeStyle = color;
			if(isMaxWidth){
				ctx.strokeText(text,x,y,maxWidth);
			}else{
				ctx.strokeText(text,x,y);
			}
		}
	}
```
调用：
```
drawText(context,"Hello World!",w/2,h/2-50,"green",true,false);
drawText(context,"Hello World!",w/2,h/2-50,"red",false,false);
drawText(context,"Hello World!",w/2,h/2,"green",true,true,200);
drawText(context,"Hello World!",w/2,h/2+50,"red",false,true,200);
```
<p data-height="300" data-theme-id="29657" data-slug-hash="VbVNrR" data-default-tab="result" data-user="BNightowl" data-embed-version="2" data-pen-title="fillTex" class="codepen">See the Pen <a href="https://codepen.io/BNightowl/pen/VbVNrR/">fillTex</a> by Eugenc (<a href="http://codepen.io/BNightowl">@BNightowl</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>