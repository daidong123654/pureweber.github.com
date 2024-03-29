---
layout: post
title: 'Mysql按条件计数的几种方法'
description: Mysql中按照字段的值，对符合不同条件的记录进行计数和统计。用一条SQL语句实现。描述了3种方法，分别使用GROUP BY，嵌套SELECT和COUNT加CASE WHEN。
author: 段志岩
github: dzy0451
tags:
  - case
  - count
  - mysql
  - '条件计数'
  - '分类统计'
  - '分类求和'

---

最近在给<a href="http://www.xilexile.com" rel="nofollow">喜乐喜乐网</a>的后台添加一系列的统计功能，遇到很多需要按条件计数的情况。尝试了几种方法，下面简要记录，供大家参考。

##问题描述

<small>为使讨论简单易懂，我将问题稍作简化，去掉诸多的背景。</small>

从前有一个皇帝，他有50个妃子，这些妃子很没有天理的给他生了100,000个儿子，于是，皇帝很苦恼，海量的儿子很难管理，而且，他想知道每个妃子给他生了多少个儿子，从而论功行赏，这很难办。于是，皇帝请了一个程序员帮他编了一个程序，用数据库来存储所有的儿子的信息，这样就可以用程序来统计和管理啦。


数据库的结构如下：

<table>
<tr><th>id</th><td>皇子的唯一编号</td></tr>
<tr><th>mother</th><td>皇子母亲的唯一编号</td></tr>
</table>

皇帝把妃子分成了两个等级，天宫娘娘(编号小于25)和地宫娘娘(编号大于等于25)，他想知道天宫娘娘们和地宫娘娘们的生育能力孰强孰弱。于是，程序员开始写SQL Query了。

##方法1：使用GROUP BY

###SQL Query
{% highlight sql %}
SELECT COUNT(*) FROM `prince` GROUP BY `mother` > 24;
{% endhighlight %}

###执行结果

	count(*)
	50029
	49971

在100,000行数据上的运行时间：0.0335 秒

###分析

这种GROUP BY方法的最大问题在于：无法区分所得到的结果。这两个数字哪一个是天宫娘娘们所生的皇子数，哪一个是地宫娘娘们所生的皇子数呢？不知道。所以，尽管它统计出了总数，但是没有什么意义。

因此，为了区分统计结果，必须要把条件 mother > 24 也作为一个字段在结果集中作为一个字段体现出来，修改后的sql如下：

{% highlight sql %}
SELECT COUNT(*) AS `number`, `mother` > 24 AS `type` FROM `prince` GROUP BY `mother` > 24;
{% endhighlight %}

执行结果

	number	type
	50029	0
	49971	1

条件表达式作为字段时，该字段的值就是该条件表达式的值，因此，对应我们的例子，type = 1 也就是表示 mother > 24 的值为1，因此，第二行中的数字代表地宫娘娘们所生的皇子数。

经过修改后，我们看出，天宫娘娘们略胜一筹。

###优缺点

缺点是显而易见的，由于使用了条件表达式作为分组依据，它只能做二元的划分，对于要分成多类进行统计的情况不能够胜任。比如要分别统计1~10号、11~24号，25号~50号妃子的产子数，就无法实现了。

另外，由于使用了GROUP BY，因此涉及到排序，执行时间上要更长。

我暂时没有发现这种方法的优点。

##方法2：使用嵌套的SELECT

使用嵌套的SELECT也可以达到目的，在每个SELECT子句中统计一个条件下的数据，然后用一个主SELECT把这些统计数据整合起来。

###SQL Query

{% highlight sql %}
SELECT 
    ( SELECT COUNT( * ) FROM `prince` WHERE `mother` >24 ) AS `digong`, 
    ( SELECT COUNT( * ) FROM `prince` WHERE `mother` <=24 ) AS `tiangong`
{% endhighlight %}

###执行结果

	digong	tiangong
	49971	50029

在100,000行数据上的运行时间：0.0216 秒

###分析

这种嵌套SELECT的方法非常直观，就是分别统计各个条件下的数值，最后进行汇总，通俗易懂，跟自然语言没啥区别了。

###优缺点

优点就是直观，而且速度也比GROUP BY要快。虽然是3条SELECT语句，看起来比GROUP BY的方案多了2条语句，但是它不涉及到排序，这就节省了很多时间。

缺点可能就是语句稍多，对语句数量有洁癖的同学可能会比较不舒服。

##方法3：使用CASE WHEN

<a href="http://dev.mysql.com/doc/refman/5.0/en/case-statement.html">CASE WHEN</a>语句的功能很强大，可以定义灵活的查询条件，很适合进行分类统计。

###SQL Query

{% highlight sql %}
SELECT 
    COUNT( CASE WHEN `mother` >24 THEN 1 ELSE NULL END ) AS `digong`, 
    COUNT( CASE WHEN `mother` <=24 THEN 1 ELSE NULL END ) AS `tiangong`
FROM prince
{% endhighlight %}

###执行结果

	digong	tiangong
	49971	50029

在100,000行数据上的运行时间：0.02365825 秒

###分析

此方法的关键在于 

{% highlight sql %}
COUNT( CASE WHEN `mother` >24 THEN 1 ELSE NULL END ) 
{% endhighlight %}

这里的COUNT和CASE WHEN联合使用，做到了分类计数。先使用CASE WHEN，当满足条件时，将字段值设置为 1， 不满足条件时，将字段值设置为NULL，接着COUNT函数仅对非NULL字段进行计数，于是，问题解决。

###优缺点

优点嘛，此方法也不涉及到排序，因此运行时间上与方法2相当，SELECT语句减少到了 1 条。

缺点就是语句比较长，对语句长度有洁癖的同学可能会比较不舒服。

##总结

对于确定分类的按条件计数，可以尽量不用GROUP BY，从而避免排序动作，加速Query的执行。

如果需要根据某个字段的值进行分类，而该字段的值是可变的，比如皇帝要统计每一个妃子的产子数，而他可能不停的再娶很多妃子，这种情况下，使用方法2和方法3就不太灵光了，还是使用一个GROUP BY来得简单便捷。

原文地址：<a href="http://www.zhiyan.info/2011/02/24/mysql-conditional-count.html">http://www.zhiyan.info/2011/02/24/mysql-conditional-count.html</a>
