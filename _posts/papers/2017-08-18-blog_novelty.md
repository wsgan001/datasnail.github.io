---
layout: post
categories: Papers
title: 微博的新颖度
author: datasnail
comments: true
show: index
intro: 看了一篇文章，介绍微博的新颖度
tags:
- 论文笔记+1
---


首先用LDA，得出词条（entry）在主题下的分布，从而获得一个关于词条的向量。
首先计算词项的新颖度：
词项与转发的微博中词项的相似度的最小值。
一条微博的新颖度：
含有词项新颖度的平均值。