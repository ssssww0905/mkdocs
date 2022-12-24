# 剑指 Offer II 008. 

[原题](https://leetcode.cn/problems/2VG8Kg/?favorite=e8X3pBZi)

给定一个含有 `n` 个正整数的数组和一个正整数 `target` **。**

找出该数组中满足其和 `≥ target` 的长度最小的 **连续子数组** `[numsl, numsl+1, ..., numsr-1, numsr]` ，并返回其长度**。**如果不存在符合条件的子数组，返回 `0` 。

## 解法1【超出时间限制】

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        length = len(nums)
        shortest_len = length + 1
        for i in range(0, length):
            j = i
            s = nums[i]
            while (j < length-1) and (s < target):
                j += 1
                s += nums[j]
            if s >= target and j - i + 1 < shortest_len:
                shortest_len = j - i + 1
        
        return shortest_len if shortest_len <= length else 0
```

思路：暴力，遍历

1. 线性遍历列表，记录以`nums[i]`为首元素的`sum>=target`的最短长度
2. **缺点：没有任何判断**

## 解法2【滑动窗口】

!!! note "例`[4, 1, 1, 1, 1, 5, 4, 1, 2], target=7`"

	* 如果首元素`a<=0`，一定不包含`a`得到的长度更短
	* *虽然这道题目已经限定了元素都是正整数*
     * `i=0,j=4,[4, 1, 1, 1, 1]`是以`4`为首且满足条件的最短子列，`s=j-i+1=5`
     * `i=1,j=4->5,[1, 1, 1, 1, 5]`是以`1`为首且满足条件的最短子列，`s=j-i+1=5`
     * `i=2,j=5,[1, 1, 1, 5]`是以`1`为首且满足条件的最短子列，`s=j-i+1=4`
     * `i=3,j=5->6,[1, 1, 5, 4]`是以`1`为首且满足条件的最短子列，`s=j-i+1=4`
     * `i=4,j=6,[1, 5, 4]`以`1`为首且满足条件的最短子列，`s=j-i+1=3`
     * `i=5,j=6,[5, 4]`以`5`为首且满足条件的最短子列，`s=j-i+1=2`
     * ...

```python title="滑动窗口"
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        length = len(nums)
        # 特殊情形判断
        if length == 0:
            return 0
          
       	# 按照上面的方法来进行判断
        shortest = length + 1
        sum_ = nums[0]
        for start in range(0, length):
            if start == 0:
                end = start
                while end < length - 1 and sum_ < target:
                    end += 1
                    sum_ += nums[end]
                    
            else:
                sum_ -= nums[start-1]
                while end < length - 1 and sum_ < target:
                    end += 1
                    sum_ += nums[end]
                    
            if sum_ >= target and (end - start + 1) < shortest:
                shortest = end - start + 1
        
        return shortest if shortest <= length else 0


            
```



