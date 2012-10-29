---
layout: post
title: jQuery性能优化
tags:
  - javascript
  - jquery
  - '%e4%bc%98%e5%8c%96'
  - '%e6%95%88%e7%8e%87'

---

这里总结了几篇博文的内容，方便日后查阅。
<h3>1.总是从ID选择器开始继承</h3>
JQuery中最快的筛选器是ID筛选器($('#someid'))。这是因为它直接和JavaScript的getElementById()方法对应。
<h3>2. 在class前使用tag</h3>
第二快的选择器是tag选择器($('head')). 因为它和JavaScript的getElementsByTagName() 方法对应。例如：$('div.someclass')。

综合第一点和第二点:

如果需要$('.someclass')，应该使用$('#someid &gt; tag.someclass')来缩小DOM Tree的搜索范围
#someid 前面不要用tag来修饰。写成$('div#someid')会降低性能，因为JS会遍历所有的div元素来查找id为'someid'的哪一个节点:
#someid也不需要由#otherid来修饰。写成$('#otherid #someid')也会降低性能。
<h3>3.缓存JQuery对象</h3>
要养成将jquery对象缓存进变量的习惯。

永远不要这样做：

[coolcode lang="javascript"]

$('#traffic_light input.on').bind('click', function(){...});
$('#traffic_light input.on').css('border', '3px dashed yellow');
$('#traffic_light input.on').css('background-color', 'orange');
$('#traffic_light input.on').fadeIn('slow');

[/coolcode]

最好先将对象缓存进一个变量然后再操作:

[coolcode lang="javascript"]

var $active_light = $('#traffic_light input.on');
$active_light.bind('click', function(){...});
$active_light.css('border', '3px dashed yellow');
$active_light.css('background-color', 'orange');
$active_light.fadeIn('slow');

[/coolcode]

永远不要让相同的选择器在你的代码里出现多次。
<h3>4.用for替代each</h3>
原生函数总是比辅助组件更快。
<h3>5. 合理使用链式操作</h3>
可以减少对DOM Tree的访问以及代码量。
<h3>6.使用子查询</h3>
使用children(), find(), filter()来进行子查询。
<h3>7.对直接的DOM操作进行限制</h3>
尽量减少对DOM Tree的直接操作。

几种可用的方法：
<ol>
	<li>先将元素从document中删除，完成修改后再把元素放回原来的位置</li>
	<li>将元素的display设置为”none”，完成修改后再把display修改为原来的值</li>
	<li>在插入之前将多个元素包裹进一个单独的父级节点会更快</li>
	<li>尽可能少的修改元素style上的属性</li>
	<li>尽量通过修改className来修改样式</li>
</ol>
<h3>8. 事件冒泡的利用</h3>
除非在特殊情况下, 否则每一个js事件(例如:click, mouseover, 等.)都会冒泡到父级节点. 当我们需要给多个元素调用同个函数时这点会很有用。

代替这种效率很差的多元素事件监听的方法就是, 你只需向它们的父节点绑定一次, 并且可以计算出哪个节点触发了事件。

例如, 我们要为一个拥有很多输入框的表单绑定这样的行为: 当输入框被选中时为它添加一个class。

像这样绑定事件是低效的:

[coolcode lang="javascript"]

$('#entryform input).bind('focus', function(){
$(this).addClass('selected');
}).bind('blur', function(){
$(this).removeClass('selected');
});

[/coolcode]

我们需要在父级监听获取焦点和失去焦点的事件:

[coolcode lang="javascript"]

$('#entryform).bind('focus', function(e){
var cell = $(e.target);  // e.target 保存事件的触发者
cell.addClass('selected');
}).bind('blur', function(e){
var cell = $(e.target);
cell.removeClass('selected');
});

[/coolcode]

父级元素扮演了一个调度员的角色, 它可以基于目标元素绑定事件. 如果你发现你给很多元素绑定了同一个事件监听, 那么你肯定哪里做错了。
<h3>9. 将某些函数推迟到 $(window).load执行</h3>
尽管$(document).ready确实很有用, 它可以在页面渲染时,其它元素还没下载完成就执行. 如果你发现你的页面一直是载入中的状态, 很有可能就是$(document).ready函数引起的.

你可以通过将jquery函数绑定到$(window).load 事件的方法来减少页面载入时的cpu使用率. 它会在所有的html(包括&lt;iframe&gt;)被下载完成后执行.
<h3>10. 合并、最小化脚本</h3>
脚本都是排队一一加载的，所以要尽量减少JS文件的个数，以及利用压缩工具压缩JS文件。

原文地址：http://www.fancycedar.info/2010/02/jquery-tuning/
