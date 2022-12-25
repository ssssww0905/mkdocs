# 剑指 Offer II 006.

[原题](https://leetcode.cn/problems/kLl5u1/description/?favorite=e8X3pBZi)

给定一个已按照 **升序排列** 的整数数组 `numbers` ，请你从数组中找出两个数满足相加之和等于目标数 `target` 。

函数应该以长度为 `2` 的整数数组的形式返回这两个数的下标值*。*`numbers` 的下标 **从 0 开始计数** ，所以答案数组应当满足 `0 <= answer[0] < answer[1] < numbers.length` 。

假设数组中存在且只存在一对符合条件的数字，同时一个数字不能使用两次。

## 解法1【排序+双指针】

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        # 1. 第一个数增大 -> 第二个减少
        # 2. 第一个下标变大 -> 第二个下标减少
        length = len(numbers)
        
        end = length - 1
        for start in range(0, length-1):
            # 升序数组的逻辑
            while (start < end) and numbers[start] + numbers[end] > target:
                end -= 1

            # 同一个数字不能出现两次
            if start == end:
                break
            
            if numbers[start] + numbers[end] == target:
                return [start, end]
        
        return None
```

思路：与[II007](II007_three_sum_zero.md)逻辑一致