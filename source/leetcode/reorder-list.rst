==========================
143. 重排链表
==========================

https://leetcode-cn.com/problems/reorder-list/

给定一个单链表 L：L0→L1→…→Ln-1→Ln ，
将其重新排列后变为： L0→Ln→L1→Ln-1→L2→Ln-2→…

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

示例 1:

给定链表 1->2->3->4, 重新排列为 1->4->2->3.
示例 2:

给定链表 1->2->3->4->5, 重新排列为 1->5->2->4->3.


.. code:: python

    # Definition for singly-linked list.
    # class ListNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.next = None

    class Solution(object):
        def reorderList(self, head):
            """
            :type head: ListNode
            :rtype: None Do not return anything, modify head in-place instead.
            """
            if not head:
                return
            node_list = []
            cur = head
            while cur:
                node_list.append(cur)
                cur = cur.next

            i, j = 0, len(node_list) - 1
            while i < j:
                node_list[i].next = node_list[j]
                i += 1
                if i == j:
                    break
                node_list[j].next = node_list[i]
                j -= 1
            node_list[i].next = None



------------------------------------------------------

通过观察，可以将重排链表分解为以下三个步骤：

首先重新排列后，链表的中心节点会变为最后一个节点。所以需要先找到链表的中心节点
可以按照中心节点将原始链表划分为左右两个链表。
2.1. 按照中心节点将原始链表划分为左右两个链表，左链表：1->2->3 右链表：4->5。
2.2. 将右链表反转，就正好是重排链表交换的顺序，右链表反转：5->4。
合并两个链表，将右链表插入到左链表，即可重新排列成：1->5->2->4->3.


.. code:: python

    # Definition for singly-linked list.
    # class ListNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.next = None

    class Solution(object):
        def reorderList(self, head):
            """
            :type head: ListNode
            :rtype: None Do not return anything, modify head in-place instead.
            """
            if not head:
                return
            middle_node = self.find_middle(head)
            left = head
            right = middle_node.next
            middle_node.next = None
            right = self.reverse(right)
            self.merge(left, right)

        def find_middle(self, head):
            slow = fast = head
            while fast and fast.next:
                fast = fast.next.next
                slow = slow.next
            return slow

        def reverse(self, head):
            pre = None
            cur = head
            while cur:
                tmp = cur.next
                cur.next = pre
                pre = cur
                cur = tmp
            return pre

        def merge(self, left, right):
            while left and right:
                left_temp = left.next
                right_temp = right.next

                left.next = right;
                right.next = left_temp

                left = left_temp
                right = right_temp

