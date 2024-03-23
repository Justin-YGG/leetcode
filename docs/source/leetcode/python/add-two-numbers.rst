==============
2. 两数相加
==============

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：

输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807

.. code:: python

    # Definition for singly-linked list.
    # class ListNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.next = None

    class Solution(object):
        def addTwoNumbers(self, l1, l2):
            """
            :type l1: ListNode
            :type l2: ListNode
            :rtype: ListNode
            """
            pre = ListNode(0)
            cur = pre

            carry = 0
            while l1 or l2:
                x = l1.val if l1 else 0
                y = l2.val if l2 else 0

                sum_ = x + y + carry
                carry = sum_ / 10
                sum_ = sum_ % 10

                cur.next = ListNode(sum_)
                cur = cur.next

                if l1:
                    l1 = l1.next
                if l2:
                    l2 = l2.next
            if carry > 0:
                cur.next = ListNode(carry)
            return pre.next
