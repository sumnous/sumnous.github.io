---
layout: post
title: "随机数生成函数面试题"
date: 2014-05-13 16:10:28 +0800
comments: true
categories: 面试
---

前阵子去某公司笔试，有道题是

> 已知随机数生成函数f()，返回0的概率是60%，返回1的概率是40%。根据f()求随机数函数g()，使返回0和1的概率是50%，不能用已有的随机生成库函数。

分析：

调用f()两次即可，会出现4种结果(0,0), (0,1), (1,0), (1,1)，其中出现(0,1), (1,0)的概率是一样的，可以构造出等概率事件，比如出现(0,1)可返回0，出现(1,0)可返回1，如果出现其他两种情况则舍掉重新调用。

代码如下：

```python
def g():
    while(true):
        a = f()
        b = f()
        if [a,b] == [0,1]:
            return 0
        if [a,b] == [1,0]:
            return 1
```

这道笔试题到此为止。

接下来扩展一下，*如何实现这个随机数生成函数f()，可用random()，也就是以指定概率获取元素*。《Python Cookbook》中有此示例。分析一下，也就是在(0, 0.6]区间内取0，在(0.6, 1]区间内取1。扩展到多个数也一样。

<!--more-->

```
def withProbRandomPick(probList):
    import random
    import sys
    r, s = random.random(), 0
    for num in probList:
        s += num[1]
    	if s >= r:
    	    return num[0]
    print >> sys.stderr, "Error: shouldn't get here"
```

验证一下：

```
probList = [[0, 0.6], [1, 0.4]]
import collections
count = collections.defaultdict(int)
for i in xrange(10000):
    count[withProbRandomPick(probList)] += 1
for n in count:
    print n, count[n] / 10000.0
```

得到的结果是：

```
0 0.5953
1 0.4047
```

《程序员面试金典第5版》(Cracking the Coding Interview)中也有一道给定一个随机数函数生成另一个随机数函数的题目。

> 给定rand5()，实现一个方法rand7()。也即，给定一个产生0到4（含）随机数方法，编写一个产生0到6（含）随机数的方法。（第105页）

分析：随机数函数的关键是确保产生每一个数的的概率相等。我们可用通过5 * rand5() + rand5()产生[0:24]，舍弃[21:24]，最后除以7取余数，则可得到概率相等的[0:6]的数值。

```
def rand7():
    while(true):
        num = 5 * rand5() + rand5()
        if num < 21:
            return num % 7
```

变形一下，给定rand7()，如何实现rand5()？


