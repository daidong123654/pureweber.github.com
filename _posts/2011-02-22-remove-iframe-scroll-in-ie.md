---
layout: post
title: IE中如何去掉IFrame的边框和滚动条
description: 在IE浏览器中使用iFrame标签时，设定边框和滚动条的显示与否与标准CSS定义的方式不同，本文说明如何在IE中去除iframe标签的边框和滚动条。
author: 段志岩
github: dzy0451
tags:
  - ie
  - iframe
  - '滚动条'
  - '边框'

---

## 问题描述

IE中使用IFrame时，无法用CSS属性来去掉IFrame的边框和滚动条。

{% highlight cpp %}
<iframe  style="border:none;overflow:hidden" src="http://sina.com.cn"></iframe>
{% endhighlight %}

## 解决方法

使用HTML中IFrame标签的`frameborder`和`scrolling`属性来控制，将`frameborder`属性的值设置为`0`，`scrolling`属性的值设置为`no`即可。

{% highlight cpp %}
<iframe  frameborder="0" scrolling="no" src="http://sina.com.cn"></iframe>
{% endhighlight %}
