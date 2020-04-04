====================
98. 验证二叉搜索树
====================

https://leetcode-cn.com/problems/validate-binary-search-tree/

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

节点的左子树只包含小于当前节点的数。
节点的右子树只包含大于当前节点的数。
所有左子树和右子树自身必须也是二叉搜索树。
示例 1:

输入:
    2
   / \
  1   3
输出: true
示例 2:

输入:
    5
   / \
  1   4
     / \
    3   6
输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
     根节点的值为 5 ，但是其右子节点值为 4 。


.. code:: python

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution(object):
        def __init__(self):
            self.nodes = []

        def isValidBST(self, root):
            """
            :type root: TreeNode
            :rtype: bool
            """
            self.inorder(root)
            return self.nodes == sorted(set(self.nodes))

        def inorder(self, root):
            if root:
                self.inorder(root.left)
                self.nodes.append(root.val)
                self.inorder(root.right)