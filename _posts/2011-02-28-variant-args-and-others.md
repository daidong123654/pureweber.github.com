---
layout: post
title: 'PHP中的可变参数个数的函数及其他'
author: 田大龙
description: 
tags:
  - php
  - 可变个数参数
  - 模板
  - 正则表达式

---

##可变参数个数的函数

使用 fun_get_args() 和 call_user_func_array()

{% highlight php %}
<?php
function user_func()
{
    $arg = func_get_args();
    call_user_func_array("sprintf", $arg);
}
?>
{% endhighlight %}

func_get_args函数的功能是把所有参数存到$arg变量中

call_user_func_array函数的作用是将 $arg 中所有接收到的参数传递给指定的函数，这里是sprintf。

使用 func_get_args() 即可定义你自己的具有可变参数个数的函数了。 而 call_user_func_array() 函数可以很方便的用来调用具有可变参数个数的函数。(有点拗口啊)

例如：

{% highlight php %}
<?php
function oot()
{
    $pa = func_get_args();
    $sql = call_user_func_array("sprintf", $pa);
    return $sql;
}

$a = 10;
$b = fingers;

echo oot("I have %d %s", $a, $b);
?>
{% endhighlight %}

输出的就是 : I have 10 fingers.

##浏览器缩进问题

问：为什么在div里的ul嵌套无法正常缩进？

不同浏览器对HTML各标签的样式是有默认值设定的，虽然作为开发者的我们无法控制这些默认值，但可以通过CSS Reset来重置设定，比较常见的就是

{% highlight css %}
* { margin:0; padding:0 }
{% endhighlight %}

还有许多其他更为复杂的 CSS Reset 方案，这些CSS Reset 方案的一个共同目的就是：将不同浏览器的默认设置重置一下，从而保证所有浏览器下，样式能够全部统一。

##模板技术

使用模板引擎可以使业务逻辑与显示逻辑分开，可以简单的理解模板为“PHP与HTML代码分离的方法”

让程序（PHP）与显示（HTML）分离可以使代码更清晰易懂，职责的分离使得维护变得更容易。更重要的是这样的设计可以让不懂PHP的前台美工也能修改页面。它能让程序开发者专注于资料的控制或是功能的达成；而网页设计师则可专注于网页排版，让网页看起来更具有专业感。因此，模化引擎很适合公司的Web开发团队使用，使每个人都能发挥其专长。

##正则表达式

正则表达式（Regular Expression>，缩写为regexp，regex或regxp)，又称正规表达式、正规表示式或常规表达式或正规化表示法或正规表示法，是指一个用来描述或者匹配一系列符合某个句法规则的字符串的单个字符串。在很多文本编辑器或其他工具里，正则表达式通常被用来检索和/或替换那些符合某个模式的文本内容，可以很容易的选出具有某一类特点的式子。许多程序设计语言都支持利用正则表达式进行字符串操作。 
