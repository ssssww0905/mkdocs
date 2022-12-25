# 剑指 Offer II 004. 

[原题](https://leetcode.cn/problems/WGki4K/description/?favorite=e8X3pBZi)

给你一个整数数组 `nums` ，除某个元素仅出现 **一次** 外，其余每个元素都恰出现 **三次 。**请你找出并返回那个只出现了一次的元素。

## 解法一【哈希表】

!!! note "示例"
    输入：`nums = [0, 1, 0, 1, 0, 1, 99]`
    

    输出：`99`

!!! success "python中的dict用的就是哈希表"

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        num_dict = {}
        for num in nums:
            count = num_dict.get(num)
            if count is None:
                num_dict[num] = 1
            
            elif count == 1:
                num_dict[num] += 1
            
            elif count == 2:
                num_dict.pop(num)
        
        return [key for key in num_dict.keys()][0]
```

## 字典的操作

```python title="The dict() Constructor"
thisdict = dict(name = "John", age = 36, country = "Norway")
print(thisdict)
```



```python title="Check if Key Exists"
for key in thisdict:  # 直接用for循环得到键
	print(key in thisdict)  # 直接用in判断键是否在字典中
```



```python title="Update Dictionary"
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}
thisdict.update({"year": 2020, "new":2022})
# 老的key会更新，新的key会添加
# {'brand': 'Ford', 'model': 'Mustang', 'year': 2020, 'new': 2022}
```



| Method                        | Description                                                  |
| :---------------------------- | :----------------------------------------------------------- |
| clear()                       | Removes all the elements from the dictionary                 |
| copy()                        | Returns a copy of the dictionary                             |
| fromkeys()                    | Returns a dictionary with the specified keys and value       |
| get(key, default=None)        | Returns the value of the specified key                       |
| items()                       | Returns a list containing a tuple for each key value pair    |
| keys()                        | Returns a list containing the dictionary's keys              |
| pop()                         | Removes the element with the specified key                   |
| popitem()                     | Removes the last inserted key-value pair                     |
| setdefault(key, default=None) | Returns the value of the specified key. <br />If the key does not exist: insert the key, with the specified value |
| update()                      | Updates the dictionary with the specified key-value pairs    |
| values()                      | Returns a list of all the values in the dictionary           |
