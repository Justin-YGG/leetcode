======================
 199. 二叉树的右视图
======================

https://leetcode-cn.com/problems/binary-tree-right-side-view/

给定一棵二叉树，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。

示例::

    输入: [1,2,3,null,5,null,4]
    输出: [1, 3, 4]
    解释:

       1            <---
     /   \
    2     3         <---
     \     \
      5     4       <---



.. code:: python

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution(object):
        def rightSideView(self, root):
            """
            :type root: TreeNode
            :rtype: List[int]
            """
            if not root:
                return []
            queue = [root]
            res = []
            while queue:
                nxt = []
                res.append(queue[-1].val)
                for node in queue:
                    if node.left:
                        nxt.append(node.left)
                    if node.right:
                        nxt.append(node.right)
                queue = nxt
            return res