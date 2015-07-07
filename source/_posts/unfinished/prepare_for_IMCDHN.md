Goal: 

Find the most influenced users in DBLP citation network.

Input:

G = {Author, Paper, Conference; Edges}

Output: 

Step 1: communities(topics)

Step 2: Top-k influenced communities

Step 3: Top-k users in each communities

Step 4: Top-k users in networks

Methods: 

Stage 1: LabelRank [[Xie, 2013]]()

Stage 2: cross-community influence [[AAAI2012]](), [[WSDM13]]()

Stage 3: Influence Maximization (IC or AIR) [[ICDM12]]()

Stage 4: improved CCN [[KDD10]]()

