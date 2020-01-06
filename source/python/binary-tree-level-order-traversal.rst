=====================================
102. 二叉树的层次遍历
=====================================

https://leetcode-cn.com/problems/binary-tree-level-order-traversal/

给定一个二叉树，返回其按层次遍历的节点值。 （即逐层地，从左到右访问所有节点）。

例如:
给定二叉树: [3,9,20,null,null,15,7],
::

    3
   / \
  9  20
    /  \
   15   7

返回其层次遍历结果：
::

    [
      [3],
      [9,20],
      [15,7]
    ]

----------------------------------------

.. note::

    - 时间复杂度：O(n)
    - 空间复杂度：O(n)

----------------------------------------

.. code::  python

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution(object):
        def levelOrder(self, root):
            """
            :type root: TreeNode
            :rtype: List[List[int]]
            """
            q, res = [root], []
            while any(q):
                res.append([c.val for c in q])
                q = [n for node in q for n in (node.left, node.right) if n]
            return res