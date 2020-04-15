==========================
23. 合并K个排序链表
==========================

https://leetcode-cn.com/problems/merge-k-sorted-lists/

合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

示例::

    输入:
    [
      1->4->5,
      1->3->4,
      2->6
    ]
    输出: 1->1->2->3->4->4->5->6


.. note::

    - 归并排序


.. code:: python

    # Definition for singly-linked list.
    # class ListNode(object):
    #     def __init__(self, x):
    #         self.val = x
    #         self.next = None

    class Solution(object):
        def mergeKLists(self, lists):
            """
            :type lists: List[ListNode]
            :rtype: ListNode
            """
            if not lists:
                return lists
            return self.merge(lists, 0, len(lists)-1)

        def merge(self, lists, left, right):
            if left == right:
                return lists[left]
            mid = left + (right-left) / 2
            l1 = self.merge(lists, left, mid)
            l2 = self.merge(lists, mid+1, right)
            return self.merge_two_lists(l1, l2)

        def merge_two_lists(self, l1, l2):
            pre = ListNode(-1)
            cur = pre
            while l1 and l2:
                if l1.val <= l2.val:
                    cur.next = l1
                    l1 = l1.next
                else:
                    cur.next = l2
                    l2 = l2.next

                cur = cur.next
            cur.next = l1 or l2
            return pre.next