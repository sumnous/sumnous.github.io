---
layout: post
title: "[论文学习笔记] ICDM12-Topic-aware Social Influence Propagation Models(话题感知社会影响力传播模型)"
date: 2012-09-04 17:10:28 +0800
comments: true
categories: PaperNote
---

> Barbieri, N., Bonchi, F., & Manco, G. (2012, December). Topic-aware social influence propagation models. In Data Mining (ICDM), 2012 IEEE 12th International Conference on (pp. 81-90). IEEE.
 
社交网络传播模型的共同特征：



  1. 用户成为活跃用户的可能性随着他的邻居中活跃用户的数量单调增加。
  2. 影响过程遵循Progressive规则，即用户只可能从非活跃受影响变成活跃，而不可能由活跃变成非活跃。



Linear Threshold Model 线性阈值模型：是以接受者为中心的模型
Independent Cascade Model 独立级联模型：是以发射者为中心的模型


考虑时间延迟的模型(Continuous Time Delay Model)：在传统的IC，LT基础上引入连续时间延迟，也就是CTIC，CTLT。用于话题传播行为分析。


目标问题：确定有影响力的用户（例如病毒式营销中）


问题：离散对待的时间和大量参数（效率，可扩展行和过度拟合（过适，是指在调适一个统计模型时，使用过多参数。））


观察：1）用户有不同的兴趣；2）物品有不同的特征；3）用户有可能喜欢相似的物品
研究对象：物品特征，用户兴趣，社会影响


本文贡献：


  1. TIC和TLT
  2. Expectation Maximization (EM) 估计TIC模型的参数
  3. AIR (Authoritativeness-Interest-Relevance) 用户权威和话题兴趣取代user-to-user influence，减少参数
  4. Generalized Expectation Maximization (GEM) 用来学习最大似然来估计AIR模型的参数
  5. 使传统的IC模型可预测所接受的特定物品
  6. 考虑物品特征

在之前的topic-wise social influence加入Viral Marketing (病毒式营销) & Influence Maximization方法


σm(S) is monotone & submodular （子模函数，随着加入集合的元素越多,  F 函数值获得的受益越少(效用边际递减)。）


Influence maximization


TIC (Topic-aware Independent Cascade Model)
TLT (Topic-aware Linear Threshold Model)


  1. learning parameters of TIC model using Expectation-Maximization method (Complete-Data Expectation Likelihood[14], or log-likelihood maximization)

  2. 加入新物品item

AIR propagation model
parameters:


  1. authoritativeness of a user in a topic
  2. interest of a user for a topic
  3. relevance of an item for a topic

principle: general threshold model [2]
用selection scaling factors来控制时间衰变对信息传播的影响


Influence Maximization in AIR: 


   * Greedy
   * Top-k authorities

存在的问题和可以改进的地方：


  1. 这篇文章只是一个网络，不是异构网络，可以考虑构成user,item,topic三个网络的异构网络
  2. 只考虑到影响，并没有考虑到同质（personal影响，不只是结构影响，有可能是节点的属性影响传播）和环境
  3. 权威模型并不代表真的有效，容易被影响的人才能决定网络中信息的传播
  4. 网络的update，这篇文章只有item的update，并未涉及user关系的update

未来工作的难点：


  1. 加入点东西使得影响的人更多影响力更大（Influence Maximization）
  2. 改进模型使得计算速度更快

> 重要参考文献：
> [Kempe, D., Kleinberg, J., & Tardos, É. (2003, August). Maximizing the spread of influence through a social network. In Proceedings of the ninth ACM SIGKDD international conference on Knowledge discovery and data mining (pp. 137-146). ACM.](http://pdf.aminer.org/000/472/900/maximizing_the_spread_of_influence_through_a_social_network.pdf)