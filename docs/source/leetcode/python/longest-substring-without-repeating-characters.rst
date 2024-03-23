=============================
3. 无重复字符的最长子串
=============================

https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/

给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1::

    输入: "abcabcbb"
    输出: 3
    解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
    示例 2:

    输入: "bbbbb"
    输出: 1
    解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
    示例 3:

    输入: "pwwkew"
    输出: 3
    解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
         请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。


.. note::

    - 时间复杂度：O(n)
    - 空间复杂度：O(n)


.. code:: python

    class Solution(object):
        def lengthOfLongestSubstring(self, s):
            """
            :type s: str
            :rtype: int
            """
            length = len(s)
            if length == 0:
                return length

            window = {}
            res = 0
            left, right = 0, 0

            while right < length:
                c = s[right]
                window[c] = window.get(c, 0) + 1
                right += 1

                while window[c] > 1:
                    t = s[left]
                    window[t] -= 1
                    left += 1
                res = max(res, right - left)
            return res

