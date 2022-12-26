# 剑指 Offer II 013. 

[原题](https://leetcode.cn/problems/O4NDxx/?favorite=e8X3pBZi)

给定一个二维矩阵 `matrix`，以下类型的多个请求：

- 计算其子矩形范围内元素的总和，该子矩阵的左上角为 `(row1, col1)` ，右下角为 `(row2, col2)` 。

实现 `NumMatrix` 类：

- `NumMatrix(int[][] matrix)` 给定整数矩阵 `matrix` 进行初始化
- `int sumRegion(int row1, int col1, int row2, int col2)` 返回左上角 `(row1, col1)` 、右下角 `(row2, col2)` 的子矩阵的元素总和。



## 解法1【超出时间限制】

```python
class NumMatrix:

    def __init__(self, matrix: List[List[int]]):
        self.matrix = matrix


    def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:
        ans = 0
        for row in range(row1, row2+1):
            for col in range(col1, col2+1):
                ans += self.matrix[row][col]
        
        return ans
```

思路：暴力两层遍历

!!! note "注意提示" 
    最多调用 `104` 次 `sumRegion` 方法

## 解法2【前缀和】

```python title="1维前缀和"
class NumMatrix:

    def __init__(self, matrix: List[List[int]]):
        # self.matrix = matrix  # 没必要保存matrix 
        rows = len(matrix)
        cols = len(matrix[0])

        # 前缀和注意 rows + 1
        self.sum_matrix = [[0]*(cols+1) for _ in range(rows)]
        for row in range(rows):
            for col in range(1, cols+1):
                self.sum_matrix[row][col] = self.sum_matrix[row][col-1] + matrix[row][col-1]
    

    def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:
        ans = 0
        for row in range(row1, row2+1):
            ans += self.sum_matrix[row][col2+1] - self.sum_matrix[row][col1]
        
        return ans

      
# Your NumMatrix object will be instantiated and called as such:
# obj = NumMatrix(matrix)
# param_1 = obj.sumRegion(row1,col1,row2,col2)
```



- [ ] 二维前缀和