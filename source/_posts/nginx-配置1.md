---
title: nginx--同时支持443-80
date:  2019-02-23 15:40:15
tags:  [nginx]
scategories: "NGINX"
---

```
  既要80 http访问，又要443https访问。
  要让https和http并存，不能在配置文件中使用ssl on，配置listen 443 ssl;
 
 实例
  server
 {
 listen 80;
 listen 443 ssl;
 server_name www.xxx.com;
 index index.html index.htm index.php;
 root /xxxx/www.xxx.com/;
 #ssl on; 这里要注释掉
 ssl_certificate /usr/local/nginx/conf/ssl/www_xxx_com.crt;
 ssl_certificate_key /usr/local/nginx/conf/ssl/www_xxx_com.key;
 
 #以下配置省略
 
 }
```