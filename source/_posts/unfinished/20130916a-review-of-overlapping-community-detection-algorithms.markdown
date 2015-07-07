---
layout: post
title: "A review of overlapping commuity detection algorithms"
date: 2013-09-16 16:10:28 +0800
comments: true
categories: Algorithm
---

##Overlapping Community Detection

[Overlapping Community Detection in Networks : the State of the Art and Comparative Study](http://arxiv.org/abs/1110.5813)

[Community detection algorithms: a comparative analysis](http://arxiv.org/abs/0908.1062)

###0 OLD METHOD
+ Clustering
+ Graph Cut
+ Modularity-Based Method(is NP-hard to optimize) [[Newman, 2006]](http://arxiv.org/pdf/physics/0602124.pdf)
	<center><img src="modularity.png"></center>
	+ Greedy
	+ Simulated Annealing
+ Girvan-Newman Algorithm (Betweenness, split)
+ Spectral Method

###1 Clique Percolation
#### CPM (Clique Percolation Method)
+ Indentify all the k-cliques in network. *Clique* is an intensively structure, each two nodes are connected in a clique. Connect two nodes if their two k-cliques they belong to share k-1 members. [[Palla, 2005, Nature](http://www.nature.com/nature/journal/v435/n7043/full/nature03607.html)]
+ Implementation: [CFinder](http://www.cfinder.org/) (support directed and weighted graph)
+ Time Complexity: **polynomial** (NP-complete maximal cliques finding)

###2 Local Expansion and Optimization
#### LFM
+ expands a community from a random seed node to form a natural community until fitness function is locally maximal. [[Lancichinetti, 2009, New J. Phys.](http://arxiv.org/pdf/0802.1218.pdf)]
+ fitness function: 
<center><img src="fitness_function.png"></center>
+ where n<sub>c</sub> is the number of communities, s is the average size of communities.
+ **O(n<sub>c</sub>s<sup>2</sup>)**, computation complexity is depended on parameter \alpha.  
+ worst-case complexity: **O(n<sup>2</sup>)**

#### GCE (Greedy Clique Expansion)
+ takes all maximum cliques as initial seeds to greedily expand the fitness function to find overlapping communities. [[Lee, 2010]](http://arxiv.org/abs/1002.1827)
+ [GCE Implementation](https://sites.google.com/site/greedycliqueexpansion.)
+ Greedy expansion complexity: **O(|E|M)**, M is the number of cliques to be expanded. 
+ merge complexity: **O(2(|C1|+|C2|)-1)**(not sure)

#### OSLOM (Order Statistics Local Optimization Method)(IMPORTANT)
+ optimizes locally the statistical significance information of a cluster with respect to random fluctuation with Extreme and Order Statistics. It tests the statistical significance of a cluster with respect to a global null model. It can deal with weighted, directed edges, overlapping communities, hierarchies and dynamic communities. [[Lancichinetti, 2011]](http://oslom.org/oslom.pdf)
<center><img src="oslom.png"></center>
+ Implementation: [www.oslom.org](http://www.oslom.org)
+ worst-case complexity: **O(n<sup>2</sup>)**

#### EAGLE
+ All maximal cliques is as initial communities, merged by maximum similarity -> dendrogram. The optimal cut on the dendrogram is determined by the extended modularity with a weight based on the number of overlapping memberships. [[Shen, 2008]](http://arxiv.org/pdf/0810.3093.pdf) [[code]](http://code.google.com/p/eaglepp/)
+ Extended Modularity: 
<center><img src="extended_modularity.png"></center>
+ where O<sub>i</sub> is the number of communities to which node i belongs.
+ **O(n<sup>2</sup>+(h+n)s)**, where s is the number of maximal cliques, h is the number of pairs of maximal cliques which are neighbors. 

###3 Mixturl Model (TODO)
+ [[Newman, 2007]](http://www.bradblock.com.s3-website-us-west-1.amazonaws.com/Mixture_models_and_exploratory_analysis_in_networks.pdf)
+ GMM(Gaussian Mixture Model)
+ SBM(Stochastic block model)
+ NMF(Non-negativeMatrix Factorization)

###4 Label Propagation Algorithm (Dynamical Algorithm)
#### COPRA
+ [[Gregory,2010]](http://arxiv.org/pdf/0910.5516.pdf)
+ **O(vmlog(vm/n))** per iteration, v controls the number of communities a node can belong to, m is the number of edges, n is the number of nodes. 

#### SLPA(IMPORTANT TODO)
+ is a general speaker-listener based information propagation process. [[Xie, 2011]](http://arxiv.org/pdf/1202.2465.pdf)
+ [code](https://sites.google.com/site/communitydetectionslpa/)
+ **O(t|E|)**, linear, t is the predefined maximum number of iterations. 

#### InfoMAP(IMPORTANT TODO)
+ The map equation framework
<center><img src="map_equation.png"></center>
+ [papers](http://www.mapequation.org/publications.html)
	+ [The Map Equation [Rosvall, 2009]](http://www.mapequation.org/assets/publications/EurPhysJ2010Rosvall.pdf)
+ [codes](http://www.tp.umu.se/~rosvall/code.html)


