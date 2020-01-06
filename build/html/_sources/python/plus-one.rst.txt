===========
66. 加一
===========

https://leetcode-cn.com/problems/plus-one/

给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

示例 1:
::

    输入: [1,2,3]
    输出: [1,2,4]

解释: 输入数组表示数字 123。

示例 2:
::

    输入: [4,3,2,1]
    输出: [4,3,2,2]

解释: 输入数组表示数字 4321。

---------------------------------------

``length  = len(digits) - 1``

从后往前遍历，如果当前位置数字为 9，我们就将值修改为 0，遍历结束后如果 length < 0，说明全部为 9，需要增加一个最高位；否则在中断位置加 1 即可

.. note::

    - 时间复杂度：O(n)
    - 空间复杂度: O(1)

---------------------------------------

.. code::  python

    class Solution(object):
        def plusOne(self, digits):
            """
            :type digits: List[int]
            :rtype: List[int]
            """
            length = len(digits) - 1
            while digits[length] == 9:
                digits[length] = 0
                length -= 1

            if length < 0:
                digits.insert(0, 1)
            else:
                digits[length] += 1
            return digits