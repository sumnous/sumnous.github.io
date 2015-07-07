---
layout: post
title: "[Leetcode] Edit Distance @Python"
date: 2014-05-10 10:06:08 +0800
comments: true
categories: Leetcode
---
[Problem](http://oj.leetcode.com/problems/edit-distance/)

```python
class Solution:
    # @return an integer
    def minDistance(self, word1, word2):
        len1 = len(word1)
        len2 = len(word2)
        dp = [[0 for j in xrange(len2+1)] for i in xrange(len1 +1)]
        for i in xrange(len1+1):
            dp[i][0] = i
        for j in xrange(len2+1):
            dp[0][j] = j
        for i in xrange(1, len1+1):
            for j in xrange(1, len2+1):
                if word1[i-1] == word2[j-1]:
                    dp[i][j] = dp[i-1][j-1]
                else:
                    dp[i][j] = min(dp[i-1][j-1], dp[i][j-1],dp[i-1][j]) + 1
        return dp[len1][len2]	
```

