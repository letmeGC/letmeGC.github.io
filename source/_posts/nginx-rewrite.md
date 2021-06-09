---
title: nginx重写
date: 2019-12-10 17:47:41
tags:
---
```
 #去掉url中的api,并转发到http://ym.shixiaoli.com
  location ~ /api/ {
     rewrite ^/api/(.*) /$1 break;
     proxy_pass http://ym.shixiaoli.com; 
  } 
```