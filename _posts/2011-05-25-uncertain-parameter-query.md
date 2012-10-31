---
layout: post
title: 使用不定个数的参数构造查询字符串
author: 田大龙
github: glovenone
tags:
 - php

---

寒假开始制作Cyber-Reader写CDB类库的时候,就有一个查询是要求写出一个,具有可变参数个数的函数，类似于sprintf，fsql定义了数据格式，v1, v2等变量定义了要替换的值，然后将替换后的字符串作为数据库查询进行执行.

这个东西我纠结了好久,也想了不少方法,最后因为开学了没有写完,里面不少东西都是老段完成的.现在说说关于这个查询时遇到的问题和解决的方案.

先举一个实现后的例子:

{% highlight php %}
<?php
queryf("select * from glove_user where name = '%s' and site = '%s'", 'glove', 'glovely.info');
?>
{% endhighlight %}

这其实就是一个select语句,其中不同的地方就是第一个参数中的name的值%s用后面的’glove’来替换,site的值%s用后面的’glovely.info’来替换,这些可以替换的参数是不限定个数的.
也就是说这个函数像我们用的sprintf一样,是带有不定个数的参数的.

最初我的想法是得到用户的输入,将其传递给sprintf,这样变将要赋值的参数通过sprintf完成,然后最后得到的结果便是我们要执行的mysql命令.下面是实现的方法.

实例1:

{% highlight php %}
<?php
function queryf(){
       $pa = func_get_args();                        //得到用户的输入
       $sql = call_user_func_array("sprintf", $pa);  //将得到的输入传递给sprintf
       $result = mysql_query($sql);     //这个函数的返回值便是sprintf处理后的我们要执行的</code>mysql命令</pre>
       return $result;
       if(is_bool($result))
         return $result;
       else
         return mysql_fetch_array($result);    //根据所得值是bool还是array来确定不同的返</code>回值类型.</pre>
}
?>
{% endhighlight %}

虽然有部分命令可以执行,但这显然不是一个很好的办法,毕竟这里要求的功能不是和sprintf一模一样的.

下面便是我们现在的CDB类库中使用的queryf.
它的思路:

得到输入的命令,通过判断其中%的位置和数量,来找到要传入的数据类型和数据个数,并进行相应的错误判断.
实例2:

{% highlight php %}
<?php
const NUM = 'd';
const STR = 's';
const RAW = 'r';
const ESC = '%';

function queryf()
{
        $args = func_get_args();    //获得输入的命令
        if( ($argCount = count($args)) == 0 )     //检查命令长度是否为0
            return false;
        $format = $args[0];             //命令的第一部分
        $arg_pos = 1;
        $esc_pos = false;
        $v_pos = 0;
        $sql = '';
    while(true)
    {
        $esc_pos = strpos($format, CDB::ESC, $v_pos);       //查找符号"%"在字符串$format中出现的位置,偏移量为$v_post,初始为0.
        if($esc_pos === false)  //第一次查找%位置时$esc_pos的值应该是false
        {
                $sql .= substr($format, $v_pos);     //找到字符串$format中初始位置到$v_post字符并存入$sql中
                break;
        }
        $sql .= substr($format, $v_pos, $esc_pos - $v_pos);    //将%之间的字符串存入
        $esc_pos++;    //用来保存匹配到%的位置,这里加一用于下面的比较操作
        $v_pos = $esc_pos + 1;              //$v_pos的位置在$esc_pos的后一位
        if($esc_pos == strlen($format)) //如果esc的位置等于$format的长度,则返回false,及%后无类型字符
        {// % 后面没有类型字符
            return false;
         }
        $v_char = $format{$esc_pos};              //$format中的第esc个字符
        if($v_char != CDB::ESC)
        {
            if($argCount <= $arg_pos)
            {// 参数个数不够
                return false;
            }
            $arg = $args[$arg_pos++];
        }
        switch($v_char){ //判断%后的字符是什么,即我们要替换什么类型的数据
            case CDB::NUM:
                $sql .= intval($arg);
                break;
            case CDB::STR:
                $sql .= $this->escape($arg);
                break;
            case CDB::RAW:
                $sql .= $arg;
                break;
            case CDB::ESC:
                $sql .= CDB::ESC;
                break;
            default: //非法的符号
                return false;
        }
}
$rs = $this->query($sql);
if(is_bool($rs))            //判断最后结果的类型
    {
        return $rs;
    }
    else
    {
        $r = array();
        while( ($row = mysql_fetch_array($rs)) )    $r[] = $row;
        return $r;
    }
}
?>
{% endhighlight %}
