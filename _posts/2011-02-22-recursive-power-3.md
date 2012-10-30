---
layout: post
title: 递归的力量（三）：更多例子
description: 以汉诺塔问题为例，说明递归的使用方法，并分析该汉诺塔问题递归实现的时间复杂度。
author: 段志岩
github: dzy0451
tags:
 - '递归'
 - '汉诺塔问题'
latex: true
---

昨天说了一些递归的简单应用，今天再说一点其他的应用吧。

不得不提的一个经典的问题是汉诺塔问题。问题是这样的：
<blockquote>有三个柱子，其中的一个上面套着八个圆盘，从下到上，圆盘按从大到小的顺序排列。要求把所有圆盘移动到另一个柱子上，并遵循以下规则：
<ul>
<li>一次只能移动一个圆盘</li>
<li>圆盘只能套在柱子上</li>
<li>小圆盘只能放在比它大的圆盘上</li>
</ul>
</blockquote>

要解决这个问题，用普通的方法来作实在是很困难。而用递归来解决呢？ 会不会有一个容易的解决方案呢？

还是考虑递归的两个条件，<strong>是否可把问题规模缩小，是否存在简单情境</strong>。为了便于讨论，我们把圆盘现在所在的柱子称为源，把圆盘要移动到的柱子成为目的，另外一个柱子称为辅助。我们容易发现，要把最大的圆盘移动到目的，首先要把上面较小的七个圆盘移动到辅助上（注意，这是一个与原问题有着相同的形式且规模更小的问题），然后把大圆盘移动到目的上，在把七个较小圆盘从辅助移动到目的。可以看到，移动七个小圆盘其实与原问题形式相同而规模更小。好了，我们已经成功地缩小了问题规模。下面来找找简单情境。

很容易看到，当只有一个圆盘时，只要把它从源移动到目的就行了。这就是简单情境。

好，两个条件都具备了，我们可以开始写程序了。

{% highlight cpp linenos %}
void move_single_disk(char source, char target){
    printf("%c --> %c\n", source, target);
}
void move_hanoi_tower(char source, char target, char tmp, int n){
    if(n == 1)
          move_single_disk(source, target);
    else{
          move_hanoi_tower(source, tmp , target, n - 1);
          move_single_disk(source, target);
          move_hanoi_tower(tmp, target, source, n - 1)
    }
}
{% endhighlight %}

以上就是实现输出汉诺塔问题解的主要函数了。你可以编写一个主程序来调用它们。像这样：
{% highlight cpp linenos %}
int main(){
    move_hanoi_tower('A', 'B', 'C', 8);
    return 0;
}
{% endhighlight %}

不错吧，很简洁的，几行代码，就解决了这个问题。是不是很爽呢？不过这个递归调用的算法的复杂性如何呢？让我们来看看。

记规模为n的输入耗时T(n)，则：

`\( T(1) = 1 \\
T(n) = 2*T(n-1) + 1 \\
T(n) + 1= 2*(T(n-1) + 1) \\
T(n) + 1 = (T(1) + 1) * ( 1 - (T(1)+1)^n) / ( 1 - (T(1)+1)) \\
T(n) = 2^n - 1
\)`

这是一个很经典的例子，我们来给它改个版，留为今天的作业吧：

<blockquote>所有要求不变，添加如下要求：
圆盘不能从源直接移动到目的。
如何解决此问题？复杂度是多少？</blockquote>

原文链接：<a href="http://www.zhiyan.info/2007/03/21/recurence-power-3.html">http://www.zhiyan.info/2007/03/21/recurence-power-3.html</a>
