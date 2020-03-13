===========================
429. N叉树的层序遍历
===========================

https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/submissions/

给定一个 N 叉树，返回其节点值的层序遍历。 (即从左到右，逐层遍历)。

例如，给定一个 3叉树 :

.. image:: ../_static/images/429.png 

返回其层序遍历:
::

    [
         [1],
         [3,2,4],
         [5,6]
    ]
 

说明:

- 树的深度不会超过 1000。
- 树的节点总数不会超过 5000。

----------------------------------------------------

注意列表推导时多层循环的写法：

``[ <RETURNED_VALUE>  <OUTER_LOOP1>  <INNER_LOOP2>  <INNER_LOOP3> ... <OPTIONAL_IF> ]``

.. note::

    - 时间复杂度：O(n)
    - 空间复杂度：O(n)

----------------------------------------------------

.. code::  python

    """
    # Definition for a Node.
    class Node(object):
        def __init__(self, val=None, children=None):
            self.val = val
            self.children = children
    """
    class Solution(object):
        def levelOrder(self, root):
            """
            :type root: Node
            :rtype: List[List[int]]
            """
            q, res = [root], []
            while any(q):
                res.append(c.val for c in q)
                q = [c for node in q for c in node.children if c]
            return res

