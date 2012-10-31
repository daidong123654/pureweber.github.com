---
layout: post
title: FireBug和YSlow介绍
author: 陈云飞
github: cloudfly
tags:
  - chrome
  - firebug
  - firefox
  - javascript
  - yslow
  - '开发者工具'

---

<strong>注：本文中的所有操作可以随意打开一个网页进行，因为操作都很简单，建议每看一步就实际操作一下，这样还可以发现一些文中没提到的功能。</strong>

>Firebug是Firefox浏览器最好的插件之一，对于网页开发人员来说是一个利器，能够极大地提升工作效率。当你在浏览网页时，它能使你实时的在任何一个页面上编辑，测试css，DOM，Html，javascript。
>Yslow也是Firefox的一个扩展，可以对网站的页面进行分析，并告诉你为了提高网站性能，如何基于某些规则而进行优化。


<strong>
</strong>
<h2>Firebug窗口预览</h2>

<a rel="attachment wp-att-1072" href="http://www.pureweber.com/article/firebug-yslow/firebug_win/"><img class="alignnone size-full wp-image-1072" src="http://www.pureweber.com/wp-content/uploads/2011/09/firebug_win.png" alt="" width="469" height="97" /></a>

运行Firefox浏览器后，按F12键就可启动Firebug。
<ul>
	<li> Console标签：	主要使用javascript命令行操作，显示javascript错误信息。</li>
	<li> HTML标签：	显示HTML源码 CSS标签：		浏览所有已经装入的样式表。</li>
	<li> Script标签： 	显示javascript文件及其所在页面。</li>
	<li> DOM标签： 	显示所有的页面对象和window物体的属性。</li>
	<li>Net标签：		显示本页面涉及的所有下载，以及它们各自花费的时间，各自的HTTP请求头信			息和服务器响应的头信息。</li>
	<li> Yslow标签：	Yslow工具，安装后就会嵌套在Firebug工具当中随时编辑页面</li>
</ul>
<h2>随时编辑页面</h2>

<a rel="attachment wp-att-1074" href="http://www.pureweber.com/article/firebug-yslow/g0ho3r/"><img class="alignnone size-full wp-image-1074" src="http://www.pureweber.com/wp-content/uploads/2011/09/g0Ho3r.png" alt="" width="450" height="276" /></a>

<a rel="attachment wp-att-1074" href="http://www.pureweber.com/article/firebug-yslow/g0ho3r/"></a>
点击窗口上方的“inspect”命令（如图），然后滑动鼠标选择页面中的文本节点，下面的html也会瞬时定位到你选择的节点。你也可以对其进行修改，修改结果会马上反应在页面中。反之亦然，若鼠标停留在下方代码中的某个节点上，页面上也会瞬时显示出该节点的width,border和margin等信息。

<a rel="attachment wp-att-1075" href="http://www.pureweber.com/article/firebug-yslow/html-2/"><img class="alignnone size-full wp-image-1075" src="http://www.pureweber.com/wp-content/uploads/2011/09/html.gif" alt="" width="214" height="164" /></a>

Firebug同时是源码浏览器和编辑器。所有HTML、CSS和Javascript文件中的对象，都可以用单击或双击进行编辑。当你输入完毕，浏览器中的页面立刻会发生相应变化，你可以得到瞬时反馈。

<h2>用Firebug处理CSS</h2>

在CSS标签中，Firebug会自动补全你的输入。在DOM标签中，当你按Tab键时，Firebug会自动补全属性名。
<a rel="attachment wp-att-1076" href="http://www.pureweber.com/article/firebug-yslow/css/"><img class="alignnone size-full wp-image-1076" src="http://www.pureweber.com/wp-content/uploads/2011/09/css.gif" alt="" width="214" height="164" /></a>

