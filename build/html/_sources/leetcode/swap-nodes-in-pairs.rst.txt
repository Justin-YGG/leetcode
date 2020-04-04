=============================
24. 两两交换链表中的节点
=============================

https://leetcode-cn.com/problems/swap-nodes-in-pairs/

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

 
示例:
::

    给定 1->2->3->4, 你应该返回 2->1->4->3.

----------------------------------

为了使链表从 ``pre -> a -> b -> b.next`` 变为 ``pre -> b -> a -> b.next``

我们需要三个指针，新建一个 pre 节点并指向 head 节点作为前驱节点，a 为当前节点，b 为当前节点的下一个节点

我们一次性把各个节点更新到最终结果，由于不便于记忆，我们还是采用分步走的写法

可以把整个链表想成两部分：已经两两交换过的前链，还没有交换的后链，完成一次交换后的 a 变为前链的最后一个节点，此时更新 pre = a，继续往下走

.. note::

    ``pre.next = b``

    ``pre.next, b.next = b, a``

    ``pre.next, b.next, a.next = b, a, b.next``

    pre 节点我们直接用 self 来充当，self 本身没有 `next` 属性，我们在 ``pre, pre.next = self, head`` 为其增加了该属性

----------------------------------

.. code::  python

    # Definition for singly-linked list.
    # class ListNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.next = None

    class Solution(object):
        def swapPairs(self, head):
            """
            :type head: ListNode
            :rtype: ListNode
            """
            pre = ListNode(0)
            pre.next = head
            c = pre
            while c.next and c.next.next:
                a = c.next
                b= a.next
                c.next, b.next, a.next = b, a, b.next
                c = a
            return pre.next