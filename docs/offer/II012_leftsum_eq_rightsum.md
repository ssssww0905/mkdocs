# 剑指 Offer II 012. 

[原题](https://leetcode.cn/problems/tvdfij/description/)

给你一个整数数组 `nums` ，请计算数组的 **中心下标** 。

数组 **中心下标** 是数组的一个下标，其左侧所有元素相加的和等于右侧所有元素相加的和。

如果中心下标位于数组最左端，那么左侧数之和视为 `0` ，因为在下标的左侧不存在元素。这一点对于中心下标位于数组最右端同样适用。

如果数组有多个中心下标，应该返回 **最靠近左边** 的那一个。如果数组不存在中心下标，返回 `-1` 。

```python
class Solution:
    def pivotIndex(self, nums: List[int]) -> int:
        # 1. ls = sum([0,...,i-1])
        # 2. rs = sum([i+1, ..., len-1])
        # 3. ls + rs + nums[i] = SUM
        ans = -1
        lsum = 0
        allsum = sum(nums)
        for i, num in enumerate(nums):
            if 2 * lsum + num == allsum:
                ans = i
                return ans
            lsum += num
        return ans
```

