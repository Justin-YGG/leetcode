=================================
235. 二叉搜索树的最近公共祖先
=================================

https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/


.. code:: python

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution(object):
        def lowestCommonAncestor(self, root, p, q):
            """
            :type root: TreeNode
            :type p: TreeNode
            :type q: TreeNode
            :rtype: TreeNode
            """
            if not root:
                return
            if p.val > root.val and q.val > root.val:
                return self.lowestCommonAncestor(root.right, p, q)
            elif p.val < root.val and q.val < root.val:
                return self.lowestCommonAncestor(root.left, p, q)
            return root