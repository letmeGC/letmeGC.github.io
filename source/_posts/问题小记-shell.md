---
title: 问题小记-shell
date: 2020-03-11 17:05:57
tags:
categories: 问题小记
---
```
编写shell程序执行的时候出现以下错误提示：
curl: (3) Illegal characters found in URL
: numeric argument required
是因为程序文本中含有\r等换行符。

检查是否含有\r等换行符，也可以使用以下命令检查：
vi test.sh
① :set ff?
如果出现fileforma＝dos那么就可以确定是这个问题。
可以使用以下命令转换程序格式
② :set fileformat=unix
③ :wq

就把\r\n变成了\n
```