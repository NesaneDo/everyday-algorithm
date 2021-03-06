> 解法一：根据性质

```shell
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

杨辉三角肉眼可见的特性有：数组两头都是 1，中间数字是其上一行肩上两数之和，即：f\[i\]\[j\] = f\[i-1][j-1] + f\[i-1][j]，而 f\[0][0] = 1, f\[1][0] = 1, f\[1][1]=1, 则状态转移方程可为：
$$
f[i][j]=\begin{cases}1,\quad i,j=0 \quad 或 \quad i,j=1
\\ f[i-1][j-1] + f[i-1][j],\quad i>1\end{cases}
$$




> **补充：杨辉三角特性**

1. 每行数字左右对称，由 1 开始逐渐变大再变小，并最终回到 1。

2. 第 n 行（从 0 开始编号）的数字有 n+1 项，前 n 行共有 $\frac{n(n+1)}{2}$ 个数。

3. 第 n 行的第 m 个数（从 0 开始编号）可表示为可以被表示为组合数 $C(n,m)$, 记作 $C^m_n$ 或 $(^n_m)$, 即为从 n 个不同元素中取 m 个元素的组合数。我们可以用公式来表示它：$C^m_n=\frac{n!}{m!\times(n-m)!}$

4. 每个数字等于上一行的左右两个数字之和，可用此性质写出整个杨辉三角。即第 n 行的第 i 个数等于第 n-1 行的第 i-1 个数和第 i 个数之和。这也是组合数的性质之一，即 $C^i_n=C^i_{n-1}+C^{i-1}_{n-1}$。

5. ${(a+b)^n}$ 的展开式（二项式展开）中的各项系数依次对应杨辉三角的第 n 行中的第一项。

   



> 作者：LeetCode-Solution
> 链接：https://leetcode-cn.com/problems/pascals-triangle/solution/yang-hui-san-jiao-by-leetcode-solution-lew9/
> 来源：力扣（LeetCode）
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。