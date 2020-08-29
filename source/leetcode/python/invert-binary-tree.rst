=================
226. 翻转二叉树
=================

https://leetcode-cn.com/problems/invert-binary-tree/description/


翻转一棵二叉树。

示例：

输入::

         4
       /   \
      2     7
     / \   / \
    1   3 6   9

输出::

         4
       /   \
      7     2
     / \   / \
    9   6 3   1



.. code:: python

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution(object):
        def invertTree(self, root):
            """
            :type root: TreeNode
            :rtype: TreeNode
            """
            stack = [root]
            while stack:
                node = stack.pop()
                if node:
                    node.left, node.right = node.right, node.left
                    stack.extend([node.left, node.right])
            return root