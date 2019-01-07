---
title: mysql索引一
date: 2018-12-20 15:49:10
tags:
categories: "MYSQL"
---
### 一MyISAM索引实现

``` bash
MyISAM引擎使用B+Tree作为索引 ,索引文件的data存储指向数据文件的指针。辅索引与主索引基本一致，但是辅索引不用保证唯一性.
因此，MyISAM中索引检索的算法为首先按照B+Tree搜索算法搜索索引，如果指定的Key存在，则取出其data域的值，然后以data域的值为地址读取相应数据记录。

MyISAM的索引方式也叫做“非聚集”的，之所以这么称呼是为了与InnoDB的聚集索引区分。
```
{% asset_img MyISAM索引的原理图.png MyISAM引擎 %}

### 二 InnoDB索引实现

``` bash
InnoDB使用B+Tree作为索引结构,实现方式却与MyISAM截然不同。

第一个重大区别是InnoDB的数据文件本身就是索引文件。从上文知道，MyISAM索引文件和数据文件是分离的，索引文件仅保存数据记录的地址。
而在InnoDB中，表数据文件本身就是按B+Tree组织的一个索引结构，这棵树的叶结点data域保存了完整的数据记录。这个索引的key是数据表的主键，
因此InnoDB表数据文件本身就是主索引,这也是为什么INNODB会在你不设置主键的时候生成一个隐含字段作为主键
```

{% asset_img innodb.png innodb主键索引 %}

```
INNODB 辅助索引搜索需要检索两遍索引：首先检索辅助索引获得主键，然后用主键到主索引中检索获得记录
```
{% asset_img 对比图.png 查找过程对比图 %}