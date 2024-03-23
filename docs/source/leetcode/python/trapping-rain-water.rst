===============
42. 接雨水
===============

https://leetcode-cn.com/problems/trapping-rain-water/

给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

.. image::  ../../_static/images/42.png

上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 感谢 Marcos 贡献此图。

示例:
::

    输入: [0,1,0,2,1,0,1,3,2,1,2,1]
    输出: 6

-------------------------------------------------

**FYI:**

- https://www.cnblogs.com/grandyang/p/8887985.html
- https://leetcode-cn.com/problems/trapping-rain-water/solution/bao-li-jie-fa-yi-kong-jian-huan-shi-jian-zhi-zhen-/

首先理解``单调栈 Monotone Stack``，以``单调递减栈``为例，比如有一家店在发 free food，很多人在排队，于是你也赶过去凑热闹。但是由于来晚了，队伍已经很长了，想着不然就插个队啥的。但发现排在队伍最前面的都是一些有纹身的大佬，惹不起。于是往队伍后面走，发现是一群小屁孩，直接全部撵走，然后排在了社会大佬们的后面。那么这就是一个单调递减的栈，按实力递减。

**单调栈的一大优势就是线性的时间复杂度，所有的元素只会进栈一次，而且一旦出栈后就不会再进来了**

- 单调递减栈可以找到 ``左起第一个`` 比当前数字 ``大`` 的元素
- 单调递增栈可以找到 ``左起第一个`` 比当前数字 ``小`` 的元素

对于此题，如果能盛水，需要两边高，中间低。

使用一个单调递减栈，将递减的边界存进去，一旦发现当前的数字大于栈顶元素了，那么就有可能会有能装水的地方产生。此时我们当前的数字是右边界，我们从栈中至少需要有两个数字，才能形成一个坑槽，先取出的那个最小的数字，就是坑槽的最低点，再次取出的数字就是左边界，我们比较左右边界，取其中较小的值为装水的边界，然后此高度减去水槽最低点的高度，乘以左右边界间的距离就是装水量。

**注意：栈中存的数字并不是递减的高度，而是递减的高度的坐标**

.. note::

   - 时间复杂度：O(n)

       + 单次遍历 O(n) ，每个条形块最多访问两次（由于栈的弹入和弹出），并且弹入和弹出栈都是 O(1) 的

   - 空间复杂度：O(n)

       +  栈最多在阶梯型或平坦型条形块结构中占用 O(n) 的空间


-------------------------------------------------

.. code::  python

    class Solution(object):
        def trap(self, height):
            """
            :type height: List[int]
            :rtype: int
            """
            if not height or len(height) < 3:
                return 0

            res = 0
            stack = []
            for i in range(len(height)):
                # 每次循环，其实是在填平
                while stack and height[stack[-1]] < height[i]:
                    bottom_index = stack.pop()
                    if not stack:
                        break
                    res += (min(height[stack[-1]], height[i]) - height[bottom_index]) * (i - stack[-1] - 1)
                stack.append(i)
            return res
