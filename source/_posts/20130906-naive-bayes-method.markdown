---
layout: post
title: "朴素贝叶斯法"
date: 2013-09-06 16:10:28 +0800
comments: true
categories: [Bayes]
---


> 本文摘抄参考自：[李航-统计学习方法](http://pan.baidu.com/share/link?shareid=2848109060&uk=2184178031)

### 1 朴素贝叶斯法

1. 朴素贝叶斯法是典型的生成学习方法. 生成方法由训练数据学习联合概率分布 *P(Y|X)* , 然后求得后验概率分布*P(Y|X)*. 具体来说，利用训练数据学习*P(Y|X)*和*P(Y)*的估计，得到联合概率分布: 

	$$P\left( X,Y \right) =P\left( Y \right) P\left( { X }|{ Y } \right)$$
	
2. 朴素贝叶斯法的基本假设是条件独立性，

	$$P\left( { X=x }|{ Y=c_k } \right) =P\left( { { X }^{ \left( 1 \right)  }={ x }^{ \left( 1 \right)  },{ X }^{ \left( 2 \right)  }={ x }^{ \left( 2 \right)  },\cdots, { X }^{ \left( n \right)  }={ x }^{ \left( n \right)  } }|{ { Y=c_k } } \right)$$
	
	$$=\overset { n }{ \underset { j=1 }{ \prod  }  } P\left( { { X }^{ \left( j \right)  }={ x }^{ \left( j \right)  } }|{ Y=c_k } \right)$$
	
> 朴素贝叶斯法中假设输入变量都是条件独立的，如果假设它们之间存在概率依存关系，模型就变成了贝叶斯网络，参见文献[Bishop C. Pattern Recognition and Machine Learning, Springer, 2006] [[pdf]](http://pan.baidu.com/share/link?shareid=2811968744&uk=2184178031)

3. 朴素贝叶斯法利用贝叶斯定理与学到的联合概率模型进行分类预测. 

	$$P(Y|X)=\frac { P(X|Y) }{ P(X) } =\frac { P(Y)P(X|Y) }{ \sum _{ Y }^{  }{P(Y)P(X|Y)}}$$
	
	将输入x分到后验概率最大的类y.
	
	<center>aaa</center>
	
	$$y=arg{\max_{c_k}} P(Y=c_k) \overset { n }{ \underset { j=1 }{ \prod  }  } P\left( { { X^{(j)} }={ x }^{ \left( j \right)  } }|{ Y=c_k} \right)$$

### 2 朴素贝叶斯法的参数估计

#### 2.1 极大似然估计

先验概率*P(Y=c<sub>k</sub>)*的极大似然估计是

$$P(Y=c_k)=\frac {\sum_{i=1}^{N}I(y_i=c_k)}{N}, k=1,2,\cdots,K$$


设第*j*个特征*x<sup>(j)</sup>*可能取值的集合为{*a<sub>j1</sub>,a<sub>j2</sub>,…,a<sub>jS<sub>j</sub></sub>*}，条件概率*P(X<sup>(j)</sup>=a<sub>jl</sub>|Y=c<sub>k</sub>)*的极大似然估计是

<center><img src="https://raw.githubusercontent.com/sumnous/sumnous.github.io/source/source/images/bayes_likelihood_maximization.png" /></center>

$$j=1,2,\cdots,n; l=1,2,\cdots,S_j; k=1,2,\cdots,K$$

式中，x<sub>i</sub><sup>(j)</sup>是第*i*个样本的第*j*个特征；*a<sub>jl</sub>*是第*j*个特征可能取的第*l*个值；*I*为指示函数.


#### 2.2 贝叶斯估计 

用极大似然估计可能会出现所要估计得概率值为0的情况，会影响后验概率的计算结果，使分类产生偏差。解决方法是引入常量$\lambda$>=0. 等于0时为极大似然估计，常取1，这时称为拉普拉斯平滑（Laplace smoothing）. 

先验概率的贝叶斯估计是

$$\underset{\lambda}P(Y=c_k)=\frac {\sum_{i=1}^{N}I(y_i=c_k)+\lambda}{N+K\lambda}$$

条件概率的贝叶斯估计是

<center><img src="https://raw.githubusercontent.com/sumnous/sumnous.github.io/source/source/images/bayes_estimation.png" /></center>



