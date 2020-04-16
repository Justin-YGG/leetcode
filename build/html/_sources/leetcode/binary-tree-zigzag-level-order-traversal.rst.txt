====================================
103. 二叉树的锯齿形层次遍历
====================================

https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/

.. code::python

    # Definition for a binary tree node.
    # class TreeNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None

    class Solution(object):
        def __init__(self):
            self.result = []

        def zigzagLevelOrder(self, root):
            """
            :type root: TreeNode
            :rtype: List[List[int]]
            """
            if not root:
                return []

            s1, s2 = [root], []
            while s1 or s2:
                tmp = []
                while s1:
                    p = s1.pop()
                    tmp.append(p.val)
                    if p.left:
                        s2.append(p.left)
                    if p.right:
                        s2.append(p.right)
                if tmp:
                    self.result.append(tmp)
                    tmp = []
                while s2:
                    q = s2.pop()
                    tmp.append(q.val)
                    if q.right:
                        s1.append(q.right)
                    if q.left:
                        s1.append(q.left)
                if tmp:
                    self.result.append(tmp)
            return self.result


--------------------------------------------------------

.. code:: python

    class Solution:
        def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
            res = []

            def helper(root, depth):
                if not root:
                    return

                if len(res) == depth:
                    res.append([])
                if depth % 2 == 0:
                    res[depth].append(root.val)
                else:
                    res[depth].insert(0, root.val)

                helper(root.left, depth + 1)
                helper(root.right, depth + 1)

            helper(root, 0)
            return res
