====================
322. 零钱兑换
====================

https://leetcode-cn.com/problems/coin-change/

给定不同面额的硬币 coins 和一个总金额 amount。

编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。

示例 1:
::

    输入: coins = [1, 2, 5], amount = 11
    输出: 3
    解释: 11 = 5 + 5 + 1

示例 2:
::

    输入: coins = [2], amount = 3
    输出: -1

说明:
你可以认为每种硬币的数量是无限的。

------------------------------------------

- dp[i] 代表要凑到金额 i 所需的最少【硬币数】
- 要求凑到金额 i 的最少硬币数，如果知道凑出 amount = i-1 的最少硬币数（子问题），你只需要把子问题的答案加一（再选一枚面值为 1 的硬币）就能得到凑成金额 i 的最少硬币数; dp 公式： ``dp[i] = min(dp[i], dp[i-coin]+1)`` ，此处 **+1** 的含义是指 **数量** ，因为你选取了一个面值的硬币，所以硬币数加1，要和上面 **加一** 做区别，不要混淆；因为我们的 coins 里面 有可能是 ``[2, 3, 5]`` , 最后选取的不一定是面值为 1 的硬币。
- base case：金额未 0 时，显然 dp[0] = 0

初始化 dp table 的值都为 amount + 1，因为最坏的情况是都选面值为 1 的硬币(有的话)，所以 amount + 1 等价于正无穷，便于在遍历时获取最小值。

因为我们最终要获得 dp[amount] 的值，所以遍历区间为 [1, amount+1)

.. note::

    - 时间复杂度：O(n)。
    - 空间复杂度：O(n)。

-------------------------------------------------------

.. code:: python

    class Solution(object):
        def coinChange(self, coins, amount):
            """
            :type coins: List[int]
            :type amount: int
            :rtype: int
            """
            dp = [amount+1] * (amount + 1)
            dp[0] = 0
            for i in range(1, amount+1):
                for coin in coins:
                    if i - coin < 0:
                        continue
                    else:
                        dp[i] = min(dp[i], dp[i-coin] + 1)
            return dp[amount] if dp[amount] != amount + 1 else -1

--------------------------------------------------------

- 遍历起始值 ``min(coins)`` 可以提升一些性能
- 代码简化

.. code:: python

    class Solution(object):
        def coinChange(self, coins, amount):
            """
            :type coins: List[int]
            :type amount: int
            :rtype: int
            """
            dp = [0] + [amount+1] * amount
            for i in range(min(coins), amount+1):
                dp[i] = min([dp[i-c] for c in coins if i - c >= 0]) + 1
            return dp[amount] if dp[amount] <= amount else -1

-----------------------------------------------

.. code:: python

    class Solution(object):
        def coinChange(self, coins, amount):
            """
            :type coins: List[int]
            :type amount: int
            :rtype: int
            """
            memo = dict()
            def dp(n):
                if n == 0:
                    return 0
                if n < 0:
                    return -1

                if n in memo:
                    return memo[n]

                res = float('inf')
                for c in coins:
                    sub = dp(n-c)
                    if sub == -1:
                        continue
                    res = min(res, sub+1)
                memo[n] = res if res != float('inf') else -1
                return memo[n]
            return dp(amount)