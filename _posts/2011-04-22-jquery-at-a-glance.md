---
layout: post
title: '浅谈jQuery'
tags:
  - ajax
  - jquery
  - '%e4%ba%8b%e4%bb%b6%e7%bb%91%e5%ae%9a'
  - '%e5%88%86%e4%ba%ab%e4%bc%9a'
  - '%e7%ae%80%e4%bb%8b'

---

<a href="http://www.pureweber.com/wp-content/uploads/2011/04/jquery_icon.png"><img style="clear:both;" src="http://www.pureweber.com/wp-content/uploads/2011/04/jquery_icon.png" alt="" title="jquery_icon" width="256" height="256" class="alignright size-full wp-image-670" /></a>第一次分享会开始，第一次分享的是表面上的东西。这里所说的表面上的东西并不是指十分浅显的东西，而是直接与用户交互的那一部分。我们重点来说一说JavaScript的一个比较流行的库——jQuery。

JavaScript和HTML还有CSS一样，都是下载到用户本地，由用户的浏览器进行解释和执行的。

<h3>1、jQuery是什么</h3>

刚才已经说过了，它是一个JavaScript的库。这些库被用来简化JavaScript的开发，利用这些库，可以降低开发人员JavaScript的技术门槛，使用一些简单的方法实现高兼容性，高移植性的功能。比如对于初学者来说，难以写出同时兼容IE，Firefox，Chrome，Opera的JavaScript代码来，因为需要考虑的方面比较多。但是利用第三方库，这些兼容性问题就可以忽略掉了。说着说着感觉有点像Java的样子。

第三方库是怎么个作用呢？打个比方吧。比如说你想吃饺子，就得活面，做饺子馅，然后包饺子，再煮饺子。经过了这么多过程才终于可以吃了。库呢，就是把活面，做馅，包饺子这些过程全都交给一个包饺子机去做。你只要把原料放到里面，一按按钮，饺子就出来了。生活一下子就简单了！

除了jQuery，还有其他一些比较优秀的JavaScript库。例如Prototype，YUI，MooTools等等。其中Prototype是最早成型的JavaScript库之一，因为成型年代比较早，对面向对象的编程思想把握不是很到位，所以结构比较松散，现在似乎在慢慢改进，仍旧有一些网站使用这个库。

YUI是由Yahoo公司开发的JavaScript工具集，封装了一系列比较丰富的功能。现在和大龙在做的Moodle开发中，其中的JavaScript库使用的便是YUI。看过YUI2的部分文档，YUI2虽然封装了很多工具，但是使用上还是不够方便，有很多类似JavaScript的原始方法。YUI3作出了很大改进，向着简单易用的方向，改善了许多。

jQuery如此流行的原因就是因为它简单易用，容易上手。拥有轻量级的库，强大的选择器，出色的DOM操作，各种事件处理，兼容性解决方案等等特性。

jQuery强调的理念是写得少，做得多。虚的东西不多说了，咱们主要是分享经验，不是给jQuery做广告。

<h3>2、代码示例</h3>

<a href="http://www.pureweber.com/works/demos/jquery-kick-off/basic.html" target="_blank">点我穿越</a>

一般来说，一个button的点击不会出现任何效果。但是可以利用JavaScript来控制它的点击效果。比如，我点这个按钮，浏览器就显示出个OK。再点一下又出来个OK。这都是浏览器解释出来的，并没有写到html文档中。我再刷新一下这个页面，这些OK就消失了。

$()，美元符号，这个是jQuery的工厂函数。能做选择器来用，也能用来创建节点。示例代码中的$("button")就是选中下面文档里&lt;button&gt;&lt;/button&gt;这个节点。同理，$("#box")是选中ID为box的节点。这里括号里面的选择方法和CSS是一样的。Click还有append就是jQuery的一系列方法中的两个。前者是监测点击事件，后者是用来向HTML中添加字符串或者各种元素。

这里说到了节点，为什么说成是节点，我们往下看。

<h3>3、jQuery对象 VS DOM对象</h3>

初次接触jQuery，经常分不清jQuery对象和DOM对象。冷不丁写出来一段代码，很有可能就不知道用什么方法来进行下一步。对用惯了JavaScript直接编码的人来说，这种障碍可能更大一些。初学者直接跨过JavaScript而是用jQuery的话，也需要对这两个对象深入理解才能进行更深入的学习。

什么是DOM？英文全称是Document Object Model，即文档对象模型。每一份DOM都可以表示成一棵树。树中的每个节点都是DOM元素节点。通过JavaScript方法获得的DOM元素就是DOM对象。而通过jQuery选择器取得的DOM元素，是对DOM对象进行的一个包装，此时得到的就是jQuery对象。对于jQuery对象，就可以使用相应的jQuery方法。

