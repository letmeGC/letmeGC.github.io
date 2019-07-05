---
title: HTTP 传输大文件的方法
date: 2019-06-05 22:20:36
tags:
categories: "HTTP"
---

``` bash
① 压缩 HTML 等文本文件是传输大文件最基本的方法；
② 分块传输可以流式收发数据，节约内存和带宽，使用响应头字段“Transfer-Encoding: chunked”来表示，分块的格式是 16 进制长度头 + 数据块；
③ 范围请求可以只获取部分数据，即“分块请求”，实现视频拖拽或者断点续传，使用请求头字段“Range”和响应头字段“Content-Range”，响应状态码必须是 206；
④ 也可以一次请求多个范围，这时候响应报文的数据类型是“multipart/byteranges”，body 里的多个部分会用 boundary 字符串分隔。
```
