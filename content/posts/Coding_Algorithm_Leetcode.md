---
title: Algorithm_Leetcode
author: "Misty"
tags: ["Algorithm"]
categories: ["Coding"]
date: 2021-06-11
---

## 1. 两数之和

#### 题目
* https://leetcode-cn.com/problems/two-sum/

#### 解答

```python
class Solution(object):
    def twoSum(self, nums, target):
        n=len(nums)
        for i in range(n):
            for j in range(i+1,n):
                if nums[i]+nums[j]==target:
                    return i,j
```

```python
def twoSum(nums, target):
    hashmap={}
    for ind,num in enumerate(nums):
        hashmap[num] = ind
    for i,num in enumerate(nums):
        j = hashmap.get(target - num)
        if j is not None and i!=j:
            return [i,j]
```