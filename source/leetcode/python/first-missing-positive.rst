=======================
41. 缺失的第一个正数
=======================

https://leetcode-cn.com/problems/first-missing-positive/

给你一个未排序的整数数组，请你找出其中没有出现的最小的正整数。



示例 1:

输入: [1,2,0]
输出: 3
示例 2:

输入: [3,4,-1,1]
输出: 2
示例 3:

输入: [7,8,9,11,12]
输出: 1


提示：

你的算法的时间复杂度应为O(n)，并且只能使用常数级别的额外空间。

使用额外空间解法：

.. code:: python

    class Solution(object):
        def firstMissingPositive(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            length = len(nums)
            dic = {n:n for n in nums}
            for i in range(1, length+1):
                if i not in dic:
                    return i
            return length + 1


不使用额外空间解法：

.. code:: python

    class Solution(object):
        def firstMissingPositive(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            length = len(nums)
            for i in range(length):
                while 1 <= nums[i] <= length and nums[i] != nums[nums[i] - 1]:
                    self.swap(nums, i, nums[i] - 1)

            for i in range(length):
                if i+1 != nums[i]:
                    return i + 1

            return length + 1

        def swap(self, nums, index_i, index_j):
            nums[index_i], nums[index_j] = nums[index_j], nums[index_i]