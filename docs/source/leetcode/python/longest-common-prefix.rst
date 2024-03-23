===================
14. 最长公共前缀
===================

https://leetcode-cn.com/problems/longest-common-prefix/

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

示例 1::

    输入: ["flower","flow","flight"]
    输出: "fl"
    示例 2:

    输入: ["dog","racecar","car"]
    输出: ""
    解释: 输入不存在公共前缀。

说明::

    所有输入只包含小写字母 a-z 。


.. code:: python

    class Solution(object):
        def longestCommonPrefix(self, strs):
            """
            :type strs: List[str]
            :rtype: str
            """
            if not strs:
                return ''

            base = strs[0]
            for i in range(1, len(strs)):
                j = k = 0
                while j < len(strs[i]) and k < len(base):
                    if strs[i][j] != base[k]:
                        break
                    j += 1
                    k += 1
                base = base[:k]
                if base == '':
                    return base
            return base


