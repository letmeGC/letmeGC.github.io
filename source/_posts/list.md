---
title: list
date: 2018-12-11 11:07:59
tags: [php,小记]
categories : "PHP"
---
### 一 情景

``` bash
list() 用于在一次操作中给一组变量赋值。

$arr = ['a','b','c'];
list($a,$b) = $arr;
echo $a,'---',$b;

//输出 : a---b

谨记 ：list()只用于数字索引的数组，且假定数字索引从 0 开始。
```

### 二 错误用法

{% asset_img list1.png %}
{% asset_img list2.png %}