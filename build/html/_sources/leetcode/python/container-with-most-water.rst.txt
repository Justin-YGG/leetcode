======================
11. 盛最多水的容器
======================

https://leetcode-cn.com/problems/container-with-most-water/

给定 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

**说明：你不能倾斜容器，且 n 的值至少为 2。**

.. image::  ../../_static/images/11.jpg

图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。

 
示例:
::

    输入: [1,8,6,2,5,4,8,3,7]
    输出: 49

---------------------------------

**方法一：暴力求解**

.. note::

    - 时间复杂度：O(n^2)
    - 空间复杂度：O(1)

.. code::  python

    class Solution(object):
        def maxArea(self, height):
            """
            :type height: List[int]
            :rtype: int
            """
            max_area = 0
            for i in range(len(height)- 1):
                for j in range(i+1, len(height)):
                    max_area =  max(max_area, (j-i)*min(height[i], height[j]))
            return max_area

---------------------------------

**方法一：双指针法**

``S(i, j) = (j - i) * min(height[i], height[j]) (0 < i < j < n)``

假设 height[i] < height[j], 无论移动短板还是长板，宽度都会减 1，
无论是移动短板或者长板，我们都只关注移动后的【新短板】会不会变长

每次移动的木板都只有三种情况，比原短板短，比原短板长，与原短板相等

如果向内移动长板：

- 比原短板短，短板变短，面积更小

- 大于等于原短板，短板不变，面积变小

如果向内移动短板：

- 比原短板，短板变短，面积更小

- 等于原短板，短板不变，面积更小

- 大于原短板，面积有可能变大

``min(height[i], height[j])`` 有可能会变大

**实质就是在移动的过程中不断消去不可能成为最大值的状态**，提供一个图解 https://leetcode-cn.com/problems/container-with-most-water/solution/zhi-guan-de-shuang-zhi-zhen-fa-jie-shi-by-na-kong/

.. note::

    时间复杂度：O(n)

    空间复杂度：O(1)

.. warning::

    对于最大盛水面积的判断可以从 ``if`` 判断中抽离，写成

    ``water = max(water, (r-l) * min(height[l], height[r]))``

    但是 ``min`` 操作本身的时间复杂度是 O(n)，虽然只是两个数的判断，但在我们已知较小者的情况下，不再判断，以提高程序执行速度

-------------------------------------------------

.. code::  python

    class Solution(object):
        def maxArea(self, height):
            """
            :type height: List[int]
            :rtype: int
            """
            l, r = 0, len(height) - 1
            water = 0
            while l < r:
                if height[l] < height[r]:
                    water = max(water, (r-l) * height[l])
                    l += 1
                else:
                    water = max(water, (r-l) * height[r])
                    r -= 1
            return water
