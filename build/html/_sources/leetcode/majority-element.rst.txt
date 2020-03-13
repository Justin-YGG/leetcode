==========================
169. 多数元素
==========================

https://leetcode-cn.com/problems/majority-element/

给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

示例 1:
::

    输入: [3,2,3]
    输出: 3

示例 2:
::

    输入: [2,2,1,1,1,2,2]
    输出: 2

---------------------------------------

**方法一:** 哈希表
::

    用字典统计数字出现的次数

.. note::

    - 时间复杂度：O(n)
    - 空间复杂度：O(n)

.. code:: python

    class Solution(object):
        def majorityElement(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            a = {}
            for n in nums:
                a[n] = a.get(n, 0) + 1
            for k, v in a.iteritems():
                if v > len(nums) // 2:
                return k