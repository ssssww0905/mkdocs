# 剑指 Offer II 014. 

[原题](https://leetcode.cn/problems/MPnaiL/description/?favorite=e8X3pBZi)

给定两个字符串 `s1` 和 `s2`，写一个函数来判断 `s2` 是否包含 `s1` 的某个变位词。

换句话说，第一个字符串的排列之一是第二个字符串的 **子串** 。

!!! note "注意：`s1`的排列之一都可以"
    因此需要判断的是该长度的子串各字母出现的次数是否相同

## 解法1【滑动窗口】

```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        l1 = len(s1)
        l2 = len(s2)
        if l1 > l2:
            return False
        
        # 1. s1的长度l1是固定的
        # 2. 判断s2[i]结尾的l1长的字符串中字母出现的次数是否相同
        # 3. 维护一个长度为26的字典用以记录每个单词出现的次数
        s1_dict = {chr(ord("a")+i):0 for i in range(26)}
        s2_dict = {chr(ord("a")+i):0 for i in range(26)}
        for i in range(l1):
            s1_dict[s1[i]] += 1
            s2_dict[s2[i]] += 1
        if s1_dict == s2_dict:
            return True
        for i in range(l1, l2):
            s2_dict[s2[i-l1]] -= 1
            s2_dict[s2[i]] += 1
            if s1_dict == s2_dict:
                return True
        return False
```

## 