# 剑指 Offer II 010. 

[原题](https://leetcode.cn/problems/QTMn0o/?favorite=e8X3pBZi)

给定一个整数数组和一个整数 `k` **，**请找到该数组中和为 `k` 的连续子数组的个数。

## 解法1【超出时间限制】

```python title="枚举"
# python太慢了【72/89】
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        count = 0
        length = len(nums)

        # 以i为结束下标
        for i in range(length):
            s = 0
            for j in range(i, -1, -1):
                s += nums[j]
                count += (s==k)                    
        
        return count
        
```

```C++
// C++ 【86/89】
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int count = 0;
        for(int i=0; i<nums.size(); i++) {
            int s = 0;
            for(int j=i; j>=0; j--) {
                s += nums[j];
                if(s==k) {
                    count++;
                }
            }
        }
        return count;
    }
};
```

思路：

1. 暴力求解，遍历 $O(N^2)$

## 解法2【哈希】

思路：

1. 记录`pre_i = sum([0,...,num_i])`
2. `sum([num_j,...num_i])=pre_i - pre_{j-1}`
3. 统计`pre_{j-1}=pre_i - k`的数量
4. 细节：考虑以`i`为结尾的子数列->保证`pre_j`已存在【内循环】

```python title="哈希"
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        count = 0
        pre_sum = 0
        pre_count_dict = {pre_sum:1}
        for i in range(0, len(nums)):
            pre_sum += nums[i]
            count += pre_count_dict.get(pre_sum - k, 0)
            # 注意先计算count再更新dict
            pre_count_dict[pre_sum] = 1 + pre_count_dict.get(pre_sum, 0)
        
        return count        
```

