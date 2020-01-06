==========================
21. 合并两个有序链表
==========================

https://leetcode-cn.com/problems/merge-two-sorted-lists/

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

示例：
::

    输入：1->2->4, 1->3->4
    输出：1->1->2->3->4->4

----------------------------

新建一个节点，基于 l1 和 l2 的 **公共长度** 进行遍历，选取较小值进行追加，在循环终止的时候， l1 和 l2 至多有一个是非空的，直接追加即可

.. note::

    - 时间复杂度：O(m+n) 即 O(n)
    - 空间复杂度：O(1)

-----------------------------

.. code::  python

    # Definition for singly-linked list.
    # class ListNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.next = None

    class Solution(object):
        def mergeTwoLists(self, l1, l2):
            """
            :type l1: ListNode
            :type l2: ListNode
            :rtype: ListNode
            """
            if not all((l1, l2)):
                return l1 or l2

            p = ListNode(-1)
            head = p
            while l1 and l2:
                if l1.val < l2.val:
                    p.next = l1
                    l1 = l1.next
                else:
                    p.next = l2
                    l2 = l2.next
                p = p.next
            p.next = l1 or l2
            return head.next