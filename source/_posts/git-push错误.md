---
title: git push错误
categories: "Git"
date: 2018-12-10 16:34:45
tags: [错误,git]
---
### 一 情景

``` bash
git push yuhaoblog
error: The requested URL returned error: 403 Forbidden while accessing https://github.com/letmeGC/blog.git/info/refs

fatal: HTTP request failed
```
{% asset_img 情景.png %}

### 二 解决

``` bash
$  vim .git/config
错误的: https://github.com/letmeGC/blog.git
正确的: https://letmeGC@github.com/letmeGC/blog.git
```
{% asset_img 解决.png %}