DOM对象，jQuery对象，我想了很久，想到一个比较形象的比喻可以解释他们的关系。想在用户交互界面实现一个功能，可以使用JavaScript方法操作DOM，也可以使用jQuery方法来操作DOM实现同样的功能。这就像是煮饭。有米有水，一个人选择生火用大锅煮饭，另一个人选择用电饭锅来煮。这两个人呢相当于不同的选择器；使用的灶台大铁锅，或者是电饭锅就是不同的封装；灶台点火，电饭锅插电，这就是两种不同方法。当然最后的结果都是生米煮成熟饭。而灶台不能插电，电饭锅不能点火，两种不同的对象不能使用此对象不存在的方法。不知道说清楚了没有，大家还要自己主动去研究研究理解理解。

分清DOM对象和jQuery对象对以后的使用会有很大帮助。DOM对象和jQuery对象之间还可以进行转换，这里就不详细介绍了，很简单。

<h3>4、DOM操作</h3>

DOM操作是JavaScript控制里最常用的操作之一。做前端，那必然会对页面显示的样式做各种各样的控制。这就离不开DOM操作。我将示例代码1做了一点点小修改，于是就诞生了示例代码2。我当时学jQuery的时候基本就是这样一点点研究这东西怎么用的。其实特别容易上手，有一些地方跟Java的语法比较像。

示例代码1里面已经提到了DOM的选择器以及向文档中插入文本。插入节点也是同样的道理，只要把文本换成HTML代码就是了。插入这个节点以后呢，DOM那棵树里面就多了一个节点。

看代码示例2，<a href="http://www.pureweber.com/works/demos/jquery-kick-off/dom.html" target="_blank">点我穿越</a>。这段代码比示例代码1多了一个变量，用于标记一下是第几次点击。JavaScript中的变量是用var来声明的，和PHP中的变量类似，也是弱类型的，随着使用，可以随时将它的类型改变成需要的类型。然后，我每点击一次 "It works!"，就向id为box的盒中的ul节点下面添加li节点。这就是基本的向DOM中添加节点的方法。很简单，和添加字符串一样。Append方法和appendTo方法，这俩挺有意思。这个我就不说了，你们如果有兴趣研究jQuery的话，查文档的时候就能看到，然后实际编码实现一下就知道怎么回事了。

既然有创建和添加节点，那肯定有删除节点对吧。删除一个节点是使用remove方法。$("#box").remove();只要执行这一句，ID为box的节点就被删除了。我在给Cybery Reader添加Ajax效果的时候我就想，用户点击一个订阅源，我要把中间的内容清空，然后显示这个订阅源下的文章。然后呢，我就用了remove()方法。结果发现，整个盒都被删了。难道我还得新建一个盒？然后我就把删掉的盒子又用前面创建节点的方法添加回去了……再把订阅源中的文章添加到这个节点下。想想这种方法挺对的是吧？

我就想，我这办法也太闹心了吧，就没有个简单点的办法？后来我翻了一下方法列表，给找到了。清空节点中的内容可以使用empty方法，empty方法只清除当前选中元素的子元素。我们试一下，在代码示例2里面，给$("#box ul")对象添加一个empty()方法是什么效果。注意，jQuery支持方法的连接操作。用“.”将一个jQuery对象要执行的方法依次连接起来，执行的时候浏览器就会按照方法连接的顺序依次执行。

DOM操作中还有属性操作，样式操作以及文本操作。以<a href="http://www.pureweber.com/cybery-reader/" target="_blank">Cybery Reader</a>的<a href="http://www.pureweber.com/cybery-reader/static/actions.js" target="_blank">actions.js</a>中的代码为例说明一下属性操作的方法attr()。Attr()接收两个参数，第一个参数是属性名称，第二个参数是属性的值，这两个参数都是字符串。如果只有一个参数，返回值是DOM元素中这个属性的值。如果再加上第二个参数，则把第一个参数指定的属性的值设置为第二个参数的值。例如actions.js第100行这段代码里面。首先取src属性的值，判断一下它是什么，然后108行和116行就是对这个属性进行修改。

样式操作、设置和获取HTML、文本的示例可以参考jQuery手册，不外乎使用几个方法，可能对一些值进行转换，也是比较简单的内容。不再举例了。

<h3>5、事件绑定</h3>

看代码示例3，<a href="http://www.pureweber.com/works/demos/jquery-kick-off/bind1.html" target="_blank">点我穿越</a>。一般的理解，我点击“伤不起有木有！”以后呢，这个列表中会再添加一个“伤不起”的项。这都没问题。我点新添加的“伤不起”，看看会不会再向列表中添加一个“伤不起”呢？

啊哦，一点反应都没有。这是为什么呢？因为新添加的节点对于浏览器来说是一个全新的对象，而脚本中并没有给这个新对象绑定任何动作。就好象我新买个电饭锅放家里，但是不插电，那它就永远无法工作。

