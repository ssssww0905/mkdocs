# 剑指 Offer II 005. 

[原题](https://leetcode.cn/problems/aseY1I/?favorite=e8X3pBZi)

给定一个字符串数组 `words`，请计算当两个字符串 `words[i]` 和 `words[j]` 不包含相同字符时，它们长度的乘积的最大值。假设字符串中只包含英语的小写字母。如果没有不包含相同字符的一对字符串，返回 0。

## 解法1【位运算】

```python
class Solution:
    def maxProduct(self, words: List[str]) -> int:
        # 1. 制作掩码
        # 2. 遍历掩码【内循环】
        max_product = 0
        mask_list = []
        for t, word in enumerate(words):
            length = len(word)
            mask_t = 0
            # 若单词长度>26，遍历[a~z]
            if length > 26:
                for i in range(26):
                    mask_t |= int(chr(ord("a") + i) in word) << i
            # 若单词长度<=26，遍历单词的每个字母 
            else:
                for s in word:
                    mask_t |= 1 << ord(s) - ord("a")
            
            mask_list.append(mask_t)
            
            # 内循环，用&判断是否包含相同字符
            for j in range(t):
                if mask_list[j] & mask_t == 0:
                    max_product = max(len(words[t]) * len(words[j]), max_product)

        return max_product
```



思路：

1. 26个字母，给`word`编码，记录`[a~z]`是否出现在`word`中
1. 制作掩码时，用`|`，例如单词`foo`
1. 判断掩码是否相交时，判断`mask_1 & mask_2 == 0`



!!! bug  "难点：python 的位运算"
    > 在进行位运算时，无需转换为二进制，只要使用位运算符，python就会按照二进制来进行计算。



```python title="& |"
a, b = 5, 4

print(f"{a:b} & {b:b} = {(a&b):b}")
print(f"{a:b} | {b:b} = {(a|b):b}")
```



| Operator | Name                 | Description                                                  |
| :------- | :------------------- | :----------------------------------------------------------- |
| &        | AND                  | Sets each bit to 1 if both bits are 1                        |
| \|       | OR                   | Sets each bit to 1 if one of two bits is 1                   |
| ^        | XOR                  | Sets each bit to 1 if only one of two bits is 1              |
| ~        | NOT                  | Inverts all the bits                                         |
| <<       | Zero fill left shift | Shift left by pushing zeros in from the right and let the leftmost bits fall off |
| >>       | Signed right shift   | Shift right by pushing copies of the leftmost bit in from the left, and let the rightmost bits fall off |

| Operator | Example | Same As    |
| :------- | :------ | :--------- |
| &=       | x &= 3  | x = x & 3  |
| \|=      | x \|= 3 | x = x \| 3 |
| ^=       | x ^= 3  | x = x ^ 3  |
| >>=      | x >>= 3 | x = x >> 3 |
| <<=      | x <<= 3 | x = x << 3 |