======================
二分查找
======================

针对有序是数据进行高效查找，可以使用二分查找，时间复杂度为 ``O(n)`` ，实现上类似分治思想，每次都和区间中间的值比较
然后缩小查找区间，知道找到目标元素或者区间缩小为 0。

二分查找依赖的是顺序表结构，即数组，在内存中拥有连续的数据，使用场景有一定的局限性：

- 数据必须是有序的

- 数据量太小的，无需使用二分查找；如果比较本身比较耗时，可以考虑使用二分查找减少比较次数

- 数据量太大也不宜使用二分查找，需要申请大量的 ``连续`` 内存

.. tip::

    计算中点位置时，可以用 ``mid = left + (right - left) / 2`` ，防止数字过大时溢出

---------------------------------------------


**查找某个目标元素**
---------------------------------------------

递增序列，无重复元素，查找某个元素 target 在数组的中的下标。

.. code:: python

    def binary_search(nums, target):

        length = len(nums)
        if length == 0:
            return -1

        left, right = 0, length - 1

        while left <= right:
            mid = left + (right - left) / 2
            if nums[mid] == target:
                return mid
            # 查找区间为 [mid+1, right]
            elif nums[mid] < target:
                left = mid + 1
            # 查找区间为 [left, mid-1]
            elif nums[mid] > target:
                right = mid - 1
        return -1

---------------------------------------------

**查找某个目标第一个或左后一个出现的位置**
---------------------------------------------

给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置::

    输入: nums = [5,7,7,8,8,10], target = 8

    输出: [3,4]

    输入: nums = [5,7,7,8,8,10], target = 6

    输出: [-1,-1]a

查找 target 出现的第一个位置
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. tip::

    以查找 target 出现的第一个位置为例（同理，适用于查找最后一个位置）

    ``nums[mid] >= target`` ，我们重点分析一下这一行代码：

    - 当 ``nums[mid] > target`` 时，显然我们要缩小查找区间，将搜索的右边界往左移动即 ``right = mid - 1``

    - 当 ``nums[mid] == target`` 时，因为我们要查找元素出现的第一个位置，此时我们无法确定当前的 ``target`` 是否为第一个出现，
      所以我们也要向左缩小区间（因为数组是升序的，第一个位置不可能出现在当前 target 之后）；

      我们在第一次找到 ``target`` 后通过判断通过 ``index`` 保存了其坐标

      右边界在左移以后：如果下一个扫描区间 [left, mid-1] 里面仍然有 ``target``，我们会在后面的逻辑里更新 ``index`` 的值；
      如果下个扫描区间里不再包含 ``target``，那么就会一直执行 ``left = mid + 1`` ，直到循环退出

    - 如果 ``target`` 不存在，返回默认 index


.. code:: python

    def left_bound(nums, target):
        length = len(nums)
        if length == 0:
            return -1

        left, right = 0, length - 1
        index = -1

        while left <= right:
            mid = left + (right - left) / 2
            if nums[mid] >= target:
                right = mid - 1
            else:
                left = mid + 1

            # 保存并更新 target 坐标
            if nums[mid] == target:
                index = mid
        return index

------------------------------------------------------

查找 target 出现的最后一个位置
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: python

    def right_bound(nums, target):
        length = len(nums)
        if length == 0:
            return -1

        left, right = 0, length - 1
        index = -1

        while left <= right:
            mid = left + (right - left) / 2
            if nums[mid] <= target:
                left = mid + 1
            else:
                right = mid - 1

            if nums[mid] == target:
                index = mid
        return index
