---
layout: post
categories: Papers
title: DeepInf:Social Influence Prediction with Deep Learning论文笔记
author: datasnail
show: index
comments: true
intro: 神经网络做的影响力文章。
tags:
- 论文阅读
---
{:.center}
![](/postimg/deepInf/deepInf_head.png)  
{:.center} 

**2018 SIGKDD**的文章。一看又是清华唐杰老师做的，兴奋之处有点绝望。  

文中指出传统的影响力预测方法均为设计很多手动的规则来提取用户特征，还有就是挖掘网络特征。但是它的有效性**很大程度上依赖领域知识**。所以往往**很难将他们推广到不同的领域**。所以基于这一点，启发于具有广泛应用的深度神经网络，设计了一个端到端的框架，**学习用户潜在的特征表示**，并预测影响力。DeepInf把用户的局部网络作为输入，学习他潜在的社交表示（social representation）。并且设计了一个策略，既包含网络结构和用户特定特征的**卷积神经和注意力机制网络**。并在**Academic Graph, Twitter, Weibo, Digg**数据集上实验，表示不同的社交和信息网络，证明了DeepInf表现良好，证明了这种表示学习的有效性。  

你周围人已经做了某事，你是否会做某事?
你周围的环境是这样的，你之前在这样的环境中是这么做的，你现在还会这么做么？