<a rel="attachment wp-att-1076" href="http://www.pureweber.com/article/firebug-yslow/css/"></a>
此外，我们还可以利用Firebug来查看某元素的盒模型和其所有的CSS样式。在CSS窗口上方，有一个“布局”按钮，点击后会展示与该元素相关的方块模型，包括padding、margin和border的值。还有一个“计算出的样式”按钮，点击后可以查看该节点的所有CSS样式，在这里我们可以看到我们并没有进行设置而是有浏览器自己默认出来的属性。如下图：

<a rel="attachment wp-att-1077" href="http://www.pureweber.com/article/firebug-yslow/he/"><img class="size-full wp-image-1077 alignnone" src="http://www.pureweber.com/wp-content/uploads/2011/09/he.gif" alt="" width="214" height="164" /></a> <a rel="attachment wp-att-1078" href="http://www.pureweber.com/article/firebug-yslow/screenshot-at-2011-09-14-192252/"><img class="size-full wp-image-1078 alignnone" src="http://www.pureweber.com/wp-content/uploads/2011/09/Screenshot-at-2011-09-14-192252.png" alt="" width="267" height="175" /></a>
<h2>评估下载速度</h2>

Net标签中图形化了页面中所有http请求所用的时间。你可以用这项功能评估javascript文件下载，占用整个页面显示的时间。并且可以查看AJAX信息。

<a rel="attachment wp-att-1079" href="http://www.pureweber.com/article/firebug-yslow/net/"><img class="alignnone size-full wp-image-1079" src="http://www.pureweber.com/wp-content/uploads/2011/09/net.png" alt="" width="413" height="143" /></a>
<h2>Javascript调试</h2>


在script标签中，可以查看整个页面的所有javascript代码，并在代码中设置断点进行debug，左上角有下一步和继续等按钮，窗口右侧是代码中变量和一些DOM的值，他们会随着javascript代码的运行而变化，同时debug时如果代码对页面内容或效果作出改变，页面也会作出即使的响应。这个debug过程和codeblock和netbeans等IDE都非常相似而且操作要简单的多。

<a rel="attachment wp-att-1080" href="http://www.pureweber.com/article/firebug-yslow/script/"><img class="alignnone size-full wp-image-1080" src="http://www.pureweber.com/wp-content/uploads/2011/09/script.png" alt="" width="556" height="213" /></a>
<h2>Firebug控制台使用</h2>


控制台(console)非常强大，也是firebug里最重要的面板，主要作用是显示网页加载过程中产生各类信息。

它能列出javascript调用的所有函数，及其所花的时间。对javascript调试非常有用。而且它还提供了一个console对象，我们可以利用这个对象的各种函数来对javascript代码进行测试。给前端开发带来了极大的方便。下面简单介绍下console对象的使用，在javascript代码中加入下列代码。
{% highlight javascript %}var dog = {};//声明一个对象
dog.name = "大黄";//为dog对象设定一些属性
dog.color = "黄色";
dog.bark = function(){alert("wa kakaka");};

//分组开始——group
console.group("group");
console.log("%o",dog);
console.log("%d年%d月%d日",2011,9,17);
console.info("this is a %s","info");
console.debug("a debug");
console.error("this is a error");
console.warn("this is a warn");
console.dir(dog);
console.groupEnd();
//分组结束

//判断表达式——assert
var result = 0;
console.assert(result == 1);

//计时功能——time
console.time("firsttime");
for(var i = 0;i < 1000;i++)
{
	for(var j = 0;j < 1000;j++){}
}
console.timeEnd("firsttime");

//创建两个函数foo和foo2
function foo(){
	for(var i = 0;i < 1000;i++){
		for(var j = 0;j < 30;j++){ foo2();}
	}
}
function foo2(){
	for(var k = 0;k < 1000;k++){}
}

//性能分析器——profile
console.profile("性能分析器");
foo();
foo2();
console.profileEnd();{% endhighlight %}

运行之后在firebug控制台可看到下面的效果

<a href="http://www.pureweber.com/wp-content/uploads/2011/09/consolelog2.png"><img class="alignnone size-full wp-image-1110" src="http://www.pureweber.com/wp-content/uploads/2011/09/consolelog2.png" alt="" width="579" height="371" /></a>

