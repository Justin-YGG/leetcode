================================
82. 删除排序链表中的重复元素 II
================================

https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/

给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 没有重复出现 的数字。

示例 1::

    输入: 1->2->3->3->4->4->5
    输出: 1->2->5
    示例 2:

    输入: 1->1->1->2->3
    输出: 2->3


.. code:: python

    # Definition for singly-linked list.
    # class ListNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.next = None

    class Solution(object):
        def deleteDuplicates(self, head):
            """
            :type head: ListNode
            :rtype: ListNode
            """
            dummy = ListNode(-1)
            dummy.next = head
            cur = dummy
            while cur.next and cur.next.next:
                if cur.next.val == cur.next.next.val:
                    tmp = cur.next
                    while tmp and tmp.next and tmp.val == tmp.next.val:
                        tmp = tmp.next
                    cur.next = tmp.next
                else:
                    cur = cur.next
            return dummy.next