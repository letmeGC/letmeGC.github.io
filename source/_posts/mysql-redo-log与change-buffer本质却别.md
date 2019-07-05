---
title: mysql redo log与change buffer本质却别
date: 2019-07-05 20:31:16
tags: "笔记"
categories: "MYSQL"
---

```bash
redo log 主要节省的是随机写磁盘的 IO 消耗（转成顺序写），而 change buffer 主要节省的则是随机读磁盘的 IO 消耗。
```