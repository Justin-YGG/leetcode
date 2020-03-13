==========================
88. 合并两个有序数组
==========================

https://leetcode-cn.com/problems/merge-sorted-array/

给定两个有序整数数组 nums1 和 nums2，将 nums2 合并到 nums1 中，使得 num1 成为一个有序数组。

说明:

初始化 nums1 和 nums2 的元素数量分别为 m 和 n。
你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。

示例:
::

    输入:

    nums1 = [1,2,3,0,0,0], m = 3
    nums2 = [2,5,6],       n = 3

    输出: [1,2,2,3,5,6]

--------------------------------------

**双指针/从后往前**

我们从 nums1 的 ``m+n-1`` 位置（即完成合并后的最后一个位置）开始填充，循环长度为 n

由于两个数组都是有序的，我们每次从 num1 和 nums2 中取最后一个值进行比较，将较大值填充进nums1

如果 m 先消耗完，剩余就是把 nums2 的元素填充到剩余位置

.. note::

   - 时间复杂度： O(m+n) 即 O(n)
   - 空间复杂度： O(1)

-------------------------------------

.. code::  python

    class Solution(object):
        def merge(self, nums1, m, nums2, n):
            """
            :type nums1: List[int]
            :type m: int
            :type nums2: List[int]
            :type n: int
            :rtype: None Do not return anything, modify nums1 in-place instead.
            """
            while n:
                if m <= 0 or nums1[m-1] < nums2[n-1]:
                    nums1[m+n-1] = nums2[n-1]
                    n -= 1
                else:
                    nums1[m+n-1] = nums1[m-1]
                    m -= 1
