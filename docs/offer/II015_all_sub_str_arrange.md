# 剑指 Offer II 015. 

[原题](https://leetcode.cn/problems/VabMRr/description/?favorite=e8X3pBZi)

给定两个字符串 `s` 和 `p`，找到 `s` 中所有 `p` 的 **变位词** 的子串，返回这些子串的起始索引。不考虑答案输出的顺序。

**变位词** 指字母相同，但排列不同的字符串。

```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        ans = []
        p_length = len(p)
        s_length = len(s)
        if p_length > s_length:
            return ans
        
        # 1. 遍历完整 for i in range(p_length, s_length)
        # 2. 维护两个dict
        p_dict = {chr(ord("a")+i):0 for i in range(26)}
        s_dict = {chr(ord("a")+i):0 for i in range(26)}
        for i in range(p_length):
            p_dict[p[i]] += 1
            s_dict[s[i]] += 1
        
        if p_dict == s_dict:
            ans.append(0)
        
        for i in range(p_length, s_length):
            s_dict[s[i - p_length]] -= 1
            s_dict[s[i]] += 1
            if p_dict == s_dict:
                ans.append(i-p_length+1)
        
        return ans
```

思路：与[II014](II014_sub_str_arrange.md)相似