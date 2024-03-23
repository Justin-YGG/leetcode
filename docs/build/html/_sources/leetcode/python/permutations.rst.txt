===================
46. 全排列
===================

https://leetcode-cn.com/problems/permutations/

给定一个 没有重复 数字的序列，返回其所有可能的全排列。

示例:

输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]


.. code:: python

    class Solution(object):
        def __init__(self):
            self.result = []

        def permute(self, nums):
            """
            :type nums: List[int]
            :rtype: List[List[int]]
            """
            self.backtrack(nums, [])
            return self.result

        def backtrack(self, nums, track):
            if len(nums) == len(track):
                self.result.append(track[:])

            for n in nums:
                if n in track:
                    continue
                track.append(n)
                self.backtrack(nums, track)
                track.pop()