---
layout: post
categories: Papers
title: 关于影响力最大化问题的小记
author: datasnail
comments: true
show: index
paperTime:
tags:
- 技术学习
---


#### **一、评价标准的浅度思考**

关于影响力研究方面，经常会看到一些论文，首先提出一种影响力的衡量方法或者是提出一个影响力传播的建模方法，然后利用影响力最大化，验证提出衡量方法或者建模方法的有效性。

一般情况：文章中的影响力最大化评价标准往往有以下几个方面的标准：
1. 种子节点数量-影响范围的比较；（相同种子节点数，影响的节点数量越多越好）
2. 算法运行的时间；

其实，一直存在疑问，为什么影响力最大化一般都要用这两个指标来作为评判标准，算法的运行时间比较容易解释，提出的一种算法，运行时间越短，在结果相差无几的情况下，肯定越高效。

但是对于，影响范围，一直存在误解，觉得种子节点对于其后续的节点影响，非常不具有说服力。主要原因是因为，利用的传播模型是理想的，不具有实际意义。但是理解成：作为在此理想的模拟状态下的问题解决方法，还是合理的。

**首先**，对于后续的节点，一般都选用理想传播模型（独立级联模型[IC]、线性阈值模型[LT]、病毒传播模型[SIR]）来模拟种子节点的后续影响，像独立级联中的传播概率一般选择从0到1的实验过程，比较好的实验结果是，在传播概率从0到1的过程中，所选的种子节点的影响范围都比较广。

**其次**，对于衡量影响力，之后用于影响最大化解决，来表明影响力衡量的正确性，也具有一定说服力。因为，影响力的衡量可以找出影响最大的N个种子节点，然后文中一般是要设计一种影响力最大化的算法（基于贪心思想或者启发式思想），来利用前面得出的结论，换了一个问题[影响力最大化问题]来解决，如果得到的传播范围更广，则一定程度上也说明了，影响力衡量的大小是合理的。