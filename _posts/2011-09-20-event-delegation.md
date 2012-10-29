---
layout: post
title: JavaScript事件冒泡和事件委托
tags:
  - event-bubble
  - event-delegation
  - javascript
  - '%e4%ba%8b%e4%bb%b6%e5%86%92%e6%b3%a1'
  - '%e4%ba%8b%e4%bb%b6%e5%a7%94%e6%89%98'

---

<a href="http://www.pureweber.com/wp-content/uploads/2011/09/bubbles.jpg"><img src="http://www.pureweber.com/wp-content/uploads/2011/09/bubbles-225x300.jpg" alt="" title="bubbles" width="225" height="300" class="alignright size-medium wp-image-1172" /></a>接触JavaScript不久，学的东西也不是特别多。小雨就是习惯把平时学到的东西拿出来分享。一方面加强自己的印象，一方面可以让自己的经验为他人答疑解惑。我们知道JavaScript可以监控页面上元素的各种事件，常用的事件有很多，例如点击，鼠标移入、移出，元素改变等等。这次主要说一下事件冒泡及其一个比较酷的应用，事件委托。不做特殊说明，以下都在jQuery框架内执行。
<h3>事件冒泡</h3>
什么是“事件冒泡”呢？假设这里有一杯水，水被用某种神奇的方式分成不同颜色的几层。这时，从最底层冒出了一个气泡，气泡会一层一层地上升，直到最顶层。而你不管在水的哪一层观察都可以看到并捕捉到这个气泡。好了，把“水”改成“DOM”，把“气泡”改成“事件”。这就是“事件冒泡”。

为了可以直观地观察到这一现象，我写了一个<a href="http://www.pureweber.com/works/demos/js-event-delegation/event-bubble.html">小程序</a>。这个页面中一共有4个嵌套的正方形。最大的那个在最顶层，最小的那个在最底层。我为每一层都单独绑定了一个点击事件，当这一层被点击时，会为这层涂色。试试看，点击最小的正方形会发生什么？点击其他的又会发生什么呢？ (<a href="http://www.pureweber.com/works/demos/js-event-delegation/event-bubble.html">点击这里查看demo</a>)

<h4>CSS</h4>
<coolcode lang="css">
<style>
		div{background-color:#fff;}
		#d1{width:400px;height:400px;border:1px solid #000;margin:50px 50px;}
		#d2{width:300px;height:300px;border:1px solid #000;margin:50px 50px;}
		#d3{width:200px;height:200px;border:1px solid #000;margin:50px 50px;}
		#d4{width:100px;height:100px;border:1px solid #000;margin:50px 50px;}
</style>
</coolcode>

<h4>HTML</h4>
<coolcode lang="html">
<div class="www-7lemon-net-d1">
	<div class="www-7lemon-net-d1">
		<div class="www-7lemon-net-d1">
			<div class="www-7lemon-net-d1"></div>
		</div>
	</div>
</div>
<button>重置</button>
</coolcode>

<h4>Javascript</h4>
<coolcode lang="javascript">
	jQuery('#www-7lemon-net-d14').click(function(){jQuery(this).css('background-color', 'yellow')});
	jQuery('#www-7lemon-net-d13').click(function(){jQuery(this).css('background-color', 'green')});
	jQuery('#www-7lemon-net-d12').click(function(){jQuery(this).css('background-color', 'blue')});
	jQuery('#www-7lemon-net-d11').click(function(){jQuery(this).css('background-color', 'red')});
	jQuery('#www-7lemon-net-reset1').click(function(){jQuery('.www-7lemon-net-d1').css('background-color', '#fff')});
</coolcode>

没错，点击最小的那个，外面所有的都会被上色。你会发现，点击里层的正方形，外层所有的正方形都会被上色。因为它们也都捕捉到了点击事件。看，他们抓到“气泡”了！

<h3>事件委托</h3>

上一节的例子我们做一点小小的修改。气泡带上了某种信息，会告诉其经过的每一层自己是在哪一层产生的。JavaScript的事件确实会带着这个属性。当程序捕获一个事件的时候，它会知道这个事件来自于页面上哪个元素。修改上面的程序，使用事件委托来处理点击事件。当最顶层捕获点击事件时，查看事件来源于哪一层，然后只将那一层涂色。再次点击每一层，查看实际效果。只有当前点击的正方形变色了，其他的都毫无反应。(<a href="http://www.pureweber.com/works/demos/js-event-delegation/event-delegate.html">点击这里查看demo</a>)

<coolcode lang="javascript">
	jQuery('#www-7lemon-net-d21').click(function(e){
		var t = jQuery(e.target);
		var id = t.attr('id');
		if (id==='www-7lemon-net-d24'){
			t.css('background-color', 'yellow');
		} else if (id==='www-7lemon-net-d23') {
			t.css('background-color', 'green');
		} else if (id==='www-7lemon-net-d22') {
			t.css('background-color', 'blue');
		} else {
			t.css('background-color', 'red');
		}
	});
</coolcode>

当然，如果你有这样嵌套的页面元素，使用了事件委托，委托到了最顶层，这时需要注意：如果其中某个元素，你不希望它的事件冒泡，那么可以使用某种方式阻止事件的冒泡。在jQuery框架中，可以使用stopPropagation()方法来实现而不必关心浏览器兼容性。

<coolcode lang="javascript">
$('#bind').click(function(){
	if ($(this).attr('checked')) {
		$('#d4').bind('click', function(e){
			e.stopPropagation();
			alert('冒泡被阻止，这块将不会改变颜色');
		});
	} else {
		$('#d4').unbind('click');
	}
});
</coolcode>

重置后选中“阻止最小的方块的事件冒泡”，再点击最小的方块，看是否变色。显然是不会变色，阻止了冒泡，父层将无法接收到点击事件。

<h3>注意事项</h3>

事件委托是事件冒泡的一个应用，可以减少绑定元素的个数，也不必担心子节点被替换后可能需要进行重新的事件绑定。因为事件的捕获和后续代码的执行已经完全委托给了其父节点。如果页面中含有大量元素需要绑定事件，这样做会减少事件绑定数量，为浏览器减负，无疑会提高页面性能。

但也有些需要注意的。如果用于捕获事件的节点会在某些情况下return false，而你的一个点击事件未委托给父节点，那么，你可能需要阻止这个节点的事件冒泡来达到正确的目的。例如：我在一个div里面有一些按钮和其他元素。利用事件委托来处理这些按钮的点击，如果不是按钮则return false。这时，错误就出现了。如果其他元素中含有链接，那么链接的点击事件也会被委托给div。然而点击链接，会没有任何反应。解决办法一是在委托的代码中对链接进行处理，二是阻止链接的事件冒泡。
<h3>源代码</h3>
<p><a href="http://www.pureweber.com/works/demos/js-event-delegation/js-event-delegation.tar.gz" target="_blank">源代码打包下载</a></p>
