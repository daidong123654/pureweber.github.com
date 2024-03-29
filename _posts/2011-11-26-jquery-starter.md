---
layout: post
title: 初识jQuery
author: 朱柯军
github: KJlmfe
tags:
  - javascript
  - jquery

---

初步了解JavaScript后，其实对于新手来说，很难写出兼容性良好的JavaScript代码。
这里对上述的兼容性，做一点补充：对于相同的一段JavaScript代码，不同的浏览器可能会给出不一样的解释与运行结果。如果你想了解一些兼容性的例子，可以看看这篇文章<a href="http://www.cnblogs.com/wiky/archive/2010/01/09/IE-and-Firefox-Javascript-compatibility.html" target="_blank">《IE和Firefox的Javascript兼容性总结》</a>

不过，如果依靠一些JavaScript框架，就能很容易构建出适应各种浏览器的代码。比较流行的JavaScript框架有jQuery，YUI等等。它们的使用都很简单，只要在页面中引入框架的js脚本文件，就能在接下来的编程中使用框架中提供的各种方法了。

<a rel="attachment wp-att-1336" href="http://www.pureweber.com/article/%e5%88%9d%e8%af%86jquery/jquery/"><img class="size-full wp-image-1336 alignright" src="http://www.pureweber.com/wp-content/uploads/2011/11/jquery.jpg" alt="" width="204" height="211" /></a>
<h4>1.什么是DOM （DOM——HTML与JavaScript的桥梁）</h4>
DOM是Document Object Model的缩写，从字面翻译看，叫做“文档对象模型”

以下是我对它的理解：
<ol> 1.一种抽象的树形结构（将文档中的各个对象通过树形结构链接起来）
2.一种抽象的编程接口 （通过DOM我们可以访问文档的API）</ol>
总的来说，DOM将文档文件解析成为一种树形结构，树的结点是文档中的元素，然后我们可以通过这颗树的节点选取文档中的元素，通过文档元素的属性、方法和事件来掌控、操纵和创建动态的html元素。

我们可以将HTML文档理解为一座大楼，文档中的的房间、物品等相当于HTML文档中的对象，JavaScript看做是一个在大楼外面的人，DOM看做是大楼所有入口的集合。大楼外的人是无法访问大楼内部的事物的，除非这个人会穿墙术，当然这是不可能的，作为大楼的HTML为了让大楼外的人可以访问、修改它内部的东西，提供了许多入口，人通过入口进入大楼后，就可以对大楼内部经行操作了。

&nbsp;
<h4>2.JavaScript对象和jQuery对象的区别</h4>
JavaScript对象 = 通过JavaScript方法获得的DOM元素的对象
jQuery对象 = 通过jQuery选择器取得的DOM元素的对象

其实对于同一个DOM元素，我们既可以通过JavaScript选取它，也可以通过jQuery选取它。

他们的区别是：
<ul> 对于JavaScript对象我们只能使用JavaScript里的方法
对于jQuery对象我们只能使用jQuery里的方法
如果非要使用对方的方法，我们可以先将其转换为对方对象。</ul>
&nbsp;
<h4>3.如何为页面元素绑定事件（点击，鼠标移入，鼠标移除，失去焦点等事件）</h4>
<ul>
	<li>用JavaScript绑定
<ul>
	<li>方法一：调用addEventListenr()方法
例子：element.addEventListenr("click",function(){},true)</li>
	<li>方法二：直接绑定
例子：element.onclick=function(){}</li>
	<li>方法三：调用attachEvent()（IE的绑定模式）
例子：element.attachEvent("onclick",function(){})</li>
</ul>
</li>
	<li>用jQuery绑定
<ul>
	<li> 方法一：调用bind()方法
例子：$("#div1").bind("click",function(){})</li>
	<li>方法二：使用快捷事件
例子：$("#div1").click(function(){})</li>
</ul>
</li>
</ul>
注：用jQuery绑定事件是多浏览器兼容的，因此可以忽略浏览器对于绑定事件的差异

&nbsp;
<h4>4.如何使用简单的动画效果（淡入，淡出，滑动等）</h4>
jQuery的动画效果函数主要有：animate()  fadeIn()  fadeOut()  fadeTo()
通过调用这些函数，就可以实现相应的动画效果
具体用法：<a href="http://www.w3school.com.cn/jquery/jquery_ref_effects.asp">《jQuery 参考手册 - 效果》</a>

&nbsp;
<h4>5.一个小动画页面示例（采用jQuery框架）</h4>
演示地址：<a href="http://www.pureweber.com/works/demos/jquery-kick-off/example.html">jQuery小动画示例</a>

动画效果说明：
第一个按钮：以滑动效果出现一个白色黑边框的正方形 第二个按钮：正方形变成红色 第三个按钮：正方形淡出消失
第四个按钮：点击依次循环执行上述三个按钮的功能

<strong>HTML代码</strong>
{% highlight html %}
<button id="one">淡入</button>
<button id="two">变红</button>
<button id="three">消失</button>
<button id="four">只点我</button>
{% endhighlight %}

<strong>Javascript代码</strong>

{% highlight javascript %}
$(document).ready(function() 
{
	var count = 0;

	$("#one").bind("click",function(){
		$("#block").css("left","100");
		$("#block").css("opacity","0");
		$("#block").css("background-color","white");
		$("#block").animate({opacity: "1",left: "200px"},1500)
	});

	$("#two").bind("click",function(){
		$("#block").css("opacity","0")
		$("#block").css("background-color", "red")
		$("#block").animate({opacity: "1"}, 1000)
	});

	$("#three").click(function(){
		$("#block").animate({opacity: "0"}, 1000)
	});

	$("#four").click(function(){
		count++;
		count = count % 3;
		if( count == 1 ){
			$("#block").css("left","100");
			$("#block").css("opacity","0");
			$("#block").css("background-color","white");
			$("#block").animate({opacity: "1",left: "200px"},1500)
		}
		if( count == 2 ){
			$("#block").css("opacity","0")
			$("#block").css("background-color", "red")
			$("#block").animate({opacity: "1"}, 1000)
		}
		if( count == 0 ){
			$("#block").animate({opacity: "0"}, 1000)
		}
	});
});
{% endhighlight %}
