=============
189. 旋转数组
=============

https://leetcode-cn.com/problems/rotate-array/

给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。

示例 1:
::

    输入: [1,2,3,4,5,6,7] 和 k = 3
    输出: [5,6,7,1,2,3,4]

解释:
::

    向右旋转 1 步: [7,1,2,3,4,5,6]
    向右旋转 2 步: [6,7,1,2,3,4,5]
    向右旋转 3 步: [5,6,7,1,2,3,4]

示例 2:
::

    输入: [-1,-100,3,99] 和 k = 2
    输出: [3,99,-1,-100]

解释:
::

    向右旋转 1 步: [99,-1,-100,3]
    向右旋转 2 步: [3,99,-1,-100]

说明:

尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
要求使用空间复杂度为 O(1) 的原地算法。

------------------------------------

把数组中的元素比作学生，坐标比作座位。然后开始换座位，nums[0] 上的同学起身坐到 nums[k+0] 座位上，nums[k+0] 上的同学被挤走，
去到nums[k+k]座位上，反复执行；有一种情况，其中有同学被挤出来后做到了空座位，没人被挤走，此时如果还有同学坐在自己原来的位置上,
那么就要顺着从第二个位置上的同学换位置，直到所有同学做到他最终该坐的位置上，n 个同学换 n 次，用 count 计数，count == len(nums) 时，所有同学完成换座

.. note::

    - 时间复杂度：O(n)，总共移动了 n 次
    - 空间复杂度: O(1)

-----------------------------------

.. code::  python

    class Solution(object):
        def rotate(self, nums, k):
            """
            :type nums: List[int]
            :type k: int
            :rtype: None Do not return anything, modify nums in-place instead.
            """
            length = len(nums)
            k %= length
            if k == 0:
                return
            start = 0
            count = 0

            # n 个位置共需要移动 n 次
            while count < length:
                current = start
                pre = nums[start]

                while True:
                    # 将当前位置移动到后k位置
                    next_ = (current + k) % length
                    tmp = nums[next_]
                    nums[next_] = pre

                    # 更新当前位置
                    current = next_
                    pre = tmp

                    # 完成一次移动，count加1
                    count += 1

                    # 当前位置如果是本轮开始位置，说明一件完成一轮
                    if current == start:
                        break
                # 如果一轮无法完全所有元素的移动，顺延从第二个位置继续下一轮
                start += 1
