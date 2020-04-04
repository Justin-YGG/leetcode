======================
111. 二叉树的最小深度
======================

https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

说明: 叶子节点是指没有子节点的节点。

示例::

    给定二叉树 [3,9,20,null,null,15,7],

        3
       / \
      9  20
        /  \
       15   7
    返回它的最小深度  2.


---------------------------------

.. code:: python

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution(object):
        def minDepth(self, root):
            """
            :type root: TreeNode
            :rtype: int
            """
            if not root:
                return 0

            left = self.minDepth(root.left)
            right = self.minDepth(root.right)
            # 注意判断，有子树为空的时候
            return 1 + min(left, right) if all((left, right)) else 1 + max(left, right)