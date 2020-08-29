======================
209. 长度最小的子数组
======================

https://leetcode-cn.com/problems/minimum-size-subarray-sum/

给定一个含有 n 个正整数的数组和一个正整数 s ，找出该数组中满足其和 ≥ s 的长度最小的连续子数组。如果不存在符合条件的连续子数组，返回 0。

示例::

    输入: s = 7, nums = [2,3,1,2,4,3]
    输出: 2
    解释: 子数组 [4,3] 是该条件下的长度最小的连续子数组。
    进阶:

    如果你已经完成了O(n) 时间复杂度的解法, 请尝试 O(n log n) 时间复杂度的解法。



.. code:: python

    class Solution(object):
        def minSubArrayLen(self, s, nums):
            """
            :type s: int
            :type nums: List[int]
            :rtype: int
            """
            # 注意判断边界
            if not nums:
                return 0
            sum_ = left = right = 0
            res = float('inf')
            while right < len(nums):
                sum_ += nums[right]
                right += 1
                while sum_ >= s:
                    res = min(res, right - left)
                    sum_ -= nums[left]
                    left += 1

            # 注意判断结果
            return 0 if res == float('inf') else res
