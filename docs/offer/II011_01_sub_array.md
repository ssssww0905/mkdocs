# 剑指 Offer II 011. 

[原题](https://leetcode.cn/problems/A1NYOS/description/)

给定一个二进制数组 `nums` , 找到含有相同数量的 `0` 和 `1` 的最长连续子数组，并返回该子数组的长度。

 ## 解法1【超出时间限制】

```python
# 没有用哈希表->慢
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        # 1. count0[i]记录[0,...,i]中有多少个零
        # 2. count0[i] - count0[j-1]记录[j,...,i]中有多少个0
        # 3. 寻找满足 2*(count0[i] - count0[j-1]) == i-j+1
        count0 = 0
        count0_list = [count0]
        max_length = 0
        for i in range(len(nums)):
            count0 += int(nums[i] == 0)
            for j in range(i-1, -1, -2):
                if 2 * (count0 - count0_list[j]) == i - j + 1:
                    max_length = max(max_length, i - j + 1)
            count0_list.append(count0)
        return max_length
```

## 解法2【哈希】

```python
# 将01个数的比较转化为sum+-
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        # 1. sum02i[i]记录[0,...,i]中#0 -#1
        # 2. sum02i_minj_dict记录最小的j <-> 保证最长
        sum02i = 0
        sum02i_minj_dict = {0:-1}
        max_length = 0
        for i in range(len(nums)):
            if nums[i] == 0:
                sum02i += 1
            else:
                sum02i -= 1
            
            if sum02i in sum02i_minj_dict:
                max_length = max(max_length, i - sum02i_minj_dict[sum02i])
            else:
                sum02i_minj_dict[sum02i] = i
        return max_length
```

思路：

1. 与[II010](II010_sub_array_sum_k.md)类似：哈希表+内循环
2. 考虑最长的子数组 <-> 记录最小的j
