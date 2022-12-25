# 剑指 Offer II 009. 

[原题](https://leetcode.cn/problems/ZVAVXX/description/?favorite=e8X3pBZi)

## 解法1【滑动窗口】

```python title="滑动窗口"
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        # 特殊情况判断
        if k <= 0:
            return 0
        
        length = len(nums)
        if length == 0:
            return 0
        
        count = 0

        # 找到以start为首的乘积小于k的最长子数组
        # 然后count += 子数组的长度
        p = nums[0]
        for start in range(0, length):
            if start == 0:
                end = start
                
            else:
                p /= nums[start-1]
            
            while end < length - 1 and p < k:
                    end += 1
                    p *= nums[end]
            
            if p < k:
                count += end - start + 1
            elif p / nums[end] < k:
                count += end - start


        return count
```

思路：

1. 与[II 008](II008_shortest_sum_geq_target.md)相同的滑动窗口的思路
