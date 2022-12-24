# 剑指 Offer II 007. 数组中和为 0 的三个数

给你一个整数数组 `nums` ，判断是否存在三元组 `[nums[i], nums[j], nums[k]]` 满足 `i != j`、`i != k` 且 `j != k` ，同时还满足 `nums[i] + nums[j] + nums[k] == 0` 。请

你返回所有和为 `0` 且不重复的三元组。

**注意：**答案中不可以包含重复的三元组。

## 解法1【超出时间限制】

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        # 1. 注意唯一性
        # 2. 如何少遍历
        # 3. c = - a - b
        max_min_dict = {}
        l = len(nums)
        for i, a in enumerate(nums):
            for j in range(i+1, l-1):
                for k in range(j+1, l):
                    if a + nums[j] + nums[k] == 0:
                        max_ = max(a, nums[j], nums[k])
                        min_ = min(a, nums[j], nums[k])
                        if max_min_dict.get(max_):
                            if min_ in max_min_dict.get(max_):
                                continue
                            max_min_dict[max_] += [min_]
                        else:
                            max_min_dict[max_] = [min_]
        
        return [[k, vv, -k-vv] for k, v in max_min_dict.items() for vv in v]
```

思路：解法1的思路比较暴力

1. 没有对列表进行预处理【**即排序**】
2. 用字典保存最大和最小来保证唯一性
3. 由于无序，整体的复杂度为$O(N^3)$.



## 解法2【排序+双指针】

逻辑：

1. 三个数中的两个数字确定后，第三个数字也由之确定
2. 将数字从小到大排列，第一个数字大于0一定不存在解
3. 当第一个数字固定后，**若第二个数字变大，第三个数字一定变小**
4. 对于有序的列表，防止重复的方法就是判断是否与上一个值相同

!!! note "例`[-1, -1, 0, 0, 0, 1, 1, 2]`"

    * `i=0, a=-1`,
      * `j=1, b=-1`,
        * `k=7, c=2`,找到了就可以增大`j`
      * `j=2, b=0`,
        * `k=6, c=1`
        * `k=5, c=1`
        * `k=4, c=0`,找到了就可以增大`j`
      * `j=3, b=0`
      * `j=4, b=0`
        * `j == k`,可以break该循环了 

```python
# 双指针的逻辑：两个指针可以夹逼列表
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        # 对原始列表进行排序
        # 默认升序
        nums.sort()

        length = len(nums)
        res_list = []

        for i in range(0, length-2):
            # 若最小的数字与上一次相同 -> 重复/无解
            if i > 0 and nums[i] == nums[i-1]:
                continue
            # 若最小的数字大于0 -> 无解
            if nums[i] > 0:
                break
            
            k = length - 1
            for j in range(i+1, length-1):
                # 若第二个数字与上一次相同 -> 重复/无解
                if j > i + 1 and  nums[j] == nums[j-1]:
                    continue
                
                # 在没有找到之前，只移动第三个数字
                # 第三个数字太大就往前移动
                while (j < k) and (nums[i] + nums[j] + nums[k] > 0):
                    k -= 1
                
                # 移动完之后若j>=k则没有找到
                # 并且再增大j也不会再找到和为0的三个数
                if j == k :
                    break
                
                if nums[i] + nums[j] + nums[k] == 0:
                    res_list.append([nums[i], nums[j], nums[k]])

        return res_list
```

