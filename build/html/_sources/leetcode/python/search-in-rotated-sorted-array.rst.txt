================================
33. 搜索旋转排序数组
================================

https://leetcode-cn.com/problems/search-in-rotated-sorted-array/


假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 ``[0,1,2,4,5,6,7]`` 可能变为 ``[4,5,6,7,0,1,2]`` )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 O(log n) 级别。

示例 1::

    输入: nums = [4,5,6,7,0,1,2], target = 0
    输出: 4

示例 2::

    输入: nums = [4,5,6,7,0,1,2], target = 3
    输出: -1


--------------------------------------------------------

.. tip::

    旋转后的数组实际是有两部分有序数组组成的，题目中指出是升序数组，我们只要找到两个有序数组的 ``pivot point`` ，
    然后判断出 ``target`` 在哪个区间，调用二分查找即可。

    旋转后数组的 ``pivot point`` 其实就是数组中的最小值，我们使用改造的二分查找来定位 ``pivot point``


.. code:: python

    class Solution(object):
        def search(self, nums, target):
            """
            :type nums: List[int]
            :type target: int
            :rtype: int
            """
            length = len(nums)
            if length == 0:
                return -1

            left, right = 0, length - 1
            while left < right:
                mid = left + (right - left) / 2
                # 如果 nums[mid] > nums[right] 很奇怪，说明含有整个数组最小值的【升序小分队】在右面，
                # 左移左边界，只有满足此条件，left 就会根据计算得出的mid 往右移动，直到移动的最小值位置
                if nums[mid] > nums[right]:
                    left = mid + 1
                else:
                    # 如果 nums[mid] <= nums[right] 说明已经进入 【升序小分队】的区间，不断根据计算的mid，右移区间右边界
                    # 直到 left == right 循环退出
                    right = mid

            pivot = left

            left, right = 0, length - 1

            if nums[pivot] <= target <= nums[right]:
                left = pivot
            else:
                right = pivot - 1

            while left <= right:
                mid = left + (right - left) / 2
                if nums[mid] == target:
                    return mid
                elif nums[mid] < target:
                    left = mid + 1
                elif nums[mid] > target:
                    right = mid - 1

            return -1
