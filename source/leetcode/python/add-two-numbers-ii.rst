=====================
445. 两数相加 II
=====================


https://leetcode-cn.com/problems/add-two-numbers-ii/

给定两个非空链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储单个数字。将这两数相加会返回一个新的链表。

 

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

进阶::

    如果输入链表不能修改该如何处理？换句话说，你不能对列表中的节点进行翻转。

    示例:

    输入: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
    输出: 7 -> 8 -> 0 -> 7



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
            def push_stack(l, stack):
                while l:
                    stack.append(l)
                    l = l.next

            stack1, stack2 = [], []
            push_stack(l1, stack1)
            push_stack(l2, stack2)
            dummy = ListNode(-1)

            carry = 0
            while stack1 or stack2 or carry:
                x = stack1.pop().val if stack1 else 0
                y = stack2.pop().val if stack2 else 0

                sum_ = x + y + carry
                carry = sum_ / 10
                sum_ = sum_ % 10

                # 头插法
                new_node = ListNode(sum_)
                new_node.next = dummy.next
                dummy.next = new_node
            return dummy.next