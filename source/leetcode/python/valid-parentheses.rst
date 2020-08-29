=======================
20. 有效的括号
=======================

https://leetcode-cn.com/problems/valid-parentheses/

给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

- 左括号必须用相同类型的右括号闭合。
- 左括号必须以正确的顺序闭合。
- 注意空字符串可被认为是有效字符串。

示例 1:
::

    输入: "()"
    输出: true

示例 2:
::

    输入: "()[]{}"
    输出: true

示例 3:
::

    输入: "(]"
    输出: false

示例 4:
::

    输入: "([)]"
    输出: false

示例 5:
::

    输入: "{[]}"
    输出: true

----------------------------------

提供一个左右括号的哈希表，遇到“左”括号就入栈，遇到“右”括号，从栈中弹出最后一个元素比对，如果不匹配则返回 False，遍历完成后栈中无剩余元素则匹配，否则不匹配。

.. note::

    - 时间复杂度：O(n)
    - 空间复杂度：O(n)，最坏情况是都为“左”括号，全部入栈

----------------------------------

.. code::  python

    class Solution(object):
        def isValid(self, s):
            """
            :type s: str
            :rtype: bool
            """
            stack, match = [], {')': '(', ']': '[', '}': '{'}
            for c in s:
                if c in match:
                    if not (stack and stack.pop() == match[c]):
                        return False
                else:
                    stack.append(c)
            return not stack