给这段代码加一点小改进，就可以让新建元素工作了。看代码示例4，<a href="http://www.pureweber.com/works/demos/jquery-kick-off/bind2.html" target="_blank">点我穿越</a>，用count变量记录添加节点的顺序，为每个节点制定一个ID，然后新建节点以后用选择器选取此ID的节点，为它绑定一个click事件。这样就可以工作了。看看效果。我再点击“伤不起”的时候，这个伤不起的后面就出现了“有木有！”。有木有！有木有！

在一个jQuery对象后面加上.click这样就给这个对象绑定了click事件。还可以显示地使用bind("click", function(){…})来绑定click事件。如果想要取消绑定，可以使用unbind方法。

<h3>6、Ajax</h3>

Ajax全称Asynchronous JavaScript and XML，即异步JavaScript和XML。具体的技术细节这里就不研究了，直接说说jQuery中Ajax的使用。第一次作业里有的同学使用的iframe方法在当前页面载入其他页面的内容。有兴趣可以换成Ajax方法试试。

最简单的是load()方法了，这个方法有3个参数，url, data, callback。其中后两个参数都是可选参数。url参数是请求HTML页面的URL地址，data是发送至服务器的数据，callback是请求完成时的回调函数，无论请求成功或失败都会执行这个函数。

看下一个代码示例，<a href="http://www.pureweber.com/works/demos/jquery-kick-off/load.html" target="_blank">点我穿越</a>。看这段代码能不能大致了解一下我要做什么？点击"It works!"，然后向服务器发出GET请求，获取test.html页面。把这个页面中的内容添加到box中。

Load()方法通常用来从Web服务器上获取静态的数据文件，但是在实际项目中，总是需要给服务器传递一些参数。或许只是悄悄地上传一些数据，并不涉及到DOM操作。这时就可以使用$.post()和$.get()方法了。

看一下<a href="http://www.pureweber.com/cybery-reader/" target="_blank">Cybery Reader</a>中的Feed列表。这里面每一项都是一个链接，理论上我点击这个链接页面会跳转到链接制定的页面。但是我点一下，它为什么没有跳转呢？在click事件的function函数的最后打一行return false，这样就阻止了页面的跳转。并且使用POST方式向服务器发送了这个链接。

$.get()方法使用GET方法来进行异步请求，$.post()方法使用POST方式来进行异步请求。参数有url，data，callback，type。比load()方法多了一个type，表示服务器端返回内容的格式，包括XML，HTML，Json等。使用这两种方法能够显示地表现出用何种方式来进行异步请求。以actions.js中的代码来解释$.post方法的使用。40行使用Ajax动态添加评论。请求的页面是/comment/，发送的数据是comment。试着发送一条评论，看看Firebug上监视到的结果，结合我们这个callback function就知道这里是如何工作的了。$.get()方法与$.post()方法使用上完全相同。

Ajax就说到这里不再深入了。有兴趣的话，可以继续研究如何使用XML或者JSON来传送数据。

<h3>7、没讲到的东西</h3>

动画没有讲，这部分我用到的不是很多，感觉和事件处理也十分相似，看看jQuery文档就能知道个大概。

表单、表格的操作没有说。这个和DOM的属性操作很像。

XML、JSON会在Ajax中有涉及。XML就是另一种文档格式了，十分强大，在很多地方都用得上。已经超出今天的范围了，有兴趣的到图书馆借本书看看。或者查在线文档。JSON这个用得比较多，也是用来传递大块数据的。比如你的PHP脚本想要和JS脚本进行数组的传递，用JSON就很方便。

各种细节问题。单纯分享经验嘛，细节问题就不讨论了，不然就变成讲课了。其实说着说着已经变成jQuery快速入门了。快餐一般都没营养，想吃点好的，多看书多研究吧！

<h3>8、示例代码目录</h3>

<ul>
	<li><a href="http://www.pureweber.com/works/demos/jquery-kick-off/basic.html" target="_blank">基本示例</a></li>
	<li><a href="http://www.pureweber.com/works/demos/jquery-kick-off/dom.html" target="_blank">DOM操作</a></li>
	<li><a href="http://www.pureweber.com/works/demos/jquery-kick-off/bind1.html" target="_blank">事件绑定1</a></li>
	<li><a href="http://www.pureweber.com/works/demos/jquery-kick-off/bind2.html" target="_blank">事件绑定2</a></li>
	<li><a href="http://www.pureweber.com/works/demos/jquery-kick-off/load.html" target="_blank">Ajax load方法</a></li>
	<li><a href="http://www.pureweber.com/works/demos/jquery-kick-off/test.html" target="_blank">test.html</a></li>
</ul>

