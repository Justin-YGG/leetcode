=========================
5. 最长回文子串
=========================

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

示例 1：

输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。
示例 2：

输入: "cbbd"
输出: "bb"

暴力

.. code:: python

    class Solution(object):
        def longestPalindrome(self, s):
            """
            :type s: str
            :rtype: str
            """
            size = len(s)
            if size < 1:
                return s

            max_len = 1
            res = s[0]

            for i in range(size-1):
                for j in range(i+1, size):
                    if  j - i + 1  > max_len and self.is_valid(s, i, j):
                        max_len =  j - i + 1
                        res = s[i:j+1]
            return res

        def is_valid(self, s, left, right):
            while left < right:
                if s[left] != s[right]:
                    return False
                left += 1
                right -= 1
            return True


.. code:: python

    class Solution(object):
        def longestPalindrome(self, s):
            """
            :type s: str
            :rtype: str
            """
            size = len(s)
            if size < 1:
                return s

            max_len = 1
            res = s[0]

            for i in range(size):
                odd, odd_len = self.spread_from_center(s, i, i)
                even, even_len = self.spread_from_center(s, i, i+1)
                max_sub = odd if odd_len > even_len else even
                if len(max_sub) > max_len:
                    max_len = len(max_sub)
                    res = max_sub
            return res

        def spread_from_center(self, s, left, right):
            if not s or left > right:
                return '', 0
            while left >= 0 and right < len(s) and s[left] == s[right]:
                left -= 1
                right += 1
            return s[left+1:right], right - left - 1
