---
title: /&/& 用法
date: 2018-12-11 11:49:11
tags: [php,'小记']
categories : "PHP"
---
### 一 传统用法 "并且" 的意思，也就是左右两边都为真

``` bash
	if ($a>0 && $b>0){ 
	     //语句； 
	}
```


### 二 作为条件语句使用

``` bash
 $a > 0 && ($b = 123);   
 计算机会先判断$a 是否为真，如果是，则执行后面的语句，如果否，后面的语句就没有执行的必要了；
 
 对比 ||,与 && 相反 

 $a>0 || ($b = 123); 
计算机先判断$a >0 是否为真，是:后面的语句不会执行，否：执行；
 
```