=======================
104. 二叉树的最大深度
=======================

https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

示例：

给定二叉树 [3,9,20,null,null,15,7]
::

    3
   / \
  9  20
    /  \
   15   7

返回它的最大深度 3 。

-----------------------------

参考 `视频`_

.. _`视频`: https://www.youtube.com/watch?v=_O-mK2g_jhI

``Height(Max Depth) of BT: 1+ Number of edges on the longest path from root to leaf``

递归深度遍历左右子树：``H = 1 + max(H(left_tree), H(right_tree))``


.. note::

    - 时间复杂度：我们每个结点只访问一次，因此时间复杂度为 O(N)
    - 空间复杂度：最坏 O(n), 如：树是完全不平衡的，只剩左节点；最好 O(log(N))，树是完全平衡的

-------------------------------

.. code:: python

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution(object):
        def maxDepth(self, root):
            """
            :type root: TreeNode
            :rtype: int
            """
            def dfs(node):
                if not node:
                    return 0
                left = dfs(node.left)
                right = dfs(node.right)
                return max(left, right) + 1
            return dfs(root)

--------------------------------

**one line version**

.. code:: python

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution(object):
        def maxDepth(self, root):
            """
            :type root: TreeNode
            :rtype: int
            """
            return 1 + max(map(self.maxDepth, (root.left, root.right))) if root else 0

