---
title: hexo博文插入图片
categories: "hexo"
tags: [hexo]
---
### 一 把主页配置文件_config.yml 里的post_asset_folder:这个选项设置为true
{% asset_img 1.jpg 主页配置文件_config.yml %}


### 二 下载图片的插件

```
在hexo目录下执行此命令 npm install hexo-asset-image --save ；
然后在 "hexo n 新文章" 会出现 .md文件 和 一个同名文件夹；
```
{% asset_img 2.png 2.1 %}
{% asset_img 3.png 2.2 %}




### 三 引入图片

``` 
格式 : {% asset_img 1.jpg 说明可省略 %}
```
