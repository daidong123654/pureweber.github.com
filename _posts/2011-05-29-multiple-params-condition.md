---
layout: post
title: '使用不定个数的参数构造查询条件'
tags:
  - array
  - join
  - mysql
  - php
  - '%e4%b8%8d%e5%ae%9a%e4%b8%aa%e6%95%b0%e5%8f%82%e6%95%b0'
  - '%e6%95%b0%e6%8d%ae%e7%bb%93%e6%9e%84'
  - '%e6%95%b0%e7%bb%84'

---

<h3>问题描述</h3>

通过get方法传过来0-3个参数,参数的个数不定,并通过这些参数构造出mysql查询语句.

下面是具体例子:
<ol>
	<li>case1_url: www.***.com?id=1&amp;name=2&amp;gender=3/</li>
	<li>case2_url: www.***.com?id=1&amp;gender=3/</li>
	<li>case3_url: www.***.com/</li>
</ol>

<ol>
	<li>在case1中我们传递了全部3个参数,这个很容易实现.</li>
	<li>在case3中我们没有传递参数,这个也很容易实现.</li>
	<li>但case2中只传递了部分参数应该怎么做呢?这个以前也纠结了不少时间,虽然实现了但方法都是很水的,这次请教了老段之后深深体会到了数据结构的强大之处.</li>
</ol>

<h3>解决方法</h3>

<h4>建立数据结构</h4>

建立2个数组,一个用来存储get中的变量名,另一个存储要构造mysql查询语句中的参数名;
<coolcode lang="php" linenum="off">$get_arrays = array(
        'id',
        'name',
        'gender',
);
$db_arrays = array(
        'user_id',	//与前一个数组中的键值相对应,不过上面存的是get中的参数,这里是数据库中的名称.
        'user_name',
        'user_gender',
);</coolcode>

<h4>构造查询串</h4>

利用循环将传递过来的参数存到新的数组中.	这里我们要新建一个数组query_array,用来存储查询语句
用到了两个函数:
<coolcode lang="php" linenum="off">
bool array_key_exists(mixed $key , array $search) //检查给定的键名或索引是否在数组中
join()// implode的别名
string implode ( string $glue , array $pieces ) //将字符串$glue加入到数组$pieces中.</li>
</coolcode>

<coolcode lang="php" linenum="off">foreach($get_arrays as $key =&gt; $value)
{
        //判断参数是否通过get方法传了过来
        $judge = array_key_exists($value, $_GET);
        if($judge)
        {
                $array[$key] = "`{$db_arrays[$key]}`= '{$_GET[$get_array[$key]]}'";
                //将要查询的变量及值用"="连接,写入数组中,此时array数组形如:$array=('id=1', 'gender=3');
        }
        $condition = join(" and ", $array);		// 使用"and"将各项条件连接起来
}</coolcode>

注：本文中的示例代码中未对输入进行转义，请勿应用在生产环境中。
