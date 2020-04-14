========================
76. 最小覆盖子串
========================

https://leetcode-cn.com/problems/minimum-window-substring/

给你一个字符串 S、一个字符串 T，请在字符串 S 里面找出：包含 T 所有字母的最小子串。

示例::

    输入: S = "ADOBECODEBANC", T = "ABC"
    输出: "BANC"

说明::

    如果 S 中不存这样的子串，则返回空字符串 ""。
    如果 S 中存在这样的子串，我们保证它是唯一的答案。


.. code:: python

    class Solution(object):
        def minWindow(self, s, t):
            """
            :type s: str
            :type t: str
            :rtype: str
            """
            left = right = 0
            start = 0
            match = 0
            min_len = float('inf')
            length_s = len(s)
            window = {}
            needs = {}

            for i in t:
                needs[i] = needs.get(i, 0) + 1

            while right < length_s:
                c = s[right]
                if c in needs:
                    window[c] = window.get(c, 0) + 1
                    if window[c] == needs[c]:
                        match += 1
                right += 1

                while len(needs) == match:
                    if right - left < min_len:
                        start = left
                        min_len = right - left
                    t = s[left]
                    if t in needs:
                        window[t] -= 1
                        if window[t] < needs[t]:
                            match -= 1
                    left += 1

            return '' if min_len == float('inf') else s[start:start+min_len]
