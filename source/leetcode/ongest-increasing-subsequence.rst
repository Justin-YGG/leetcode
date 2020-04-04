=====================
300. 最长上升子序列
=====================

https://leetcode-cn.com/problems/longest-increasing-subsequence/

.. code:: python

    class Solution(object):
        def lengthOfLIS(self, nums):
            """
            :type nums: List[int]
            :rtype: int
            """
            dp = [1] * len(nums)
            for i in range(len(nums)):
                for j in range(i):
                    if nums[j] < nums[i]:
                        dp[i]= max(dp[i], 1+dp[j])
            return max(dp) if dp else 0