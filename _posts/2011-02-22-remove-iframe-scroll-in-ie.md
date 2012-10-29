---
layout: post
title: IE中如何去掉IFrame的边框和滚动条
tags:
  - ie
  - iframe
  - '%e6%bb%9a%e5%8a%a8%e6%9d%a1'
  - '%e8%be%b9%e6%a1%86'

---

<strong>问题描述</strong>

IE中使用IFrame时，无法用CSS属性来去掉IFrame的边框和滚动条。

<em>HTML代码</em>

[coolcode lang="html"]
<iframe  style="border:none;overflow:hidden" src="http://sina.com.cn"></iframe>
[/coolcode]

<em>效果</em>

<iframe  style="border:none;overflow:hidden" src="http://sina.com.cn"></iframe>

<strong>解决方法</strong>

使用HTML中IFrame标签的<span style="color: #3366ff;">frameborder</span>和<span style="color: #3366ff;">scrolling</span>属性来控制，将<span style="color: #3366ff;">frameborder</span>属性的值设置为<span style="color: #ff0000;">0</span>，<span style="color: #3366ff;">scrolling</span>属性的值设置为<span style="color: #ff0000;">no</span>即可。

<em>HTML代码</em>

[coolcode lang="html"]
<iframe  frameborder="0" scrolling="no" src="http://sina.com.cn"></iframe>
[/coolcode]

<em>效果</em>

<iframe  frameborder="0" scrolling="no" src="http://sina.com.cn"></iframe>
