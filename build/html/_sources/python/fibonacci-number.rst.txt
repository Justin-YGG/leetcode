=======================
509. 斐波那契数
=======================

https://leetcode-cn.com/problems/fibonacci-number/

斐波那契数，通常用 F(n) 表示，形成的序列称为斐波那契数列。该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。也就是：
::

    F(0) = 0,   F(1) = 1
    F(N) = F(N - 1) + F(N - 2), 其中 N > 1.

给定 N，计算 F(N)。 

示例 1：
::

    输入：2
    输出：1
    解释：F(2) = F(1) + F(0) = 1 + 0 = 1.

示例 2：
::

    输入：3
    输出：2
    解释：F(3) = F(2) + F(1) = 1 + 1 = 2.

示例 3：
::

    输入：4
    输出：3
    解释：F(4) = F(3) + F(2) = 2 + 1 = 3.
 
提示：

0 ≤ N ≤ 30

---------------------------------

**方法一** 递归 + 记忆化搜索

用字典或者数组将计算过的值存起来，避免重复计算

.. note::

    - 时间复杂度：O(n)
    - 空间复杂度：O(n)

.. code::  python

    class Solution(object):
        def __init__(self):
            self.dic = {0:0 , 1:1}

        def fib(self, N):
            """
            :type N: int
            :rtype: int
            """
            if N not in self.dic:
                self.dic[N] = self.fib(N-1) + self.fib(N-2)
            return self.dic[N]

-------------------------------------

**方法二** 动态规划

据斐波那契数列的状态转移方程，当前状态只和之前的两个状态有关，其实并不需要那么长的一个 DP table 来存储所有的状态，只要想办法存储之前的两个状态就行了。
而通过 Python 的多变量赋值语法，a, b = b , a + b，我们可以一行解决这个问题。

斐波那契数列的例子严格来说不算动态规划，因为没有涉及求最值

**为什么返回的是 a 而不是 b：a 是 0th 个斐波那契数，经过 N 次循环赋值后，a 正好是 nth 个斐波那契数**

.. note::

    - 时间复杂度：O(n)
    - 空间复杂度：O(1)

.. code::  python

    class Solution(object):

        def fib(self, N):
            """
            :type N: int
            :rtype: int
            """
            a, b = 0, 1
            for _ in range(N):
                a, b = b , a + b
            return a
