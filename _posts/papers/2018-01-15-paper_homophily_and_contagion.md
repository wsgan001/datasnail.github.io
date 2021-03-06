---
layout: post
categories: Papers
title: Homophily and Contagion Are Generically Confounded in Observational Social Network Studies 
author: datasnail
comments: true
show: backup
intro: 。
paperTime:
tags:
- 论文阅读
---

文章题目表明：在观测的社交网络中，**趋同性(Homophily)**和**传染(Contagion)**（可以认为是影响）是非常容易混淆的。

### 一、摘要
在社交网络中，包含三种因素：① homophily，由于个体特征导致的social tie的形成；② social contagion，也叫社交影响力；③个体对其行为或其他可测量的反应产生的因果效应。
能区分以上三种，需要在社交过程或者充分利用协变量两部分的其中一个，甚至两者的参数上有较强的假设。（协变量的利用？）特别文中的证明，用了一些小例子，非对称的回归系数无法识别因果效应和非常简单的模仿模型（一种形式的社会传染）能产生显著的相关性在个体性格和选择上，甚至他们之间没有内在亲和力。

### 二、介绍
如果你的好朋友从桥上跳下来，你也会跳么？(you jump, i jump)
在社交网络中，临近的人会在很多方面比较相似，这可能有两方面原因：  
1、在网络中距离比较近的人，由于影响力会沿着social tie传播，所以他们的行为会相似。（先接近后相似）   
2、由于他们比较相似，所以他们聚集到一起，这个过程叫assortative mixing on traits，或者简单点叫趋同性。（先相似后接近）

例子：  
假设有两人互为朋友，叫Ian和Joey，有一天，Ian的父母问他一个社交影响力的经典假设问题：如果你的朋友Joey从桥上跳下去了，你也会跳么？（Ian回答YES，可能由于以下原因）  
1、Joey的例子（跳桥）启发了Ian；（社交影响力）  
2、Joey把寄生虫（parasite）传染给Ian了，Ian不再害怕坠落；（生物传染）  
3、Joey和Ian由于有共同的兴趣爱好（跳桥），而成为的朋友；（明显的趋同性，以兴趣爱好为特征）  
4、Joey和Ian通过一个寻求刺激的俱乐部而成为了朋友，这个俱乐部的成员名单是公开的；（次要的趋同性，在不同的观察特征上？？）  
5、Joey和Ian通过他们过山车的爱好而成为朋友，这是由于他们同具有需求刺激的特点，这也会导致他们跳桥；（潜在的趋同性，在不可观察的特点上）  
6、Joey和Ian都在同一时间在Tacoma Narrow桥上，跳起来比待在桥上更安全，因为桥正在撕裂。（共同外部因果关系）  
以上这些机制都是造成因果差异的原因，所以如果有任何形式的传染，能阻止Joey跳桥的措施，那么对于组织Ian跳桥肯定也是有效的。当然，如果不存在传染（影响），以上也就不会发生。然而，关键问题是，在纯粹的观察环境中，这些不同的机制是否会存在差异，由于我们通常不能进行这样的实验，即把Joey推下去，看看Ian跳不跳。（更不用说重复实验了）

这篇文章的目标就是，区分以上这些现象，总的来说，在纯观察环境中区分这些现象是很困难的。  
> It has been proposed that asymmetries in regression estimates that match asymmetries in the social network would let us establish direct social contagion;  

以上这句话在原文中，没有太理解，翻译过来大概是：有人提出，在回归估计中的不对称对应着社交网络中的不对称性，这让我们建立直接的社会传染（影响）。首先回归里的不对称性怎么理解？社交网络中的不对称性又是怎样的呢？通过这些如何建立直接的社会影响？  
在接下来的章节中（The Argument From Asymmetry），作为我们主要结论的推论，这也是不成立的。就是上面那句话中，有人提出的结论，作者这这篇文章中，也认为是不成立的。  
在很多观察性的研究中，作者意识到很多问题都有不可观察的特性。不仅仅是那些和我们在网络现象中分享明确重点的人，但是我们的关于社会传染的调查不是被一些敌意驱动的。我们 同样关心那些互联网络结构的调查。  
文中（第三章）表明，如果contagion伴随着趋同性，推断趋同性特征和输出变量例如观察到的行为将是混淆的。

当在网络里说起传染或者影响的时候，就意味着个体i在时间t时候的行为和个体i的邻居在t时刻之前的行为有一个时序上的**关系**。

>This is easiest to see when all other causes of adoption of a trait aside from the network itself are eliminated, such as person-to-person infectious diseases(M. S. Bartlett 1960; Ellner and Guckenheimer 2006; Newman 2002)

很容易的看出除了网络本身的限制以外其他所有特征采用的原因，像人与人之间的疾病传播，虽然其他例子包含的是创新传播（inovation diffusion）

更让人费解的是Christakis和Fowler在2007年的调查研究，随网络传播的行为是“变肥胖”，尽管肥胖通常并不是一种传染疾病；或者“happiness”的显示传播，Fowler和Christakis在2008年的研究。到这里，自然会问，还有多少像这样的网络自相关性（network autocorrelation），即行为在临近的互相连接的个体中是相互关联的这种趋势，这是由于i的邻居影响i的行为，而与趋同性的作用截然相反，趋同性是个体间形成的社会连接具有相似额前期特征，而接下来也可能会有相似的行为结果。  
社交网络的研究者们关心这个问题已久，像“selection versus influence”和“homophily versus contagion”