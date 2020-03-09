===============
72. 编辑距离
===============

https://leetcode-cn.com/problems/edit-distance/

给定两个单词 word1 和 word2，计算出将 word1 转换成 word2 所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

插入一个字符
删除一个字符
替换一个字符

示例 1:
::

    输入: word1 = "horse", word2 = "ros"
    输出: 3
    解释:
    horse -> rorse (将 'h' 替换为 'r')
    rorse -> rose (删除 'r')
    rose -> ros (删除 'e')

示例 2:
::

    输入: word1 = "intention", word2 = "execution"
    输出: 5
    解释:
    intention -> inention (删除 't')
    inention -> enention (将 'i' 替换为 'e')
    enention -> exention (将 'n' 替换为 'x')
    exention -> exection (将 'n' 替换为 'c')
    exection -> execution (插入 'u')

------------------------------

- dp[i][j] 代表 word1[0..i] 和 word2[0..j] 的最小编辑【距离】
- 要算出 dp[i][j]，有四种情况，从四种情况中选择最优解(最小编辑距离)

    + dp[i][j] = dp[i][j-1] + 1  # 敌动我不动，招安一名敌军(插入)
    + dp[i][j] = dp[i-1][j] + 1  # 我军叛变，斩杀一名本军(删除)
    + dp[i][j] = dp[i-1][j-1]+int(word1[i] != word2[j])  # 当前对阵士兵是孪生兄弟，直接忽略(skip)；亦或是，敌我双方都觉得当前对阵的对方士兵比较厉害，相互交换(互换)
- dp[..][0] 和 dp[0][..] 对应 base case

    + 第一行中，dp[0][i]dp[0][i]表示空字符""""到word2[0,...,i]word2[0,...,i]   需要编辑几次，易知空字符需要执行ii次插入操作才能得到。因此，dp[0][i]=idp[0][i]=i。
    + 第一列中，dp[i][0]dp[i][0]表示word[0,...,i]word[0,...,i]到空字符的编辑距离，易知word[0,...,i]word[0,...,i]需要执行ii次删除操作才能得到空字符。因此，dp[i][0]=idp[i][0]=i

.. note::

    - 时间复杂度：O(m*n)
    - 空间复杂度：O(m*n)

.. todo::
    优化空间复杂度为 O(n)

------------------------------

.. code:: python

    class Solution(object):
        def minDistance(self, word1, word2):
            """
            :type word1: str
            :type word2: str
            :rtype: int
            """
            length1, length2 = len(word1)+1, len(word2)+1
            dp = [[0] * length2 for _ in range(length1)]
            for i in range(length1):
                dp[i][0] = i
            for j in range(length2):
                dp[0][j] = j

            for i in range(1, length1):
                for j in range(1, length2):
                    dp[i][j] = min(
                        dp[i-1][j] + 1,
                        dp[i][j-1] + 1,
                        dp[i-1][j-1] + int(word1[i-1] != word2[j-1])
                    )
            return dp[-1][-1]

