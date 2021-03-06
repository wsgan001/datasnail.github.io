---
layout: post
categories: Fundamental
title: 为什么机器学习是可行的？
author: datasnail
comments: true
show: index
intro: 台湾大学机器学习课程，为什么说机器学习是可行的？有何理论依据呢？记录自己的理解，帮助日后复习。
paperTime:
tags:
- machine learning
---


主要问题如下：  
1、Hoeffding's inequality问题和PAC概念。    
2、证明在采样数据集上学习得到的h的错误率和全局是PAC的。  
3、证明机器是可以学习的。  

主要是针对此节课的笔记和思考，概念做较为简略的解释。  
#### **1、课程笔记**

{:.center}
![](/postimg/y_machine_learning_works/two_controversial_answers.jpg)  
图1. 例题
{:.center}
给了一个例子，总结给出的问题中$g(x)$的值是+1还是-1，因为可以遵循各种不同的规则（合理的原因），$g(x)$总可以认为你没有从前面的给出的内容中学到有用的知识，而说你得出的结论是错误的。再例如，给你学习资料如下图5条，估计101，110，111的值是什么。

{:.center}
![](/postimg/y_machine_learning_works/five_learning_materias.jpg)   
图2. 五条学习样本资料
{:.center}

当我们提出假设时，可以有$2^3=8$情况的假设，我们可能会根据某个规则选择其中的一个作为我们对这个学习资料的假设$g$（就像我们总结上一张图中图形的规律以一样），但是在实际情况中，因为可以遵循不同的规律，这三个值可以是任意值的一种（真实假设可以是$f_1,f_2,...,f_8$中的任意一种），所以又是总可以说我们对资料的学习方法不对（即我们没有从资料中学习到知识）。这样，可以看到，在学习资料的inside（给出的学习资料）中，我们通过各种方法总是能使得$g \approx f$,但是在资料的outside（未知的要预测的资料）中，我们可能总是得不到符合要求的$g$，也就是说我们的学习是无效的。  
以上也就说明了一个道理：**NO FREE LUNCH！**，即我们用已知的经验，我们没有任何的理由得出经验之外的推理（Hume 1939）。  
但是，机器学习就是要通过已知的经验或者资料，去推测未知啊，以上又说这是做不到的，是不是机器学习就是不可能的？？  

首先给出一个概率问题：**有一罐弹珠，如何知道罐子里面橙色弹珠的概率？**，那其实很多人看到这个问题，都会讲这很简单啊，我随机从罐子里抓出一把弹珠，然后计算橙色的概率，就可以大概估计罐子里橙色弹珠的概率，*按照这种思路，所以我们抓一把出来，看到有12颗，其中橙色的弹珠有3颗，则此样本（sample）中的橙色弹珠概率为25%，得出结论是：罐子里的橙色弹珠概率大概为25%*。但是这里出现了一个**新的问题**，在样本内（in-sample）的概率$\nu$没有告诉我们罐子里橙色的弹珠概率具体是多少？**没有。**但是为什么就可以说罐子里（out-sample)橙色弹珠概率就为25%呢？有没有可能罐子里就三颗橙色的弹珠被抓到了呢？或者有没有可能就9颗绿色弹珠呢？  
此处我们没有说罐子里（out-sample）橙色弹珠概率就是25%，只是说有很大可能、大概、可能、差不多，即**样本**中得出**概率**$\nu$跟**罐子里的真实概率**$\mu$很可能是很接近的（**误差**为$\epsilon$）。而且后面的问题答案都是：有可能。

{:.center}
![](/postimg/y_machine_learning_works/ball_probability.jpg)  
图3. 取样（sampling） 
{:.center}

看到这里好像又有点失望，不要紧，我们在上面的回答虽然是“有可能”，但是可能性就像*沙漠里下暴雨*---可能性很小。有什么依据么，依据就是**Hoeffding's Inequality**(霍夫丁不等式)：  

$$
\mathbb{P}[\|\nu-\mu\|>\epsilon] \le 2exp(-2\epsilon^2N)
$$

其中N是样本数量，可以看到$\nu$和$\mu$两个之间的差别大于$\epsilon$的概率是被框定在$2exp(-2\epsilon^2N)$这个概率范围之内的。这样，我们希望的$\nu=\mu$就能保证差不多、大概是对的，即**probably approximately correct（PAC）**：我们要做推论，我们可以从手上现有的资料样本（in-sample）直接去推理罐子里（out-sample）的橙色弹珠概率，但是要冒的风险是**可能、差不多**。  
Hoeffding's Inequality对任意的N和$\epsilon$都是成立的，而且右边的式子$2exp(-2\epsilon^2N)$是跟真实概率值$\mu$（未知）无关的，而且我们也不需要知道$\mu$，我们只知道样本中的概率$\nu$，这样就可以推论回来：Hoeffding's Inequality提供给我们的理论依据是，我们没有必要去知道未知或者待预测的真实值的假设，就可以得到未知或者待预测的内容。另一方面，可以看到用的样本数据越大，不等式后面的值就会越小，坏事发生的几率就会更小，即两个值就会更接近。同样如果把容忍的值$\epsilon$设置的大，也可以得到$\nu$和$\mu$**差不多**，虽然有点自欺欺人。  
至此，我们得出结论：如果我们使用的样本数量够大的话，就会使得样本得到的值与真实值接近。那再从弹珠问题转换到机器学习的问题。

