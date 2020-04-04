=============================
215. 数组中的第K个最大元素
=============================


https://leetcode-cn.com/problems/kth-largest-element-in-an-array

.. code:: python

    import heapq

    class Solution(object):
        def findKthLargest(self, nums, k):
            """
            :type nums: List[int]
            :type k: int
            :rtype: int
            """
            length = len(nums)
            if length < k:
                return

            h = []
            for i in range(k):
                heapq.heappush(h, nums[i])

            for i in range(k, length):
                top = h[0]
                if nums[i] > top:
                    heapq.heapreplace(h, nums[i])

            return h[0]