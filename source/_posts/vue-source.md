---
title: 研究Vue2.x的实现
date: 2019-01-12 23:45:11
category:
    - Technology
tags:
    - Vue
---

> 这是一个持续的文档，大概周期在一个月左右。会先对vue源码的各个模块进行分析，然后逐个去按照自己的理解实现一遍。

<img width="100" src="https://vuejs.org/images/logo.png" alt="Vue logo">

关于Vue的[背景和使用](https://cn.vuejs.org/)，官网已经非常详细了。而且此文章的目的不是讲如何使用vue，而是当你工作中使用后，对技术更深层次的专研。

最终达到对Vue的内部实现透彻，一是学习框架实现的机制和一些编码技巧，再者在使用中对会遇到的问题游刃有余。

## 带着问题看源码

1. 框架整体设计结构？
2. 各个模块的都是干什么用？

```base
$ git clone https://github.com/vuejs/vue.git
```

<!-- more -->