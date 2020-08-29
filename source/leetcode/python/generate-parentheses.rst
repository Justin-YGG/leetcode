======================
22. 括号生成
======================

https://leetcode-cn.com/problems/generate-parentheses/


给出 n 代表生成括号的对数，请你写出一个函数，使其能够生成所有可能的并且有效的括号组合。

例如，给出 n = 3，生成结果为::

    [
      "((()))",
      "(()())",
      "(())()",
      "()(())",
      "()()()"
    ]


--------------------------------------

.. note::

    - 当前左右括号都有大于 0 个可以使用的时候，才产生分支；

    - 产生左分支的时候，只看当前是否还有左括号可以使用；

    - 产生右分支的时候，还受到左分支的限制，右边剩余可以使用的括号数量一定得在严格大于左边剩余的数量的时候，才可以产生分支；

    - 在左边和右边剩余的括号数都等于 0 的时候结算。


.. code:: python

    class Solution(object):
        def generateParenthesis(self, n):
            """
            :type n: int
            :rtype: List[str]
            """
            res = []
            cur = ''

            def dfs(cur, left, right):
                if left == 0 and right == 0:
                    res.append(cur)
                    return

                if right < left:
                    return

                if left > 0:
                    dfs(cur + '(', left - 1, right)
                if right > 0:
                    dfs(cur + ')', left, right - 1)

            dfs(cur, n, n)
            return res