{:.center}
![](/postimg/y_machine_learning_works/hx_color.jpg)  
图4. h(x)染色弹珠规律  
![](/postimg/y_machine_learning_works/ball2machine_learning.jpg)  
图5. 弹珠问题到机器学习问题映射关系  
{:.center}

在此处，我们手中**持有一个假设**$h(x)$，真实（目标）假设为$f(x)$，按照图4的给罐子中的弹珠染色（如果$h(x) \ne f(x)$，则弹珠染成橙色；否则染成绿色。）则原来的弹珠问题可以如图5映射到机器学习问题上：
1. 未知的橙色弹珠概率$\mu$映射为目标假设$f(x)$；
2. 弹珠映射到X；
3. 黄色映射到$h(x)$是错误的$h(x) \ne f(x)$；
4. 绿色映射到$h(x)$是正确的$h(x) = f(x)$；
5. 样本数量N映射到机器学习中的学习数据集；

所以，我们只需检查$h(x)$在样本数据上的表现，就可以估计$h(x)$在罐子里（未知的）预测效果，即大概$h(x) = f(x)$。

{:.center}
![](/postimg/y_machine_learning_works/machine_learning_inference.jpg)  
图6. 机器学习对应弹珠问题的流程 
{:.center}  
其中$E_{in}$是样本中的误差，$E_{out}$是预测的误差。所以可以看到Hoeffding不等式给了我们这两个值很接近，**条件是：预测的内容要按照与样本数据同一分布产生数据**，则我们可以保证在**样本量够大**的时候，$E_{in}$很小的时候，$E_{out}$也会很小。  
到此，是不是就万事大吉了呢？不是，前文讲到我们首先是“持有一个$h(x)$”，而且最后必须正好这个$h(x)$的$E_{in}$很小才可以，此处我们假设从$h(x)$最终选择的假设为$g$，即要保证$g=f$（PAC）。如果现在有一千个、一万个$h(x)$呢？那么机器学习真正的学习是从千万个$h(x)$中找到$g$，需要验证（verify）某个$h$，具体流程如下：

{:.center}
![](/postimg/y_machine_learning_works/verification_sequence.jpg)  
图7. 机器学习中对某个假设验证的流程 
{:.center} 

现在有很多假设$h(x)$，也就是有很多罐子（图8），每个假设对数据的预测能力都是不一样的（在罐子里面真实的绿色弹珠的比例），同样还是通过抽样得到不同的$E_{in}$，如图8：

{:.center}
![](/postimg/y_machine_learning_works/many_hypothesises.jpg)  
图8. 很多假设的情况 
{:.center} 

可以看到，有一个假设在所看到的资料上全对（$h_M$)。我们是不是要选择这个全对的？  
来看一个硬币的例子：假设有150个人同时抛硬币五次，其中有一个人得到五次正面，那么可以得出结论：此人硬币获得正面的几率高么？仔细想想，肯定不是，为什么呢？因为有小几率事件发生，那么至少有一个人出现五次全正面的概率是$1-(\frac{31}{32})^{150} \gt 99\%$，这些硬币都是假设均匀的也会发生这种事情，所以我们在选择的时候就会出现偏差，即**并不是我们选择训练误差很低的假设，就能说它的泛化误差也很低**。这就是**过拟合**（overfitting）。  
Hoeffding讲取样出来的样本大部分的时候是和罐子里是一样的，只有少数时候是不好的($\mu$和$\nu$差别很大)。即在做一次（抓弹珠、抛硬币），不好的(差别很大、五次全正面)时候的概率很小。但是有很多选择的时候，选到不好的可能性就会上升。举个栗子，当我们选1个硬币，抛五次朝上的概率是1/32，那选150个硬币，有五次朝上的硬币的概率就会达到99%。（铜板=弹珠=资料）。Hoeffding保证的是在一次数据资料D上，$h(x)$表现是不好的概率较低，即图9中横着一条出现BAD的概率或者次数很少。

{:.center}
![](/postimg/y_machine_learning_works/hoeffding_guartee.jpg)  
图9. Hoeffding 不等式的保障性
{:.center} 

但是我们有很多$h(x)$啊，就像图10所示：

{:.center}
![](/postimg/y_machine_learning_works/many_hypothesises_hoeffding.jpg)  
图10. 很多假设在样本资料上的表现
{:.center} 

现在是要求能在某个资料上安心做选择，也就是在上图一列上做选择，例如在$D_1$上做选择，那么我们有不好的假设就是$h_1,h_3,h_M$等等，$D_2$也很多不好假设，只有在$D_{1126}$这种好的资料上。那么只要有D对h是不好的，这一列就是不好的数据资料（Bad data），那么出现至少一次不好的概率为：

{:.center}
![](/postimg/y_machine_learning_works/probabilities_many_data.jpg)  
图11. 很多假设在样本资料上的表现
{:.center}  
此处的M就是有几个罐子或者假设空间大小，以上结果叫做联合上界（union bound）。所以我们还是可以通过增加数据资料的大小来减少bad data的概率，换句话说，增加样本防止过拟合。  
至此，总算可以保证机器学习是可以做得到的吧？其实还不是很严谨，因为目前是设想：假设空间是有限的，如果假设空间是无限的呢？答案也是可以的。[后来再解释](../04/training_and_testing.html)。

{:.center}
![](/postimg/y_machine_learning_works/questions_end.jpg)  
图12. 问题
{:.center}

答案是1,The important thing is to note that 2 is true, which implies that 4 is true if you revist the union bound. Similar ideas will be used to conquer the M = max case。

#### **二、参考**
[1] https://www.cnblogs.com/HappyAngel/p/3495804.html  
