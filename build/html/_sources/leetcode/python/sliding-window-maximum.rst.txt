=============================
239. 滑动窗口最大值
=============================

https://leetcode-cn.com/problems/sliding-window-maximum/

给定一个数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。

返回滑动窗口中的最大值。


进阶::

    你能在线性时间复杂度内解决此题吗？



示例::

    输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
    输出: [3,3,5,5,6,7]
    解释:

      滑动窗口的位置                最大值
    ---------------               -----
    [1  3  -1] -3  5  3  6  7       3
     1 [3  -1  -3] 5  3  6  7       3
     1  3 [-1  -3  5] 3  6  7       5
     1  3  -1 [-3  5  3] 6  7       5
     1  3  -1  -3 [5  3  6] 7       6
     1  3  -1  -3  5 [3  6  7]      7


提示::

    1 <= nums.length <= 10^5
    -10^4 <= nums[i] <= 10^4
    1 <= k <= nums.length


.. code:: python

    from collections import deque

    class Solution(object):
        def maxSlidingWindow(self, nums, k):
            """
            :type nums: List[int]
            :type k: int
            :rtype: List[int]
            """
            window = deque()
            res = []

            for i in range(len(nums)):
                if i < k - 1:
                    self.push(window, nums[i])
                else:
                    self.push(window, nums[i])
                    res.append(window[0])
                    self.remove(window, nums[i-k+1])
            return res

        def push(self, window, n):
            while window and window[-1] < n:
                window.pop()
            window.append(n)

        def remove(self, window, n):
            if window and window[0] == n:
                window.popleft()
