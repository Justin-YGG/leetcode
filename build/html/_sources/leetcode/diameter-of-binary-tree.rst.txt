==================
543. 二叉树的直径
==================

https://leetcode-cn.com/problems/diameter-of-binary-tree/

给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过根结点。

示例 :

给定二叉树
::

          1
         / \
        2   3
       / \
      4   5

返回 3, 它的长度是路径 [4,2,1,3] 或者 [5,2,1,3]。

**注意：两结点之间的路径长度是以它们之间边的数目表示。**

--------------------------------

最长路径有两种情况，过 root 节点和不过 root 节点：

..

    二叉树的最长路径=max{左子树的最长路径,右子树的最长路径,经过根结点的最长路径}

    经过根结点的最长路径 = 左子树的深度加上右子树的深度，所以：

    二叉树的最长路径=max{左子树的最长路径,右子树的最长路径,左子树的深度+右子树的深度}

---------------------------------

.. note::

    - 时间复杂度：O(N)
    - 空间复杂度：O(Height)，其中 Height 为二叉树的高度

--------------------------------

.. code:: python

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution(object):
        def diameterOfBinaryTree(self, root):
            """
            :type root: TreeNode
            :rtype: int
            """
            def dfs(node):
                if not node:
                    return 0, 0
                left_depth, left_dia = dfs(node.left)
                right_depth, right_dia = dfs(node.right)

                # 最大深度
                depth = 1 + max(left_depth, right_depth)
                # 最长路径
                diameter = max(left_dia, right_dia, left_depth+right_depth)
                return depth, diameter
            depth, diameter = dfs(root)
            return diameter

--------------------------------

上述方法中我们是根据 ``left_dia``，``right_dia`` 子树的最长路径来计算当前树的最长路径，那么可以用一个全局变量来保存

.. code:: python

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution(object):
        def diameterOfBinaryTree(self, root):
            """
            :type root: TreeNode
            :rtype: int
            """
            def dfs(node):
                if not node:
                    return 0
                left = dfs(node.left)
                right = dfs(node.right)
                # 最长路径 = max{子树的最长路径, 左子树的深度+右子树的深度}
                self.diameter = max(self.diameter, left + right)
                # 返回最大深度
                return 1 + max(left, right)
            self.diameter = 0
            dfs(root)
            return self.diameter

