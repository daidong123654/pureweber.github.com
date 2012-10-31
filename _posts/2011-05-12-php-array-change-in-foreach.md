---
layout: post
title: PHP数组：遍历过程中的改值操作
description: 在PHP中使用foreach对数组进行遍历时，如果改变数组元素的值，常会遇到改变无效/丢失的问题。实际上，PHP的foreach操作的是指定数组的一个拷贝，因此，在这个拷贝上的修改都将丢失，所以，在使用foreach进行数组遍历和修改时，需要注意修改原数组，而不是拷贝。本文给出具体的实例，供大家参考。
author: 付建宇
github: 7lemon
tags:
  - array
  - foreach
  - php
  - '%e4%bf%ae%e6%94%b9'
  - '%e9%81%8d%e5%8e%86'

---

##问题描述
前段时间写代码，需要在遍历数组的时候对数组中某些元素做修改。如果数组元素的键是顺序的整数，很简单，只要用for循环就可以了。如果是关联数组呢？首先想到的是foreach遍历数组。但是foreach虽然用来输出感觉很爽，但是修改数组内元素的时候，还多少是有那么点麻烦。和老段讨论后，老段提出了一种修改值的方法，我自己也想了几个办法。下面具体说一下：


##引用操作符&amp;
看下面这段代码中的$array数组，在foreach循环时对$value使用引用操作符，这样在循环中修改$value的值的时候，便将$array中对应的元素值修改了。

{% highlight php %}
<?php
$array = array("A"=>1, "B"=>1, "C"=>1, "D"=>1);
foreach($array as &amp;$value)
    $value = 2;
print_r($array);
?>
{% endhighlight %}

上段代码的输出如下：

	Array ( [A] => 2 [B] => 2 [C] => 2 [D] => 2 ) 

可以看到，$array中各个键对应的值都被修改成了2。看来这种方法确实奏效。


##利用键值操作数组的元素
有的时候，数组中表示的可能是一些互相关联的元素，如果遇到了这些相互关联的元素中的一个，就将其他元素做一个标记的话，上面的引用肯定就不管用了。这时候修改这些关联元素的时候，就要使用其对应的键值了。先试试看管用不：
{% highlight php %}
<?php
$array = array("A"=>1, "B"=>1, "C"=>1, "D"=>1);
foreach($array as $key => $value){
	if($key == "B"){
		$array["A"] = "CHANGE";
		$array["D"] = "CHANGE";
		print_r($array);
		echo '<br />';
	}

	if($value === "CHANGE")
		echo $value.'<br />';
}
print_r($array);
?>
{% endhighlight %}

别着急看输出，我们想象中的应该是什么样呢？打印修改后的数组，打印一个“CHANGE”，再打印一遍修改后的数组。对吗？来看一下输出吧！

	Array ( [A] => CHANGE [B] => 1 [C] => 1 [D] => CHANGE )
	Array ( [A] => CHANGE [B] => 1 [C] => 1 [D] => CHANGE ) 

咦？怎么个情况？我们的CHANGE哪去了？

按照我们的想法，既然$array已经改变了，那么当遍历到键值为“D”的元素时，应当输出它的新值“CHANGE”才对！可是事实并不是我们想的那样。PHP在这里做了什么手脚呢？把上面的代码稍微修改一下。既然打印数组的时候，“D”=>CHANGE没错，那我们修改第二个if语句的判断条件：

{% highlight php %}
<?php
$array = array("A"=>1, "B"=>1, "C"=>1, "D"=>1);
foreach($array as $key => $value){
	if($key == "B"){
		$array["A"] = "CHANGE";
		$array["D"] = "CHANGE";
		print_r($array);
		echo '<br />';
	}
	
	if($array[$key] === "CHANGE")
		echo $value.'<br />';
}
print_r($array);
?>
{% endhighlight %}

猜猜它会输出什么？$value肯定不会等于“CHANGE”啦！难道等于1么？

	Array ( [A] => CHANGE [B] => 1 [C] => 1 [D] => CHANGE )
	1
	Array ( [A] => CHANGE [B] => 1 [C] => 1 [D] => CHANGE ) 

那么，它确实就是1了。

这究竟是神马原因呢？翻到<a href="http://us.php.net/manual/zh/control-structures.foreach.php" target="_blank">PHP文档的foreach那页</a>，恍然：

> Note:
> 除非数组是被引用，foreach 所操作的是指定数组的一个拷贝，而不是该数组本身。foreach对数组指针有些副作用。除非对其重置，在 foreach 循环中或循环后都不要依赖数组指针的值。 

原来foreach所操作的是指定数组的一个拷贝。怪不得，取$value不管用了呢！理解到这里，上面的问题就解决了。只要在foreach中，直接按照键取$array中的元素进行各种判断赋值操作就可以了。

##结语

好好看文档。

好好看文档。

好好看文档。