试想一下在调试代码的时候，为了方便我们可能想让程序在运行过程中就返回给我们一些变量，好让我们查错。以前很多人都喜欢用alert函数弹出个窗口，现在可以完全用console对象来完成这个功能。

不同的函数用来显示不同类型的信息。如log,info,debug,error,warn分别显示的信息类型都不同；这些函数使用起来没什么区别，都和C语言的printf()函数差不多，但只支持字符（%s）、整数（%d或%i）、浮点数（%f）和对象（%o）这四种占位符。唯一的区别就是在控制台当中显示的样式不一样。

下面看下其他的一些函数，如：
<ul>
	<li>console.dir()是用来显示一个对象里所有元素的函数。</li>
	<li>console.assert()，判断某表达式是否正确，如例子中0==1就是一个错误的表达式，所以会产生一个错误信息，如果表达式是对的就什么也不显示。</li>
	<li>console.group()和console.groupEnd()；这两个函数是一对，分组的意思，如果你在调试代码时想要输出看的东西比较多，就可以用这两个函数来进行分组，其group可带上参数，表示该组的名称。</li>
	<li>console.time()和console.timeEnd()；该函数使用来计算时间的，它会为开发者显示出在这两个函数中间的代码所运行的时间。</li>
	<li>console.profile()和console.profileEnd()；该函数被叫做性能分析器，看运行出来的效果就可知道，它能对夹在两函数中间的函数进行测试，包括被调用次数和运行时间等等。该功能和控制台界面中的概况(profile)按钮的功能是一样的。</li>
</ul>
控制台和console对象的使用比较复杂，还有用来显示xml代码的dirxml()函数和跟踪函数trace()等等。可参考下面的链接进行详细的学习。
链接：<a href="http://www.ruanyifeng.com/blog/2011/03/firebug_console_tutorial.html">http://www.ruanyifeng.com/blog/2011/03/firebug_console_tutorial.html</a>
上面的代码在文章尾部有相关<a href="http://www.pureweber.com/wp-content/uploads/2011/09/firebugyslow.zip">下载</a>，可下载下来实践一下。


<h2>Yslow分析网页性能</h2>


Yslow的功能在文章的开始处已经说明。它有四个试图，每个试图都是对整个页面在不同方面的信息显示。
<h3>组件试图</h3>
该试图中列出了整个页面所加载的所有文件，包括html,css和javascript等。并列出每个文件的详细信息和加载每个文件时的http请求信息等。

<a rel="attachment wp-att-1082" href="http://www.pureweber.com/article/firebug-yslow/a/"><img class="alignnone size-full wp-image-1082" src="http://www.pureweber.com/wp-content/uploads/2011/09/a.png" alt="" width="640" height="238" /></a>
<h3>统计信息试图</h3>
该试图会显示整个页面加载的所有文件的个数和各类文件的大小比例。

<a rel="attachment wp-att-1083" href="http://www.pureweber.com/article/firebug-yslow/b/"><img class="alignnone size-full wp-image-1083" src="http://www.pureweber.com/wp-content/uploads/2011/09/b.png" alt="" width="640" height="257" /></a>
<h3>等级试图</h3>
这个试图是YSlow最让人关注的了，它会根据不同中规则对该页面进行评测并给出相应的分数和等级划分，对做的不好的地方还会给出优化的建议。关于每个规则的说明和优化方法可参考本站的另一篇文章<a href="http://www.pureweber.com/article/high-performance-web-sites/">《读书分享：高性能网站建设指南》</a>。

<a rel="attachment wp-att-1084" href="http://www.pureweber.com/article/firebug-yslow/c/"><img class="alignnone size-full wp-image-1084" src="http://www.pureweber.com/wp-content/uploads/2011/09/c.png" alt="" width="640" height="444" /></a>
<h3>工具试图</h3>
该试图里提供了一些工具，例如对代码进行压缩等等。

<strong>示例代码：<a href="http://www.pureweber.com/wp-content/uploads/2011/09/firebugyslow.zip">下载</a></strong>
