---
layout: post
title: "[Leetcode] Valid Parentheses @Python"
date: 2014-05-10 14:21:48 +0800
comments: true
categories: Leetcode
---
[Problem](http://oj.leetcode.com/problems/valid-parentheses/)

```python
class Solution:
    # @return a boolean
    def isValid(self, s):
        if s == '':
            return True
        left = '([{'
        right = ')]}'
        stack = []
        for i in s:
            if i == '(' or i == '[' or i == '{':
                stack.append(i)
                continue
            for j in xrange(3):
                if i == right[j]:
                    if not stack or stack[-1] != left[j]:
                        return False
                    else:
                        stack.pop()
                        continue
        return not stack
# test
s = Solution()
print s.isValid('()')
```

