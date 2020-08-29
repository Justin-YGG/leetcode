========================
110. 平衡二叉树
========================

https://leetcode-cn.com/problems/balanced-binary-tree/

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。

示例 1::

    给定二叉树 [3,9,20,null,null,15,7]

        3
       / \
      9  20
        /  \
       15   7
    返回 true 。

示例 2::

    给定二叉树 [1,2,2,3,3,null,null,4,4]

           1
          / \
         2   2
        / \
       3   3
      / \
     4   4
    返回 false 。


.. code:: python

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution(object):
        def isBalanced(self, root):
            """
            :type root: TreeNode
            :rtype: bool
            """
            if not root:
                return True

            return abs(self.helper(root.left) - self.helper(root.right)) < 2 and self.isBalanced(root.left) and self.isBalanced(root.right)

        def helper(self, node):
            if not node:
                return 0
            left = self.helper(node.left)
            right = self.helper(node.right)

            return 1 + max(left, right)