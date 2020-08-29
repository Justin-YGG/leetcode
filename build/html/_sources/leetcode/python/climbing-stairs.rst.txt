=============
70. 爬楼梯
=============

https://leetcode-cn.com/problems/climbing-stairs/

假设你正在爬楼梯。需要 n 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

注意：给定 n 是一个正整数。

示例 1：
::

    输入： 2
    输出： 2

解释： 有两种方法可以爬到楼顶。

1. 1 阶 + 1 阶
#. 2 阶

示例 2：
::

    输入： 3
    输出： 3

解释： 有三种方法可以爬到楼顶。

1. 1 阶 + 1 阶 + 1 阶
#. 1 阶 + 2 阶
#. 2 阶 + 1 阶

------------------------

通过树形结构尝试画出 n 阶（比如4）的各种情况，发现从 n=3 开始
f(n) = f(n-1) + f(n-2)

所以采用递归的方式，不过要注意过程中存在的重复计算，所以采用记忆化递归，保存计算过的值，以提高效率

.. note::

    - 时间复杂度：O(n)，树形递归的大小可以达到 n。
    - 空间复杂度：O(n)，递归树的深度可以达到 n。

------------------------

**递归 + 备忘录**

.. code::  python

    class Solution(object):
        def __init__(self):
            self.dic = {1: 1, 2:2}

        def climbStairs(self, n):
            """
            :type n: int
            :rtype: int
            """
            if n not in self.dic:
                self.dic[n] = self.climbStairs(n-1) + self.climbStairs(n-2)
            return self.dic[n]

-------------------------

**动态规划**

- dp[i] 代表跳到 n 阶台阶总共有几种方法
- 跳到 n 阶台阶有两种方法，从 n 阶台阶的前一个跳上来，或者从 n 阶台阶的前两个跳上来，所以递推公式是：``dp[i] = dp[i-1] + dp[i-2]``
- base case: dp[1] = 1, dp[2] = 2

.. note::

    - 时间复杂度：O(n)。
    - 空间复杂度：O(n)。

--------------------------

.. code:: python

    class Solution(object):
        def climbStairs(self, n):
            """
            :type n: int
            :rtype: int
            """
            if n <= 2:
                return n
            dp = [0] * (n+1)
            dp[1] = 1
            dp[2] = 2
            for i in range(3, n+1):
                dp[i] = dp[i-2] + dp[i-1]
            return dp[n]
