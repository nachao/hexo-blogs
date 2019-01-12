---
title: 使用Hexo创建个人博客
date: 2019-01-11 01:56:11
category:
    - Technology
tags: 
    - Hexo
---

[Hexo](https://hexo.io/zh-cn/)是一个使用[Markdown](https://daringfireball.net/projects/markdown/)（或其他渲染引擎）解析文章的开源博客，且支持生成为Html静态文件，为搜索引擎和服务提供支持。

[官网手册](https://hexo.io/zh-cn/docs/)其实非常详细了，需要注意的是中文版中确实很多新的说明，因此建议看英文版。如果有手册意外的问题，可以在[GitHub](https://github.com/hexojs/hexo/issues)中提问。

## 快速手上

### 创建一篇文章

``` bash
$ hexo new "我的第一篇文章"
```

更多创建文章的操作，见官网的[写作](https://hexo.io/docs/writing.html)说明。

<!-- more -->

### 运行Hexo服务

``` bash
$ hexo server
```

查看更对关于[服务](https://hexo.io/docs/server.html)信息。

### 生成静态文件

``` bash
$ hexo generate
```

此操作的[详细说明](https://hexo.io/docs/generating.html)

### 部署静态文件

``` bash
$ hexo deploy
```

此操作的[详细说明](https://hexo.io/docs/deployment.html)

